> 🌐 **[English](README.md)** | **한국어**

# LOADSTAR SPEC 2.0

**Version: 2.0** (2026-08-04, draft)

AI 에이전트와 사람이 공유하는 프로젝트 메타데이터 관리 방법론. 작업 단위와 데이터 정의를 평범한 md 파일로 두고, **파일명을 유일한 신원**으로 삼는다. 빠른 조회에 필요한 것들은 그 md에서 **추출한 파생 캐시**(언제든 재생성 가능한 SQLite)로만 관리한다.

> **⚠️ Draft**
> 2.0은 [SPEC 1.0](../SPEC%201.0/README.ko.md)의 증분 개정이 아니라 그것을 대체하는 재설계입니다. 아직 열려 있는 부분이 있습니다 — `03.SCHEMA_DEF.md`는 미작성이고, 미결 사항은 `04.META_EXTRACTION.md §10`에 모여 있습니다. 피드백과 개선 제안을 환영합니다.

---

## 🔄 1.0에서 달라진 점

2.0은 **실제로 쓰인 것만 남기고, 그 자체가 또 하나의 동기화 대상이 되어버린 것들을 걷어낸** 버전이다. 아래는 전부 의도적으로 제거한 것들이다.

| 2.0에서 걷어낸 것 | 이유 | 어디로 갔나 |
| :--- | :--- | :--- |
| **주소(URI) 체계** (`M://`, `W://`, `D://`)와 주소 → 파일 경로 변환 표 | 파일시스템과 따로 맞춰줘야 하는 이름 계층이 하나 더 있는데, 그만한 조회 이득이 없었다 | 파일명이 곧 신원이고, 참조는 대상 파일명을 그대로 쓴다 (`02.ELEMENT_FORMAT.md §3`, §4) |
| **Map(`M://`)** — 필수 계층 | 계층에 의미가 없는 경우에도 모든 WayPoint를 Map 아래에 매달아야 했다 | **선택적** 조직화 컨테이너 `GROUP`으로 대체 — 어느 GROUP에도 속하지 않아도 된다 (`appendix/GROUP.md`) |
| **CODE_MAP** 슬롯 | 실제 활용도가 불명확했다 | 제거(2026-07-27). 코드 탐색 범위 안내가 다시 필요해지면 재검토 |
| **SYNCED_AT** 슬롯 | 사람이 손으로 맞춰야 하는 타임스탬프는 드리프트를 막는 장치가 아니라 드리프트 그 자체다 | 제거 — 변경 이력의 단일 소스는 git |
| **Decision/ADR 파일 체계**와 **OPEN_QUESTIONS**(`[Q{N}]`, DEFERRED/CONFIRMED) | 질문 번호·상태·별도 파일 간 정합성이 또 하나의 동기화 문제가 됐고, 1.0에서 거의 쓰이지 않았다 | 한 곳으로 — 해당 요소의 `ISSUE`에 자유 형식 텍스트 (`01.MASTER_GUIDE.md §4.1`) |
| **`.clionly/LOG/`** (요소별 변경 이력 인덱스) | git 옆에 따로 쓰는 로그는 git과 어긋날 수 있다 | git만 남긴다. 인덱스의 `history`는 `git log`를 읽어 채우는 미러일 뿐 직접 쓰지 않는다 (`04.META_EXTRACTION.md §4`) |
| **`.clionly/TODO/TODO_LIST.md`** (실체화된 TODO 목록) | 캐싱된 작업 상태는 원본이 바뀔 때마다 다시 맞춰야 한다 | 조회 시점에 WP md를 직접 읽어 계산 (`04.META_EXTRACTION.md §7`) |
| **GD(Good Dopamin)**, `COMMON/`, `NOTICE/`, `MONITOR/` | 구현되지 않았거나, 쓰이지 않았다 | 제거 |
| **`TODO_SPEC` / `META_SYNC` / `AI_TOOL_INTEGRATION` 별도 문서** | 특정 요소 타입에만 해당하는 규칙이 최상위 문서일 필요가 없다 | FORMAT별 부록으로 흡수. AI 운영 원칙은 한 개 섹션으로 (`01.MASTER_GUIDE.md §6`) |

그리고 2.0이 **더한** 것 하나: md 위에 얹은 메타 추출 파이프라인과 SQLite 파생 캐시(`04.META_EXTRACTION.md`). 덕분에 도구가 전체 파일을 훑지 않고도 날짜·타입·키워드·관계 기준으로 프로젝트를 조회할 수 있고, 그러면서도 원본은 여전히 md 하나다.

| 1.0 | 2.0 |
| :--- | :--- |
| `.loadstar/{MAP,WAYPOINT,DATA_WAYPOINT,DECISIONS,GD,COMMON,.clionly}/` | `.loadstar/{WP,DWP,GROUP,OTHER,FLOW}/` + `.loadstar/.cache/index.db` (git 제외, 재생성 가능) |
| 주소 → 디렉토리 매핑 표 | `FORMAT` 값이 곧 폴더명 |
| 스펙 문서 9개 | 스펙 문서 5개 + FORMAT별 부록 |

---

## 📂 문서 구성

| 파일 | 내용 |
| :--- | :--- |
| [01.MASTER_GUIDE](01.MASTER_GUIDE.md) | 목적, 원본과 파생의 분리, Tolerable Consistency, 요소 모델, 이력 관리, AI 운영 원칙 |
| [02.ELEMENT_FORMAT](02.ELEMENT_FORMAT.md) | 모든 요소 공통 규칙 — 명명, 신원, 참조 방식, 공통 봉투, 요소 카탈로그, 물리 저장 경로 |
| [03.SCHEMA_DEF](03.SCHEMA_DEF.md) | 공통 어휘(상태 코드, 체크박스 규약, URL 스킴) — ⚠️ 미작성 |
| [04.META_EXTRACTION](04.META_EXTRACTION.md) | 추출 파이프라인(구조 추출기 / AI 보강 / 온디맨드 도메인 조회기), DB 스키마, Validator, 미결 사항 |
| [05.CLI_SPEC](05.CLI_SPEC.md) | CLI 명령 규격 (`create`, `show`, `reindex`, `validate`, 그리고 `todo` / `issues` ⚠️ 미구현) |

### 부록 — FORMAT 하나당 하나

| 파일 | 요소 |
| :--- | :--- |
| [appendix/WP.md](appendix/WP.md) | **WayPoint** — 모든 작업의 실행 단위. `STATUS` / `GOAL` / `TODO`, 하위 WayPoint |
| [appendix/DWP.md](appendix/DWP.md) | **Data WayPoint** — 데이터의 개념적 자기소개. TODO·GOAL 없음, `TABLES`는 선택 |
| [appendix/GROUP.md](appendix/GROUP.md) | **Group** — 선택적 카테고리 컨테이너. `CONNECTIONS.ITEMS`만 갖는다 |
| [appendix/OTHER.md](appendix/OTHER.md) | **Other** — 조직화하고 싶은 자유 형식 파일. 명명 규칙과 공통 봉투가 면제되는 유일한 FORMAT |
| [appendix/FLOW.md](appendix/FLOW.md) | **Flow** — 업무·처리 흐름을 mermaid 그림 한 장으로. 각 노드는 WP / DWP / 다른 FLOW를 가리킬 수 있다 |

새 요소 타입은 부록을 하나 추가하는 것으로 확장한다 — 공통 규칙은 건드리지 않는다.

---

## 🧭 핵심 개념

- **요소(Element)** — 모든 작업 단위·데이터 정의는 `[FORMAT][VER][DATE]이름.md` 형식의 md 파일 한 개다. 구조화된 필드를 앞에 몰아둬서, 자유 텍스트인 이름에 대괄호가 들어가도 파싱 경계가 흔들리지 않는다.
- **파일명이 유일한 신원** — 별도 주소 체계도, 파일 내부의 중복 식별 라인도 없다. 요소 간 참조는 대상 파일명을 그대로 적고, `FORMAT` 접두어로 어느 폴더를 찾을지 판단한다.
- **원본과 파생의 분리** — md가 유일한 원본이다. SQLite는 거기서 추출한 메타만 담는 파생 캐시이며 언제든 재생성 가능해야 한다. 계층·그룹 뷰도 `CONNECTIONS`를 근거로 계산해내는 파생 뷰지, 따로 유지하는 인덱스 파일이 아니다.
- **Tolerable Consistency** — 코드와 메타데이터의 완전 일관성은 목표가 아니다. 목표는 **"드리프트를 알고 있는 상태"** — 매 수정마다 막는 대신, 검증 패스가 어긋난 지점을 발견 가능하게 만든다.
- **STATUS** — `S_IDL` 대기 · `S_PRG` 진행 중 · `S_STB` 완료·안정 · `S_ERR` 오류 · `S_REV` 검토 필요 · `S_OOS` 범위 제외. 진행 상태의 단일 출처이며 WayPoint에만 있다.
- **SUMMARY / GOAL / TODO** — 각각 다른 질문에 답한다: 이게 무엇인가, 무엇을 달성하려 하는가, 그러기 위한 구체 작업은 무엇인가. GOAL이 길어지면 하위 WayPoint로 쪼개라는 신호다.
- **GROUP은 선택적이고, 방향이 하나다** — GROUP만 자기 멤버를 안다. WP/DWP는 자신이 어느 GROUP에 속하는지 기록하지 않는다. 소속 변경은 오직 GROUP의 `ITEMS`를 고치는 것으로만 이뤄진다.
- **ISSUE** — 설계 시점 제약, 미결정·미해결 사항을 자유 형식으로 남기는 단 하나의 자리. 질문 번호도, 별도 결정 파일도 없다.
- **이력은 git뿐** — 옆에 따로 쓰는 로그 파일을 두지 않는다. 인덱스의 `history` 테이블은 `git log`의 미러다.
- **추출 파이프라인** — ① 결정론적 구조 추출기(파일명 필드 + `SUMMARY` + `CONNECTIONS` + 마크다운 문법 차원의 사실), ② AI 보강 단계(키워드·다각도 요약), ③ 온디맨드 도메인 조회기 — `STATUS`/`TODO`/`ISSUE`는 캐싱하지 않고 조회 시점에 md를 직접 읽어 계산한다.

## 🛠 관련 프로젝트

- 🌐 **[openLoadstar](https://github.com/openLoadstar/openLoadstar)** — 생태계 전체 안내 (설치 흐름 · AI 진입 프롬프트 · 빠른 시작)
- **[loadstar_ui](https://github.com/openLoadstar/ui)** — Go + Wails 데스크톱 탐색기, SPEC 2.0 레퍼런스 구현. 같은 실행 파일이 2.0 CLI를 겸한다 (`05.CLI_SPEC.md §1`)
- **[loadstar_cli](https://github.com/openLoadstar/cli)** — SPEC 1.0용 CLI (`init`, `show`, `todo`, `log`, `validate`, `question`)
- **[loadstar_mcp](https://github.com/openLoadstar/mcp)** — Python 기반 MCP 서버 (Claude Desktop, Cursor 등 외부 AI 클라이언트용)

---

## 📮 기여 / 보안

- 🤝 **기여 가이드**: [openLoadstar/CONTRIBUTING.md](https://github.com/openLoadstar/openLoadstar/blob/main/CONTRIBUTING.md)
- 🔒 **보안 취약점 신고**: [openLoadstar/SECURITY.md](https://github.com/openLoadstar/openLoadstar/blob/main/SECURITY.md) — GitHub Security Advisories를 이용해 주세요.
- 💬 **질문 & 아이디어**: [GitHub Discussions](https://github.com/openLoadstar/openLoadstar/discussions)

---

## 📜 License

Apache License 2.0 — [LICENSE](../LICENSE) 참조.
