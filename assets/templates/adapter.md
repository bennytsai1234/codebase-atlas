# {{WORKFLOW_ENTRYPOINT_TITLE}}

This is a thin Codebase Atlas entrypoint. The canonical workflow is
`{{WORKFLOW_FILE}}`.

## Workflow

1. Preserve the user's current request.
1. Open `{{WORKFLOW_FILE}}` and follow it as the source of truth.
1. Start from the atlas index and relevant module docs before inspecting code.
1. If the canonical workflow requires a Before / After gate, analyze first and
   wait for explicit user confirmation before editing files.
1. Finish according to the recorded delivery policy: {{DELIVERY_POLICY}}

## Do Not Do

- Do not copy or replace the canonical workflow rules here.
- Do not rerun Codebase Atlas unless the user explicitly asks for a full
  rebuild, refresh, regenerate, or rescan.
