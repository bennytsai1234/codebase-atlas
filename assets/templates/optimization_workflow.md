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

## Pre-Edit Summary

When user confirmation is expected, summarize this and wait if the user or
project rules require confirmation before edits:

- Target module
- Current problem
- Candidate optimization directions and selected direction
- Behavior before and after, including user-visible behavior and internal
  responsibility split
- Explicit non-goals
- Tests or checks to run

## Delivery Policy

{{DELIVERY_POLICY}}
