<WAYPOINT>
## [ADDRESS] W://경로/ID_입력
## [STATUS] S_IDL

### 1. IDENTITY
- SUMMARY: "무엇을(What)"에 대한 간략한 목표
- METADATA: [Priority: P2, Estimations: 2h]
- SYNCED_AT: YYYY-MM-DD

### 2. CONNECTIONS
- PARENT: M://또는_W://부모_요소_주소
- CHILDREN: [] (하위 WayPoint 목록. 예: W://경로/하위ID. 없으면 빈 배열)
- REFERENCE: [] (참조 관계 주소 리스트. 없으면 빈 배열)

### 3. CODE_MAP (선택 — 코드 수정이 수반되는 경우에만)
- scope:
  - 탐색_범위_디렉토리_경로/
  - (복수 scope 가능)

### 4. TODO
- ADDRESS: W://현재_WayPoint_주소
- SUMMARY: 작업 내용 요약
- TECH_SPEC:
  # TASK (1회성 구현 항목)
  - [ ] 미완료 항목
  - [x] YYYY-MM-DD 완료된 항목
  # RECURRING (코드 변경 시마다 재수행)
  - (R) 변경 후 mvn test 실행
  - (R) ESLint 경고 0개 유지

### 5. ISSUE
- (설계 시점 알려진 제약/미결 문제. 없으면 생략 가능)

### 6. COMMENT
- (자유 형식 코멘트. 없으면 생략 가능)
</WAYPOINT>
