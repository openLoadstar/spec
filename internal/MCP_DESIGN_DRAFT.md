# 🔌 LOADSTAR MCP 서버 설계 초안

> **상태**: 구현 진행 중 (2026-04-29~) — `loadstar_mcp` 저장소에서 Python으로 1차 구현. WP `W://root/mcp_server` 추적.
> **작성일**: 2026-04-27 (구현 결정 갱신: 2026-04-29)
> **결정 근거**: `internal/` 디렉토리 내 검토 자료. 구현 진행 상황은 `loadstar_mcp/.loadstar/WAYPOINT/root.mcp_server.md` 참조.

---

## 1. 배경 및 동기

LOADSTAR는 현재 Claude Code 환경에서 **`Read .loadstar/*.md` + `Bash loadstar ...`** 조합으로 충분히 사용 가능하다. 그러나 다음 환경에서는 Bash/파일시스템 접근이 제한되거나 부재하므로 MCP 노출이 필요해진다.

| 환경 | Read | Bash | MCP |
|:---|:---:|:---:|:---:|
| Claude Code (CLI) | ✅ | ✅ | (있어도 됨) |
| Claude Desktop | ❌ | ❌ | ✅ |
| Cursor / Cline / Continue | 부분 | 부분 | ✅ |
| 웹 Claude.ai | ❌ | ❌ | ✅ |

→ **MCP의 주된 가치는 AI 효율이 아니라 클라이언트 이식성·외부 배포**다. Claude Code 단독 사용이라면 MCP 구현의 우선순위는 낮다.

---

## 2. 구현 언어 및 전송 방식

- **언어: Python** (1차 구현 결정, 2026-04-29) — 공식 MCP Python SDK가 가장 성숙하고 외부 기여자 진입 장벽이 낮음. 얇은 래퍼(§3) 원칙상 언어가 정확도에 영향을 주지 않음.
- **전송 방식: stdio** — 1차. 로컬 사용 표준.
- 이후 팀 공유/원격 사용 수요 발생 시 **Streamable HTTP** 추가 (MCP SDK가 두 전송 방식을 동시 지원).

### 2.1 Go 포팅 가능성 (보존)

초기 검토에서는 Go를 권장했으나(loadstar_cli 코드 재사용·단일 바이너리 배포), 다음 이유로 Python 1차 구현으로 변경:

1. 공식 MCP SDK 성숙도 (Python > Go 3rd-party)
2. prototype 단계에서 외부 사용자 진입 장벽 최소화 우선
3. 얇은 래퍼라 subprocess 방식이 동작 정확도에 영향 없음

도구명·파라미터·JSON 스키마는 **언어 중립적으로 설계**하여, 외부 사용 검증 후 Go 포팅이 필요해지면 외부 클라이언트 영향 없이 교체 가능하도록 한다.

---

## 3. 구현 방식

**CLI 얇은 래퍼** 원칙:
- 새 비즈니스 로직을 만들지 않는다. 기존 CLI 명령을 호출하고 출력을 JSON으로 정형화한다.
- CLI 정확도 = MCP 정확도. CLI에서 검증한 동작이 MCP에서도 유지된다.
- 단, `get_waypoint` / `get_map` / `get_spec`은 CLI에 대응 명령이 없으므로 직접 파일 읽기로 구현한다.

---

## 4. 노출 도구 목록

### CLI 래핑 도구

| MCP 도구 | 대응 CLI | 용도 |
|:---|:---|:---|
| `loadstar_show` | `loadstar show [FILTER]` | WP 목록 조회 (필터링) |
| `loadstar_validate` | `loadstar validate` | 깨진 참조 검증 |
| `loadstar_todo_list` | `loadstar todo list` | PENDING/ACTIVE/BLOCKED 목록 |
| `loadstar_todo_history` | `loadstar todo history [MAP]` | TECH_SPEC 완료 이력 |
| `loadstar_log` | `loadstar log [TIME] [FILTER]` | 로그 조회 |
| `loadstar_log_add` | `loadstar log add ...` | 로그 기록 |
| `loadstar_question` | `loadstar question [FILTER]` | OPEN_QUESTIONS 조회 |

### 직접 파일 읽기 도구 (CLI 미존재)

| MCP 도구 | 동작 |
|:---|:---|
| `loadstar_get_waypoint(address)` | 단일 WP 파일 파싱 → JSON (CODE_MAP.scope 포함) |
| `loadstar_get_map(address)` | Map 파일 파싱 → JSON |
| `loadstar_get_spec(section?)` | loadstar_SPEC 문서 반환 (전체 또는 섹션) |

#### `loadstar_get_spec` 섹션 매핑 (예시)

```
section="master"  → 01.MASTER_GUIDE.md
section="schema"  → 02.SCHEMA_DEF.md
section="address" → 03.ADDRESS_CONVENTION.md
section="storage" → 04.STORAGE.md
section="format"  → 05.ELEMENT_FORMAT.md
section="cli"     → 06.CLI_SPEC.md
section="todo"    → 07.TODO_SPEC.md
section="meta"    → 08.META_SYNC.md
section=null      → 전체 문서 일괄 반환
```

> 외부 클라이언트(Claude Desktop 등) 사용자가 SPEC 본문에 직접 접근할 수 없는 경우를 위함. AI 세션 시작 시 컨텍스트 복원에 사용.

---

## 5. 의도적으로 제외하는 도구

| 도구 | 제외 사유 |
|:---|:---|
| `loadstar_check` | 2026-04-24 CLI 자체 제거. **"코드↔WP 정합성 의도는 폐기됨"** — 단순 보류 아닌 철학적 결정. MCP에서도 영구 제외. |
| `loadstar_init` | 1회성 초기화. AI가 사용할 일 없음. |
| `loadstar_todo_sync` | CLI 내부 캐시 관리용. AI는 결과(`todo list`)만 보면 됨. |

---

## 6. 도구 description 설계 가이드

MCP 도구 description에 워크플로우 순서를 인코딩하여 AI가 자연스럽게 LOADSTAR 흐름을 따르도록 한다.

예시:
```
loadstar_get_waypoint:
  "단일 WayPoint를 조회한다. 코드 작업 착수 전 반드시 호출하여
   CODE_MAP.scope, TECH_SPEC, STATUS를 확인한다.
   scope는 후속 LSP/grep 호출 시 탐색 범위로 전달한다."
```

CLAUDE.md가 닿지 않는 외부 클라이언트에서도 도구 description이 가이드 역할을 한다.

---

## 7. 미해결 항목 (구현 시 결정)

- **인증**: 로컬 stdio 기준 불필요. HTTP 추가 시 토큰 또는 핸드셰이크 필요.
- **다중 프로젝트 지원**: 한 MCP 인스턴스가 여러 `.loadstar/` 디렉토리를 서빙할지 (workspace 개념) 단일만 지원할지.
- **캐싱**: 파일 시스템 변경 감지 후 무효화 전략. 단순 무캐싱으로 시작 권장.
- **에러 형식**: MCP 표준 에러 vs 도메인 에러 코드. SDK 디폴트 따르는 게 안전.

---

## 8. 구현 진입 조건 (충족 → 진행 결정)

다음 조건은 v1.3.13 공개 시점에 검토되어 **2번이 활성화**됨:
1. Claude Desktop / Cursor / Cline 사용자에게 LOADSTAR 배포 수요 발생
2. **[충족]** 외부 사용자에게 단일 명령으로 설치 가능하게 만들 필요 → `uvx loadstar-mcp` 목표
3. CLI Bash 호출 비용이 측정상 유의미하게 큰 것으로 확인 (EFFECTIVENESS_METRICS M1)

→ 2026-04-29 WayPoint `W://root/mcp_server` 등록 후 구현 착수.

---

## 9. 리뷰 이력

| 날짜 | 내용 | 작성자 |
|:---|:---|:---|
| 2026-04-27 | 초안 작성. AI 효율 도구가 아닌 이식성 도구로 위치 재정의, `loadstar_check` 영구 제외, `get_spec` 신규 추가 | AI (Opus 4.7) |
| 2026-04-29 | 상태 DEFERRED → 구현 진행 중. 언어 결정 Go → Python (공식 SDK 성숙도, 외부 진입 장벽 우선). Go 포팅 가능성은 §2.1로 보존. WP `W://root/mcp_server` 등록 | AI (Opus 4.7) |
