# Claude Code Adapter

comemo keeps `AGENTS.md` as the shared memory and instruction source. Claude Code reads `CLAUDE.md`, so the Claude adapter should stay thin and import the shared file instead of duplicating the full comemo template.

## Project-level bridge

Use this when a project has both files in the same directory:

```text
<project-root>/CLAUDE.md
<project-root>/AGENTS.md
```

Install `adapters/claude/CLAUDE.project.md` as `CLAUDE.md`, or copy the same content from `adapters/claude/CLAUDE.md`:

```md
@AGENTS.md
```

This works only when `AGENTS.md` is next to the installed `CLAUDE.md`.

## Global bridge

Use this when Claude Code should load the shared global comemo entry from `~/.claude/CLAUDE.md`.

Install `adapters/claude/CLAUDE.global.md` as:

```text
~/.claude/CLAUDE.md
```

Then replace the placeholder import with the resolved absolute path to `CODEX_HOME/AGENTS.md`.

macOS/Linux example:

```md
@/Users/<user>/.codex/AGENTS.md
```

Windows example:

```md
@C:\Users\<user>\.codex\AGENTS.md
```

Do not install this global bridge as `@AGENTS.md` unless `AGENTS.md` is also in `~/.claude/`.

## Rule

- `@AGENTS.md`: project-level bridge, same directory only.
- `@/absolute/path/to/.codex/AGENTS.md`: global bridge.
- Keep Claude-specific behavior in `CLAUDE.md` only when it cannot be shared through `AGENTS.md`.
