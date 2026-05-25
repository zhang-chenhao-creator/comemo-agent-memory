# FAQ

## What is comemo?

comemo is a Markdown memory layout for coding agents. It separates memory into three layers: global rules, project memory, and personal long-term memory, so agents can read the right context at the right time.

## Is comemo an installer?

No. The core flow does not provide `.sh`, `.ps1`, `.py`, binary installers, or package-manager installers. An agent should read the installation guide, inspect existing files, and then safely create or adapt Markdown files.

## Why not use fully automatic memory?

Fully automatic memory can mix temporary facts, project status, and long-term preferences into one growing context pile. comemo is intentionally semi-automatic: the human and the AI decide together what is worth preserving, then compress it into durable rules or background context.

## Why three layers?

- Global layer: hard rules that should apply to every task.
- Project layer: current project facts, workflow, and record locations.
- Long-term layer: cross-project preferences, goals, ability, experience, and identity.

This prevents temporary project state from leaking into global memory and avoids loading a full personal profile for every task.

## Why not store all memory in one file?

A single large file is convenient at first, but it becomes slower, noisier, and harder to maintain. comemo uses a routing table so agents can read only the files that are relevant to the task.

## What if I already use Claude Code, Cursor, Aider, or Gemini CLI memory files?

Do not rewrite them by default. Existing native memory files should be treated as user assets. comemo recommends thin bridging: point the native file to the shared `AGENTS.md`, or provide merge suggestions without copying the full memory system.

## Can `AGENTS.md` be renamed to `AGENT.md`?

No. comemo keeps `AGENTS.md` as the fixed Codex-style instruction filename.

## Can I store API keys, tokens, or passwords in long-term memory?

No. Do not store secrets, API keys, passwords, private tokens, financial credentials, or highly sensitive personal data in comemo memory files. Redact sensitive content first.

## Where should project experiment data go?

Project data should stay inside the project directory, for example in `records/experiment-record.md`. Do not store it in the global layer or personal long-term memory.

## Does comemo guarantee compatibility with every coding agent?

No. comemo is a Markdown template layout with thin adapter examples, not a runtime integration layer. Tool behavior can change over time, so compatibility notes should be re-verified periodically.
