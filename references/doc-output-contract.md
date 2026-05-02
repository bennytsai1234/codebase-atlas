# Doc Output Contract

Use this contract for every atlas. Keep files concise and navigable; the atlas is
a map, not a full architecture book.

## Naming

- Default output directory: `docs/` at the target project root.
- Use lowercase snake_case slugs for generated file and folder names.
- Use relative links for new docs. Preserve absolute links only when updating an
  existing atlas that already uses them.
- Replace `target` and `reference` labels in headings with the actual project or
  reference names when it improves readability.

## Language

- Generated atlas docs and workflow docs may be written in English or
  Traditional Chinese.
- Follow the user's requested language or the target project's documented
  language rules.
- If no language is clear, ask before creating docs.
- Translate headings and prose when writing Traditional Chinese docs, but keep
  code identifiers, file paths, commands, API names, package names, and product
  names unchanged.
- The bundled templates are English starting shapes, not mandatory English
  output.

## Delivery Policy

- During atlas initialization, ask what future workflow runs should do after
  work is complete: no commit, commit only, or commit and push.
- Record the selected policy in the index and every workflow document.
- For commit-only workflows, require a focused commit after validation.
- For commit-and-push workflows, require validation, a focused commit, and a push
  to the confirmed target remote/branch.
- If the target remote or branch is unclear during a future workflow run, the
  workflow must ask before pushing.
- For no-commit workflows, explicitly leave changes uncommitted and summarize
  validation status.

## Standalone Output

```text
docs/
  <project>_index.md
  <project>/
    <module_slug>.md
  <project>_bug_workflow.md
  <project>_feature_workflow.md
  <project>_optimization_workflow.md
```

## Reference-Assisted Output

```text
docs/
  <project>_<reference>_index.md
  <project>_<reference>/
    <module_slug>.md
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_optimization_workflow.md
```

Add `<project>_<reference>_feature_workflow.md` only when the user explicitly
asks for feature parity or reference-driven feature expansion.

## Index Document

Include:

- Purpose and usage principles.
- One-time usage guidance: initialize once, then use generated workflow docs for
  follow-up work.
- Rebuild semantics: running Codebase Atlas again means a full codebase rescan
  and index/module-doc rebuild from current project reality.
- Delivery policy for future workflow runs.
- Module list with links.
- 2-4 line summary per module.
- A clear statement of the reference boundary when in reference-assisted mode.

## Standalone Module Document

Use these sections:

- Current State
- Scope
- Upstream Dependencies
- Downstream Impact
- Key Flows
- Common Change Entry Points
- Known Risks
- Do Not Do

## Reference-Assisted Module Document

Use these sections:

- Target Current State
- Target Upstream/Downstream
- Reference Counterpart
- Useful Patterns
- Do Not Do

## Workflow Documents

Each workflow must tell future agents how to:

- Start from the index.
- Choose the module or boundary.
- Inspect code after reading atlas context.
- Continue development from the generated workflow docs, not by running
  Codebase Atlas, unless the user explicitly asks for a full rebuild.
- Summarize planned changes before broad edits when user confirmation is
  expected.
- Update affected atlas docs if structure or ownership changes.
- Finish according to the recorded delivery policy: no commit, commit only, or
  commit and push.
