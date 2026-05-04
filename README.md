# Codebase Atlas

**A precise navigation protocol for AI agents and an engineering architecture governance system for human engineers.**

## Vision

Codebase Atlas is a systematic protocol designed to solve the common issues of "context loss" and "architectural drift" encountered by AI agents when working with large and complex codebases. It is not merely a documentation generator, but an engineering solution that transforms project intelligence from volatile conversation context into durable, versionable assets.

Through this system, developers can establish a complete "navigation layer" for AI agents, enabling them to understand module boundaries, dependencies, potential risks, and mandatory engineering standards before they start modifying code.

## Core Value: The "Initialize Once, Reuse Often" Strategy

Current AI tools typically rediscover the codebase in every session, causing significant waste of computational resources and tokens. Codebase Atlas advocates a strategic separation of roles:

*   **The Architect (Strong Model Initialization)**: Use the strongest model available to perform a deep, one-time scan. This model acts as a senior architect, identifying hidden patterns, module boundaries, and cross-module impacts to create the Atlas.
*   **The Worker (Standard Model Execution)**: Once the Atlas exists, daily development tasks can be handled by more cost-effective models. These models follow the "architect's" pre-defined maps and workflows, achieving high-quality results with minimal context overhead.

## Operating Model

### 1. Initialization and Decision Making
When the protocol is first activated, the AI agent will not scan immediately. It must first resolve four critical decisions with the user to ensure the Atlas matches project requirements:

1.  **Output Language**: Traditional Chinese or English.
2.  **Atlas Mode**: Standalone (sole source of truth) or Reference-Assisted (learning from an external repository or spec).
3.  **Delivery Policy**: Recorded rule for future tasks (No commit, Commit only, or Commit and Push).
4.  **Feature Parity Workflow**: (Reference-Assisted mode only) Whether to enable specific workflows for migration equivalence or feature expansion.

### 2. Atlas Construction
The AI agent performs a deep scan of the repository, ignoring non-source directories (e.g., node_modules, dist, .git), and organizes the codebase into 6-20 stable modules based on product or architectural boundaries.

### 3. Workflow Implementation
The system embeds specific engineering standards into the execution path of future AI tasks, ensuring every change is validated and documented according to the Atlas.

## Output Structure

The generated atlas is stored in the `docs/` folder at the project root:

### Standalone Output
```text
docs/
  <project>_index.md
  <project>/
    <module_slug>.md
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
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_optimization_workflow.md
  <project>_<reference>_investigation_workflow.md
  <project>_<reference>_refactor_workflow.md
  <project>_<reference>_validation_workflow.md
  <project>_<reference>_feature_workflow.md (Optional: for parity)
```

## Detailed Mode Selection

### Standalone Mode
Use this when the target project is its own primary source of truth. The AI focuses exclusively on the existing code to derive boundaries and flows.

### Reference-Assisted Mode
Use this when the target project should be understood alongside a reference repository, folder, API specification, or design document.
*   **Guidance over Parity**: By default, the reference is used for architecture, boundaries, and stability patterns. It does not turn into a feature-parity backlog unless explicitly requested.
*   **Ideal for**: Migrations, refactoring toward a standard, or implementing a specific API pattern.

## Standard Development Workflows

After the atlas exists, do not run Codebase Atlas again for ordinary development. Use the generated workflow docs to guide the AI:

*   **Bug Fix**: `Read docs/<project>_bug_workflow.md and follow it to fix this bug: [description]`
*   **Feature Expansion**: `Read docs/<project>_feature_workflow.md and follow it to implement: [description]`
*   **Optimization**: `Read docs/<project>_optimization_workflow.md to improve: [description]`
*   **Investigation**: `Read docs/<project>_investigation_workflow.md to understand: [description]`
*   **Refactor**: `Read docs/<project>_refactor_workflow.md to restructure: [description]`
*   **Validation**: `Read docs/<project>_validation_workflow.md to verify: [description]`

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

## License

MIT
