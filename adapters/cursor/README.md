# Cursor Adapter

Use the project-level `AGENTS.md` as the shared project instruction file.

comemo v0.1.0 does not generate `.cursor/rules` by default because that would duplicate the same memory system in another format.

Recommended flow:

1. Install the project-level template as `<project-root>/AGENTS.md`.
2. Keep long-term memory in the selected `MEMORY_PATH` directory. The default is `~/comemo`.
3. If a project later needs Cursor-specific rules, create them as thin pointers to `AGENTS.md` instead of copying the full template.

The shared filename remains `AGENTS.md`, not `AGENT.md`.
