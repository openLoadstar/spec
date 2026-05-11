<WAYPOINT>
## [ADDRESS] W://root/spec_v1_3_13_patch
## [STATUS] S_STB

### IDENTITY
- SUMMARY: SPEC v1.3.12 → v1.3.13 드리프트 해소 패치 — Map STATUS 제거, NOTICE 비표준 확장 명시, DONE 상태 추가, DECISIONS 파일명 규약 갱신, question 명령 v2 문서화
- METADATA: [Priority: P1, Created: 2026-04-29]
- SYNCED_AT: 2026-04-29

### CONNECTIONS
- PARENT: M://root
- CHILDREN: []
- REFERENCE: []

### CODE_MAP
- scope:
  - ./
  - ../loadstar_cli/.loadstar/MAP/
  - ../loadstar_ui/.loadstar/MAP/

### TODO
# TASK — SPEC 본문 패치
- [x] 2026-04-29 02.SCHEMA_DEF §1 — STATUS 코드는 WayPoint 전용임을 명시 (Map은 STATUS 미보유)
- [x] 2026-04-29 02.SCHEMA_DEF §4 — `[Q{N} DONE <file>]` 상태 추가
- [x] 2026-04-29 05.ELEMENT_FORMAT — Map 포맷에서 `## [STATUS]` 줄 제거 + 주석 추가
- [x] 2026-04-29 01.MASTER_GUIDE §2 — Map 설명에 "상태 미보유" 한 줄 보강
- [x] 2026-04-29 04.STORAGE §1 — 디렉토리 트리에 NOTICE 추가 (UI 전용 비표준 확장 표기)
- [x] 2026-04-29 04.STORAGE §1.1 (신설) — 비표준 확장 영역 규칙
- [x] 2026-04-29 04.STORAGE §2.2 — DECISIONS 파일명 규약을 `{wp_id}.YYYY-MM-DD.NNN.md`로 변경
- [x] 2026-04-29 06.CLI_SPEC §5 — `question done`, `question close`, `--with-resolved` 추가
- [x] 2026-04-29 README.md — 버전 표기 v1.3.12 → v1.3.13

# TASK — 메타데이터 정리
- [x] 2026-04-29 loadstar_cli Map md 3건에서 `## [STATUS]` 줄 제거 (root, root.cli, root.maintenance)
- [x] 2026-04-29 loadstar_ui Map md 5건에서 `## [STATUS]` 줄 제거 (root, root.backend, root.frontend, root.maintenance, root.test)
- [x] 2026-04-29 loadstar_SPEC Map md 1건 STATUS 미포함으로 작성 (root)
- [x] 2026-04-29 세 프로젝트 `loadstar validate` 통과 확인

# RECURRING
- (R) SPEC 변경 후 README의 버전 표기 동기화 확인
- (R) loadstar_cli/loadstar_ui/loadstar_SPEC 세 프로젝트에서 `loadstar validate` 통과 확인

### ISSUE
- OPEN_QUESTIONS: []

### COMMENT
- D1 결정: B 형식(`{wp_id}.YYYY-MM-DD.NNN.md`)으로 SPEC 승격. 기존 `2026-04-24.check_command_removal.001.md` 1건은 SPEC 04.STORAGE §2.2 마지막 단락("기존 파일은 그대로 유지")에 따라 보존. 다음 결정 발생 시 자연스럽게 새 규칙으로 교체된다.
- MCP 구현은 v1.3.13 공개 후 별도 WP(`W://root/mcp_server`)에서 진행 예정.
</WAYPOINT>
