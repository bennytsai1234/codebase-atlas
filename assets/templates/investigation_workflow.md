# {{ATLAS_TITLE}} Investigation Workflow

## Purpose

- Use this workflow when the behavior, ownership, feasibility, or root cause is
  unclear and the first task is to understand the system.
- Do not edit code during investigation unless the user explicitly asks for a
  fix or implementation.
- Do not run Codebase Atlas again for ordinary investigation; use this workflow
  and note any atlas updates that would be needed.

## Workflow

1. Preserve the user's original question or symptom.
1. Open `{{INDEX_FILE}}` and choose the most likely owning module or boundary.
1. Read the relevant module docs for scope, upstream dependencies, downstream
   impact, key flows, and known risks.
1. Inspect the actual code, tests, docs, runtime paths, logs, or configs needed
   to verify the behavior.
1. Separate confirmed facts, hypotheses, unknowns, and assumptions.
1. Trace the flow until the likely owner, failure point, or decision boundary is
   clear enough for the next task.
1. Recommend the next workflow if follow-up work is needed: bug, feature,
   optimization, refactor, or validation.
1. Finish according to this delivery policy when files changed; otherwise
   summarize findings and state that no commit is needed: {{DELIVERY_POLICY}}

## Investigation Summary

Before finalizing findings, provide a plain-language summary for human review:

- **Inquiry**: What specific question or behavior were we investigating?
- **The Map**: Which modules were traced?
- **Discoveries**:
    - **Knowns**: Confirmed facts about the current behavior.
    - **Hypotheses**: What we suspect but haven't proven yet.
    - **Unknowns**: What remains unclear.
- **Next Steps**: Recommended implementation workflow (Bug, Feature, etc.).

If the next step would edit files, include a plain-language Before / After
summary for that proposed change and wait for explicit user confirmation before
starting follow-up edits.

## Delivery Policy

{{DELIVERY_POLICY}}
