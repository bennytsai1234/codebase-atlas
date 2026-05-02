# {{ATLAS_TITLE}} Feature Workflow

## Purpose

- Use this workflow for new behavior that does not already exist in the target
  project.
- Do not run Codebase Atlas again for ordinary feature work; use this workflow
  and update affected atlas docs only if ownership, APIs, or flows changed.

## Workflow

1. Preserve the user's original request.
2. Open `{{INDEX_FILE}}` and find the natural owning module.
3. Read the owning module doc and any boundary module docs.
4. Define the feature boundary: included behavior, excluded behavior, interfaces,
   state, persistence, external systems, and user-visible changes.
5. Implement through the owning module's established patterns.
6. Verify the new behavior and update atlas docs when ownership, APIs, or flows
   changed.
7. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Pre-Edit Summary

When user confirmation is expected, summarize:

- Original request
- Owning module and boundary modules
- Included and excluded scope
- Implementation approach
- Behavior after completion
- Tests or checks to run

## Delivery Policy

{{DELIVERY_POLICY}}
