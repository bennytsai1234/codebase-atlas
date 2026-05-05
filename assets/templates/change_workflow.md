# {{ATLAS_TITLE}} Change Workflow

## Purpose

Use this workflow for bugs, features, optimizations, and refactors.

Do not rerun Codebase Atlas for ordinary change work. Use this workflow and
update affected atlas docs only when ownership, APIs, flows, risks, or module
boundaries change.

## Workflow

1. Preserve the user's original request.
1. Open `{{INDEX_FILE}}`.
1. Choose the primary owning module and any boundary modules.
1. Read relevant module docs for scope, dependencies, impact, change routes, and
   known risks.
1. Inspect the relevant code, tests, docs, configs, runtime paths, or reference
   material.
1. Classify the task:
   - **Bug**: current behavior is wrong or unstable.
   - **Feature**: new target-project behavior is requested.
   - **Optimization**: existing behavior, reliability, clarity,
     maintainability, or performance should improve.
   - **Refactor**: structure, ownership, API shape, naming, duplication, or
     boundaries should change while intended behavior stays the same.
1. Calibrate scope before proposing edits: owning module, boundary modules,
   contracts, shared state, persistence, generated artifacts, tests, downstream
   users, and uncertain surfaces.
1. Use that analysis to write a plain Before / After gate. Do not turn the gate
   into a secondary engineering report.
1. Wait for explicit user confirmation.
1. After confirmation, implement the change.
1. Validate the affected behavior and boundaries.
1. Update atlas docs if ownership, APIs, flows, risks, or module boundaries
   changed.
1. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Before / After Gate

Before editing files, provide only:

- **Before**: Current behavior or structure, and what is wrong, missing,
  confusing, or risky.
- **After**: What the change will make true.

Do not edit files until the user explicitly confirms. Supporting engineering
details may be kept for implementation, but they should not replace or dilute
the Before / After checkpoint.
