# {{PROJECT_NAME}} Project Memory

> Scope: `{{PROJECT_ROOT}}` and its subdirectories.
> Upstream entry: `{{CODEX_HOME}}/AGENTS.md`.
> Language: {{LANGUAGE}}.

## Upstream Relationship

- Global hard rules, memory capture process, and comemo routing are defined by `{{CODEX_HOME}}/AGENTS.md`.
- This file only adds the current project's scope, directory responsibilities, fact boundaries, and working style.
- If this file conflicts with the upstream entry, the upstream entry wins.

## Project Fact Boundary

- Project goals, status, parameters, data, results, conclusions, and next steps belong in this project directory.
- Cross-project preferences, goals, abilities, experience, and identity do not belong in this file; route them to long-term memory under comemo.
- Mark unconfirmed facts as `to confirm`.
- Experiment and project status must include dates.

## Recommended Record Locations

- `records/project-log.md`: project log and key decisions.
- `records/experiment-record.md`: experiment records, parameters, data, and results.
- `records/handoff-note.md`: staged handoff context.
- `outputs/`: deliverables and generated outputs.
- `archive/`: stale material and historical versions.

If the actual directory structure differs, update this section to match the project.

## Working Style

- Confirm the current project goal before changing files.
- Prefer existing frameworks, scripts, and directory structure.
- Do not fabricate experiment data, cases, or citations. Mark missing sources as `to confirm`.
- For high-risk actions, list the impact first and wait for user confirmation.
