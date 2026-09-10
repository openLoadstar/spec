> 🌐 **English** | **[한국어](README.ko.md)**

# LOADSTAR SPEC 2.0

**Version: 2.0** (2026-08-04, draft)

A project metadata methodology shared between AI agents and humans. Work units and data definitions live as plain markdown files; **the filename is the only identity**, and everything a tool needs for fast lookup is *derived* from those files into a rebuildable SQLite cache.

> **⚠️ Draft**
> 2.0 is a redesign that replaces [SPEC 1.0](../SPEC%201.0/README.md), not an increment on it. Some sections are still open — `03.SCHEMA_DEF.md` is not written yet, and `04.META_EXTRACTION.md §10` lists the undecided points. Feedback and improvement suggestions are welcome.

---

## 🔄 What changed from 1.0

2.0 keeps what was actually used in practice and removes what turned into synchronization work of its own. Everything below was dropped deliberately.

| Dropped in 2.0 | Why | Where it went |
| :--- | :--- | :--- |
| **URI address system** (`M://`, `W://`, `D://`) and the address → file-path conversion table | An extra naming layer to keep in sync with the filesystem for no lookup benefit | The filename *is* the identity; references are written as the plain target filename (`02.ELEMENT_FORMAT.md §3`, §4) |
| **Map (`M://`)** as a mandatory hierarchy | Every WayPoint had to be hung under a Map even when the hierarchy carried no meaning | `GROUP`, an **optional** organizing container — a WayPoint need not belong to any (`appendix/GROUP.md`) |
| **CODE_MAP** slot | Real-world usefulness was unclear | Removed (2026-07-27). If scoping code search becomes necessary again, it will be reconsidered |
| **SYNCED_AT** slot | A timestamp that has to be maintained by hand is drift, not a defense against it | Removed — git is the single source of change history |
| **Decision / ADR files** and **OPEN_QUESTIONS** (`[Q{N}]`, DEFERRED/CONFIRMED) | Question numbers, states and separate files became their own consistency problem, and were barely used in 1.0 | One place: free-form text in the element's `ISSUE` section (`01.MASTER_GUIDE.md §4.1`) |
| **`.clionly/LOG/`** (per-element change-history index) | A log written next to git that can disagree with git | Git only. `history` in the index is a *mirror* filled from `git log`, never written directly (`04.META_EXTRACTION.md §4`) |
| **`.clionly/TODO/TODO_LIST.md`** (materialized TODO list) | Cached work state has to be re-synced on every edit | Computed on demand by reading the WP markdown at query time (`04.META_EXTRACTION.md §7`) |
| **GD (Good Dopamin)**, `COMMON/`, `NOTICE/`, `MONITOR/` | Never implemented, or never used | Removed |
| **Separate `TODO_SPEC` / `META_SYNC` / `AI_TOOL_INTEGRATION` documents** | Rules that belong to one element type do not need a top-level document | Folded into the per-FORMAT appendices; the AI operating principle is one section (`01.MASTER_GUIDE.md §6`) |

And the one thing 2.0 **adds**: a metadata extraction pipeline over a SQLite derived cache (`04.META_EXTRACTION.md`), so a tool can browse a project by date / type / keyword / relationship without walking every file — while the markdown stays the only original.

| 1.0 | 2.0 |
| :--- | :--- |
| `.loadstar/{MAP,WAYPOINT,DATA_WAYPOINT,DECISIONS,GD,COMMON,.clionly}/` | `.loadstar/{WP,DWP,GROUP,OTHER}/` + `.loadstar/.cache/index.db` (git-ignored, rebuildable) |
| Address → directory mapping table | `FORMAT` *is* the directory name |
| 9 spec documents | 5 spec documents + one appendix per FORMAT |

---

## 📂 Document Index

| File | Contents |
| :--- | :--- |
| [01.MASTER_GUIDE](01.MASTER_GUIDE.md) | Purpose, original/derived separation, Tolerable Consistency, the element model, history, AI operating principles |
| [02.ELEMENT_FORMAT](02.ELEMENT_FORMAT.md) | Rules common to every element — naming, identity, references, the shared envelope, the element catalog, physical paths |
| [03.SCHEMA_DEF](03.SCHEMA_DEF.md) | Shared vocabulary (status codes, checkbox conventions, URL schemes) — ⚠️ not written yet |
| [04.META_EXTRACTION](04.META_EXTRACTION.md) | Extraction pipeline (structure extractor / AI enrichment / on-demand domain query), DB schema, validator, open points |
| [05.CLI_SPEC](05.CLI_SPEC.md) | CLI command specification (`create`, `show`, `reindex`, and `todo` / `issues` / `validate` ⚠️ not implemented yet) |

### Appendices — one per FORMAT

| File | Element |
| :--- | :--- |
| [appendix/WP.md](appendix/WP.md) | **WayPoint** — the execution unit for all work. `STATUS` / `GOAL` / `TODO`, and child WayPoints |
| [appendix/DWP.md](appendix/DWP.md) | **Data WayPoint** — the conceptual self-description of a data artifact. No TODO, no GOAL; optional `TABLES` |
| [appendix/GROUP.md](appendix/GROUP.md) | **Group** — an optional category container. Only `CONNECTIONS.ITEMS` |
| [appendix/OTHER.md](appendix/OTHER.md) | **Other** — free-form files that need to be organizable. The one FORMAT exempt from the naming rule and the common envelope |

A new element type is added by writing a new appendix — the common rules do not change.

---

## 🧭 Core Concepts

- **Element** — Every work unit and data definition is exactly one markdown file named `[FORMAT][VER][DATE]이름.md`. The structured fields sit up front so the free-text label can contain anything, brackets included.
- **The filename is the identity** — No address scheme, no duplicated identity line inside the file. References between elements are written as the target filename, and the `FORMAT` prefix tells a tool which folder to look in.
- **Original vs. derived** — Markdown is the single source of truth. The SQLite index holds only metadata extracted from it and must be regenerable at any time; hierarchy and group views are computed from `CONNECTIONS`, never maintained as a separate index file.
- **Tolerable Consistency** — Perfect code/metadata consistency is not the goal; *knowing where the drift is* is. A validation pass makes drift discoverable instead of trying to prevent it at every edit.
- **STATUS** — `S_IDL` idle · `S_PRG` in progress · `S_STB` stable · `S_ERR` error · `S_REV` review required · `S_OOS` out of scope. The single source for progress, on WayPoints only.
- **SUMMARY / GOAL / TODO** — Three different questions: what this *is*, what it is *trying to achieve*, and the concrete steps. A GOAL that keeps growing is the signal to split into child WayPoints.
- **GROUP is optional, and one-directional** — Only a GROUP knows its members; a WP/DWP never records which GROUP it belongs to. Membership changes by editing the GROUP's `ITEMS` and nothing else.
- **ISSUE** — The single place for constraints, open questions and unresolved decisions, in free-form text. No question numbering, no separate decision files.
- **Git is the only history** — No log file is written beside it. The index's `history` table is a mirror of `git log`.
- **Extraction pipeline** — ① a deterministic structure extractor (filename fields + `SUMMARY` + `CONNECTIONS` + markdown-level facts), ② an AI enrichment step (keywords, multi-angle summaries), ③ an on-demand domain query layer that reads the markdown at call time for `STATUS` / `TODO` / `ISSUE`, which are never cached.

## 🛠 Related Projects

- 🌐 **[openLoadstar](https://github.com/openLoadstar/openLoadstar)** — Full ecosystem overview (installation flow · AI entry prompt · quick start)
- **[loadstar_ui](https://github.com/openLoadstar/ui)** — Go + Wails desktop explorer, the SPEC 2.0 reference implementation. The same binary is also the 2.0 CLI (`05.CLI_SPEC.md §1`)
- **[loadstar_cli](https://github.com/openLoadstar/cli)** — The SPEC 1.0 CLI (`init`, `show`, `todo`, `log`, `validate`, `question`)
- **[loadstar_mcp](https://github.com/openLoadstar/mcp)** — Python-based MCP server (for external AI clients: Claude Desktop, Cursor, etc.)

---

## 📮 Contributing / Security

- 🤝 **Contributing**: [openLoadstar/CONTRIBUTING.md](https://github.com/openLoadstar/openLoadstar/blob/main/CONTRIBUTING.md)
- 🔒 **Security**: [openLoadstar/SECURITY.md](https://github.com/openLoadstar/openLoadstar/blob/main/SECURITY.md) — Please use GitHub Security Advisories.
- 💬 **Questions & Ideas**: [GitHub Discussions](https://github.com/openLoadstar/openLoadstar/discussions)

---

## 📜 License

Apache License 2.0 — see [LICENSE](../LICENSE).
