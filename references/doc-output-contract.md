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
- `feature_parity`: `disabled` by default, or `enabled` only when the user
  explicitly wants parity, compatibility, migration equivalence, or
  reference-driven feature expansion.

Before asking, briefly explain what Codebase Atlas will do: scan the target
repo, create durable Markdown docs under `docs/`, produce a module index and
module notes, and generate workflow docs for future work. State that generated
workflows should be used for ordinary follow-up work, while rerunning Codebase
Atlas means a full atlas rebuild.

Infer decisions from the user request and project rules only when they are
explicit or clearly documented. If the user request only names the target repo
and says to use Codebase Atlas, ask all initial decisions before the full scan:

1. Should the output be English or Traditional Chinese?
1. Should this be standalone mode, or reference-assisted mode? If
   reference-assisted, get the reference path, URL, or artifact.
1. After each generated workflow finishes, should it do no commit, commit only,
   or commit and push?
1. In reference-assisted mode, should feature parity be enabled?
   Default to disabled unless the user explicitly wants parity, compatibility,
   migration equivalence, or reference-driven feature expansion.

If `mode` is `reference-assisted`, get the reference path, URL, or artifact
before the full scan and resolve whether `feature_parity` is enabled.

## Naming

- Default output directory: `docs/` at the target project root.
- Use lowercase snake_case slugs for generated file and folder names.
- Use relative links for new docs. Preserve absolute links only when updating an
  existing atlas that already uses them.
- Replace `target` and `reference` labels in headings with the actual project or
  reference names when it improves readability.

## Source Of Truth

Generated docs must describe repository-persistent facts, not invocation-local
facts.

Repository-persistent facts are supported by committed target-repo files,
project docs, config, templates, references, commands, public APIs, package
metadata, or explicit integrations represented in the repo.

Invocation-local facts depend on who ran Codebase Atlas this time, such as the
current agent, model, CLI, editor, shell, chat session, temporary workspace
state, or tools available only in this session.

Use invocation-local facts to execute the scan when needed, but do not write
them into module scope, upstream dependencies, downstream impact, ownership,
risks, or key flows. For every dependency or upstream/downstream note, ask:
"Can I point to a committed file or project doc that proves this?" If not,
remove it or rewrite it generically.

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
  <project>_introduction_workflow.md
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
  <project>_<reference>_introduction_workflow.md
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_feature_workflow.md
  <project>_<reference>_optimization_workflow.md
  <project>_<reference>_investigation_workflow.md
  <project>_<reference>_refactor_workflow.md
  <project>_<reference>_validation_workflow.md
```

In reference-assisted mode, always generate the feature workflow for new target
project behavior. When `feature_parity` is disabled, the feature workflow must
state that the reference is guidance, not a feature backlog.

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
- 2-4 line summary per module. Each summary must be routing-oriented, not a
  generic file description. It should answer:
  - What this module owns.
  - When a future agent should start here.
  - Which symptoms, task types, or entry conditions point to it.
- A clear statement of the reference boundary when in reference-assisted mode.

## Standalone Module Document

Use these sections:

- Current State
- Scope
- Upstream Dependencies
- Downstream Impact
- Key Flows
- Common Change Entry Points
- Change Routes
- Known Risks
- Do Not Do

Each module document must include inspected, concrete routing facts:

- `Current State`: what responsibility the module owns now.
- `Scope`: representative files, folders, commands, public APIs, or entrypoints.
- `Common Change Entry Points`: the first files or symbols to inspect for likely
  future tasks.
- `Change Routes`: common multi-file update paths, including what to edit first
  and what must stay synchronized.
- `Known Risks`: facts that affect future edits, such as stale docs, missing
  tests, unclear ownership, brittle state, or contract/template drift.

Avoid module docs that only say what a file is. The doc must help a future agent
decide whether to start there.

## Reference-Assisted Module Document

Use these sections:

- Target Current State
- Target Upstream/Downstream
- Reference Counterpart
- Useful Patterns
- Target Change Entry Points
- Target Change Routes
- Known Risks
- Do Not Do

## Workflow Documents

Each workflow must tell future agents how to:

- Start from the index.
- Choose the module or boundary.
- Inspect code after reading atlas context.
- Treat explicit invocation of the workflow as an analysis gate before edits.
  The agent may inspect code, read docs, run non-destructive checks, and reason
  through engineering details, but it must not edit files for the requested
  change until the user confirms.
- When a task crosses modules, choose one primary owning module based on where
  responsibility, state, data, or behavior first belongs or first becomes wrong.
  Treat other modules as boundary modules and keep those changes minimal unless
  the user explicitly asks for a broader refactor.
- Continue development from the generated workflow docs, not by running
  Codebase Atlas, unless the user explicitly asks for a full rebuild.
- The analysis report may include engineering details such as module ownership,
  affected files, risks, and validation notes, but its final user-facing section
  must be a short plain-language Before / After summary:
  - `Before`: current behavior or state, and what is wrong, confusing, missing,
    or risky.
  - `After`: what the agent will change the behavior or state into.
- Wait for explicit user confirmation after the Before / After summary before
  editing files for bug, feature, optimization, or refactor work.
- Update affected atlas docs if structure or ownership changes.
- Finish according to the recorded delivery policy: no commit, commit only, or
  commit and push.

Generate these workflow types:

- Introduction: explain what the project does in plain language without editing
  files or turning the explanation into an architecture report.
- Bug: defects, regressions, crashes, failing tests, or unstable behavior.
- Feature: new target-project behavior. In reference-assisted mode, the
  reference may guide boundaries and patterns, but it is not a feature backlog
  unless feature parity was explicitly enabled.
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

- Run `references/atlas-quality-checklist.md` as the final human-readable
  quality gate after creating or updating the atlas.
- No unreplaced template placeholders remain, such as `{{ATLAS_TITLE}}`.
- Relative links point to generated files that exist.
- Generated docs contain only repository-persistent facts in module scope,
  dependencies, ownership, risks, and flows. Any invocation-local fact is omitted
  or rewritten generically.
- The index records one-time usage guidance, rebuild semantics, module links,
  workflow links, routing-oriented module summaries, and delivery policy.
- Index module summaries are 2-4 lines each and tell future agents when to start
  from that module.
- Each workflow records the same delivery policy as the index.
- Each code-changing workflow requires a plain-language Before / After summary
  and explicit user confirmation before edits.
- Reference-assisted output includes introduction, bug, feature, optimization,
  investigation, refactor, and validation workflows by default. Feature parity
  changes only whether the feature workflow may treat the reference as a parity
  source.
- Module docs use the required sections for the selected mode.
- Reference-assisted module docs include target change entry points and known
  risks in addition to reference counterparts and useful patterns.
- Any remaining TODOs represent real uncertainty from the repo or reference, not
  skipped inspection.
