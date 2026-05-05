---
name: {{WORKFLOW_ENTRYPOINT_NAME}}
description: {{WORKFLOW_ENTRYPOINT_DESCRIPTION}} Use the canonical workflow at {{WORKFLOW_FILE}}.
---

# {{WORKFLOW_ENTRYPOINT_TITLE}}

This is a thin Codebase Atlas entrypoint. The canonical workflow is
`{{WORKFLOW_FILE}}`.

## Workflow

1. Preserve the user's current request as the task input.
1. Open `{{WORKFLOW_FILE}}` and follow that workflow as the source of truth.
1. Start from the atlas index and relevant module docs before inspecting code.
1. If the canonical workflow requires a Before / After gate, analyze first and
   wait for explicit user confirmation before editing files.
1. Finish according to the recorded delivery policy: {{DELIVERY_POLICY}}

## Do Not Do

- Do not copy or replace the canonical workflow rules here.
- Do not run Codebase Atlas again unless the user explicitly asks for a full
  rebuild, refresh, regenerate, or rescan.
