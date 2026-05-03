# Doc Output Contract

Use this contract for every atlas. Keep files concise and navigable; the atlas is
a map, not a full architecture book.

This contract is the source of truth for initial decisions, output shape, and
final validation. Keep the skill text-only: use Markdown templates and direct
edits rather than helper scripts or runtime-specific metadata.

## Initial Decisions

Resolve these before scanning the whole repo:

- `mode`: `standalone` or `reference-assisted`.
- `output_language`: `English` or `Traditional Chinese`.
- `delivery_policy`: `no commit`, `commit only`, or `commit and push`.

Infer decisions from the user request and project rules when possible. Ask only
for missing decisions. If `mode` is `reference-assisted`, get the reference
path, URL, or artifact before the full scan.

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
- When consistency matters, read `references/zh-tw-glossary.md` before writing
  Traditional Chinese atlas docs.

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

## Scan Boundaries

Ignore generated, vendored, dependency, cache, and VCS directories when inferring
module boundaries unless the user explicitly asks to document those assets:

- `.git/`, `.hg/`, `.svn/`
- `node_modules/`, `vendor/`, `third_party/`
- `.venv/`, `venv/`, `env/`, `.tox/`
- `dist/`, `build/`, `out/`, `target/`, `.next/`, `.nuxt/`
- `coverage/`, `.cache/`, `.turbo/`, `.parcel-cache/`
- generated lockfile outputs, compiled artifacts, minified bundles, and binary
  assets that do not define source ownership

Generated code may be mentioned as downstream impact, but it should not create a
module boundary unless engineers normally edit or review it directly.

## Standalone Output

```text
docs/
  <project>_index.md
  <project>/
    <module_slug>.md
  <project>_bug_workflow.md
  <project>_feature_workflow.md
  <project>_optimization_workflow.md
  <project>_investigation_workflow.md
  <project>_refactor_workflow.md
  <project>_validation_workflow.md
```

## Reference-Assisted Output

```text
docs/
  <project>_<reference>_index.md
  <project>_<reference>/
    <module_slug>.md
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_optimization_workflow.md
  <project>_<reference>_investigation_workflow.md
  <project>_<reference>_refactor_workflow.md
  <project>_<reference>_validation_workflow.md
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
- Workflow document list with links.
- Module list with links.
- 2-4 line summary per module. Each summary should include routing hints: what
  symptoms, task types, or entry conditions should make a future agent start
  from that module.
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
- Target Change Entry Points
- Known Risks
- Do Not Do

## Workflow Documents

Each workflow must tell future agents how to:

- Start from the index.
- Choose the module or boundary.
- Inspect code after reading atlas context.
- When a task crosses modules, choose one primary owning module based on where
  responsibility, state, data, or behavior first belongs or first becomes wrong.
  Treat other modules as boundary modules and keep those changes minimal unless
  the user explicitly asks for a broader refactor.
- Continue development from the generated workflow docs, not by running
  Codebase Atlas, unless the user explicitly asks for a full rebuild.
- Summarize planned changes before broad edits when user confirmation is
  expected, including before/after behavior, user-visible behavior, internal
  responsibility split, primary module, boundary modules, and checks to run. If
  user or project rules require confirmation, wait after the summary.
- Update affected atlas docs if structure or ownership changes.
- Finish according to the recorded delivery policy: no commit, commit only, or
  commit and push.

Generate these workflow types:

- Bug: defects, regressions, crashes, failing tests, or unstable behavior.
- Feature: new target-project behavior. In reference-assisted mode, generate
  only for explicit feature parity or reference-driven expansion.
- Optimization: improve existing behavior, reliability, clarity,
  maintainability, or performance without unrelated features.
- Investigation: understand unclear behavior, ownership, feasibility, or root
  cause before choosing an implementation workflow.
- Refactor: change structure, ownership, API shape, naming, duplication, or
  module boundaries while preserving intended behavior.
- Validation: check, verify, review, reproduce, or assess risk without
  immediately changing code.

## Final Validation

Before finishing an atlas initialization or rebuild, check the Markdown directly:

- No unreplaced template placeholders remain, such as `{{ATLAS_TITLE}}`.
- Relative links point to generated files that exist.
- The index records one-time usage guidance, rebuild semantics, module links,
  workflow links, routing-oriented module summaries, and delivery policy.
- Each workflow records the same delivery policy as the index.
- Reference-assisted output includes investigation, refactor, validation, bug,
  and optimization workflows by default, and includes a feature workflow only
  when feature parity or reference-driven feature expansion was explicitly
  requested.
- Module docs use the required sections for the selected mode.
- Reference-assisted module docs include target change entry points and known
  risks in addition to reference counterparts and useful patterns.
- Any remaining TODOs represent real uncertainty from the repo or reference, not
  skipped inspection.
