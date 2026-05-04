# Reference-Assisted Mode

Use reference-assisted mode when a target project should be understood alongside
reference material. The reference may be another repo, a folder, technical docs,
API docs, product screenshots, specs, or a prior implementation.

## Exploration

1. Inspect the target project first. Build the target module split from target
   reality, not from the reference.
2. Inspect the reference only after the target's likely modules are known.
3. For each target module, find the closest reference counterpart only when it is
   relevant. Some target modules may have no reference counterpart.
4. Compare responsibility boundaries, data flow, state lifecycle, error handling,
   validation, diagnostics, test strategy, and operational safeguards.

Apply the scan boundaries from `references/doc-output-contract.md` to both the
target and any repository-like reference material.

## Reference Boundary

By default, the reference is not a backlog. Use it for:

- Responsibility and module boundary ideas.
- Stable flow design and sequencing.
- Failure mode handling and recovery points.
- Diagnostics and testing patterns.
- Naming or conceptual alignment when it reduces confusion.

Do not use the reference to:

- Add unrelated features.
- Force the target project into the reference's architecture.
- Expand scope beyond the user's stated goal.
- Treat missing target features as bugs.

Only produce feature-parity docs when the user explicitly enables feature
parity, or asks for parity, compatibility, migration equivalence,
reference-driven feature expansion, or feature alignment.

## Documentation Rules

- Name both sides clearly, for example `Target Current State` and
  `Reference Counterpart`, or replace those with project-specific names.
- Use the selected output language. In Traditional Chinese docs, translate
  headings and prose while preserving code identifiers, file paths, commands,
  API names, and product names.
- Keep the target project as the primary subject.
- Record useful reference patterns as possible guidance, not required changes.
- Include representative target change entry points and known risks so future
  work can move from the atlas into code without rediscovering the module.
- Include `Do Not Do` sections to prevent accidental feature creep.

## Workflows

Generate bug, optimization, investigation, refactor, and validation workflows by
default. Add a feature workflow only when feature parity was explicitly enabled
or the user asked for feature parity, compatibility, migration equivalence, or
reference-driven feature expansion.
