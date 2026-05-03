# {{ATLAS_TITLE}} Refactor Workflow

## Purpose

- Use this workflow for structure, ownership, API-shape, naming, duplication, or
  module-boundary changes where intended behavior should stay the same.
- Do not use refactoring as a cover for unrelated feature work or behavior
  changes.
- Do not run Codebase Atlas again for ordinary refactors; use this workflow and
  update affected atlas docs when ownership, APIs, or flows changed.

## Workflow

1. Preserve the user's original request and identify the behavior that must not
   change.
1. Open `{{INDEX_FILE}}` and choose the owning module plus any boundary modules.
1. Read the relevant module docs for scope, dependencies, downstream impact,
   common change entry points, and known risks.
1. Define the smallest refactor boundary and explicit non-goals.
1. If the refactor crosses modules, choose the primary module by the ownership
   being clarified or moved. Treat other modules as boundary modules and explain
   each boundary adjustment separately.
1. Identify tests, type checks, build checks, or smoke checks that protect the
   unchanged behavior.
1. Make the refactor in focused steps, keeping public interfaces stable unless
   the interface change is the explicit goal.
1. Verify behavior and downstream integrations still work.
1. Update atlas docs if structure, ownership, APIs, or flows changed.
1. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Pre-Edit Summary

When user confirmation is expected, summarize this and wait if the user or
project rules require confirmation before edits:

- Original request
- Primary owning module and boundary modules
- Behavior that must stay unchanged
- Refactor boundary and non-goals
- Behavior before and after, including user-visible behavior and internal
  responsibility split
- Files likely to change
- Tests or checks to run

## Delivery Policy

{{DELIVERY_POLICY}}
