---
name: codebase-atlas
description: Use only when the user asks to initialize, create, rebuild, refresh, regenerate, or rescan a compact repository atlas and workflow docs under docs/ for future code navigation. Supports standalone and reference-assisted scans. Before a full scan, explain what Codebase Atlas will create and resolve output language, atlas mode, workflow delivery policy, and feature parity workflow preference.
---

# Codebase Atlas

Turn a repository into a compact engineering map that future work can navigate
before editing code. Keep the skill generic: do not assume a language,
framework, product type, app architecture, or reference material format.

Use this skill as a one-time initializer, or as an explicit full rebuild
workflow, for project docs, module maps, dependency and impact summaries, and
bug, feature, optimization, investigation, refactor, and validation workflows.
After an atlas exists, ordinary development should use the generated workflow
docs instead of running this skill again.

This skill is intentionally text-only and generic. Do not add helper scripts,
runtime-specific agent metadata, or product-specific assumptions to the skill
itself. Create and update atlas files by editing Markdown directly.

## Opening Briefing

Before scanning the whole repo, briefly explain what this skill does in the
user's language:

- It scans the target repository and creates durable Markdown docs under
  `docs/`.
- It produces a module index, per-module ownership/dependency notes, known
  risks, common change entry points, and workflow docs for future work.
- After the atlas exists, ordinary bug, feature, optimization, investigation,
  refactor, and validation work should use the generated workflow docs instead
  of rerunning Codebase Atlas.
- In reference-assisted mode, the reference is guidance for boundaries, flows,
  failure handling, and stabilization. It is not a feature backlog unless the
  user explicitly asks for feature parity.

If the user's request only says to use Codebase Atlas for a target repo, for
example "use Codebase Atlas to process reader", do not start the full scan yet.
Ask for the missing initial decisions first:

1. Output language: English or Traditional Chinese.
1. Atlas mode: standalone, or reference-assisted with the reference path, URL,
   or artifact.
1. Workflow delivery policy: no commit, commit only, or commit and push.
1. In reference-assisted mode, whether to enable feature parity workflow docs.
   Default to no unless the user explicitly wants parity, compatibility,
   migration equivalence, or reference-driven feature expansion.

## Usage Model

Use this skill to set up the development navigation layer once after the project
environment is ready.

- First run: scan the target codebase, create the atlas, and generate the
  workflow docs under `docs/`.
- Later bug, feature, optimization, investigation, refactor, and validation
  work: do not run this skill again. Open the generated workflow docs and follow
  them.
- Run this skill again only when the user explicitly asks to rebuild, refresh,
  regenerate, or rescan the atlas. Running it again means performing a full codebase
  scan again and rebuilding the index/module docs from current project reality.
- When rebuilding, inspect existing atlas docs first, then update them to match
  the current codebase. Preserve still-accurate project-specific notes, but do
  not keep stale module boundaries just because they already exist.

## First Decisions

Before scanning the whole repo, read `references/doc-output-contract.md` and
resolve the initial decisions it defines:

- atlas mode: standalone or reference-assisted
- output language: English or Traditional Chinese
- workflow delivery policy: no commit, commit only, or commit and push
- feature parity workflow: disabled by default; enabled only for explicit
  parity, compatibility, migration-equivalence, or reference-driven feature
  expansion work

Infer these from an explicit user request or project rules when they are clear.
If the user only names the skill and target repo, treat these decisions as
missing and ask before scanning. If reference-assisted mode is selected, get the
reference path, URL, or artifact before the full scan and ask whether feature
parity workflow docs should be enabled.

## Mode Decision

- Use **standalone mode** when the target project is the only source of truth.
- Use **reference-assisted mode** when the user provides a reference repo,
  folder, docs, screenshots, product, API specification, or prior implementation.
- In reference-assisted mode, treat the reference as guidance for boundaries,
  flows, failure handling, and stabilization by default. Do not turn it into a
  feature-parity backlog unless the user explicitly asks for feature parity.
- Generate feature parity workflow docs in reference-assisted mode only when the
  user enables feature parity or asks for parity, compatibility, migration
  equivalence, or reference-driven feature expansion.
- If the user expects a reference but no path or artifact is available, ask for
  that missing reference. Otherwise continue in standalone mode.

## Core Workflow

1. Read `references/doc-output-contract.md`, give the opening briefing, then
   resolve the atlas mode, output language, workflow delivery policy, feature
   parity workflow preference, and any required reference material.
1. Ground in the target project. Inspect manifests,
   entrypoints, source roots, tests, build/config files, existing docs, and
   major package boundaries with fast search tools. Apply the scan boundaries in
   the output contract so generated, vendored, and cache directories do not
   shape the atlas.
1. Read exactly one mode guide:
   - `references/standalone-mode.md`
   - `references/reference-assisted-mode.md`
1. Split the project into 6-20 stable modules. Prefer product/domain boundaries
   when visible; otherwise use architectural or package boundaries.
1. Create or update the atlas under the target project's `docs/` directory.
   Preserve existing docs style when updating an existing atlas.
1. Generate workflow docs that make future bug fixes, features, optimizations,
   investigations, refactors, and validations start from the atlas before code
   edits.
1. Add usage guidance to the index and workflow docs: future work should use the
   generated workflows, while running this skill again is reserved for a full atlas
   rebuild.

## Skeleton Prompt

When creating a new atlas or adding missing atlas files, read
`references/create-doc-skeleton-prompt.md` and use it as the generation
checklist. Prefer direct file edits with the bundled templates. Do not generate
automation for this task unless the user explicitly asks for automation outside
the skill itself.

The bundled templates are English starting shapes. When the selected output
language is Traditional Chinese, translate headings and prose and optionally read
`references/zh-tw-glossary.md` for consistent terms. Keep code identifiers, file
paths, command names, API names, and product names unchanged.

Never blindly overwrite existing docs. If an atlas file already exists, inspect
it and update it intentionally while preserving useful project-specific content.

## Core Philosophy: Verifiable Problem-Solving

This skill is governed by three pillars to ensure accuracy and trust:

1.  **Map-Based Reasoning**: Never guess. Always use the Atlas index and module
    docs to locate the context before inspecting code.
2.  **The Trust Bridge**: AI must use plain language to explain its
    understanding and intent. Complexity is a sign of poor understanding.
3.  **Human-in-the-Loop (HITL)**: The AI proposes, the human confirms. No
    significant code edit should occur without a verified plan that describes
    the "before vs. after" state.

## Atlas Usage For Later Code Changes

When an atlas exists, use it as the first navigation layer for future work:

- For bugs, locate the likely module, read upstream/downstream dependencies, then
  inspect the failing path in code.
- For features, find the natural owning module and any boundary modules before
  proposing interfaces or behavior.
- For optimizations, choose one module and one layer of change at a time unless
  the user's request explicitly requires a wider refactor.
- For investigations, read atlas context before tracing code and separate facts,
  hypotheses, and unknowns.
- For refactors, identify owning and boundary modules, preserve behavior, and
  update atlas docs when ownership, APIs, or flows changed.
- For validations, choose the affected module first, then run or inspect only
  the checks needed for the requested confidence level.
- If code structure changes, update the affected atlas documents before closing
  the task.
- Do not use this skill for ordinary follow-up work unless the user asks for a
  full rescan/rebuild. The atlas workflows are the normal continuation path.

When implementation is requested, still use the atlas to scope the work before
editing. When the user expects confirmation before changes, present a concise
change summary first.
