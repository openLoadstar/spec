> 🌐 **[English](README.md)** | **한국어**

# LOADSTAR SPEC

**Version: v1.6.0** (2026-05-11, prototype)

AI 에이전트와 사람이 공유하는 프로젝트 메타데이터 관리 방법론. 코드 수정 의도와 작업 단위를 **WayPoint** 로 추적하고, 탐색 비용을 최소화하기 위해 **주소(URI) 기반 핀포인트 접근**을 원칙으로 한다.

> **⚠️ 프로토타입**
> 본 문서·CLI·UI는 개념 검증 단계의 프로토타입입니다. 피드백과 개선 제안을 환영합니다.

> **📢 레퍼런스 환경**
> CLI·UI 레퍼런스 구현은 **Claude Code** 기준으로 작성되어 있습니다. SPEC 본문은 도구 중립적이지만, 메타 동기화 메커니즘(CLAUDE.md, Hook 등)은 Claude Code 환경을 전제합니다. 다른 AI 환경에서도 **동등한 동기화 장치는 필수**입니다 — 상세는 `08.META_SYNC.md` 참조.

---

## 📂 문서 구성

| 파일 | 내용 |
| :--- | :--- |
| [01.MASTER_GUIDE](01.MASTER_GUIDE.md) | 시스템 철학, 핵심 요소, AI 행동 강령, 자원 최적화 규약 |
| [02.SCHEMA_DEF](02.SCHEMA_DEF.md) | 상태 코드, Link 타입, TODO 체크박스, SYNCED_AT 규칙 |
| [03.ADDRESS_CONVENTION](03.ADDRESS_CONVENTION.md) | URI 주소 체계 (`M://`, `W://`, `D://`) 및 물리 파일 경로 변환 |
| [04.STORAGE](04.STORAGE.md) | 디렉토리 구조, 파일 명명, Git 연동 규약 |
| [05.ELEMENT_FORMAT](05.ELEMENT_FORMAT.md) | Map/WayPoint/dwp/LOADSTAR_INIT/Decision 포맷, GOAL 슬롯, TODO 아카이브, RECURRING 항목 규약 |
| [06.CLI_SPEC](06.CLI_SPEC.md) | CLI 명령어 명세 (`init`, `show`, `todo`, `log`, `question`, `validate`) |
| [07.TODO_SPEC](07.TODO_SPEC.md) | TODO 시스템 규격 — WayPoint STATUS 기반 자동 동기화 |
| [08.META_SYNC](08.META_SYNC.md) | 메타 동기화 전략 (프롬프트 + CLAUDE.md + Hook + 사후검증) |
| [09.AI_TOOL_INTEGRATION](09.AI_TOOL_INTEGRATION.md) | 외부 AI 도구(LSP, grep, MCP) 통합 가이드 — CODE_MAP.scope 활용 패턴, 안티패턴, CLAUDE.md 템플릿 |

### 참고 자료
- [examples/WP_TEMPLATE.md](examples/WP_TEMPLATE.md) — WayPoint 생성용 표준 템플릿
- [examples/DWP_TEMPLATE.md](examples/DWP_TEMPLATE.md) — Data WayPoint(dwp) 생성용 표준 템플릿
- [examples/root_map.md](examples/root_map.md) — 루트 Map 예시
- [examples/decision_sample.md](examples/decision_sample.md) — Decision 기록 예시
- [internal/](internal/) — 설계 검토 드래프트 (**SPEC 본문 아님**, AI 도구는 로딩 제외)

---

## 🧭 핵심 개념

- **Map (M://)** — WayPoint 탐색을 위한 구조적 길잡이. 계층만 표현하며 작업 주체가 되지 않는다. 하위 트리의 큰 의도를 담는 **GOAL** 슬롯을 가진다.
- **WayPoint (W://)** — 모든 작업의 실행 단위. IDENTITY / CONNECTIONS / CODE_MAP / TODO / ISSUE 로 구성. 해당 WP가 달성해야 할 단일 의도를 담는 **GOAL** 슬롯을 가진다.
- **Data WayPoint (D://)** — 코드와 독립적으로 변화하는 데이터 아티팩트(설정 파일, 참조 데이터, 정적 상태)에 대한 메타 레코드. `.loadstar/DATA_WAYPOINT/`에 저장. `loadstar validate`가 ORPHAN / DANGLING dwp를 감지한다.
- **GOAL** — Map과 WayPoint 양쪽에 존재하는 *의도* 필드. SUMMARY(정체성)·TODO(실행)와 구분된다. Map은 넓은 목표, WayPoint는 부모 Map GOAL에서 파생된 좁은 목표를 기술한다. Goals Report 화면에서 의도 계층을 한 화면에 조망할 수 있다.
- **CODE_MAP** — WayPoint 내 섹션. 코드 수정 작업의 탐색 범위(scope)를 디렉토리 단위로 한정.
- **Link / SavePoint** — 논리적 관계 vs 물리적 위치의 엄격한 분리.
- **Tolerable Consistency** — 완전 일관성 대신 "드리프트를 알고 있는 상태"를 목표로 한다.
- **TASK / RECURRING** — 1회성 구현 항목(`[ ]` / `[x]`) vs 코드 변경 시마다 재수행하는 검증 항목(`(R)`).
- **OPEN_QUESTIONS / Decision** — AI가 제기한 미결 질문(`[Q{N}]`)과, 사람의 판단이 남긴 결정 근거 파일(`.loadstar/DECISIONS/`). AI 세션 간 "왜 이렇게 결정했는가"를 보존한다.

## 🛠 참여 프로젝트

- 🌐 **[openLoadstar](https://github.com/openLoadstar/openLoadstar)** — 전체 생태계 안내 (설치 흐름·AI 진입 프롬프트·빠른 시작)
- **[loadstar_cli](https://github.com/openLoadstar/cli)** — Go 기반 CLI (`init`, `show`, `todo`, `log`, `validate`, `question`)
- **[loadstar_ui](https://github.com/openLoadstar/ui)** — Spring Boot + React 기반 Explorer UI
- **[loadstar_mcp](https://github.com/openLoadstar/mcp)** — Python 기반 MCP 서버 (Claude Desktop·Cursor 등 외부 AI 클라이언트 연동)

---

## 📮 기여 / 보안

- 🤝 **기여 가이드**: [openLoadstar/CONTRIBUTING.ko.md](https://github.com/openLoadstar/openLoadstar/blob/main/CONTRIBUTING.ko.md)
- 🔒 **보안 신고**: [openLoadstar/SECURITY.ko.md](https://github.com/openLoadstar/openLoadstar/blob/main/SECURITY.ko.md) — GitHub Security Advisories를 우선 사용해 주세요.
- 💬 **질문·아이디어**: [GitHub Discussions](https://github.com/openLoadstar/openLoadstar/discussions)

---

## 📜 라이선스

Apache License 2.0 — [LICENSE](LICENSE) 참조.
