<WAYPOINT>
## [ADDRESS] W://root/initial_spec_v1_3_12
## [STATUS] S_STB

### IDENTITY
- SUMMARY: LOADSTAR SPEC 초기 정립 (v0 → v1.3.12) — 핵심 개념, 주소 체계, 요소 포맷, CLI/UI 통합 가이드의 9개 문서 정의 및 검증
- METADATA: [Priority: P1, Created: 2026-02-26]
- SYNCED_AT: 2026-04-28

### CONNECTIONS
- PARENT: M://root
- CHILDREN: []
- REFERENCE: []

### TODO
- ADDRESS: W://root/initial_spec_v1_3_12
- SUMMARY: 약 2개월 동안 SPEC 본문(01~09) 정립, CLI/UI 레퍼런스 구현과 동기 진화, Decision 패턴 도입 등 v1.3.12 공개 직전까지의 정합성 정리
- TECH_SPEC:
  # TASK
  - [x] 2026-03-05 01.MASTER_GUIDE — 시스템 철학, AI 행동 강령, Tolerable Consistency 정립
  - [x] 2026-03-08 02.SCHEMA_DEF — STATUS 코드, Link 타입, OPEN_QUESTIONS 상태, SYNCED_AT 규칙
  - [x] 2026-03-10 03.ADDRESS_CONVENTION — `M://`, `W://` 주소 체계 및 물리 파일 경로 변환 규칙
  - [x] 2026-03-12 04.STORAGE — `.loadstar/` 디렉토리 구조, `.clionly/` 분리, Git 연동
  - [x] 2026-03-18 05.ELEMENT_FORMAT — Map/WayPoint 포맷, TECH_SPEC TASK/RECURRING, Decision/LOADSTAR_INIT
  - [x] 2026-03-22 06.CLI_SPEC — init/show/todo/log/validate/question 명령 명세
  - [x] 2026-04-02 history/diff/rollback/link 등 git 대체 가능 명령 제거
  - [x] 2026-04-08 checkpoint·monitor·todo add/update/done/delete 제거 — sync 기반으로 전환
  - [x] 2026-04-08 07.TODO_SPEC — WP STATUS 기반 자동 동기화 규격 분리
  - [x] 2026-04-08 08.META_SYNC — 프롬프트/CLAUDE.md 중심 메타 동기화 전략 확정
  - [x] 2026-04-10 findlog → log 통합, 로그 KIND 정의
  - [x] 2026-04-14 LOADSTAR_INIT.md 포맷 정의
  - [x] 2026-04-24 CodeBrief 개념 폐기, check 명령 제거
  - [x] 2026-04-24 Decision 파일 패턴(05.ELEMENT_FORMAT Decision 섹션) 정립
  - [x] 2026-04-27 09.AI_TOOL_INTEGRATION — CODE_MAP.scope 활용, 외부 LSP/grep/MCP 통합 가이드
  - [x] 2026-04-28 internal/MCP_DESIGN_DRAFT — 외부 배포 시점 MCP 설계 초안 보존

### ISSUE
- OPEN_QUESTIONS: []

### COMMENT
- 본 WP는 v1.3.12 공개 직전 시점에 소급 등록된 초기 정립 기록이다. 세부 변경 이력은 각 SPEC 문서의 "리뷰 이력" 섹션과 git 로그를 정본으로 한다.
- 후속 작업은 W://root/spec_v1_3_13_patch 에서 추적한다.
</WAYPOINT>
