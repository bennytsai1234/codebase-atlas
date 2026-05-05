# Quality Checklist

Run this checklist before reporting that an atlas initialization or rebuild is
complete.

## Decisions

- Mode is recorded.
- Delivery policy is recorded in the index and every workflow.
- Workflow entrypoint choice is recorded.
- Reference-assisted output records whether feature parity is enabled.

## Output Shape

- Output follows the standalone or reference-assisted tree from
  `references/atlas-contract.md`.
- Index links to all workflow docs.
- Index links to all module docs.
- Local Markdown links resolve.
- No unreplaced placeholders remain.

## Module Quality

- Module boundaries are stable change surfaces.
- Module summaries route future work instead of listing files.
- Each module doc names scope, dependencies, change entry points, change routes,
  known risks, and do-not-do boundaries.
- Repository facts are supported by committed files or project docs.
- Invocation-local facts are absent.

## Workflow Quality

- Understand, change, and validate workflows exist.
- Each workflow starts from the index.
- Each workflow requires module and boundary selection before code inspection.
- Change workflow requires a Before / After gate before edits.
- Understand and validate workflows require a Before / After gate before
  follow-up edits.
- Workflows use Before / After as the user-facing confirmation gate, not
  secondary engineering reports.
- Workflows reason through scope and prefer complete, bounded plans.
- Workflows require atlas updates when ownership, APIs, flows, risks, or module
  boundaries change.

## Reference-Assisted Quality

- Target project remains the primary subject.
- Reference material is guidance unless feature parity was explicitly enabled.
- Reference notes prevent feature creep.

## Final Report

- Report created, updated, and removed files.
- Report remaining TODOs and why they represent real uncertainty.
- Report validation status.
- Apply the selected delivery policy only after validation.
