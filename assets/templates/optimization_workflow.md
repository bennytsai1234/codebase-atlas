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

## Before / After Gate

When this workflow is invoked, do not edit code first. Analyze the optimization
target using the atlas and code inspection, then provide an analysis report for
human confirmation.

The upper part of the report may include engineering details such as affected
module, improvement direction, likely files, risks, and checks. The final part
must be only a plain-language Before / After summary:

- **Before**: Explain the current behavior or structure and why it is suboptimal.
- **After**: Explain what will be clearer, faster, safer, or easier to maintain.

Wait for explicit user confirmation after the Before / After summary before
editing files for the optimization.

## Delivery Policy

{{DELIVERY_POLICY}}
