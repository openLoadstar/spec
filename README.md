# LOADSTAR SPEC

**Version: v1.3.10** (2026-04-24)

AI 에이전트와 사람이 공유하는 프로젝트 메타데이터 관리 방법론. 코드 수정 의도와 작업 단위를 **WayPoint** 로 추적하고, 탐색 비용을 최소화하기 위해 **주소(URI) 기반 핀포인트 접근**을 원칙으로 한다.

---

## 📂 문서 구성

| 파일 | 내용 |
| :--- | :--- |
| [01.LOADSTAR_MASTER_GUIDE](01.LOADSTAR_MASTER_GUIDE.md) | 시스템 철학, 핵심 요소, AI 행동 강령, 자원 최적화 규약 |
| [02.SCHEMA_DEF](02.SCHEMA_DEF.md) | 상태 코드, Link 타입, TECH_SPEC 체크박스, SYNCED_AT 규칙 |
| [03.ADDRESS_CONVENTION](03.ADDRESS_CONVENTION.md) | URI 주소 체계 (`M://`, `W://`) 및 물리 파일 경로 변환 |
| [04.LOADSTAR_STORAGE](04.LOADSTAR_STORAGE.md) | 디렉토리 구조, 파일 명명, Git 연동 규약 |
| [05.ELEMENT_FORMAT](05.ELEMENT_FORMAT.md) | Map/WayPoint/LOADSTAR_INIT 포맷 정의, TECH_SPEC 아카이브 |
| [07.WP_TEMPLATE](07.WP_TEMPLATE.md) | WayPoint 생성용 표준 템플릿 |
| [08.LOADSTAR_CLI](08.LOADSTAR_CLI.md) | CLI 명령어 명세 (`init`, `show`, `todo`, `log`, `validate`) |
| [09.FLOW_CATALOG](09.FLOW_CATALOG.md) | 프로젝트 흐름 유형 레지스트리 |
| [10.MAP_ROOT](10.MAP_ROOT.md) | 루트 Map 예시 |
| [11.TODO_SPEC](11.TODO_SPEC.md) | TODO 시스템 규격, WayPoint STATUS 기반 자동 동기화 |
| [12.EFFECTIVENESS_METRICS](12.EFFECTIVENESS_METRICS.md) | 방법론 효과 측정 지표 (M1~M5) |
| [13.MONITOR_SPEC](13.MONITOR_SPEC.md) | 메타 동기화 전략 (프롬프트 + CLAUDE.md + Hook + 사후검증) |

---

## 🧭 핵심 개념

- **Map (M://)** — WayPoint 탐색을 위한 구조적 길잡이. 계층만 표현하며 작업 주체가 되지 않는다.
- **WayPoint (W://)** — 모든 작업의 실행 단위. IDENTITY / CONNECTIONS / CODE_MAP / TECH_SPEC / ISSUE 로 구성.
- **CODE_MAP** — WayPoint 내 섹션. 코드 수정 작업의 탐색 범위(scope)를 디렉토리 단위로 한정.
- **Link / SavePoint** — 논리적 관계 vs 물리적 위치의 엄격한 분리.
- **Tolerable Consistency** — 완전 일관성 대신 "드리프트를 알고 있는 상태"를 목표.

## 🛠 참여 프로젝트

- **loadstar_cli** — Go 기반 CLI (`init`, `show`, `todo`, `log`, `validate`)
- **loadstar_ui** — Spring Boot + React 기반 Explorer UI

---

## 📜 라이선스

Apache License 2.0 — [LICENSE](LICENSE) 참조.
