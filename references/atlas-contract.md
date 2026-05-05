# Atlas Contract

Use this contract for every Codebase Atlas initialization or rebuild.

The atlas is a compact engineering map, not a full architecture book. Keep
generated docs concise, navigable, and grounded in repository-persistent facts.

## Initial Decisions

Resolve these before the full scan:

- `mode`: `standalone` or `reference-assisted`.
- `delivery_policy`: `no commit`, `commit only`, or `commit and push`.
- `workflow_entrypoints`: `docs only` by default; generate tool-specific
  entrypoints only when explicitly requested.
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
- `adapter.md` only when workflow entrypoints were requested

Replace all placeholders with concrete project values. Do not leave template
tokens such as `{{ATLAS_TITLE}}` or `{{DELIVERY_POLICY}}` in generated docs.

## Index Requirements

The index must include:

- Purpose and usage rules.
- Initial decisions: mode, delivery policy, entrypoints, and feature parity when
  relevant.
- Rebuild semantics: rerunning Codebase Atlas means a full rescan and atlas
  rebuild from current repository reality.
- Links to the three workflow docs.
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

Generate exactly three canonical workflows:

- `understand`: introductions, explanations, feasibility questions, ownership
  questions, and investigations.
- `change`: bugs, features, optimizations, and refactors.
- `validate`: checks, reviews, reproductions, verification, and risk assessment.

Every workflow must:

- Start from the index.
- Choose the owning module and any boundary modules.
- Inspect code only after reading relevant atlas context.
- Use generated workflows for ordinary work instead of rerunning Codebase Atlas.
- Record the same delivery policy as the index.
- Require atlas updates when ownership, APIs, flows, risks, or module boundaries
  change.

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

Generate adapters only when requested. They may target Codex skills, prompt
files, or a custom prompt directory.

Adapters must:

- Point back to the canonical workflow doc.
- Include the delivery policy.
- Remind the agent to start from the atlas index.
- Preserve Before / After gates by reference.
- Stay thin and avoid copying the full workflow body.
