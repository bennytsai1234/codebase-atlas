# Atlas Contract

Use this contract for every Codebase Atlas initialization or rebuild.

The atlas is a compact engineering map, not a full architecture book. Keep
generated docs concise, navigable, and grounded in repository-persistent facts.

## Initial Decisions

Resolve these before the full scan:

- `mode`: `standalone` or `reference-assisted`.
- `working_language`: explicit repository language rule first, user's
  initialization request language second, English third.
- `delivery_policy`: `no commit`, `commit only`, or `commit and push`.
- `workflow_entrypoints`: a default thin adapter is always generated. Additional
  tool-specific entrypoints may be generated when explicitly requested.
- `feature_parity`: only relevant in reference-assisted mode. It is disabled by
  default and enabled only for explicit parity, compatibility, migration
  equivalence, or reference-driven expansion.

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
- Initial decisions: mode, working language, delivery policy, entrypoints, and
  feature parity when relevant.
- Rebuild semantics: rerunning Codebase Atlas means a full rescan and atlas
  rebuild from current repository reality.
- Links to the main workflow and three internal workflow docs.
- Links to every module doc.
- Routing-oriented summaries for each module: what it owns, when future work
  should start there, and what symptoms or task types point to it.
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
- Keep technical details for internal reasoning and report to the user in plain
  language.
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
- Use plain-language user reports and avoid exposing module names, file paths,
  function names, or code snippets.
- Treat Before / After as the only human confirmation interface.

The `change` workflow must require a plain Before / After gate before file
edits. `understand` and `validate` must require the same gate before any
follow-up edit. The gate is the user-facing checkpoint; do not replace it with
secondary engineering reports.

Before any proposed implementation route, workflows must calibrate scope:
owning module, boundary modules, contracts, shared state, persistence, generated
artifacts, tests, downstream users, and uncertain surfaces. Prefer complete,
bounded plans over shortcut-oriented local patches. Scope calibration is
reasoning support; the user-facing confirmation remains Before / After.

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
