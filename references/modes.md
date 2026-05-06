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

Split the project into stable modules. Judge the split by quality:

- Each module should be an independent change boundary, where future engineers
  can work without heavy cross-module coordination.
- Too many modules means the boundaries are too fragmented and most changes
  still cross several modules.
- Too few modules means the boundary is not meaningful and most work starts in
  the same place.
- Small repositories naturally have fewer modules. Do not split modules just to
  create more files.
- Large monorepos may have more modules, but prefer product or domain
  boundaries over technical-layer boundaries.

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
