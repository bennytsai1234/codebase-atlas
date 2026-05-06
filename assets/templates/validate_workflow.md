# {{ATLAS_TITLE}} Validate Workflow

## Role

This is an internal agent module routed by the main workflow.
The user does not need to know this workflow exists.

Use it internally for checks, reviews, reproductions, verification, and risk
assessment when the user is not asking for immediate implementation.

## Internal Reasoning Layer

Do not output this layer to the user.

1. Preserve the validation question, expected behavior, or risk.
1. Receive the task and already-read index summary from the main workflow.
1. Choose the most relevant module docs for the validation question.
1. Internally confirm validation scope:
   - The specific behavior or assumption being validated.
   - Relevant boundaries and downstream impact.
1. Collect evidence:
   - Read relevant code, tests, configuration, or docs.
   - Read only the minimum content needed to answer the validation question.
1. Internally separate:
   - Conclusions supported by evidence.
   - Parts that still cannot be confirmed.

## External Reporting Layer

1. Report using the Before / After format below.
1. If validation shows a fix is needed, ask whether the user wants to continue
   with a change. Do not start editing immediately.

## Reporting Rules

- Use plain language for every user-facing report.
- Do not expose module names, file paths, function names, or code snippets in
  user-facing reports.
- Before / After is the only human confirmation interface.
- Keep technical details for internal reasoning only.

## Before / After Format

**Before**: In one to three plain sentences, explain what is being validated and
what was uncertain or risky before validation.

**After**: In one to three plain sentences, explain the validation result or
what still cannot be confirmed.

Wait for explicit user confirmation before any file-editing operation.

## Atlas Update Conditions

Update the atlas only when this validation finds existing atlas facts are
inaccurate, such as incorrect module boundary descriptions or changed
ownership. Report newly discovered risks to the user; do not write them back to
the atlas unless they make existing atlas facts inaccurate.

## Delivery Policy

{{DELIVERY_POLICY}}
