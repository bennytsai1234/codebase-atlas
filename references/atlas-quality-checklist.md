# Atlas Quality Checklist

Use this checklist after every Codebase Atlas initialization or full rebuild.
It is a human-readable quality gate for a Markdown skill, not a CI substitute.
The agent that created the atlas should run through it before reporting the
work complete.

## Initial Decisions

- The atlas records the selected output language.
- The atlas records standalone or reference-assisted mode.
- The atlas records the future workflow delivery policy: no commit, commit
  only, or commit and push.
- Reference-assisted output records whether feature parity is disabled or
  enabled.
- Any missing decision was resolved before the full scan.

## Output Shape

- The generated files follow the selected standalone or reference-assisted tree
  from `references/doc-output-contract.md`.
- The index links to every generated workflow document.
- The index links to every module document.
- All local Markdown links resolve.
- No unreplaced placeholders remain, including `{{ATLAS_TITLE}}`,
  `{{DELIVERY_POLICY}}`, `{{INDEX_FILE}}`, or `{{REFERENCE_STEP}}`.

## Module Quality

- The atlas uses 6-20 stable modules unless the repository is too small to make
  that honest.
- Modules are change surfaces, not one file per folder.
- Each index module summary is 2-4 lines and tells future agents when to start
  from that module.
- Each module document names concrete scope, common change entry points, change
  routes, known risks, and do-not-do boundaries.
- Dependencies, ownership, flows, and risks are repository-persistent facts,
  not facts about the current agent, model, editor, shell, or chat session.

## Workflow Quality

- Introduction, bug, feature, optimization, investigation, refactor, and
  validation workflows exist.
- Each workflow starts from the index and then chooses the owning module or
  boundary.
- Bug, feature, optimization, and refactor workflows require a plain-language
  Before / After gate before edits.
- Investigation and validation workflows require a plain-language summary before
  final conclusions, and require a Before / After gate before follow-up edits.
- Each workflow says ordinary follow-up work should use the generated docs
  instead of rerunning Codebase Atlas.
- Each workflow records the same delivery policy as the index.
- Workflows require atlas docs to be updated when ownership, APIs, flows, or
  module boundaries change.

## Reference-Assisted Quality

- The target project remains the primary subject.
- Reference material is guidance for boundaries, flows, failure handling, and
  stabilization unless feature parity was explicitly enabled.
- The feature workflow is present even when feature parity is disabled.
- Module docs include target change entry points, target change routes, known
  risks, reference counterparts, and useful patterns.
- `Do Not Do` sections prevent accidental feature creep from the reference.

## Final Report

- The agent reports created and updated files.
- The agent reports any TODOs that remain and why they represent real
  uncertainty.
- The agent reports validation status, including skipped or inconclusive checks.
- If the selected delivery policy requires a commit or push, the agent performs
  that only after validation is complete.
