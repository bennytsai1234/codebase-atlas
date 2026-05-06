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
1. Check whether the Decision Gate triggers apply (see below). If any trigger
   matches, use the Decision Gate format instead of the plain Before / After.
1. Inspect code, tests, docs, configs, runtime paths, or reference material only
   when needed.

## External Reporting Layer

1. If Decision Gate triggers matched, present the Decision Gate format first.
   Wait for the user to choose before continuing.
1. Confirm with the user using the Before / After format below.
1. Wait for explicit user confirmation before editing any files.
1. After confirmation, implement the change.
1. Validate the affected behavior and boundaries.
1. Finish with one plain-language sentence describing what changed.

## Reporting Rules

- Before / After is the only human confirmation interface.
- Reporting level for this project: {{REPORTING_LEVEL}}
  - Plain: do not expose module names, file paths, function names, or code
    snippets in user-facing reports.
  - Technical: include module names, file paths, and relevant code context in
    user-facing reports to help the developer locate changes.
- Keep internal reasoning separate from the user-facing summary.

## Before / After Format

**Before**: In one to three plain sentences, explain the current situation and
what is wrong, missing, or risky.

**After**: In one to three plain sentences, explain what will be true after the
change is complete.

Wait for explicit user confirmation before any file-editing operation.

## Decision Gate

The Decision Gate is an escalation from Before / After for changes with broader
impact. Use it when any of these triggers match:

- The change would alter module boundaries (create, remove, or merge modules).
- The change affects an external API contract or public interface.
- There are two or more viable approaches with different trade-offs.
- The change involves an irreversible operation (large-scale deletion, database
  migration, framework replacement).

When triggered, present this format instead of the plain Before / After:

```markdown
## Decision: <one-sentence title>

### Context
Why this decision is needed.

### Options
A. <option A> — <advantages / costs>
B. <option B> — <advantages / costs>

### Impact
Which areas are affected and how.

### Recommendation
Which option is recommended and why.
```

After the user chooses, continue with a Before / After that implements the
chosen option. Record the decision:

- Cross-module decisions: add a row to the Architecture Decisions table in the
  index.
- Module-level decisions: add a note to the affected module's Known Risks or
  Do Not Do section.

## Atlas Update Conditions

Update affected atlas docs only when the change truly changes module
boundaries, ownership, or external APIs. Ordinary bug fixes and small features
do not require atlas updates.

When an update is needed, apply it incrementally:

1. Update only the affected module doc or docs.
2. If the module list or summaries in the index changed, update the index.
3. Do not rescan unrelated modules or regenerate workflow docs.
4. Note what changed and why in the report.

## Delivery Policy

{{DELIVERY_POLICY}}
