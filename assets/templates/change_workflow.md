# {{ATLAS_TITLE}} Change Workflow

## Role

This is an internal agent module routed by the main workflow.
The user does not need to know this workflow exists.

Use it internally for bugs, features, optimizations, and refactors.

## Internal Reasoning Layer

Do not output this layer to the user.

1. Preserve the user's original request.
1. Receive the task and already-read index summary from the main workflow.
1. Choose the most relevant module docs for the task.
1. Internally classify the task:
   - Bug: current behavior is wrong or unstable.
   - Feature: new behavior is requested.
   - Optimization: behavior stays the same while quality improves.
   - Refactor: structure changes while intended behavior stays the same.
1. Calibrate scope internally so Before / After is accurate:
   - What will change.
   - What may be affected downstream.
   - Which boundaries remain uncertain.
1. Inspect code, tests, docs, configs, runtime paths, or reference material only
   when needed.

## External Reporting Layer

1. Confirm with the user using the Before / After format below.
1. Wait for explicit user confirmation before editing any files.
1. After confirmation, implement the change.
1. Validate the affected behavior and boundaries.
1. Finish with one plain-language sentence describing what changed.

## Reporting Rules

- Use plain language for every user-facing report.
- Do not expose module names, file paths, function names, or code snippets in
  user-facing reports.
- Before / After is the only human confirmation interface.
- Keep technical details for internal reasoning only.

## Before / After Format

**Before**: In one to three plain sentences, explain the current situation and
what is wrong, missing, or risky.

**After**: In one to three plain sentences, explain what will be true after the
change is complete.

Wait for explicit user confirmation before any file-editing operation.

## Atlas Update Conditions

Update affected atlas docs only when the change truly changes module
boundaries, ownership, or external APIs. Ordinary bug fixes and small features
do not require atlas updates.

## Delivery Policy

{{DELIVERY_POLICY}}
