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

## Pre-Edit Summary (The Trust Bridge)

Before editing any code, you **must** provide a summary for human confirmation.
Use plain language to build a bridge of trust. Do not proceed until the plan is
verified:

- **Symptom**: Describe what is happening in user-visible terms.
- **Root Cause**: Explain why it is happening (the logical flaw).
- **The Map**: Name the primary owning module and any affected boundary modules.
- **The Plan (Before vs. After)**:
    - **Before**: Current incorrect behavior or logic state.
    - **After**: Expected correct behavior or logic state after the fix.
- **Risk Assessment**: Any side effects or risks to boundary modules.
- **Verification**: Tests or checks that will prove the fix works.

## Delivery Policy

{{DELIVERY_POLICY}}
