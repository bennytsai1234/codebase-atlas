# {{ATLAS_TITLE}} Validate Workflow

## Purpose

Use this workflow for checks, reviews, reproductions, verification, and risk
assessment when the user is not asking for immediate implementation.

Do not edit files unless the user explicitly asks for a fix or implementation.

## Workflow

1. Preserve the validation question, expected behavior, or risk.
1. Open `{{INDEX_FILE}}`.
1. Choose the affected module and any boundary modules.
1. Read relevant module docs for scope, dependencies, downstream impact, key
   flows, and known risks.
1. Calibrate validation scope: contracts, generated artifacts, tests,
   downstream users, and uncertain surfaces.
1. Run or inspect evidence needed for the user's validation question.
1. Report only what the evidence shows and what remains unresolved.
1. If a fix is needed, recommend the change workflow instead of silently editing
   files.
1. Finish according to this delivery policy when files changed; otherwise state
   that no commit is needed: {{DELIVERY_POLICY}}

## Summary Format

- **Before**: What was being checked, and what was uncertain or risky before
  validation?
- **After**: What the validation shows now, or what remains unresolved?

If validation recommends edits, provide a plain Before / After summary and wait
for explicit user confirmation before editing.
