---
name: codebase-atlas
description: Create or rebuild a compact repository atlas and workflow docs under docs/ for future code navigation, including standalone and reference-assisted scans.
---

# Codebase Atlas

Turn a repository into a compact engineering map that future work can navigate
before editing code. Keep the skill generic: do not assume a language,
framework, product type, app architecture, or reference material format.

Use this skill as a one-time initializer, or as an explicit full rebuild
workflow, for project docs, module maps, dependency and impact summaries, and
bug/feature/optimization workflows. After an atlas exists, ordinary development
should use the generated workflow docs instead of running this skill again.

## Usage Model

Use this skill to set up the development navigation layer once after the project
environment is ready.

- First run: scan the target codebase, create the atlas, and generate the
  workflow docs under `docs/`.
- Later bug, feature, and optimization work: do not run this skill again. Open
  the generated workflow docs and follow them.
- Run this skill again only when the user explicitly asks to rebuild, refresh,
  regenerate, or rescan the atlas. Running it again means performing a full codebase
  scan again and rebuilding the index/module docs from current project reality.
- When rebuilding, inspect existing atlas docs first, then update them to match
  the current codebase. Preserve still-accurate project-specific notes, but do
  not keep stale module boundaries just because they already exist.

## First Question

After reading this file, resolve the atlas mode before scanning the whole repo.

- If the user already specified standalone or reference-assisted mode, use that
  mode.
- If the mode is not specified, ask the user whether this is a standalone
  project or whether reference material should be used.
- If the user chooses reference-assisted mode, ask for the reference material
  path, URL, or artifact before proceeding.
- If the user chooses standalone mode, proceed without reference material.

Also resolve the output language:

- Support English and Traditional Chinese.
- If the user or project rules specify a language, use that language for all
  generated atlas docs and workflow docs.
- If the language is unclear, ask whether the atlas should be written in English
  or Traditional Chinese before creating docs.
- Keep code identifiers, file paths, command names, API names, and product names
  unchanged even when the surrounding prose is translated.

Also resolve the workflow delivery policy:

- Ask what future workflow runs should do after the work is complete:
  no commit, commit only, or commit and push.
- If the user or project rules already specify a commit/push policy, use it.
- If the user chooses commit and push, the generated workflow docs must require
  the agent to confirm the target branch/remote when they are not obvious.
- Record this policy in the generated index and every workflow doc so future
  work follows the same completion rule.

## Mode Decision

- Use **standalone mode** when the target project is the only source of truth.
- Use **reference-assisted mode** when the user provides a reference repo,
  folder, docs, screenshots, product, API specification, or prior implementation.
- In reference-assisted mode, treat the reference as guidance for boundaries,
  flows, failure handling, and stabilization by default. Do not turn it into a
  feature-parity backlog unless the user explicitly asks for feature parity.
- If the user expects a reference but no path or artifact is available, ask for
  that missing reference. Otherwise continue in standalone mode.

## Core Workflow

1. Resolve the atlas mode, output language, and workflow delivery policy using
   the First Question rules above.
2. Ground in the target project. Inspect manifests,
   entrypoints, source roots, tests, build/config files, existing docs, and
   major package boundaries with fast search tools.
3. Read `references/doc-output-contract.md` for required file shapes and naming.
4. Read exactly one mode guide:
   - `references/standalone-mode.md`
   - `references/reference-assisted-mode.md`
5. Split the project into 6-20 stable modules. Prefer product/domain boundaries
   when visible; otherwise use architectural or package boundaries.
6. Create or update the atlas under the target project's `docs/` directory.
   Preserve existing docs style when updating an existing atlas.
7. Generate workflow docs that make future bug fixes, features, and
   optimizations start from the atlas before code edits.
8. Add usage guidance to the index and workflow docs: future work should use the
   generated workflows, while running this skill again is reserved for a full atlas
   rebuild.

## Skeleton Prompt

When creating a new atlas or adding missing atlas files, read
`references/create-doc-skeleton-prompt.md` and use it as the generation
checklist. Prefer direct file edits with the bundled templates over generating
code or running automation. The bundled templates are English starting shapes;
translate headings and prose to Traditional Chinese when the selected output
language is Traditional Chinese.

Never blindly overwrite existing docs. If an atlas file already exists, inspect
it and update it intentionally while preserving useful project-specific content.

## Atlas Usage For Later Code Changes

When an atlas exists, use it as the first navigation layer for future work:

- For bugs, locate the likely module, read upstream/downstream dependencies, then
  inspect the failing path in code.
- For features, find the natural owning module and any boundary modules before
  proposing interfaces or behavior.
- For optimizations, choose one module and one layer of change at a time unless
  the user's request explicitly requires a wider refactor.
- If code structure changes, update the affected atlas documents before closing
  the task.
- Do not use this skill for ordinary follow-up work unless the user asks for a
  full rescan/rebuild. The atlas workflows are the normal continuation path.

When implementation is requested, still use the atlas to scope the work before
editing. When the user expects confirmation before changes, present a concise
change summary first.
