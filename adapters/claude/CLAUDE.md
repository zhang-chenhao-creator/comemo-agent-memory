@AGENTS.md

# Claude Code Project Adapter

This file is kept as the default project-level Claude Code adapter.

Use it only when the installed `CLAUDE.md` and `AGENTS.md` are in the same directory, for example:

```text
<project-root>/CLAUDE.md
<project-root>/AGENTS.md
```

For a global Claude Code bridge at `~/.claude/CLAUDE.md`, do not use `@AGENTS.md` as-is. Use `adapters/claude/CLAUDE.global.md` and replace its import with the resolved absolute path to `CODEX_HOME/AGENTS.md`.

## Claude-Specific Notes

- Keep this file thin.
- Put shared project rules in `AGENTS.md`.
- Put durable cross-project memory in the selected `MEMORY_PATH` directory. The default is `~/comemo`.
- Do not copy the full comemo template into this file unless the project explicitly needs Claude-only behavior.
