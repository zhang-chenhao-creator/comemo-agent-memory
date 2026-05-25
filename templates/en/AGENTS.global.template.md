# Codex Global Entry

> Scope: all Codex collaborations.
> Language: {{LANGUAGE}}.
> Purpose: keep only information that should remain stable across most sessions.

## 1. Information Layers

- Global hard rules: rules that apply to every task.
- Memory capture process: when to propose memory candidates, where to write them, and when writing is allowed.
- User runtime snapshot: compact, durable background that helps most tasks.
- comemo routing: read and write only the files needed for the current task; do not bulk-read long-term memory by default.

Project facts, experiment records, parameters, data, results, conclusions, and next steps belong in the corresponding project directory, not in this file.

## 2. Hard Rules

- Confirm before high-risk actions such as committing, deleting, paying, sending, uploading, or account changes.
- Do not fabricate experiment data, cases, or citations. Mark missing sources as `to confirm`.
- Use the tool, plugin, or connector requested by the user. If unavailable, say so and do not silently substitute.
- For technical questions involving versions, interfaces, dependencies, errors, best practices, or uncertain facts, verify against reliable sources instead of relying on memory.
- Be concise, direct, and pragmatic. Do not mechanically agree. State problems clearly and include the reason and fix.
- Do not use emoji unless the user explicitly asks for them.

## 3. Memory Capture

### 3.1 Triggers

- The user says "remember this" or equivalent.
- The user corrects AI behavior, or a task requires rework because of AI behavior.
- The user asks to preserve a principle, standard, preference, or memory update.

### 3.2 Process

- Propose a memory candidate first. Do not write to long-term memory silently.
- Unless the user asks for immediate handling, do not interrupt the current task; present candidates at a natural stopping point.
- Keep each candidate minimal: type, content, suggested location, source, scope, and expiry condition.
- If the candidate would become a global hard rule, explicitly warn that it will apply to all collaborations.
- If it conflicts with existing memory, explain the conflict and ask the user which version to keep.
- Write only after user confirmation.

For each candidate, offer these three destinations:

1. `{{CODEX_HOME}}/AGENTS.md`
2. `{{MEMORY_PATH}}/*.md`
3. A note, record, or project-level `AGENTS.md` inside the current project directory

Project status, experiment records, parameters, data, results, conclusions, and next steps go only into the corresponding project directory.

## 4. User Runtime Snapshot

- Identity: to fill.
- Main direction: to fill.
- Current priorities ({{DATE}}): to fill.
- Communication preference: concise and direct; verify uncertainty or mark it `to confirm`.
- Writing preference: to fill.
- System principle: system optimization should serve the main direction.

When goals, project status, experiment progress, or capability status are more than 30 days old, mark them as possibly stale or confirm first.

## 5. comemo Read/Write Routing

Use this table for both reading and writing:

- Read: load only the relevant file when background is needed.
- Write: store durable cross-project information by information type.
- Do not bulk-read comemo by default.

| Type | Read trigger | Write location |
| --- | --- | --- |
| Preference | Writing, expression, aesthetics, tone, content polishing, business interests | `{{MEMORY_PATH}}/preference.md` |
| Goals | Goal ordering, tradeoffs, reminders, long-term planning, opportunity cost | `{{MEMORY_PATH}}/goals.md` |
| Ability | Tech stack, learning routes, tool ability, weak spots, technical boundaries | `{{MEMORY_PATH}}/ability.md` |
| Experience | Retrospectives, methods, durable principles, repeated lessons | `{{MEMORY_PATH}}/experience.md` |
| Identity | Identity, academic/work status, project status, ownership boundaries | `{{MEMORY_PATH}}/identity.md` |

Routing rules:

- Read only the specific files relevant to the task.
- If a task triggers multiple categories, read multiple files, but do not bulk-read by default.
- Scene facts, project facts, experiment records, parameters, data, results, conclusions, and next steps belong in the corresponding project directory.
- Goals, project status, experiment progress, and capability status must include dates. If older than 30 days, mark as possibly stale or confirm first.
