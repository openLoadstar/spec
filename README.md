> 🌐 **English** | **[한국어](README.ko.md)**

# LOADSTAR SPEC

The specification repository for **LOADSTAR** — a project metadata methodology shared between AI agents and humans. Work units, data definitions and their relationships live as plain markdown files that both a person and an AI session can read, so intent survives across sessions.

> 📌 New to LOADSTAR? Start with the [openLoadstar overview](https://github.com/openLoadstar/openLoadstar).

---

## 📕 Which version do I read?

| Version | Status | Start here |
| :--- | :--- | :--- |
| **[SPEC 2.0](SPEC%202.0/README.md)** | **Current** (draft) — a redesign that replaces 1.0 | [SPEC 2.0/README.md](SPEC%202.0/README.md) |
| [SPEC 1.0](SPEC%201.0/README.md) | Previous (v1.8.0, prototype) — kept for projects still on it | [SPEC 1.0/README.md](SPEC%201.0/README.md) |

**2.0 is not an increment on 1.0.** It keeps what was actually used and drops what became synchronization work of its own — the URI address system, mandatory Maps, `CODE_MAP`, `SYNCED_AT`, decision/ADR files and `OPEN_QUESTIONS`, the CLI-owned log and TODO files — while adding a rebuildable SQLite cache derived from the markdown. The full before/after table is in [SPEC 2.0's README](SPEC%202.0/README.md#-what-changed-from-10).

Elements written for 1.0 are not readable by a 2.0 tool as-is: the naming rule, the directory layout and several slots all changed. Pick one version per project.

## 📂 Repository layout

```
SPEC 2.0/        Current specification — 5 documents + one appendix per element FORMAT
SPEC 1.0/        Previous specification (v1.8.0)
examples/        Templates and samples for 1.0 (WP / dwp / root map / decision record)
internal/        Design drafts and brainstorming — NOT part of the SPEC; AI tools should skip
```

## 🛠 Related Projects

- 🌐 **[openLoadstar](https://github.com/openLoadstar/openLoadstar)** — Full ecosystem overview (installation flow · AI entry prompt · quick start)
- **[loadstar_ui](https://github.com/openLoadstar/ui)** — Go + Wails desktop explorer, the SPEC 2.0 reference implementation. The same binary is also the 2.0 CLI
- **[loadstar_cli](https://github.com/openLoadstar/cli)** — The SPEC 1.0 CLI (`init`, `show`, `todo`, `log`, `validate`, `question`)
- **[loadstar_mcp](https://github.com/openLoadstar/mcp)** — Python-based MCP server (for external AI clients: Claude Desktop, Cursor, etc.)

---

## 📮 Contributing / Security

- 🤝 **Contributing**: [openLoadstar/CONTRIBUTING.md](https://github.com/openLoadstar/openLoadstar/blob/main/CONTRIBUTING.md)
- 🔒 **Security**: [openLoadstar/SECURITY.md](https://github.com/openLoadstar/openLoadstar/blob/main/SECURITY.md) — Please use GitHub Security Advisories.
- 💬 **Questions & Ideas**: [GitHub Discussions](https://github.com/openLoadstar/openLoadstar/discussions)

---

## 📜 License

Apache License 2.0 — see [LICENSE](LICENSE).
