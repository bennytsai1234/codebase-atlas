# Atlas Contract

Use this contract for every Codebase Atlas initialization or rebuild.

The atlas is a compact engineering map, not a full architecture book. Keep
generated docs concise, navigable, and grounded in repository-persistent facts.

## Initial Decisions

Resolve these before the full scan:

- `mode`: `standalone` or `reference-assisted`.
- `working_language`: explicit repository language rule first, user's
  initialization request language second, English third.
- `reference_template_mode`: `none`, `partial reference`, or `full alignment`.
  This user-facing decision determines whether the run is standalone or
  reference-assisted, and whether reference functionality is in scope.
- `delivery_policy`: `no commit`, `commit only`, or `commit and push`.
- `reporting_level`: `plain` or `technical`. Plain hides module names, file
  paths, and code snippets from user-facing reports. Technical includes them
  for developer-oriented workflows.
- `workflow_entrypoints`: a default thin adapter is always generated. Additional
  tool-specific entrypoints may be generated when explicitly requested.

Internal decision keys are for atlas generation only. User-facing confirmation
must present these decisions as plain-language questions in the working
language, with the recommended value and reason. Do not expose internal setting
names such as `mode`, `reference_template_mode`, `delivery_policy`,
`reporting_level`, `workflow_entrypoints`, or `feature_parity` directly to the
user.

The reference-template decision must be presented as three plain-language
choices:

- No reference: build the atlas from the target project only.
- Partial reference: use only the user-selected parts of the reference.
- Full alignment: fully match the reference's functionality, only when the user
  explicitly asks for full alignment, parity, compatibility, migration
  equivalence, or reference-driven expansion.

When existing project guidance is found, the confirmation dialog must list each
preserved rule with concrete content and handling:

```text
[Category]
Rule: <specific inherited rule>
Handling: <how this rule will be recorded or applied>
```

## Source Of Truth

Generated docs must describe facts supported by committed files, project docs,
configuration, templates, commands, public APIs, package metadata, or explicit
integrations in the repository.

Do not write invocation-local facts into the atlas: current agent, model,
editor, shell, chat session, temporary workspace state, or session-only tools.

For every dependency, risk, flow, and ownership note, ask whether a committed
file or project doc proves it. If not, remove it or write it as uncertainty.

## Scan Boundaries

Ignore generated, vendored, dependency, cache, build, and VCS directories when
inferring module boundaries unless the user explicitly asks to document them:

- `.git/`, `.hg/`, `.svn/`
- `node_modules/`, `vendor/`, `third_party/`
- `.venv/`, `venv/`, `env/`, `.tox/`
- `dist/`, `build/`, `out/`, `target/`, `.next/`, `.nuxt/`
- `coverage/`, `.cache/`, `.turbo/`, `.parcel-cache/`
- compiled artifacts, minified bundles, and binary assets that do not define
  source ownership

Generated code may be mentioned as downstream impact, but should not define a
module unless engineers normally edit or review it directly.

## Output Shape

Standalone output:

```text
docs/
  <project>_index.md
  <project>/
    <module_slug>.md
  <project>_understand_workflow.md
  <project>_change_workflow.md
  <project>_validate_workflow.md
  <project>_main_workflow.md
  <project>_adapter.md
```

Reference-assisted output:

```text
docs/
  <project>_<reference>_index.md
  <project>_<reference>/
    <module_slug>.md
  <project>_<reference>_understand_workflow.md
  <project>_<reference>_change_workflow.md
  <project>_<reference>_validate_workflow.md
  <project>_<reference>_main_workflow.md
  <project>_<reference>_adapter.md
```

Use lowercase snake_case slugs for generated files and folders. Use relative
links for generated Markdown.

## Required Templates

Use the templates under `assets/templates/`:

- `index.md`
- `module.md`
- `understand_workflow.md`
- `change_workflow.md`
- `validate_workflow.md`
- `main_workflow.md`
- `adapter.md`

Replace all placeholders with concrete project values. Do not leave template
tokens such as `{{ATLAS_TITLE}}` or `{{DELIVERY_POLICY}}` in generated docs.

## Index Requirements

The index must include:

- Purpose and usage rules.
- Initial decisions: mode, working language, reference template mode, delivery
  policy, reporting level, and entrypoints.
- Project operating constraints inherited from existing guidance. This section
  must capture concrete rules that all workflows must follow, such as language,
  architecture, testing, release flow, maintenance state, CI, and work style.
- Rebuild semantics: rerunning Codebase Atlas means a full rescan and atlas
  rebuild from current repository reality.
- Links to the main workflow and three internal workflow docs.
- Links to every module doc.
- Routing-oriented summaries for each module: what it owns, when future work
  should start there, and what symptoms or task types point to it.
- Architecture Decisions table for cross-module decisions recorded during
  development. Starts empty at initialization.
- Reference boundary when in reference-assisted mode.

## Module Requirements

Each module doc must include:

- Current responsibility.
- Scope: representative folders, files, public APIs, entrypoints, commands, or
  tests.
- Dependencies and downstream impact.
- Key flows.
- Common change entry points.
- Change routes: where to start and what must stay synchronized.
- Known risks.
- Do not do boundaries.
- Reference notes only when reference-assisted mode makes them useful.

Avoid file inventories. A module doc is successful when it helps a future agent
decide whether to start there.

## Workflow Requirements

Generate four canonical workflows:

- `understand`: introductions, explanations, feasibility questions, ownership
  questions, and investigations.
- `change`: bugs, features, optimizations, and refactors.
- `validate`: checks, reviews, reproductions, verification, and risk assessment.
- `main`: the universal daily entrypoint that reads the index first, confirms
  in plain language what the project does, and routes to understand, change,
  validate, or a combination.

All workflows must:

- Inspect code only after reading relevant atlas context.
- Use generated workflows for ordinary work instead of rerunning Codebase Atlas.
- Record the same delivery policy as the index.
- Keep technical details for internal reasoning and report to the user
  according to the selected reporting level.
  - Plain: plain language only, no module names, file paths, or code snippets.
  - Technical: include module names, file paths, and relevant code context.
- Require atlas updates only when module boundaries, ownership, external APIs,
  or documented repository facts change.

Every internal workflow must choose the relevant module context and any
necessary boundary context before inspecting code.

The `main` workflow must:

- Be the only entrypoint for daily operations.
- Receive any request, read the index first, and confirm in one plain sentence
  what the project does.
- Route automatically to understand, change, validate, or a composed execution.
- Pass conclusions forward during composed execution so later workflows do not
  reread the index or module docs unless they need context that was not already
  gathered.
- After each completed task, ask whether anything else needs handling. If the
  user continues, route the new request without rereading the index, while
  preserving plain-language reporting and Before / After gates.
- Use reporting-level-appropriate user reports and avoid exposing internal
  reasoning as the user-facing summary.
- Treat Before / After as the only human confirmation interface.

The `change` workflow must require a plain Before / After gate before file
edits. `understand` and `validate` must require the same gate before any
follow-up edit. The gate is the user-facing checkpoint; do not replace it with
secondary engineering reports.

The `change` workflow must escalate to a Decision Gate when the change alters
module boundaries, affects external API contracts, involves irreversible
operations, or has multiple viable approaches with different trade-offs. The
Decision Gate presents options and trade-offs before the Before / After step.

Before any proposed implementation route, workflows must calibrate scope:
owning module, boundary modules, contracts, shared state, persistence, generated
artifacts, tests, downstream users, and uncertain surfaces. Prefer complete,
bounded plans over shortcut-oriented local patches. Scope calibration is
reasoning support; the user-facing confirmation remains Before / After.

## Incremental Atlas Updates

During ordinary workflow operations, atlas updates are incremental:

1. Update only the affected module doc or docs.
2. If the module list or module summaries in the index changed, update the
   index to match.
3. Do not rescan unrelated modules or regenerate workflow docs.
4. Note what changed and why in the report.

A full rescan and rebuild requires the user to explicitly request it by running
Codebase Atlas again.

## Decision Recording

When a Decision Gate is used during a workflow:

- Cross-module decisions: add a row to the Architecture Decisions table in the
  index with the decision title, chosen option, affected modules, and rationale.
- Module-level decisions: add a note to the affected module's Known Risks or
  Do Not Do section, referencing the index entry if cross-module.
- Do not create separate decision log files.

## Entrypoint Adapters

Generate the default adapter for every atlas initialization or rebuild.
Additional adapters may target Codex skills, prompt files, or a custom prompt
directory when requested.

Adapters must:

- Point to `<project>_main_workflow.md`, not the three individual workflow
  docs.
- Include the delivery policy.
- Remind the agent to start from the atlas index.
- Stay extremely thin and avoid copying any workflow body.
