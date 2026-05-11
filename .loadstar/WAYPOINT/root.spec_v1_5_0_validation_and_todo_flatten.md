<WAYPOINT>
## [ADDRESS] W://root/spec_v1_5_0_validation_and_todo_flatten
## [STATUS] S_STB

### IDENTITY
- SUMMARY: SPEC v1.4.0 → v1.5.0 — 검증 명세 보강(dwp/D:// 검증 + 역방향 정합성) 및 TODO/TECH_SPEC 통합(평탄화). WP/dwp 파일 마이그레이션과 외부 텍스트 표면 갱신 포함.
- METADATA: [Priority: P1, Created: 2026-05-11]
- SYNCED_AT: 2026-05-11

### CONNECTIONS
- PARENT: M://root
- CHILDREN: []
- REFERENCE: [W://root/spec_v1_4_0_dwp_introduction]

### CODE_MAP
- scope:
  - ./

### TODO
# TASK — SPEC 본문 패치 (검증)
- [x] 2026-05-11 06.CLI_SPEC.md §6 — validate에 dwp(D://) 검증 명시: WAYPOINTS의 D:// 파일 존재 확인, dwp의 PARENT 검증
- [x] 2026-05-11 06.CLI_SPEC.md §6 — 역방향 정합성 검증 추가: WP/dwp.PARENT가 가리키는 Map의 WAYPOINTS에 본인 등록 여부 / Map.WAYPOINTS의 자식 PARENT 일치 여부
- [x] 2026-05-11 08.META_SYNC.md — 검증 절차 설명에 dwp/역방향 항목 반영

# TASK — SPEC 본문 패치 (TODO 평탄화)
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — TODO 섹션 평탄화: ADDRESS/SUMMARY 제거, TECH_SPEC 래퍼 제거, TASK/RECURRING 헤더 평탄화
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — "TECH_SPEC 아카이브 규칙" → "TODO 아카이브 규칙" 개명 및 본문 갱신
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — dwp 작성 원칙의 "TODO/TECH_SPEC 불보유" 문구를 "TODO 불보유"로 정리
- [x] 2026-05-11 07.TODO_SPEC.md — TECH_SPEC 용어 정리
- [x] 2026-05-11 02.SCHEMA_DEF.md — TECH_SPEC 용어 정리
- [x] 2026-05-11 examples/WP_TEMPLATE.md — 신규 포맷 적용
- [x] 2026-05-11 examples/DWP_TEMPLATE.md — TECH_SPEC 미사용 확인 (변경 불필요)
- [x] 2026-05-11 09.AI_TOOL_INTEGRATION.md — TECH_SPEC 용어 정리

# TASK — 메타데이터 / 버전
- [x] 2026-05-11 README.md / README.ko.md — v1.4.0 → v1.5.0, Document Index 용어 정리
- [x] 2026-05-11 M://root에 본 WP 등록, SYNCED_AT 갱신

# TASK — WP 파일 마이그레이션 (loadstar_SPEC/cli/ui/mcp)
- [x] 2026-05-11 모든 .loadstar/WAYPOINT/*.md의 TODO 섹션 평탄화 (26개 파일, migrate_todo.py로 일괄 처리)
- [x] 2026-05-11 마이그레이션 후 네 프로젝트에서 `loadstar validate` 통과 확인 — loadstar_SPEC (4 wp, 1 map), loadstar_cli (11 wp, 3 maps), loadstar_ui (35 wp, 5 maps), loadstar_mcp (1 wp, 1 map)

# TASK — 외부 텍스트 표면 갱신 (동작 무영향, 용어 정리)
- [x] 2026-05-11 워크스페이스 루트 CLAUDE.md — TECH_SPEC 표현을 TODO로 정리
- [x] 2026-05-11 loadstar_cli/CLAUDE.md, loadstar_mcp/CLAUDE.md, loadstar_ui/CLAUDE.md — TECH_SPEC 표현 정리
- [x] 2026-05-11 loadstar_cli/cmd/todo.go — 도움말 텍스트("completed TODO items") 갱신, OR 파싱 조건은 legacy 호환을 위해 유지
- [x] 2026-05-11 loadstar_cli/internal/storage/fs.go — Hook 리마인더 텍스트 갱신
- [x] 2026-05-11 loadstar_mcp/src/loadstar_mcp/server.py — tool description의 "TECH_SPEC" → "TODO"
- [x] 2026-05-11 loadstar_ui/frontend TodoView.tsx, WayPointEditor.tsx — 사용자 노출 라벨 및 주석 갱신 (변수명 techSpecItems 등은 후속 리네임 WP로 분리)
- [x] 2026-05-11 loadstar_ui/backend WayPointDetailResponse.java, ScheduleService.java — 코멘트 정리
- [x] 2026-05-11 .claude/hooks/loadstar-drift-check.sh (워크스페이스/각 프로젝트 3개) — 리마인더 텍스트 갱신

# RECURRING
- (R) SPEC 변경 후 README 버전 표기 동기화 확인
- (R) loadstar_SPEC / loadstar_cli / loadstar_ui / loadstar_mcp 네 프로젝트에서 `loadstar validate` 통과 확인

### ISSUE
- OPEN_QUESTIONS: []
- 본 WP는 SPEC 본문 + 메타 + 마이그레이션 + 외부 표면 갱신까지 포함. CLI 검증 로직 자체(dwp/역방향)를 실제 구현하는 작업은 loadstar_cli의 별도 WP로 분리한다.
- 프론트엔드 변수명 리네임(techSpecItems → todoItems 등)은 본 WP에서 다루지 않음. 동작 영향 없는 표면 라벨/주석만 정리.

### COMMENT
- 평탄화 결정 핵심:
  - TODO 컨테이너의 ADDRESS/SUMMARY는 WP의 동일 필드와 1:1 중복이라 제거.
  - TECH_SPEC 래퍼는 의미 없는 1:1 중첩이므로 제거하고 TASK/RECURRING 헤더로 평탄화.
  - loadstar_cli/todo.go와 loadstar_ui/ElementParser.java가 이미 legacy 호환을 가지고 있어 동작 회귀 없음.
- 버전 정책: 호환성 깨는 포맷 변경은 minor bump (v1.4.0 → v1.5.0).
</WAYPOINT>
