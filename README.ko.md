> 🌐 **[English](README.md)** | **한국어**

# LOADSTAR SPEC

**LOADSTAR** 스펙 저장소입니다 — AI 에이전트와 사람이 공유하는 프로젝트 메타데이터 관리 방법론. 작업 단위와 데이터 정의, 그리고 그 관계를 사람도 AI 세션도 그대로 읽을 수 있는 평범한 md 파일로 남겨, 의도가 세션을 넘어 살아남게 하는 것이 목적입니다.

> 📌 LOADSTAR가 처음이라면 [openLoadstar 전체 안내](https://github.com/openLoadstar/openLoadstar)부터 보세요.

---

## 📕 어느 버전을 보면 되나

| 버전 | 상태 | 시작 지점 |
| :--- | :--- | :--- |
| **[SPEC 2.0](SPEC%202.0/README.ko.md)** | **현행** (draft) — 1.0을 대체하는 재설계 | [SPEC 2.0/README.ko.md](SPEC%202.0/README.ko.md) |
| [SPEC 1.0](SPEC%201.0/README.ko.md) | 이전 버전 (v1.8.0, 프로토타입) — 아직 1.0을 쓰는 프로젝트를 위해 유지 | [SPEC 1.0/README.ko.md](SPEC%201.0/README.ko.md) |

**2.0은 1.0의 증분 개정이 아닙니다.** 실제로 쓰인 것만 남기고, 그 자체가 또 하나의 동기화 대상이 되어버린 것들을 걷어냈습니다 — 주소(URI) 체계, 필수 Map 계층, `CODE_MAP`, `SYNCED_AT`, Decision/ADR 파일과 `OPEN_QUESTIONS`, CLI가 관리하던 로그·TODO 파일. 대신 md에서 추출해 언제든 재생성 가능한 SQLite 파생 캐시를 더했습니다. 전체 대조표는 [SPEC 2.0 README](SPEC%202.0/README.ko.md#-10에서-달라진-점)에 있습니다.

1.0으로 작성한 요소는 2.0 도구가 그대로 읽지 못합니다 — 명명 규칙, 디렉토리 구조, 일부 슬롯이 모두 바뀌었습니다. 프로젝트 하나당 한 버전을 고르세요.

## 📂 저장소 구성

```
SPEC 2.0/        현행 스펙 — 문서 5개 + 요소 FORMAT별 부록
SPEC 1.0/        이전 스펙 (v1.8.0)
examples/        1.0용 템플릿·샘플 (WP / dwp / 루트 Map / 결정 기록)
internal/        설계 드래프트·브레인스토밍 — 정식 SPEC 아님, AI 도구는 건너뜁니다
```

## 🛠 관련 프로젝트

- 🌐 **[openLoadstar](https://github.com/openLoadstar/openLoadstar)** — 생태계 전체 안내 (설치 흐름 · AI 진입 프롬프트 · 빠른 시작)
- **[loadstar_ui](https://github.com/openLoadstar/ui)** — Go + Wails 데스크톱 탐색기, SPEC 2.0 레퍼런스 구현. 같은 실행 파일이 2.0 CLI를 겸합니다
- **[loadstar_cli](https://github.com/openLoadstar/cli)** — SPEC 1.0용 CLI (`init`, `show`, `todo`, `log`, `validate`, `question`)
- **[loadstar_mcp](https://github.com/openLoadstar/mcp)** — Python 기반 MCP 서버 (Claude Desktop, Cursor 등 외부 AI 클라이언트용)

---

## 📮 기여 / 보안

- 🤝 **기여 가이드**: [openLoadstar/CONTRIBUTING.md](https://github.com/openLoadstar/openLoadstar/blob/main/CONTRIBUTING.md)
- 🔒 **보안 취약점 신고**: [openLoadstar/SECURITY.md](https://github.com/openLoadstar/openLoadstar/blob/main/SECURITY.md) — GitHub Security Advisories를 이용해 주세요.
- 💬 **질문 & 아이디어**: [GitHub Discussions](https://github.com/openLoadstar/openLoadstar/discussions)

---

## 📜 License

Apache License 2.0 — [LICENSE](LICENSE) 참조.
