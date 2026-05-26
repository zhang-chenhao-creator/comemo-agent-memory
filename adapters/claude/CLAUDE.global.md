# Claude Code Global Adapter

@/ABSOLUTE/PATH/TO/.codex/AGENTS.md

Use this file as the template for `~/.claude/CLAUDE.md`.

Claude Code reads `CLAUDE.md`, not Codex `AGENTS.md`. For a global Claude Code bridge, replace the import above with the user's resolved absolute path to `CODEX_HOME/AGENTS.md`.

Examples:

```md
@/Users/<user>/.codex/AGENTS.md
```

```md
@C:\Users\<user>\.codex\AGENTS.md
```

Do not use `@AGENTS.md` in `~/.claude/CLAUDE.md` unless `AGENTS.md` is also in `~/.claude/`. Relative imports are resolved from the importing file's location.
