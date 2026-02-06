# Orchestrated tasks schema (v1)

Paste a YAML block into the issue body:

```yaml
tcm_tasks:
  - id: billing-handoff
    repo: tooleyantoine/tcm-monorepo
    branch: feat/billing-handoff
    title: "Billing: handoff"
    depends_on: []
    claude:
      mode: safe   # safe|unsafe|manual
      comment: |
        @claude Create EXACTLY ONE handoff...



### 1B) Issue template: `.github/ISSUE_TEMPLATE/orchestrated-task.yml`
So every issue starts in the right format:

```yaml
name: Orchestrated Task Chain
description: Create a chain of cross-repo tasks and PRs
title: "[Orch] "
body:
  - type: textarea
    id: tasks
    attributes:
      label: Task chain (YAML)
      description: Paste tcm_tasks YAML here
      value: |
        ```yaml
        tcm_tasks:
          - id: example-handoff
            repo: tooleyantoine/tcm-monorepo
            branch: feat/example-handoff
            title: "Example: handoff"
            depends_on: []
            claude:
              mode: safe
              comment: |
                @claude Create EXACTLY ONE handoff...
        ```
    validations:
      required: true
