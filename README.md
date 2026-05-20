# A2A: Git-based file bus (JSON-RPC 2.0)

This repository defines an **Agent-to-Agent** messaging environment through the file system and **state versioning via Git**.

## Layout

| Path | Purpose |
|------|---------|
| `inbox/` | Incoming JSON-RPC requests queue (**PENDING**) |
| `processing/` | Active tasks (**LOCKED** — claimed by a specific agent) |
| `outbox/` | Completed responses (**COMPLETED**): **always** `res_{id}.*` with the JSON-RPC body (section 2.2); **optionally** a `{id}/` directory with attachments and `metadata.json` (see `docs/SYSTEM_INSTRUCTIONS.md` section 2.3) |
| `archive/` | Archive of processed requests |
| `.well-known/agents/` | Agent manifests |
| `config/` | Environment configuration (paths, protocol version) |
| `docs/` | Specifications and system instructions |

## Documents for agents

1. **[PROTOCOL.md](PROTOCOL.md)** — short protocol overview and link to **Iteration Policy** (iterations and `parent_id`).
2. **[docs/SYSTEM_INSTRUCTIONS.md](docs/SYSTEM_INSTRUCTIONS.md)** — formal system instructions (workflow, invariants, state transitions, **Envelope pattern** for `outbox/`, section 2.3; **iterations — section 7**). Response examples: **[docs/examples/README.md](docs/examples/README.md)**.
3. **[docs/ATOMIC_CAPTURE.md](docs/ATOMIC_CAPTURE.md)** — atomic task capture model and collision avoidance.
4. **[docs/VERSIONING.md](docs/VERSIONING.md)** — how Git records snapshots of queue and message state.

## For AI assistants

- **[CLAUDE.md](CLAUDE.md)** — short navigation over instructions (link table).
- Cursor rule: [.cursor/rules/a2a-file-bus.mdc](.cursor/rules/a2a-file-bus.mdc) (`alwaysApply`).
- Claude skill “text → `inbox/`”: [.claude/skills/a2a-task-from-text/SKILL.md](.claude/skills/a2a-task-from-text/SKILL.md).
- Claude worker skill (`inbox/` → response): [.claude/skills/a2a-inbox-worker/SKILL.md](.claude/skills/a2a-inbox-worker/SKILL.md).

## Quick start

- Agent manifest: `.well-known/agents/{agent_id}.json`.
- **Data Analyst** role template: [.well-known/agents/data_analyst.json](.well-known/agents/data_analyst.json).
- **Product Manager** role template: [.well-known/agents/product_manager.json](.well-known/agents/product_manager.json).
- Root paths are set in `config/a2a-environment.json`.
