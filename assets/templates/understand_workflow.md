# {{ATLAS_TITLE}} Understand Workflow

## Role

This is an internal agent module routed by the main workflow.
The user does not need to know this workflow exists.

Use it internally for introductions, explanations, ownership questions,
feasibility questions, and investigations.

## Internal Reasoning Layer

Do not output this layer to the user.

1. Preserve the user's question or symptom.
1. Receive the task and already-read index summary from the main workflow.
1. Choose the most relevant module docs for the task. Do not read every module
   doc by default.
1. Inspect code, tests, docs, logs, or config only when module context is not
   enough to answer accurately.
1. Internally separate:
   - Confirmed facts supported by docs or code.
   - Reasonable assumptions that have not been verified.
   - Unknowns that remain.

## External Reporting Layer

1. Answer the user's question in plain language.
1. If there are assumptions or unknowns, state them directly as uncertainty.
1. If follow-up implementation is needed, ask whether the user wants to
   continue with a change.

## Reporting Rules

- Use plain language for every user-facing report.
- Do not expose module names, file paths, function names, or code snippets in
  user-facing reports.
- Before / After is the only human confirmation interface.
- Keep technical details for internal reasoning only.

## Before / After Format

**Before**: In one to three plain sentences, explain the current situation and
what is wrong, unclear, missing, or risky.

**After**: In one to three plain sentences, explain what will be true after the
operation is complete.

Wait for explicit user confirmation before any file-editing operation.

## Atlas Update Conditions

Update the atlas only when this investigation finds existing atlas facts are
inaccurate, such as incorrect module boundary descriptions or changed
ownership. Report newly discovered risks to the user; do not write them back to
the atlas unless they make existing atlas facts inaccurate.

## Delivery Policy

{{DELIVERY_POLICY}}
