# Installation Checklist

## Language And Paths

- [ ] `LANGUAGE` is confirmed as `en`.
- [ ] English template content and English comemo filenames are used together.
- [ ] `CODEX_HOME` is confirmed. The recommended default is `~/.codex`.
- [ ] If Claude Code support is requested or detected, `CLAUDE_HOME` is confirmed. The recommended default is `~/.claude`.
- [ ] `MEMORY_PATH` is confirmed. The recommended default is `~/comemo`.
- [ ] If a custom `MEMORY_PATH` is selected, generated routes and adapter notes use that path consistently.
- [ ] `PROJECT_ROOT` is confirmed.
- [ ] `PROJECT_NAME` is confirmed.
- [ ] Date is confirmed in `YYYY-MM-DD` format.
- [ ] `~` has been resolved to the real home directory for the current system.

## Cross-Platform And Encoding

- [ ] Markdown files are read and written as UTF-8.
- [ ] The current extraction method preserves filenames correctly.
- [ ] Windows paths are understood as `C:\Users\<user>\...`.
- [ ] macOS paths are understood as `/Users/<user>/...`.
- [ ] Linux paths are understood as `/home/<user>/...`.

## Existing System Detection

- [ ] Checked whether `CODEX_HOME/AGENTS.override.md` or `CODEX_HOME/AGENTS.md` exists.
- [ ] Checked whether `CLAUDE_HOME/CLAUDE.md` exists when Claude Code support is requested or detected.
- [ ] Checked whether `PROJECT_ROOT/AGENTS.override.md` or `PROJECT_ROOT/AGENTS.md` exists.
- [ ] Checked whether `PROJECT_ROOT/CLAUDE.md` or `PROJECT_ROOT/.claude/CLAUDE.md` exists.
- [ ] Checked whether `MEMORY_PATH` exists.
- [ ] Listed existing comemo files.
- [ ] Listed missing comemo files.
- [ ] Checked for tool-native memory files such as `CLAUDE.md`, `.claude/`, `GEMINI.md`, `.gemini/`, `.cursor/rules/`, `.cursorrules`, and `.aider.conf.yml`.
- [ ] If an existing system was detected, showed the current memory architecture to the user first.
- [ ] If `AGENTS.override.md` exists, explained that it has higher priority than `AGENTS.md` in the same scope.

## Files

- [ ] In an empty environment, `CODEX_HOME/AGENTS.md` was created or updated.
- [ ] In an empty environment, `PROJECT_ROOT/AGENTS.md` was created or updated.
- [ ] Long-term memory directory `MEMORY_PATH` was created.
- [ ] `MEMORY_PATH/preference.md` was created according to the selected install mode.
- [ ] `MEMORY_PATH/goals.md` was created according to the selected install mode.
- [ ] `MEMORY_PATH/ability.md` was created according to the selected install mode.
- [ ] `MEMORY_PATH/experience.md` was created according to the selected install mode.
- [ ] `MEMORY_PATH/identity.md` was created according to the selected install mode.
- [ ] If selected, `CLAUDE_HOME/CLAUDE.md` was installed as a global Claude Code bridge.
- [ ] If selected, exactly one project-level Claude Code bridge was installed at `PROJECT_ROOT/CLAUDE.md` or `PROJECT_ROOT/.claude/CLAUDE.md`, unless the user explicitly requested both.

## Claude Code Bridge Checks

- [ ] The global Claude Code bridge stays thin and does not duplicate the full comemo template.
- [ ] `CLAUDE_HOME/CLAUDE.md`, if installed, imports the resolved absolute path to `CODEX_HOME/AGENTS.md`.
- [ ] `CLAUDE_HOME/CLAUDE.md` does not use plain `@AGENTS.md` unless `AGENTS.md` is also in `CLAUDE_HOME`.
- [ ] Project-level `CLAUDE.md`, if installed with `@AGENTS.md`, is in the same directory as `AGENTS.md`.
- [ ] Existing useful Claude-specific rules were preserved or presented as merge suggestions instead of being overwritten silently.

## Safety Checks

- [ ] Existing systems defaulted to installation adaptation: create only missing files and do not overwrite existing files.
- [ ] Tool-native memory systems were bridged or left untouched by default, not migrated by rewriting native files.
- [ ] If the user chose custom installation, only the selected layers were installed.
- [ ] The user confirmed before any existing file was replaced.
- [ ] Any replaced file was backed up as `.backup.YYYY-MM-DD`.
- [ ] Every newly installed or changed target file was read after installation.
- [ ] Every newly installed or changed target file is non-empty.
- [ ] No newly installed or changed target file contains a remaining `{{...}}` placeholder.
- [ ] The global layer does not contain project facts, experiment data, results, conclusions, or next steps.
- [ ] The project layer says project facts and experiment records belong in the project directory.
- [ ] The long-term memory layer only stores durable cross-project information.
- [ ] The user was told which existing files were skipped and which merge suggestions apply.
- [ ] The user was told whether Claude Code bridge files were installed and whether they are global or project-level.