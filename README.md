# Codebase Atlas

**A precise navigation protocol for AI agents and an engineering architecture governance system for human engineers.**

## Vision

Codebase Atlas is a systematic protocol designed to solve the common issues of "context loss" and "architectural drift" encountered by AI agents when working with large and complex codebases. It is not merely a documentation generator, but an engineering solution that transforms project intelligence from volatile conversation context into durable, versionable assets.

Through this system, developers can establish a complete "navigation layer" for AI agents, enabling them to understand module boundaries, dependencies, potential risks, and mandatory engineering standards before they start modifying code.

## Core Value

### 1. Reducing Architectural Hallucinations
AI agents, when lacking a global perspective, often make changes that break module encapsulation or introduce circular dependencies. Codebase Atlas forces the AI to read a defined "map" before starting a task, ensuring all changes align with the intended design.

### 2. Intelligence Persistence and Leverage
Current AI tools typically rediscover the codebase in every session, causing significant waste of computational resources and tokens. Codebase Atlas advocates a "one-time deep initialization" strategy, solidifying the analysis results of the **strongest available model** so that subsequent daily tasks can receive high-quality guidance at a lower cost.

### 3. Engineering Governance and Workflow Standardization
The system produces not just static documentation, but dynamic workflow guides for different development scenarios (e.g., Bug Fix, Feature Expansion, System Refactoring), embedding the team's engineering standards directly into the AI's execution path.

## Operating Model

Codebase Atlas follows a "Initialize Once, Reuse Often" mechanism:

1.  **Atlas Construction (Initialization)**:
    Performed during project startup or major architectural changes. It is highly recommended to use the **strongest model available** in your environment for this stage's deep scanning and logical reasoning, ensuring the resulting map has sufficient strategic depth and accuracy.

2.  **Daily Navigation (Navigation)**:
    Once the map is established, Codebase Atlas should not be run again for standard development tasks. Instead, AI agents are directed to read the generated `docs/` files and follow the workflows within. This allows lighter or more cost-effective models to perform precise code development aided by a high-quality map.

3.  **Full Rebuild**:
    Codebase Atlas is only invoked again when the user explicitly requests to rescan, refresh, or rebuild the atlas.

## Output Structure

The generated atlas is stored in the `docs/` folder at the project root, following strict naming conventions:

*   **Project Index (`_index.md`)**: Defines the project overview, delivery policy, module summaries, and workflow entry points.
*   **Module Documentation (`docs/project/module.md`)**: Details the current state, scope, upstream dependencies, and downstream impact of each functional module.
*   **Workflow Guides (`_workflow.md`)**: Specific guides for Bug Fix, Feature, Optimization, Investigation, Refactor, and Validation, including pre-change checklists and post-change validation standards.

## Modes

*   **Standalone Mode**: Uses the target codebase as the sole source of truth, building a pure description of the status quo.
*   **Reference-Assisted Mode**: Used when the project needs to refer to another baseline repository, API specification, or design document. This mode emphasizes "learning" rather than "feature parity" unless explicitly requested.

## Installation and Getting Started

### Installation

1.  Clone this repository to your development environment:
    ```bash
    git clone https://github.com/bennytsai1234/codebase-atlas.git
    ```

2.  Ensure your AI agent (e.g., Cursor, Claude Code, Windsurf) has permission to read files.

### Initialization Guide

Direct your AI agent to execute the following command (using the strongest model during the initialization phase):

> Read `/path/to/codebase-atlas/SKILL.md` and use the Codebase Atlas protocol to build a map for this repository. Before scanning starts, resolve initial decisions regarding language (English or Traditional Chinese), mode, and delivery policy.

### Daily Development

Once the map is built, point the AI directly to the generated documents for specific tasks:

> Read `docs/target_bug_workflow.md` and follow its specifications to fix the following issue: [Issue Description]

## Technical Features

*   **Language Agnostic**: Not tied to specific programming languages or frameworks.
*   **Text-Only Design**: Entirely Markdown-based, requiring no additional databases or runtimes.
*   **Bilingual Support**: Supports Traditional Chinese and English output with a built-in glossary for consistency.
*   **Delivery Policy Control**: Define `no commit`, `commit only`, or `commit and push` for automated workflows.

## License

MIT
