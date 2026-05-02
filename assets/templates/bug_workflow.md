# {{ATLAS_TITLE}} Bug Workflow

## Purpose

- Use this workflow for clear bugs, failing tests, regressions, crashes, or
  unstable behavior.
- Do not run Codebase Atlas again for ordinary bug fixes; use this workflow and
  update affected atlas docs only if ownership or flows changed.

## Workflow

1. Open `{{INDEX_FILE}}` and choose the most likely owning module.
2. Read that module's dependencies, key flows, known risks, and scope boundary.
3. Inspect the failing runtime path or test path in code.
4. Decide whether the defect is local to the module or caused by upstream input.
5. Keep the fix concentrated in the owning module. Boundary changes require a
   clear reason.
6. Verify the bug is fixed and update atlas docs if ownership or flows changed.

## Pre-Edit Summary

When user confirmation is expected, summarize:

- Symptom
- Root cause hypothesis or confirmed root cause
- Owning module
- Files likely to change
- Behavior before and after
- Tests or checks to run
