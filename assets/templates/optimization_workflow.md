# {{ATLAS_TITLE}} Optimization Workflow

## Purpose

- Use this workflow to improve existing behavior, reliability, clarity,
  maintainability, or performance without adding unrelated features.
- Do not run Codebase Atlas again for ordinary optimization work; use this
  workflow and update affected atlas docs only if structure or ownership changed.

## Workflow

1. Open `{{INDEX_FILE}}` and choose one target module.
2. Read the module's current state, dependencies, key flows, and known risks.
{{REFERENCE_STEP}}{{LAYER_STEP_NUMBER}}. Identify the smallest layer that should change: UI, API, runtime, service,
   data, integration, infrastructure, or tooling.
{{BEHAVIOR_STEP_NUMBER}}. Keep user-visible behavior unchanged unless the user requested otherwise.
{{VERIFY_STEP_NUMBER}}. Verify upstream and downstream behavior still works.
{{DOC_STEP_NUMBER}}. Update atlas docs if structure, ownership, or risk changed.

## Pre-Edit Summary

When user confirmation is expected, summarize:

- Target module
- Current problem
- Optimization direction
- Behavior before and after
- Explicit non-goals
- Tests or checks to run
