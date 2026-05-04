# {{ATLAS_TITLE}} Validation Workflow

## Purpose

- Use this workflow when the user asks to check, verify, review, reproduce, or
  assess risk without immediately changing code.
- Do not edit code unless the user explicitly asks for a fix or implementation.
- Do not run Codebase Atlas again for ordinary validation; use this workflow and
  report any stale atlas docs as findings.

## Workflow

1. Preserve the validation question, expected behavior, or risk to check.
1. Open `{{INDEX_FILE}}` and choose the affected module or boundary.
1. Read the relevant module docs for scope, dependencies, downstream impact,
   key flows, and known risks.
1. Choose the smallest useful validation method: tests, lint, type checks,
   build, static inspection, smoke checks, reproduction steps, or manual review.
1. Run or inspect only what is needed for the requested confidence level.
1. Record pass, fail, blocked, skipped, and inconclusive results separately.
1. If a fix is needed, recommend the next workflow instead of silently changing
   code.
1. Finish according to this delivery policy when files changed; otherwise
   summarize validation status and state that no commit is needed:
   {{DELIVERY_POLICY}}

## Validation Summary (The Trust Bridge)

Before finalizing the assessment, provide a summary for human review. Use plain
language to build a bridge of trust:

- **Scope**: What specific change, fix, or risk are we validating?
- **The Map**: Which modules are affected?
- **Assessment**:
    - **Evidence**: What did the tests, logs, or code review show?
    - **Confidence**: How certain are we of the result?
- **Conclusion**: Pass/Fail or Risk Level (Low/Medium/High).

## Delivery Policy

{{DELIVERY_POLICY}}
