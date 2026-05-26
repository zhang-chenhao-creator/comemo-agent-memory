@AGENTS.md

# Claude Code Project Adapter

Use this file as the template for a project-level Claude Code bridge, such as:

```text
<project-root>/CLAUDE.md
```

or, if the project uses a Claude-specific directory:

```text
<project-root>/.claude/CLAUDE.md
```

This adapter assumes `AGENTS.md` is in the same directory as the installed `CLAUDE.md`.

Keep this file thin. Put shared project rules in `AGENTS.md`, and put durable cross-project memory in the selected `MEMORY_PATH` directory. The default is `~/comemo`.

Do not copy the full comemo template into `CLAUDE.md` unless the project explicitly needs Claude-only behavior.
