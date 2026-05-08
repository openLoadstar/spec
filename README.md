> 🌐 **English** | **[한국어](README.ko.md)**

# LOADSTAR SPEC

**Version: v1.4.0** (2026-05-08, prototype)

A project metadata management methodology shared between AI agents and humans. Tracks code modification intent and work units as **WayPoints**, with **URI-based pinpoint access** to minimize lookup costs.

> **⚠️ Prototype**
> This document, CLI, and UI are at the concept-validation stage. Feedback and improvement suggestions are welcome.

> **📢 Reference Environment**
> The CLI and UI reference implementations are written for **Claude Code**. The SPEC body is tool-neutral, but meta-synchronization mechanisms (CLAUDE.md, Hooks, etc.) assume the Claude Code environment. **Equivalent synchronization mechanisms are required** in other AI environments — see `08.META_SYNC.md` for details.

---

## 📂 Document Index

| File | Contents |
| :--- | :--- |
| [01.MASTER_GUIDE](01.MASTER_GUIDE.md) | System philosophy, core elements, AI behavioral guidelines, resource optimization conventions |
| [02.SCHEMA_DEF](02.SCHEMA_DEF.md) | Status codes, Link types, TECH_SPEC checkboxes, SYNCED_AT rules |
| [03.ADDRESS_CONVENTION](03.ADDRESS_CONVENTION.md) | URI address system (`M://`, `W://`, `D://`) and physical file path conversion |
| [04.STORAGE](04.STORAGE.md) | Directory structure, file naming, Git integration conventions |
| [05.ELEMENT_FORMAT](05.ELEMENT_FORMAT.md) | Map/WayPoint/dwp/LOADSTAR_INIT/Decision formats, TECH_SPEC archive, RECURRING item conventions |
| [06.CLI_SPEC](06.CLI_SPEC.md) | CLI command specification (`init`, `show`, `todo`, `log`, `question`, `validate`) |
| [07.TODO_SPEC](07.TODO_SPEC.md) | TODO system specification — WayPoint STATUS-based auto-sync |
| [08.META_SYNC](08.META_SYNC.md) | Meta-sync strategy (prompt + CLAUDE.md + Hook + post-verification) |
| [09.AI_TOOL_INTEGRATION](09.AI_TOOL_INTEGRATION.md) | External AI tool integration guide (LSP, grep, MCP) — CODE_MAP.scope usage patterns, anti-patterns, CLAUDE.md template |

### Reference Materials
- [examples/WP_TEMPLATE.md](examples/WP_TEMPLATE.md) — Standard WayPoint creation template
- [examples/DWP_TEMPLATE.md](examples/DWP_TEMPLATE.md) — Standard Data WayPoint (dwp) creation template
- [examples/root_map.md](examples/root_map.md) — Root Map example
- [examples/decision_sample.md](examples/decision_sample.md) — Decision record example
- [internal/](internal/) — Design discussion drafts (**not part of SPEC**, AI tools should skip)

---

## 🧭 Core Concepts

- **Map (M://)** — A structural guide for navigating WayPoints. Represents hierarchy only; not a work unit.
- **WayPoint (W://)** — The execution unit for all work. Composed of IDENTITY / CONNECTIONS / CODE_MAP / TECH_SPEC / ISSUE.
- **CODE_MAP** — A section within a WayPoint. Constrains the search scope for code-change work to specific directories.
- **Link / SavePoint** — A strict separation between logical relationships and physical locations.
- **Tolerable Consistency** — Rather than perfect consistency, the goal is "knowing where the drift is."
- **TASK / RECURRING** — One-time implementation items (`[ ]` / `[x]`) vs. verification items re-run on every code change (`(R)`).
- **OPEN_QUESTIONS / Decision** — Unresolved questions raised by the AI (`[Q{N}]`) and decision-rationale files left by humans (`.loadstar/DECISIONS/`). Preserves "why was this decided" across AI sessions.

## 🛠 Related Projects

- 🌐 **[openLoadstar](https://github.com/openLoadstar/openLoadstar)** — Full ecosystem overview (installation flow · AI entry prompt · quick start)
- **[loadstar_cli](https://github.com/openLoadstar/cli)** — Go-based CLI (`init`, `show`, `todo`, `log`, `validate`, `question`)
- **[loadstar_ui](https://github.com/openLoadstar/ui)** — Spring Boot + React Explorer UI
- **[loadstar_mcp](https://github.com/openLoadstar/mcp)** — Python-based MCP server (for external AI clients: Claude Desktop, Cursor, etc.)

---

## 📮 Contributing / Security

- 🤝 **Contributing**: [openLoadstar/CONTRIBUTING.md](https://github.com/openLoadstar/openLoadstar/blob/main/CONTRIBUTING.md)
- 🔒 **Security**: [openLoadstar/SECURITY.md](https://github.com/openLoadstar/openLoadstar/blob/main/SECURITY.md) — Please use GitHub Security Advisories.
- 💬 **Questions & Ideas**: [GitHub Discussions](https://github.com/openLoadstar/openLoadstar/discussions)

---

## 📜 License

Apache License 2.0 — see [LICENSE](LICENSE).
