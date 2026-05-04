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

## Before / After Gate

When this workflow is invoked, do not edit code first. Analyze the bug using the
atlas and code inspection, then provide an analysis report for human
confirmation.

The upper part of the report may include engineering details such as likely
module ownership, root cause, affected files, risks, and checks. The final part
must be only a plain-language Before / After summary:

- **Before**: Explain how the current behavior works and what is wrong.
- **After**: Explain what behavior the fix will produce.

Wait for explicit user confirmation after the Before / After summary before
editing files for the fix.

## Delivery Policy

{{DELIVERY_POLICY}}
