# Codex Adapter

Codex is the primary target for comemo.

Recommended layout:

```text
~/.codex/AGENTS.md
~/comemo/
<project-root>/AGENTS.md
```

`~/comemo/` is the default `MEMORY_PATH`. If the user installs long-term memory somewhere else, keep that custom path in the generated routing table.

Use `templates/<LANGUAGE>/AGENTS.global.template.md` for the global layer and `templates/<LANGUAGE>/AGENTS.project.template.md` for the project layer.

The filename is `AGENTS.md`. Do not rename it to `AGENT.md`.

Installation should be performed through `docs/agent-install.en.md` or `docs/agent-install.zh-CN.md`, not by this adapter file.
