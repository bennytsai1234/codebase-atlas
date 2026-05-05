# Codebase Atlas

**An AI navigation protocol focused on verifiable problem-solving. It uses durable maps and Human-in-the-Loop workflows to ensure AI agents truly understand and locate issues before execution.**

## Vision

Codebase Atlas is an engineering protocol that ensures AI agents accurately identify and solve real problems. It replaces "blind editing" with "map-based reasoning" and human confirmation. By forcing agents to provide plain-language summaries of their intent and "before vs. after" plans, it allows human engineers to instinctively verify if the AI has truly grasped the bug or requirement, making possible hallucinations visible and catchable before execution.

Through this system, developers can establish a complete "navigation layer" for AI agents, enabling them to understand module boundaries, dependencies, potential risks, and mandatory engineering standards before they start modifying code.

## Why Codebase Atlas?

### Better Than Simple Prompting
Simple prompting is transient and speculative. When you ask an AI to "find where to change X," it performs a shallow search that is forgotten in the next session. Codebase Atlas is **grounded and persistent**. It creates a physical map of your codebase that anchors the AI's reasoning, ensuring that every task starts with a deep understanding of the project's architecture rather than a lucky guess.

### Better Than Heavy Infrastructure
While heavy code intelligence systems (such as graph-based parsing engines or external databases) are powerful, they are often overkill for 90% of development tasks. Codebase Atlas offers a **"just enough" approach**: a lightweight, text-based protocol that provides the essential architectural boundaries and workflows an agent needs without the overhead of complex maintenance, specialized servers, or invasive indexing.

## Core Value: The "Initialize Once, Reuse Often" Strategy

Current AI tools typically rediscover the codebase in every session, causing significant waste of computational resources and tokens. Codebase Atlas advocates a strategic separation of roles:

*   **The Architect (Strong Model Initialization)**: Use the strongest model available to perform a deep, one-time scan. We strongly recommend GPT-5.5 or a comparable frontier-level model for atlas initialization and rebuilds, so module boundaries, workflow docs, and Before / After gates are generated coherently and followed consistently.
*   **The Worker (Standard Model Execution)**: Once the Atlas exists, daily development tasks can be handled by more cost-effective models. These models follow the "architect's" pre-defined maps and workflows, achieving high-quality results with minimal context overhead.

### Recommended Initialization Model

Codebase Atlas initialization is an architecture-setting task: the model must hold cross-file constraints, preserve workflow gates, and write consistent module boundaries. For atlas initialization and rebuilds, prefer GPT-5.5 or a comparable frontier-level model.

Smaller or faster models may still be useful for daily follow-up work after a strong atlas exists, because they can follow the generated workflow docs. They are not recommended as the primary initializer unless a human reviews the generated module split, workflow gates, delivery policy, and known-risk notes carefully.

## Design Philosophy & System Architecture

Codebase Atlas is built on the principle of **"Structural Persistence"**. Unlike RAG (Retrieval-Augmented Generation) which slices code into fragmented chunks, Codebase Atlas distills the repository into a hierarchical, semantically meaningful map.

### 1. The Four-Phase Lifecycle
The system operates through a structured "Decision-Scan-Distill-Govern" lifecycle:
*   **Decision Phase**: Explicitly resolves project-specific constraints (Mode, Language, Policy) before any analysis, preventing the AI from making assumptions that drift from the developer's intent.
*   **Scanning Phase**: A high-speed grounding process that ignores noise (dependencies, caches) and focuses on architectural entry points, manifests, and boundary-defining files.
*   **Distillation Phase**: Collapses thousands of files into 6-20 stable modules. This "Information Density Control" ensures that the AI's context window is spent on high-level relationships rather than redundant file-level details.
*   **Governance Phase**: Generates stateful workflow documents that act as "execution locks," forcing future AI agents to follow a pre-validated engineering path.

### 2. Why Zero-Dependency Markdown?
We intentionally avoided databases and heavy parsing engines. The reasoning is three-fold:
*   **Auditability**: Humans can read and verify the Atlas. If the AI hallucinates a module boundary, a developer can fix it with a simple text edit.
*   **Versionability**: The Atlas lives inside the Git repo. It evolves with the code, providing a historical record of architectural intent.
*   **Agent Handover**: One agent can build the Atlas, and a completely different agent (even on a different platform) can immediately use it without any synchronized state or shared database.

## Operating Model

### 1. Initialization and Decision Making
When the protocol is first activated, the AI agent will not scan immediately. It must first resolve four critical decisions with the user to ensure the Atlas matches project requirements:

1.  **Output Language**: Traditional Chinese or English.
2.  **Atlas Mode**: Standalone (sole source of truth) or Reference-Assisted (learning from an external repository or spec).
3.  **Delivery Policy**: Recorded rule for future tasks (No commit, Commit only, or Commit and Push).
4.  **Workflow Entrypoints**: Docs only by default, or optional Codex skills / prompt files when command or menu access is requested.
5.  **Feature Parity**: (Reference-Assisted mode only) Whether the reference can drive migration equivalence or feature expansion. The feature workflow is generated either way.

### 2. Atlas Construction
The AI agent performs a deep scan of the repository, ignoring non-source directories (e.g., node_modules, dist, .git), and organizes the codebase into 6-20 stable modules based on product or architectural boundaries.

### 3. Workflow Implementation
The system embeds specific engineering standards into the execution path of future AI tasks, ensuring every change is validated and documented according to the Atlas.

### 4. Optional Tool Entrypoints
The generated `docs/` workflows are the source of truth. When direct command or
menu access is needed, Codebase Atlas can optionally generate thin adapters for a
specific tool, such as Codex skills or VS Code prompt files. These adapters only
route the tool to the canonical workflow document, so the workflow rules stay in
one place.

## Output Structure

The generated atlas is stored in the `docs/` folder at the project root:

### Standalone Output
```text
docs/
  <project>_index.md
  <project>/
    <module_slug>.md
  <project>_introduction_workflow.md
  <project>_bug_workflow.md
  <project>_feature_workflow.md
  <project>_optimization_workflow.md
  <project>_investigation_workflow.md
  <project>_refactor_workflow.md
  <project>_validation_workflow.md
```

### Reference-Assisted Output
```text
docs/
  <project>_<reference>_index.md
  <project>_<reference>/
    <module_slug>.md
  <project>_<reference>_introduction_workflow.md
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_feature_workflow.md
  <project>_<reference>_optimization_workflow.md
  <project>_<reference>_investigation_workflow.md
  <project>_<reference>_refactor_workflow.md
  <project>_<reference>_validation_workflow.md
```

### Self-Bootstrap Example

This repository includes a self-bootstrap atlas under `docs/`. It is both a usable navigation layer for this project and a concrete example of the expected output shape:

*   Start with `docs/codebase_atlas_index.md`.
*   Module notes live under `docs/codebase_atlas/`.
*   Workflow docs live beside the index, such as `docs/codebase_atlas_bug_workflow.md`.
*   The initialization quality checklist is stored in `references/atlas-quality-checklist.md`.

### Optional Workflow Entrypoints
```text
.agents/skills/<project>-bug/SKILL.md
.github/prompts/<project>-bug.prompt.md
.workflow/<project>-bug.prompt.md
```

These files are optional adapters. They should point back to the canonical
workflow document under `docs/` instead of copying the workflow rules. Prompt
files may use `.github/prompts/` or a configured directory such as `.workflow/`.

## Detailed Mode Selection

### Standalone Mode
Use this when the target project is its own primary source of truth. The AI focuses exclusively on the existing code to derive boundaries and flows.

### Reference-Assisted Mode
Use this when the target project should be understood alongside a reference repository, folder, API specification, or design document.
*   **Guidance over Parity**: By default, the reference is used for architecture, boundaries, and stability patterns. It does not turn into a feature-parity backlog unless explicitly requested.
*   **Ideal for**: Migrations, refactoring toward a standard, or implementing a specific API pattern.

## Standard Development Workflows

Once the Atlas is established, **do not run Codebase Atlas again for daily development.** Rerunning the full scan is a waste of resources. Instead, use the generated workflow documents to guide the AI. These workflows are designed to turn the AI into a thoughtful collaborator rather than a reckless editor.

*   **Bug Fix**: `Read docs/<project>_bug_workflow.md and follow it to fix this bug: [description]`
*   **Feature Expansion**: `Read docs/<project>_feature_workflow.md and follow it to implement: [description]`
*   **Optimization**: `Read docs/<project>_optimization_workflow.md to improve: [description]`
*   **Investigation**: `Read docs/<project>_investigation_workflow.md to understand: [description]`
*   **Refactor**: `Read docs/<project>_refactor_workflow.md to restructure: [description]`
*   **Validation**: `Read docs/<project>_validation_workflow.md to verify: [description]`
*   **Introduction**: `Read docs/<project>_introduction_workflow.md to explain what this project does`

If workflow entrypoints were generated, use the tool-specific entrypoint instead
of typing the full document path, for example `$<project>-bug` in Codex or
`/<project>-bug` in an IDE prompt-file interface. The entrypoint should still
lead back to the matching `docs/<project>_*_workflow.md` file.

### Why These Workflows Work: Reasoning Over Hallucination

The effectiveness of Codebase Atlas lies in its **Map-Based Reasoning** and **Human-in-the-Loop (HITL)** design:

1.  **Precision Localization**: Instead of guessing where a bug might be, the AI uses the Atlas index and module notes to identify the exact "Change Entry Points" and "Downstream Impacts." The map provides the context that makes generic hallucinations easier to detect before edits begin.
2.  **Deliberate Analysis**: Every workflow requires the AI to first summarize its understanding, identify the relevant modules, and propose a specific plan. This forces the AI to "think" and "trace" before it ever touches a line of code.
3.  **Human as the Final Gatekeeper**: The protocol is designed so that the AI presents its analysis and plan to the human user for confirmation. This HITL approach ensures that the AI's logic is sound and that it truly understands the problem before execution begins.
4.  **Verification of Intent**: By requiring a summary-first approach, the user can immediately detect if the AI has misinterpreted the bug or the requirements, preventing costly rework and ensuring the final solution is both accurate and safe.

## Technical Features

*   **Agent-Neutral Protocol**: Works with any AI agent capable of reading and editing Markdown files.
*   **Text-Only Portability**: No dependencies on databases, scripts, or specific runtimes.
*   **Bilingual Consistency**: Includes a Traditional Chinese glossary to maintain professional terminology.
*   **Boundary Enforcement**: Explicitly identifies "Common Change Entry Points" and "Known Risks" per module.

## Installation

1.  Clone this repository:
    ```bash
    git clone https://github.com/bennytsai1234/codebase-atlas.git
    ```
2.  Point your AI agent to the `SKILL.md` file within the cloned directory.
3.  For a first run, ask the agent to initialize Codebase Atlas for the target repository. The agent should resolve output language, atlas mode, delivery policy, and reference-assisted feature parity before scanning.
4.  After the atlas exists, use the generated workflow docs directly. For example: `Read docs/<project>_bug_workflow.md and follow it to fix this bug: [description]`.
5.  Re-run Codebase Atlas only when you explicitly want a full rebuild, refresh, regenerate, or rescan of the atlas.

## License

MIT
