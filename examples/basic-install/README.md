# Basic Install Example

This example shows the recommended comemo layout after installation. It is not an installer and should not be treated as a real user configuration that must be copied exactly.

## Recommended layout

```text
~/.codex/AGENTS.md
~/comemo/
|-- preference.md
|-- goals.md
|-- ability.md
|-- experience.md
`-- identity.md
<project-root>/AGENTS.md
```

## Layer responsibilities

### 1. Global layer

Location:

```text
~/.codex/AGENTS.md
```

Stores only always-on collaboration rules, the memory-capture process, and the routing table for reading long-term memory on demand.

Do not store project status, experimental data, or temporary conclusions in the global layer.

### 2. Project layer

Location:

```text
<project-root>/AGENTS.md
```

Stores the current project's goals, fact boundaries, record locations, and workflow notes.

Project facts, parameters, data, results, conclusions, and next steps should stay inside the project directory.

### 3. Long-term memory layer

Location:

```text
~/comemo/
```

Stores cross-project long-term information: preferences, goals, ability, experience, and identity.

Long-term memory should not be loaded in full by default. Agents should read only the relevant files for the current task.

## Installation principles

- Inspect existing `AGENTS.md`, `AGENTS.override.md`, and native memory files before installation.
- Do not silently overwrite existing files.
- If replacement is needed, show the exact path, explain the impact, and create a backup.
- Replace all placeholders before installation is considered complete.
- After installation, read the target files and confirm they are non-empty and contain no remaining `{{...}}` placeholders.

See `docs/agent-install.en.md` for the full flow.
