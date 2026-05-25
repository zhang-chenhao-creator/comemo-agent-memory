---
name: Compatibility report
description: Report behavior for a coding agent, editor, or platform
title: "[Compatibility]: "
labels: ["compatibility"]
body:
  - type: input
    id: tool
    attributes:
      label: Tool or platform
      placeholder: "Codex, Claude Code, Cursor, Aider, Gemini CLI, Windows, macOS, Linux..."
    validations:
      required: true
  - type: input
    id: version
    attributes:
      label: Version or date verified
      placeholder: "Tool version, commit, or YYYY-MM-DD"
  - type: dropdown
    id: status
    attributes:
      label: Status
      options:
        - Works as documented
        - Partially works
        - Does not work
        - Documentation unclear
        - Needs re-verification
    validations:
      required: true
  - type: textarea
    id: setup
    attributes:
      label: Setup
      description: What files and paths were used?
      placeholder: "~/.codex/AGENTS.md, ~/comemo/, <project-root>/AGENTS.md..."
  - type: textarea
    id: observed
    attributes:
      label: Observed behavior
      description: What actually happened?
    validations:
      required: true
  - type: textarea
    id: expected
    attributes:
      label: Expected behavior
      description: What did you expect to happen?
  - type: textarea
    id: proposed
    attributes:
      label: Proposed documentation change
      description: If this is a docs issue, suggest the safer wording.
