# Compatibility

comemo is a Markdown template, not a runtime integration layer. Compatibility means the target agent can read the relevant Markdown files or can be pointed to them with a thin adapter.

## Operating Systems

Use `~` as the portable home-directory notation in docs and templates.

```text
Windows: C:\Users\<user>
macOS: /Users/<user>
Linux: /home/<user>
```

Recommended paths:

```text
~/.codex/AGENTS.md
~/comemo/
<project-root>/AGENTS.md
```

Optional Claude Code bridge paths:

```text
~/.claude/CLAUDE.md
<project-root>/CLAUDE.md
<project-root>/.claude/CLAUDE.md
```

`~/comemo/` is only the recommended default. Installers and agents should treat the long-term memory directory as `MEMORY_PATH`, and should preserve a custom path consistently across generated routing tables and adapter notes.

All Markdown files should be treated as UTF-8. English templates use ASCII filenames. Chinese templates use UTF-8 Chinese filenames under `MEMORY_PATH`.

## Integration Types

| Agent | Integration type | Notes |
| --- | --- | --- |
| Codex | Primary target | Uses `AGENTS.md` directly |
| Claude Code | Bridge | Uses thin `CLAUDE.md` files to import the shared `AGENTS.md`; project and global bridges use different paths |
| Cursor | Manual / shared instruction | Uses project `AGENTS.md` as shared project context |
| Aider | Adapter example | Adds `AGENTS.md` as read-only context |
| Gemini CLI | Adapter example | Adds `AGENTS.md` to context discovery |

## Verification Status

Tool behavior changes over time. comemo documents the intended integration pattern, not a guaranteed runtime contract.

Last verified: 2026-05-25

| Tool | Status | Note |
| --- | --- | --- |
| Codex | Primary target | Uses `AGENTS.md` as the main instruction file |
| Claude Code | Bridge example | Project bridge imports same-directory `AGENTS.md`; global bridge imports the resolved absolute path to `CODEX_HOME/AGENTS.md` |
| Cursor | Partial / manual | Use `AGENTS.md` as shared project instruction; project rules may need manual setup |
| Aider | Example adapter | Reads `AGENTS.md` as read-only context |
| Gemini CLI | Example adapter | Includes `AGENTS.md` in context discovery |

## Agent Notes

### Codex

Codex is the primary target. Use:

```text
~/.codex/AGENTS.md
<project-root>/AGENTS.md
MEMORY_PATH/
```

See `adapters/codex/README.md`.

### Claude Code

Claude Code reads `CLAUDE.md`, not Codex `AGENTS.md`. comemo therefore keeps `AGENTS.md` as the shared source of truth and uses a thin `CLAUDE.md` bridge.

Project-level bridge, when `CLAUDE.md` and `AGENTS.md` are in the same directory:

```md
@AGENTS.md
```

Global bridge, when writing to `~/.claude/CLAUDE.md`:

```md
@/absolute/path/to/.codex/AGENTS.md
```

Do not use plain `@AGENTS.md` in `~/.claude/CLAUDE.md` unless `AGENTS.md` is also in `~/.claude/`. Relative imports are resolved from the importing file's location.

See `adapters/claude/README.md`.

### Cursor

Use the project-level `AGENTS.md` as the shared project instruction file. comemo does not generate `.cursor/rules` in v0.1.0 because that would duplicate the memory system.

Cursor supports `AGENTS.md` as a root-level project instruction file for straightforward use cases, but projects may still need manual Cursor project rules for scoped behavior. If a project needs scoped rules, use Cursor project rules as thin pointers instead of copying the full comemo template.

See `adapters/cursor/README.md`.

### Aider

The adapter shows a minimal `.aider.conf.yml` that references `AGENTS.md` as a read-only context file.

See `adapters/aider/.aider.conf.yml`.

### Gemini CLI

The adapter shows a minimal settings example that includes `AGENTS.md` in Gemini CLI context-file discovery.

See `adapters/gemini/settings.json`.

## Reference Links

- AGENTS.md open format: https://agents.md/
- OpenAI Codex AGENTS.md: https://developers.openai.com/codex/guides/agents-md
- Claude Code memory: https://docs.anthropic.com/en/docs/claude-code/memory
- Cursor rules: https://docs.cursor.com/en/context
- Aider YAML config: https://aider.chat/docs/config/aider_conf.html
- Gemini CLI configuration: https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/configuration.md

## Limits

- Adapters are examples, not full installers.
- Tool behavior can change across versions.
- If an agent has a native memory format, keep that file thin and reference `AGENTS.md` instead of copying the full comemo template into another format.
- Do not treat all agents as having identical instruction precedence.
- Existing native memory files should be treated as user-owned. During installation, bridge to `AGENTS.md` or provide merge suggestions; do not rewrite them by default.
- If a Codex `AGENTS.override.md` exists at the same scope, it takes precedence over `AGENTS.md`; avoid creating competing guidance without explaining that precedence.