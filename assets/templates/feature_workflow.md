# {{ATLAS_TITLE}} Feature Workflow

## Purpose

- Use this workflow for new behavior that does not already exist in the target
  project.
- Do not run Codebase Atlas again for ordinary feature work; use this workflow
  and update affected atlas docs only if ownership, APIs, or flows changed.

## Workflow

1. Preserve the user's original request.
1. Open `{{INDEX_FILE}}` and find the natural owning module.
1. Read the owning module doc and any boundary module docs.
1. Define the feature boundary: included behavior, excluded behavior, interfaces,
   state, persistence, external systems, and user-visible changes.
1. If the feature crosses modules, choose the primary module by the module that
   owns the new behavior or state lifecycle. Treat other modules as boundary
   modules with explicit interface responsibilities.
1. Implement through the owning module's established patterns.
1. Verify the new behavior and update atlas docs when ownership, APIs, or flows
   changed.
1. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Pre-Edit Summary

When user confirmation is expected, summarize this and wait if the user or
project rules require confirmation before edits:

- Original request
- Primary owning module and boundary modules
- Included and excluded scope
- Implementation approach
- Behavior before and after, including user-visible behavior and internal
  responsibility split
- Tests or checks to run

## Delivery Policy

{{DELIVERY_POLICY}}
