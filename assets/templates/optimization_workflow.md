# {{ATLAS_TITLE}} Optimization Workflow

## Purpose

- Use this workflow to improve existing behavior, reliability, clarity,
  maintainability, or performance without adding unrelated features.
- Do not run Codebase Atlas again for ordinary optimization work; use this
  workflow and update affected atlas docs only if structure or ownership changed.

## Workflow

1. Open `{{INDEX_FILE}}` and choose one target module.
1. Read the module's current state, dependencies, key flows, and known risks.
{{REFERENCE_STEP}}1. Identify the smallest layer that should change: UI, API, runtime, service,
   data, integration, infrastructure, or tooling.
1. List 2-3 concrete optimization directions, then choose one direction for this
   task.
1. Keep user-visible behavior unchanged unless the user requested otherwise.
1. Verify upstream and downstream behavior still works.
1. Update atlas docs if structure, ownership, or risk changed.
1. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Pre-Edit Summary (The Trust Bridge)

Before editing any code, you **must** provide a summary for human confirmation.
Use plain language to build a bridge of trust. Do not proceed until the plan is
verified:

- **Target**: What specific behavior, performance, or clarity is being improved?
- **The Map**: Name the affected module and why it is the right place for this change.
- **Refinement (Before vs. After)**:
    - **Before**: The current suboptimal state (be specific about the pain point).
    - **After**: The expected improved state (be specific about the gain).
- **Safety**: Confirm that external behavior remains unchanged (regression check).
- **Verification**: How we will measure or verify the improvement.

## Delivery Policy

{{DELIVERY_POLICY}}
