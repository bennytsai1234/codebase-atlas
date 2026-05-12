# {{ATLAS_TITLE}} Main Workflow

## Role

This is the only daily entrypoint for this project.
The user does not need to know that understand, change, and validate workflows
exist. The agent routes automatically based on task intent and may compose
workflows when needed.

## Workflow

1. Open `{{INDEX_FILE}}` before any other operation, while preserving the
   user's original request and intent.
1. Confirm in one plain sentence what this project does.
1. Delivery plan check. If `docs/genius/delivery_plan.md` exists and has at
   least one phase marked 🔲, and the user's request does not point to a
   specific other task, ask in plain language whether to continue with the
   next unfinished phase. Treat the user's answer as the routing decision.
1. Route by task intent:
   - Delivery plan continuation: open `docs/genius/delivery_plan.md`, locate
     the first 🔲 phase, read its deliverables and dependencies, then run the
     change workflow with that phase as the change scope. After completion,
     update the phase marker to ✅.
   - Understanding, explanation, investigation, or feasibility: use the
     understand workflow.
   - Modification, bug fix, feature, optimization, refactor, release,
     dependency upgrade, schema or data migration, configuration change,
     hotfix, or cleanup: use the change workflow with the matching internal
     task type.
   - Validation, review, safety check, reproduction, profiling, CI or build
     failure investigation, or risk assessment: use the validate workflow.
   - Mixed intent: compose workflows in understand, validate, change order.
1. Run the matching workflow internally.
1. Report the result to the user in plain language.
1. If the task edits files, provide the Before / After gate and wait for
   explicit confirmation before editing.
1. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Routing Principles

When intent is unclear, start with understand, then decide whether validate or
change is needed. Never edit files without Before / After confirmation.

When composing workflows, pass the conclusions from the previous workflow into
the next workflow. Do not reread the index or module docs unless the next
workflow needs context that was not already gathered.

Daily maintenance tasks route to the change workflow with an explicit internal
task type. The change workflow has dedicated verification steps for each type.

## Delivery Plan Continuation

When `docs/genius/delivery_plan.md` exists, it represents the source-of-truth
build order produced upstream by Project Genius. The main workflow respects it
in these ways:

- Treat each phase as a bounded unit of change scope.
- Read the phase's `What to build`, `Dependencies`, and `Validation` sections
  before routing into the change workflow.
- Read other `docs/genius/` documents only when the phase references them or
  when the change workflow's internal reasoning needs the context.
- After the phase is delivered and validated, update its marker from 🔲 (or
  ⏳) to ✅ in `docs/genius/delivery_plan.md`. This update is incremental and
  does not require an atlas rebuild.
- If the user explicitly asks for something off-plan, follow the off-plan
  request and do not silently advance the delivery plan.

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
what is wrong, unclear, missing, or risky.

**After**: In one to three plain sentences, explain what will be true after the
operation is complete.

Wait for explicit user confirmation before executing.

## Continuous Work Mode

After each task is complete, ask the user in plain language:

```text
Is there anything else that needs to be handled?
```

If the user continues with another request:

- Do not reread the index.
- Continue from routing judgment.
- Keep plain-language reporting and the Before / After mechanism.
- If `docs/genius/delivery_plan.md` exists and the previous task closed a
  phase, the next routing decision may again offer to continue with the next
  🔲 phase.

End only when the user says there is nothing else to handle.
