<DECISION>
## [ID] 2026-04-24.orphan_cascade.001
## [STATUS] DECIDED
## [CREATED_AT] 2026-04-24 16:30
## [DECIDED_BY] USER

### SOURCE
- WP: W://root/maintenance/orphan_delete
- Question: [Q1] MAP 삭제 시 그 맵 산하 모든 WP를 어떻게 처리할 것인가?

### CONTEXT
UI에서 WayPoint/Map 삭제 시, 참조 없는 하위 요소가 파일시스템에 남는 orphan 이슈가 발견되었다. placeholder WP 4건이 실제로 orphan 상태로 남아있었고, 수동 삭제로 처리했다. 앞으로는 자동 처리 로직이 필요하다.

MAP 삭제의 경우 그 산하에 복수 WP가 존재할 수 있어, 단순 cascade는 데이터 손실 위험이 크다.

### OPTIONS
1. **Cascade** — 맵 삭제 시 산하 WP 전부 자동 삭제
   - Pro: 조작 단순, 빠름
   - Con: 실수 삭제 복구 어려움 (Git 의존)
2. **Block** — 산하 WP가 있으면 삭제 차단, 에러 반환
   - Pro: 안전, 명시적 의사결정 유도
   - Con: 번거로움 — 일일이 하위부터 지워야 함
3. **Interactive** — 산하 WP 목록을 보여주고 사용자에게 선택
   - Pro: 상황에 맞게 판단 가능
   - Con: UI 구현 복잡, 자동화 어려움

### DECISION
**Option 2 (Block) 기본 + `--cascade` 플래그로 Option 1 허용.**

UI에서는 Block을 기본 동작으로 하되, "산하 WP N개가 있습니다 — 함께 삭제하려면 [Cascade] 버튼" 형태로 명시적 cascade 경로를 제공한다.

### RATIONALE
- 이 WP 자체가 "orphan 방지"를 본 취지로 한다 — 안전 우선이 철학과 일치
- cascade가 필요한 순간은 제한적이므로 명시적 플래그로 충분
- Interactive는 초기 구현 복잡도 대비 이익 불확실 — v2로 유보

### IMPACT
- `W://root/maintenance/orphan_delete` TODO에 추가:
  - [ ] MAP 삭제 API에 산하 WP 존재 여부 사전 체크 로직 추가
  - [ ] 삭제 차단 시 "N개 하위 요소가 존재" 응답 구조화
  - [ ] `--cascade` 플래그(CLI) / Cascade 버튼(UI) 구현
  - [ ] cascade 삭제 시 모든 하위 WP에 대해 loadstar log add DELETED 자동 기록

### COMMENT
`--cascade` 플래그는 UI의 Cascade 버튼과 동일한 동작이어야 한다. 백엔드에서 단일 경로로 처리하는 편이 유지보수에 유리.
</DECISION>
