<WAYPOINT>
## [ADDRESS] W://root/spec_v1_4_0_dwp_introduction
## [STATUS] S_STB

### IDENTITY
- SUMMARY: SPEC v1.3.13 → v1.4.0 — Data WayPoint(dwp) 1급 요소 도입. 데이터의 개념적 자기소개를 D:// 주소로 식별되는 노드로 표현. 본문은 카테고리/테이블/요소 3단 구조이며 ERD 수준 구체 스펙은 제외(정확한 스펙은 CODE_MAP.scope로 코드 참조).
- METADATA: [Priority: P1, Created: 2026-05-08]
- SYNCED_AT: 2026-05-08

### CONNECTIONS
- PARENT: M://root
- CHILDREN: []
- REFERENCE: []

### CODE_MAP
- scope:
  - ./

### TODO
- ADDRESS: W://root/spec_v1_4_0_dwp_introduction
- SUMMARY: dwp 도입에 따른 SPEC 본문 패치 (주소 체계, 요소 포맷, 스키마 정의, 템플릿, README 버전)
- TECH_SPEC:
  # TASK — SPEC 본문 패치
  - [x] 2026-05-08 03.ADDRESS_CONVENTION.md — D 접두사 추가, TYPE_DIR에 DATA_WAYPOINT 매핑, 물리 경로 예시 추가
  - [x] 2026-05-08 05.ELEMENT_FORMAT.md — 역할 비교표에 dwp 컬럼 추가, dwp 포맷 신규 섹션, dwp 작성 원칙 명문화, Map ITEMS 예시에 D:// 추가
  - [x] 2026-05-08 02.SCHEMA_DEF.md §1 — STATUS 적용 대상에 dwp 포함
  - [x] 2026-05-08 examples/DWP_TEMPLATE.md 신규 생성
  - [x] 2026-05-08 README.md / README.ko.md — 버전 v1.3.13 → v1.4.0, Document Index의 05.ELEMENT_FORMAT 설명에 dwp 한 단어 보강

  # TASK — 메타데이터 정리
  - [x] 2026-05-08 M://root에 본 WP 등록 + SYNCED_AT 갱신
  - [x] 2026-05-08 loadstar_SPEC 자기 자신에서 `loadstar validate` 통과 확인 (3 waypoints, 1 maps checked)

  # RECURRING
  - (R) SPEC 변경 후 README의 버전 표기 동기화 확인
  - (R) loadstar_cli/loadstar_ui/loadstar_SPEC 세 프로젝트에서 `loadstar validate` 통과 확인

### ISSUE
- OPEN_QUESTIONS: []
- 본 WP는 SPEC 본문 패치에 한정. CLI/UI/MCP에서 D:// 주소를 처리하는 구현 작업은 v1.4.0 공개 후 각 레포의 별도 WP로 분리한다.

### COMMENT
- 설계 합의 핵심:
  - dwp 본문은 카테고리(SUMMARY) → TABLES(L2) → 요소(L3) 3단 구조.
  - 요소에 타입/길이/제약 등 구체 스펙은 적지 않는다 — 정확한 스펙이 필요하면 CODE_MAP.scope로 코드 직접 참조.
  - dwp 간 관계는 본문에 능동적으로 그리지 않는다. 기존 REFERENCE 표기 또는 wp의 작업 기록을 통해 자연스럽게 드러나도록 한다.
  - mermaid는 일단 채택하지 않는다. 향후 LOADSTAR UI 자체에 mermaid 발상(텍스트로 UI 관리)을 차용하는 검토는 별개 사안.
- 폴더명 결정: `DATA_WAYPOINT/` (사용자 선택, 2026-05-08).
- 버전 정책: 신규 1급 요소 도입은 minor bump (v1.3.13 → v1.4.0).
</WAYPOINT>
