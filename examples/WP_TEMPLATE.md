<WAYPOINT>
## [ADDRESS] W://경로/ID_입력
## [STATUS] S_IDL

### 1. IDENTITY
- SUMMARY: 이 WP가 "무엇(What)"인지 한 줄로 식별 (정체성)
- METADATA: [Priority: P2, Estimations: 2h]
- SYNCED_AT: YYYY-MM-DD

### 2. GOAL (선택 — v1.6.0)
이 WP가 달성하려는 의도. TODO 항목들이 수렴해야 할 기준선. 한 문장~한 문단.
예: "무상태 인증 기반 마련 — SSO 통합과 다중 디바이스 세션을 지원한다."

### 3. CONNECTIONS
- PARENT: M://또는_W://부모_요소_주소
- CHILDREN: [] (하위 WayPoint 목록. 예: W://경로/하위ID. 없으면 빈 배열)
- REFERENCE: [] (참조 관계 주소 리스트. 없으면 빈 배열)

### 4. CODE_MAP (선택 — 코드 수정이 수반되는 경우에만)
- scope:
  - 탐색_범위_디렉토리_경로/
  - (복수 scope 가능)

### 5. TODO
# TASK (1회성 구현 항목)
- [ ] 미완료 항목
- [x] YYYY-MM-DD 완료된 항목

# RECURRING (코드 변경 시마다 재수행)
- (R) 변경 후 mvn test 실행
- (R) ESLint 경고 0개 유지

### 6. ISSUE
- (설계 시점 알려진 제약/미결 문제. 없으면 생략 가능)

### 7. COMMENT
- (자유 형식 코멘트. 없으면 생략 가능)
</WAYPOINT>
