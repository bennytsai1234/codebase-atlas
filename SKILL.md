---
name: codebase-atlas
description: "Use only when the user asks to initialize, create, rebuild, refresh, regenerate, or rescan a compact repository atlas under docs/ for future code navigation. Creates a module index, module notes, four reusable workflows: main, understand, change, and validate, plus a default thin adapter. Supports standalone and reference-assisted scans."
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
- Determine the working language before any user-facing output. Prefer an
  explicit repository language rule, then the user's initialization request
  language, then English. Use the selected language for user-facing output and
  generated atlas docs.

## Before Scanning

If the user only asks to run Codebase Atlas on a target repository, silently
detect the working language and whether old atlas files exist before any
user-facing output. Then introduce the skill before any full scan or
user-facing decision.

### Step 0: Detect Language Silently

Before outputting anything, determine the working language:

1. Check the repository root for an explicit language rule in files such as
   `.cursorrules`, `CONTRIBUTING.md`, `README`, or existing docs.
2. If the repository has no explicit language rule, use the language of the
   user's initialization request.
3. If neither provides a clear signal, use English.

Use this language for the introduction, confirmation dialog, and generated
atlas documents. Keep this step silent; do not report the language decision
until the confirmation dialog.

### Step 1: Detect Old Atlas Silently

Before outputting anything, scan only for old Codebase Atlas artifacts:

1. Detect whether old atlas docs exist under `docs/`.
2. Detect whether generated Codebase Atlas entrypoints exist under `.agents/`
   or other configured prompt or skill directories.
3. Detect existence only. Do not deeply read old atlas content.
4. If old atlas docs or generated entrypoints exist, record them and tell the
   user after the skill introduction.
5. After the introduction, wait for the user to decide whether to delete and
   rebuild before continuing.
6. If the user chooses delete and rebuild, delete both:
   - Old atlas docs.
   - Generated Codebase Atlas entrypoints that point to those old docs.
7. Do not delete unrelated `.agents/` content or any file whose Codebase Atlas
   origin cannot be confirmed.
8. If the user wants to preserve any part, read only the parts the user asked
   to preserve after the user gives preservation instructions.

### Step 2: Introduce This Skill

Before starting any full scan or question, explain what this skill will create
for the user's project. Use the working language selected in Step 0. Render the
following meaning in that language; do not output this English template verbatim
unless English was selected:

```markdown
Before we start, let me explain what this skill will create for your project.

**What it creates:**
This skill scans your repo once and creates a durable engineering map under
`docs/`.
That map includes:
- The project's module structure and boundaries.
- A universal entrypoint skill that future work on this project should start
  from.

**How to use it later:**
After the map exists, you do not need to run this skill again.
For future requests in this project, the universal entrypoint skill will
automatically identify what you want to do and choose the right workflow,
whether the task is understanding the project, changing code, or validating
behavior.

**Why it works:**
Before every operation, the agent reads the map instead of blindly searching the
entire repo again. This helps the agent locate the right area precisely instead
of guessing.

More importantly, every file-editing operation first explains in plain language:
- Before: what the current situation is and where the problem is.
- After: what will become true after the change.

This Before / After is the only thing you need to judge.
You do not need to read code or understand technical details. If the Before
description matches the real problem and the After description is the result you
want, you can confirm. If the agent misunderstood, the Before will be wrong and
you can catch it immediately.

This initialization only needs to happen once.
```

If Step 1 detected old atlas artifacts, add this message after the introduction
in the working language:

```markdown
I found existing atlas artifacts for this project, including old atlas docs or
generated entrypoints. Should I delete them and rebuild the atlas from scratch?
If you want to preserve any parts, tell me which parts.
```

If old atlas artifacts were detected, wait for user confirmation before
continuing to Step 3. If no old atlas artifacts were detected, continue
directly to Step 3.

### Step 3: Pre-Scan Existing Rules

After the introduction and any old-atlas handling, pre-scan existing rules
before asking for configuration decisions:

1. Scan the repository root and `docs/` for `CONTRIBUTING.md`, `README`,
   `.cursorrules`, and any language or maintenance policy files.
2. Scan for explicit language rules, such as Traditional Chinese, Simplified
   Chinese, or English.
3. Scan for maintenance policy signals, such as pure maintenance mode, feature
   freeze, or active development.
4. Bring those findings into a confirmation dialog that explains:
   - Each existing rule found, grouped by category.
   - The concrete content of each rule, not a vague summary.
   - How each rule will be handled in the atlas.
   - Which rules will be written into the index as project operating
     constraints.
   - Which rules may need adjustment or removal.
   - The selected working language and why it was selected.
   - Recommended values for the initial decisions.
5. Present the initial decisions as plain-language questions in the working
   language. Do not expose internal setting names such as `mode`,
   `delivery_policy`, `workflow_entrypoints`, `reference_template_mode`, or
   `feature_parity` to the user. For each decision, include the question the
   user needs to answer, the recommended value, and why that value is
   recommended.
6. Present the reference-template decision in this plain-language shape,
   translated into the working language:

   ```markdown
   Do you have a reference template or specification?

   A. No. Build the atlas from this project only.
   B. Yes, but only use selected parts of the reference. Full feature alignment
      is not required.
   C. Yes, and this project must fully match the reference's functionality.

   If you choose B, what parts should I use as reference?
   For example: only its data-flow design, only its UI structure, or only its
   error-handling approach.
   ```

   Do not use the term "feature parity" in user-facing explanations. Keep that
   term, if needed, for internal reasoning only.
7. Use this confirmation shape for preserved rules:

   ```text
   [Category]
   Rule: <specific inherited rule>
   Handling: <how this rule will be recorded or applied>
   ```

   The user must be able to judge whether the agent correctly understood the
   existing project guidance.
8. Wait for user confirmation before starting the full scan.

## Main Workflow

1. Read `references/atlas-contract.md`.
2. Run the language detection, old-atlas detection, introduction, and pre-scan
   above, then resolve the initial decisions with the user.
3. Inspect the target repository: manifests, entrypoints, source roots, tests,
   build/config files, existing docs, and major package or domain boundaries.
4. Read `references/modes.md` and follow either standalone or
   reference-assisted guidance.
5. Split the project into stable modules using change-boundary quality, not a
   hard module count.
6. Create or update the canonical atlas under `docs/` using templates from
   `assets/templates/`.
7. Generate four canonical workflow docs:
   - `understand`: introductions and investigations.
   - `change`: bugs, features, optimizations, and refactors.
   - `validate`: checks, reviews, reproductions, and risk assessments.
   - `main`: the universal daily entrypoint, automatic router, and default
     generated workflow.
8. Generate the default thin adapter. It must point to the canonical
   `main` workflow, not the individual workflow modules.
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
- Update affected atlas docs only when module boundaries, ownership, external
  APIs, or documented repository facts change.

## When Not To Use This Skill

Do not run Codebase Atlas for ordinary bug fixes, feature work, optimization,
investigation, refactor, or validation after an atlas exists. Open the generated
workflow docs and follow them.
