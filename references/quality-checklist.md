# Quality Checklist

Run this checklist before reporting that an atlas initialization or rebuild is
complete.

## Decisions

- Mode is recorded.
- Working language is recorded and follows explicit repository rules first,
  user initialization language second, English third.
- Reference template mode is recorded as none, partial reference, or full
  alignment.
- Delivery policy is recorded in the index and every workflow.
- The default adapter and any additional entrypoint choices are recorded.
- Partial reference output records the selected reference scope.
- Full alignment output records that reference functionality is in scope.
- User-facing confirmation used plain-language questions instead of exposing
  internal decision keys.
- User-facing reference-template confirmation used no reference, partial
  reference, and full alignment choices instead of the term "feature parity".
- Preserved project rules were confirmed with concrete rule content and
  handling, not vague "will preserve" statements.

## Output Shape

- Output follows the standalone or reference-assisted tree from
  `references/atlas-contract.md`.
- Index links to all workflow docs.
- Index includes project operating constraints inherited from existing guidance.
- Project operating constraints are concrete enough for all workflows to follow.
- Main workflow exists.
- Default adapter exists.
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

- Understand, change, validate, and main workflows exist.
- Main workflow starts by reading the index.
- Main workflow reports in plain language and does not expose module names, file
  paths, function names, or code snippets.
- Main workflow uses Before / After as the only human confirmation interface.
- Understand, change, and validate workflows are internal modules routed by the
  main workflow.
- Internal workflows select relevant module context and any necessary boundary
  context before code inspection.
- Change workflow requires a Before / After gate before edits.
- Understand and validate workflows require a Before / After gate before
  follow-up edits.
- Workflows use Before / After as the user-facing confirmation gate, not
  secondary engineering reports.
- Workflows reason through scope and prefer complete, bounded plans.
- Workflows require atlas updates only when module boundaries, ownership,
  external APIs, or documented repository facts change.
- Default adapter points to the main workflow, not the individual workflow
  modules.

## Reference-Assisted Quality

- Target project remains the primary subject.
- Partial reference material is used only within the user-selected scope.
- Full alignment is used only when the user explicitly requested full
  alignment, parity, compatibility, migration equivalence, or reference-driven
  expansion.
- Reference notes prevent feature creep outside the selected mode.

## Self-Verification Actions

Before the final report:

1. Reread the index and confirm every module summary includes a situational
   description of when future work should start there.
2. Reread the main workflow and confirm its user-facing report rules do not
   expose module names, file paths, function names, or code snippets.
3. Confirm the adapter points to the main workflow, not any individual workflow
   module.
4. Confirm all placeholders have been replaced with concrete project content.

## Final Report

- Report created, updated, and removed files.
- Report remaining TODOs and why they represent real uncertainty.
- Report validation status.
- Apply the selected delivery policy only after validation.
