# {{ATLAS_TITLE}} Bug Workflow

## Purpose

- Use this workflow for clear bugs, failing tests, regressions, crashes, or
  unstable behavior.
- Do not run Codebase Atlas again for ordinary bug fixes; use this workflow and
  update affected atlas docs only if ownership or flows changed.

## Workflow

1. Open `{{INDEX_FILE}}` and choose the most likely owning module.
1. Read that module's dependencies, key flows, known risks, and scope boundary.
1. Inspect the failing runtime path or test path in code.
1. Decide whether the defect is local to the module or caused by upstream input.
1. If the symptom crosses modules, choose the primary module by where the data,
   state, or behavior first becomes wrong. Treat other modules as boundary
   modules and keep their changes minimal.
1. Keep the fix concentrated in the owning module. Boundary changes require a
   clear reason.
1. Verify the bug is fixed and update atlas docs if ownership or flows changed.
1. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Pre-Edit Summary

When user confirmation is expected, summarize this and wait if the user or
project rules require confirmation before edits:

- Symptom
- Root cause hypothesis or confirmed root cause
- Primary owning module and any boundary modules
- Files likely to change
- Behavior before and after, including user-visible behavior and internal
  responsibility split
- Reason for any cross-module or boundary change
- Tests or checks to run

## Delivery Policy

{{DELIVERY_POLICY}}
