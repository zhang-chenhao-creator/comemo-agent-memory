---
name: Change request
description: Propose a documentation, template, adapter, or example change
title: "[Change]: "
labels: ["change-request"]
body:
  - type: textarea
    id: problem
    attributes:
      label: Problem
      description: What problem should this change solve?
      placeholder: Describe the current confusion, limitation, or missing piece.
    validations:
      required: true
  - type: checkboxes
    id: scope
    attributes:
      label: Scope
      options:
        - label: README
        - label: docs
        - label: templates/en
        - label: templates/zh-CN
        - label: adapters
        - label: examples
        - label: .github
  - type: textarea
    id: proposal
    attributes:
      label: Proposed change
      description: What should be changed?
    validations:
      required: true
  - type: checkboxes
    id: constraints
    attributes:
      label: comemo constraints
      options:
        - label: Keep the core memory system Markdown-only.
        - label: Do not add shell, PowerShell, Python, binary, or package-manager installers to the core flow.
        - label: Keep adapters thin and avoid duplicating the full memory system.
        - label: Keep AGENTS.md as the fixed instruction filename.
        - label: Do not overpromise runtime compatibility.
  - type: textarea
    id: acceptance
    attributes:
      label: Acceptance criteria
      description: How do we know this issue is done?
      placeholder: "- [ ] ..."
