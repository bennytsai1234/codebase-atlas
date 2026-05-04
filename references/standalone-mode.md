# Standalone Mode

Use standalone mode when the target repository is self-contained and has no
reference material.

## Exploration

Inspect the target project in this order:

1. Existing docs and project rules.
2. Manifests and package metadata such as `package.json`, `pyproject.toml`,
   `Cargo.toml`, `go.mod`, `pubspec.yaml`, `pom.xml`, `build.gradle`, or similar.
3. Entrypoints, app shells, binaries, service starts, libraries, public APIs, and
   routing layers.
4. Source roots, domain folders, shared layers, integrations, storage, network,
   background jobs, tooling, and tests.
5. Recent or existing docs under `docs/`, `architecture/`, `adr/`, or equivalent.

Apply the scan boundaries from `references/doc-output-contract.md`; generated,
vendored, cache, and dependency directories should not define source modules.

## Module Split

Create 6-20 modules. Prefer boundaries that match how engineers would change the
system:

- Product or domain areas when visible.
- Runtime/application layers when the project is infrastructure-heavy.
- Public API, data, integrations, storage, background processing, and shared
  utilities when they carry distinct ownership.
- Tooling and diagnostics only when they are meaningful modification surfaces.

Avoid one module per folder when folders are implementation details. Avoid one
giant module for all shared code if different shared areas change for different
reasons.

For small repositories, do not create artificial modules from incidental files
just to make the list look fuller. Group related small files into meaningful
change surfaces, such as public docs and metadata, templates, language resources,
or contract rules. Every module should answer: "What future change would start
here?"

## Documentation Rules

- Keep each module doc focused on navigation, ownership, dependencies, and risk.
- Mention representative files and entrypoints, not every file.
- Make index summaries routing-oriented: include symptoms, task types, or entry
  conditions that should lead future work to each module.
- Make each module summary 2-4 lines. A single sentence that only names files is
  too thin.
- Keep the atlas agent-neutral. Do not write the current AI runtime, CLI, model,
  editor, or chat environment into upstream dependencies or module facts unless
  it is explicitly present in the repository.
- Record known uncertainty explicitly instead of inventing architecture.
- Include test commands only when they are discoverable from the repo.
- Use the selected output language and the target project's terminology.

## Workflows

Generate introduction, bug, feature, optimization, investigation, refactor, and
validation workflows. Each workflow must require future work to start from the
atlas before editing code or reporting findings. The introduction workflow
should explain what the project does in plain language, not produce a full
architecture report.
