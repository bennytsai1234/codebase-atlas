# {{ATLAS_TITLE}} Feature Workflow

## Purpose

- Use this workflow for new behavior that does not already exist in the target
  project.
- Do not run Codebase Atlas again for ordinary feature work; use this workflow
  and update affected atlas docs only if ownership, APIs, or flows changed.

## Workflow

1. Preserve the user's original request.
1. Open `{{INDEX_FILE}}` and find the natural owning module.
1. Read the owning module doc and any boundary module docs.
1. Define the feature boundary: included behavior, excluded behavior, interfaces,
   state, persistence, external systems, and user-visible changes.
1. If the feature crosses modules, choose the primary module by the module that
   owns the new behavior or state lifecycle. Treat other modules as boundary
   modules with explicit interface responsibilities.
1. Implement through the owning module's established patterns.
1. Verify the new behavior and update atlas docs when ownership, APIs, or flows
   changed.
1. Finish according to this delivery policy: {{DELIVERY_POLICY}}

## Before / After Gate

When this workflow is invoked, do not edit code first. Analyze the requested
feature using the atlas and code inspection, then provide an analysis report for
human confirmation.

The upper part of the report may include engineering details such as owning
module, boundary modules, likely files, risks, and checks. The final part must
be only a plain-language Before / After summary:

- **Before**: Explain what the system currently does or cannot do.
- **After**: Explain what behavior the feature will add or change.

Wait for explicit user confirmation after the Before / After summary before
editing files for the feature.

## Delivery Policy

{{DELIVERY_POLICY}}
