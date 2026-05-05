# Modes

## Standalone Mode

Use standalone mode when the target repository is its own source of truth.

Inspect in this order:

1. Existing project docs and rules.
2. Manifests and package metadata.
3. Entrypoints, public APIs, app shells, binaries, routes, or service starts.
4. Source roots, domain folders, shared layers, integrations, storage, jobs,
   tooling, and tests.
5. Existing architecture or decision docs.

Split the project into 6-20 stable modules when honest. Prefer product or
domain boundaries. If those are not visible, use architectural, package,
runtime, data, integration, or tooling boundaries that match how engineers
change the system.

Small repositories should have fewer modules. Do not invent modules from
incidental files.

## Reference-Assisted Mode

Use reference-assisted mode when the user provides a reference repository,
folder, docs, screenshots, product, API spec, or prior implementation.

Rules:

- Understand the target repository first.
- Build the module split from target reality, not from the reference.
- Inspect the reference only after likely target modules are known.
- For each target module, record reference counterparts only when useful.
- Keep the target project as the primary subject.

By default, the reference is guidance for:

- Responsibility boundaries.
- Flow design and sequencing.
- Failure handling and recovery points.
- Diagnostics and testing patterns.
- Naming or conceptual alignment when it reduces confusion.

Do not use the reference to:

- Add unrelated features.
- Force the target into the reference architecture.
- Treat missing target features as bugs.
- Turn the reference into a backlog.

Enable feature parity only when the user explicitly asks for parity,
compatibility, migration equivalence, or reference-driven expansion.
