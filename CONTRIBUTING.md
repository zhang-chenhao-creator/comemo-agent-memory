# Contributing

Thanks for improving comemo.

## Principles

- Keep the core memory system Markdown-only and adapters thin.
- Do not add platform-specific installers to the core flow.
- Keep `AGENTS.md` as the fixed instruction filename.
- Avoid duplicating full memory systems inside adapters.
- Keep English and Chinese templates structurally aligned.

## Suggested Changes

Useful contributions include:

- clearer installation instructions
- better compatibility notes
- safer memory-routing rules
- additional adapter examples that stay thin
- typo and encoding fixes

## Before Opening a Pull Request

- Check all Markdown files render correctly.
- Make sure Chinese filenames remain readable as UTF-8.
- Do not introduce `.sh`, `.ps1`, `.py`, or binary installers.
- Do not replace `AGENTS.md` with `AGENT.md`.
- Update `CHANGELOG.md` when the public behavior changes.
