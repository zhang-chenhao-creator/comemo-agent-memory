> This document is for an AI Agent to read and execute with the user's confirmation.

# comemo Agent Installation Guide

comemo's core memory system is Markdown-only. It has no scripts and no platform installer.

Recommended flow:

```text
Download or unzip this repository, give it to an Agent, and say:
"Read docs/agent-install.en.md and help me install comemo."
```

## 0. Agent Ground Rules

- Do not run scripts. This project intentionally has no `.sh`, `.ps1`, `.py`, binary installer, or platform-specific installer.
- Treat all Markdown files and archive filenames as UTF-8.
- Resolve `~` to the user's real home directory before writing files.
- Never silently overwrite existing memory files.
- Before replacing an existing file, show the exact path, ask for confirmation, and create a backup named `filename.backup.YYYY-MM-DD`.
- Prefer installation adaptation for existing memory systems: create only missing files and provide merge suggestions for conflicts.
- Do not move, rename, delete, or rewrite another agent's native memory files unless the user explicitly asks for that specific change.
- Replace all placeholders before finishing.
- After installation, read every target file and verify it exists, is not empty, and contains no `{{...}}` placeholders.

## 1. Choose Language

Ask the user to choose one `LANGUAGE`:

- `zh-CN`: Chinese template content and Chinese long-term memory filenames.
- `en`: English template content and English long-term memory filenames.

Language controls both file content and filenames under `MEMORY_PATH`.

For `zh-CN`, use:

```text
templates/zh-CN/
MEMORY_PATH/偏好.md
MEMORY_PATH/目标.md
MEMORY_PATH/能力.md
MEMORY_PATH/经验.md
MEMORY_PATH/身份.md
```

For `en`, use:

```text
templates/en/
MEMORY_PATH/preference.md
MEMORY_PATH/goals.md
MEMORY_PATH/ability.md
MEMORY_PATH/experience.md
MEMORY_PATH/identity.md
```

The directory name `comemo` is the recommended default for all languages. The filename `AGENTS.md` is fixed. Do not rename it to `AGENT.md`.

## 2. Resolve Paths

Ask for or infer these values:

- `CODEX_HOME`: default `~/.codex`
- `MEMORY_PATH`: default `~/comemo`
- `PROJECT_ROOT`: the current project root
- `PROJECT_NAME`: the current project name
- `DATE`: today's date in `YYYY-MM-DD`
- `LANGUAGE`: `zh-CN` or `en`

If the user chooses a custom `MEMORY_PATH`, use that exact path everywhere: template placeholder replacement, routing tables, verification, and adapter notes. Do not hardcode `~/comemo` after path resolution.

Cross-platform examples:

```text
Windows CODEX_HOME: C:\Users\<user>\.codex
Windows MEMORY_PATH: C:\Users\<user>\comemo

macOS CODEX_HOME: /Users/<user>/.codex
macOS MEMORY_PATH: /Users/<user>/comemo

Linux CODEX_HOME: /home/<user>/.codex
Linux MEMORY_PATH: /home/<user>/comemo
```

## 3. Inspect Existing Memory System

Before writing anything, inspect and show the current state:

- Whether `CODEX_HOME/AGENTS.override.md` or `CODEX_HOME/AGENTS.md` exists.
- Whether `PROJECT_ROOT/AGENTS.override.md` or `PROJECT_ROOT/AGENTS.md` exists.
- Whether `MEMORY_PATH` exists.
- Which expected comemo files already exist.
- Which expected comemo files are missing.
- Any likely conflicts, such as existing global rules, project rules, or differently named memory files.
- Tool-native memory files that may already be active, including `CLAUDE.md`, `.claude/`, `GEMINI.md`, `.gemini/`, `.cursor/rules/`, `.cursorrules`, `.aider.conf.yml`, or other obvious agent instruction files.

Classify the environment:

- Empty environment: no target memory files exist.
- Existing comemo-compatible system: at least one target file or related `AGENTS.md`/comemo file already exists.
- Tool-native memory system: a supported agent has its own memory files, but comemo target files are missing.
- Mixed system: both comemo-compatible files and tool-native memory files already exist.

For non-empty environments, show a short architecture summary before proposing changes:

```text
Detected global files:
Detected project files:
Detected long-term memory directory:
Detected tool-native memory files:
Likely conflicts:
Recommended mode:
```

## 4. Choose Install Mode

### Empty Environment

If the environment is empty:

1. Show the full install plan.
2. Ask for confirmation.
3. Install all target files.

### Existing Memory System

If an existing memory system is detected, show the current architecture first, then ask the user to choose:

1. Installation adaptation: create only missing files and provide merge suggestions for existing files. This is the recommended default.
2. Custom installation: user chooses which layers to install, such as global layer only, project layer only, comemo layer only, or preview only.
3. Replace existing files: only after explicit confirmation; back up every replaced file as `.backup.YYYY-MM-DD`.

Do not replace existing `AGENTS.md` or comemo files during installation adaptation.

If a tool-native memory system exists, prefer a bridge instead of migration:

- Keep native files thin and point them to the shared project `AGENTS.md` when the tool supports imports or read-only context files.
- Do not copy the full comemo template into `CLAUDE.md`, `GEMINI.md`, `.cursor/rules`, or `.aider.conf.yml`.
- If the native file already contains useful rules, leave it in place and provide merge suggestions instead of rewriting it.
- If `AGENTS.override.md` exists, treat it as higher priority than `AGENTS.md`; do not create a competing `AGENTS.md` at the same scope without explaining the precedence.

## 5. Target File List

Global layer:

```text
CODEX_HOME/AGENTS.md
```

If `CODEX_HOME/AGENTS.override.md` already exists, do not assume `CODEX_HOME/AGENTS.md` will be effective. Explain the precedence and ask whether the user wants to leave global comemo uninstalled, add merge suggestions for the override file, or explicitly install `AGENTS.md` as a lower-priority reference.

Long-term memory layer:

```text
MEMORY_PATH/*
```

Project layer:

```text
PROJECT_ROOT/AGENTS.md
```

If `PROJECT_ROOT/AGENTS.override.md` already exists, use the same rule: explain the precedence before creating `PROJECT_ROOT/AGENTS.md`, and do not edit the override file without explicit confirmation.

## 6. Copy Templates

Copy and replace placeholders:

| Source | Target |
| --- | --- |
| `templates/<LANGUAGE>/AGENTS.global.template.md` | `CODEX_HOME/AGENTS.md` |
| `templates/<LANGUAGE>/AGENTS.project.template.md` | `PROJECT_ROOT/AGENTS.md` |
| `templates/<LANGUAGE>/comemo/*` | `MEMORY_PATH/*` |

Replace these placeholders in every copied file:

- `{{CODEX_HOME}}`
- `{{MEMORY_PATH}}`
- `{{PROJECT_ROOT}}`
- `{{PROJECT_NAME}}`
- `{{DATE}}`
- `{{LANGUAGE}}`

When adapting an existing memory system, copy only missing files unless the user explicitly approves replacement.

## 7. Verify Installation

Read every installed or changed target file and check:

- The file exists.
- The file is not empty.
- No `{{...}}` placeholder remains.
- `CODEX_HOME/AGENTS.md`, if installed or replaced, contains the memory candidate confirmation rule.
- `PROJECT_ROOT/AGENTS.md`, if installed or replaced, says project facts, records, parameters, data, results, conclusions, and next steps belong in the project directory.
- `MEMORY_PATH` is named `comemo` by default unless the user chose another path.
- For `zh-CN`, Chinese comemo filenames can be read correctly after extraction.
- For `en`, English comemo filenames match the English routing table.

Use the checklist matching the selected language:

- Chinese: `docs/install-checklist.zh-CN.md`
- English: `docs/install-checklist.en.md`

## 8. Finish

After verification, tell the user:

- Which files were installed.
- Which files were skipped because they already existed.
- Which existing files were backed up, if any.
- Any merge suggestions for existing files.
- That future "remember this" requests should be handled as memory candidates first, not written silently.
- That project facts and experiment records should be written into the project directory, not global memory.
