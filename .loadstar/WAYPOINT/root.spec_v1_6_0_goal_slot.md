<WAYPOINT>
## [ADDRESS] W://root/spec_v1_6_0_goal_slot
## [STATUS] S_STB

### IDENTITY
- SUMMARY: SPEC v1.5.0 → v1.6.0 — WP/Map에 GOAL 섹션 신설 (선택 항목). 의도(GOAL) 표현을 정체성(SUMMARY) 및 작업(TODO)과 분리하여 추적성 향상.
- METADATA: [Priority: P1, Created: 2026-05-11]
- SYNCED_AT: 2026-05-11

### GOAL
LOADSTAR에서 "이 요소가 무엇을 달성하려 하는가"를 1급 슬롯으로 표현하여, 기획→구현→검토 흐름의 의도가 분산되지 않게 한다. WP 단위에서 TODO 항목이 GOAL을 충실히 구현하는지 사후 검토가 가능해지며, Map.GOAL을 통해 산하 WP들의 큰 목표가 자연스럽게 드러난다. 광역 정합성 검토는 별도 검토 활동의 영역으로 남기고, 일상 워크플로우의 토큰 비용은 늘리지 않는다.

### CONNECTIONS
- PARENT: M://root
- CHILDREN: []
- REFERENCE: [W://root/spec_v1_5_0_validation_and_todo_flatten]

### CODE_MAP
- scope:
  - ./

### TODO
# TASK — SPEC 본문 패치
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — Map/WP/dwp 역할 비교표에 GOAL 행 추가
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — WP 포맷에 `### GOAL` 섹션 신설 (IDENTITY 직후, CONNECTIONS 앞), 선택 항목 명시
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — Map 포맷에 `### GOAL` 섹션 신설 (IDENTITY 직후, WAYPOINTS 앞), 선택 항목 명시
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — SUMMARY/GOAL/TODO 의미 분담 가이드 추가 (정체성 vs 의도 vs 구체 작업)
- [x] 2026-05-11 05.ELEMENT_FORMAT.md — dwp는 GOAL 미보유 명시 (데이터 자기소개 노드, 작업 단위 아님)
- [x] 2026-05-11 01.MASTER_GUIDE.md — §2.2 신설: 의도 표현의 단일 출처는 GOAL 원칙 + 광역 정합성 검토는 별도 활동 영역 안내
- [x] 2026-05-11 09.AI_TOOL_INTEGRATION.md — §5.4 신설: WP 신규 생성/일반 작업/S_STB 전환/광역 분석 네 케이스로 GOAL 처리 분리
- [x] 2026-05-11 examples/WP_TEMPLATE.md — GOAL 섹션 예시 추가
- [x] 2026-05-11 examples/root_map.md — Map.GOAL 예시 추가
- [x] 2026-05-11 examples/DWP_TEMPLATE.md — 검토 결과 변경 불필요 (05.ELEMENT_FORMAT의 dwp 원칙에서 GOAL 미보유 명시로 충분)

# TASK — 메타데이터 / 버전
- [x] 2026-05-11 README.md / README.ko.md — v1.5.0 → v1.6.0, Document Index에 GOAL 슬롯 반영
- [x] 2026-05-11 M://root에 본 WP 등록 + SYNCED_AT 갱신

# TASK — 검증
- [x] 2026-05-11 네 프로젝트 `loadstar validate` 통과 확인 — loadstar_SPEC (5 wp, 1 map), loadstar_cli (11 wp, 3 maps), loadstar_ui (35 wp, 5 maps), loadstar_mcp (1 wp, 1 map)

# RECURRING
- (R) SPEC 변경 후 README 버전 표기 동기화 확인
- (R) loadstar_SPEC / loadstar_cli / loadstar_ui / loadstar_mcp 네 프로젝트에서 `loadstar validate` 통과 확인

### ISSUE
- OPEN_QUESTIONS: []
- 본 WP는 SPEC 본문 + 예시 갱신 + 버전 bump까지. 기존 WP/Map 파일의 GOAL 슬롯 추가는 점진 도입으로 본 WP 범위 밖.
- ROLE 메타(GOAL/IMPL/TEST) 도입은 GOAL 슬롯 신설로 불필요해져 본 WP에서 다루지 않는다.
- Map.GOAL 변경 시 산하 WP 영향 검토, Goal-Impl 추적 매트릭스 등 광역 정합성 분석은 별도 "프로젝트 검토 세션" 영역(사용자 별도 구상). SPEC엔 hook 한 줄만.

### COMMENT
- 의미 분담 명문화:
  - SUMMARY: "이게 무엇인가" (정체성)
  - GOAL: "이게 무엇을 달성하려 하는가" (의도) — 신설
  - TODO: "달성을 위한 구체 작업"
- 호환성: GOAL은 선택 항목이라 기존 모든 WP/Map 파일 무수정 통과. 신규/수정 시 점진 도입.
- 버전 정책: 호환 깨지지 않는 슬롯 신설은 minor bump (v1.5.0 → v1.6.0).
</WAYPOINT>
