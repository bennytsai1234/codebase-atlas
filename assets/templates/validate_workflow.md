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

- Before / After is the only human confirmation interface.
- Reporting level for this project: {{REPORTING_LEVEL}}
  - Plain: do not expose module names, file paths, function names, or code
    snippets in user-facing reports.
  - Technical: include module names, file paths, and relevant code context in
    user-facing reports to help the developer locate changes.
- Keep internal reasoning separate from the user-facing summary.

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

When an update is needed, apply it incrementally:

1. Update only the affected module doc or docs.
2. If the module list or summaries in the index changed, update the index.
3. Do not rescan unrelated modules or regenerate workflow docs.
4. Note what changed and why in the report.

## Delivery Policy

{{DELIVERY_POLICY}}
