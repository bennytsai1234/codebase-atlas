---
name: codebase-atlas
description: "Use only when the user asks to initialize, create, rebuild, refresh, regenerate, or rescan a compact repository atlas under docs/ for future code navigation. Creates a module index, module notes, and three reusable workflows: understand, change, and validate. Supports standalone and reference-assisted scans, plus optional thin workflow entrypoints when explicitly requested."
---

# Codebase Atlas

Codebase Atlas turns a repository into a compact engineering map. Use it for
atlas initialization or a deliberate full rebuild, not for ordinary follow-up
development.

Keep this skill simple:

- Generated Markdown under `docs/` is the canonical atlas.
- References define the rules; templates define the output shape.
- Do not add runtime assumptions, helper scripts, or product-specific behavior
  to this skill.
- Write atlas content in English unless the target repository has an explicit
  language rule.

## Before Scanning

If the user only asks to run Codebase Atlas on a target repository, pause before
the full scan and resolve:

1. **Mode**: standalone, or reference-assisted with a reference path, URL, or
   artifact.
2. **Delivery policy** for future workflow runs: no commit, commit only, or
   commit and push.
3. **Workflow entrypoints**: docs only by default; generate Codex skills,
   prompt files, or a custom prompt directory only when explicitly requested.
4. **Feature parity** only in reference-assisted mode: disabled by default;
   enabled only for explicit parity, compatibility, migration equivalence, or
   reference-driven expansion.

Briefly explain that the skill will scan the repository, create durable
Markdown docs under `docs/`, and generate workflows for future understanding,
changes, and validation. After the atlas exists, ordinary work should use those
generated workflows instead of rerunning this skill.

## Main Workflow

1. Read `references/atlas-contract.md`.
2. Resolve the initial decisions above.
3. Inspect the target repository: manifests, entrypoints, source roots, tests,
   build/config files, existing docs, and major package or domain boundaries.
4. Read `references/modes.md` and follow either standalone or
   reference-assisted guidance.
5. Split the project into 6-20 stable modules, unless the repository is too
   small for that to be honest.
6. Create or update the canonical atlas under `docs/` using templates from
   `assets/templates/`.
7. Generate exactly three canonical workflow docs:
   - `understand`: introductions and investigations.
   - `change`: bugs, features, optimizations, and refactors.
   - `validate`: checks, reviews, reproductions, and risk assessments.
8. Generate thin entrypoint adapters only if requested. Adapters must point back
   to the canonical `docs/` workflow files.
9. Run `references/quality-checklist.md` before reporting completion.

## Core Rules

- Do not blindly overwrite existing atlas docs. Preserve useful project-specific
  notes and remove stale boundaries during rebuilds.
- Generated docs must describe repository-persistent facts, not facts about the
  current agent, model, editor, shell, chat session, or temporary workspace.
- Code-changing workflows must require a plain Before / After gate before
  edits. This gate is the user-facing checkpoint; do not replace it with
  secondary engineering reports:
  - **Before**: current state and what is wrong, missing, confusing, or risky.
  - **After**: what the change will make true.
- Before proposing a change, calibrate scope: owning module, boundary modules,
  contracts, shared state, generated artifacts, tests, downstream users, and
  uncertain surfaces. Use this to reason, not as a substitute for the
  Before / After gate.
- Prefer complete, bounded plans over shortcut-oriented local patches.
- Update affected atlas docs when ownership, APIs, flows, risks, or module
  boundaries change.

## When Not To Use This Skill

Do not run Codebase Atlas for ordinary bug fixes, feature work, optimization,
investigation, refactor, or validation after an atlas exists. Open the generated
workflow docs and follow them.
