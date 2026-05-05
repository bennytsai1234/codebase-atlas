---
description: {{WORKFLOW_ENTRYPOINT_DESCRIPTION}} Use the canonical workflow at {{WORKFLOW_FILE}}.
---

# {{WORKFLOW_ENTRYPOINT_TITLE}}

Use the user's current chat request as the task input.

Read and follow `{{WORKFLOW_FILE}}`. Treat that file as the source of truth for
module selection, analysis gates, validation, atlas updates, and delivery
policy.

Start from the atlas index before inspecting code. If the canonical workflow
requires a Before / After gate, analyze first and wait for explicit user
confirmation before editing files.

Do not run Codebase Atlas again unless the user explicitly asks for a full
rebuild, refresh, regenerate, or rescan.
