# Gemini agent assets

- **`settings.json`** — Gemini CLI context (`GEMINI.md`, `AGENTS.md`).
- **`skills/`** (under `.gemini/`) — PM workflows tuned for Gemini (each folder: `SKILL.md` + optional `subagent-prompt.md`). Knowledge and templates still live under [`.productmap/`](../.productmap/).
- The repository root [`skills.sh.json`](../skills.sh.json) adds `.gemini/skills/` to the search paths of the open `npx skills` CLI, so these skills install from the files in this folder (see root `README.md`).

See the root [`GEMINI.md`](../GEMINI.md) for full agent instructions.
