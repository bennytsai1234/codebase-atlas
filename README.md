# Codebase Atlas

Turn a codebase into a durable engineering map that both humans and coding
agents can use.

Codebase Atlas is an agent-neutral skill for initializing project documentation
from a real repository scan. It creates a module index, focused module notes,
dependency and impact summaries, and practical workflows for future bug fixes,
features, and optimizations.

The goal is simple: stop rediscovering the same codebase from scratch every
time an agent starts a new task.

## Why This Exists

Coding agents are good at searching code, but they often start each task with no
shared project memory. That leads to repeated exploration, broad edits, weak
module boundaries, and uncertainty about whether a change should be committed or
pushed.

Codebase Atlas turns the first deep scan of a repository into versionable docs:

- a high-level module map
- per-module ownership and dependency notes
- known risks and common change entry points
- follow-up workflows for bug, feature, and optimization work
- a recorded delivery policy for whether future work should commit or push

After the atlas exists, future work starts from the generated workflow docs
instead of rerunning the skill.

## What It Creates

Standalone project:

```text
docs/
  <project>_index.md
  <project>/
    <module>.md
  <project>_bug_workflow.md
  <project>_feature_workflow.md
  <project>_optimization_workflow.md
```

Reference-assisted project:

```text
docs/
  <project>_<reference>_index.md
  <project>_<reference>/
    <module>.md
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_optimization_workflow.md
```

Feature-parity workflow docs are generated only when you explicitly ask for
feature parity.

## Key Ideas

- **Run once, reuse often**: initialize the atlas once, then use the generated
  workflow docs for normal development.
- **Agent-neutral**: works with any coding agent that can read Markdown files.
- **Standalone or reference-assisted**: map a project by itself, or compare it
  with a reference repo, spec, API docs, or product artifact.
- **No accidental feature creep**: reference material is treated as guidance for
  boundaries and flows, not as an automatic feature backlog.
- **Bilingual output**: generated docs can be written in English or Traditional
  Chinese.
- **Delivery policy built in**: future workflows can end with no commit, commit
  only, or commit and push.

## Installation

Clone the skill anywhere your agent can read:

```bash
git clone https://github.com/bennytsai1234/codebase-atlas.git
```

Then point your coding agent at the cloned folder and ask it to read
`SKILL.md` before working:

```text
Read /path/to/codebase-atlas/SKILL.md and use the Codebase Atlas skill for this repo.
```

## Quick Start

Ask the agent to read the skill and choose the setup options first:

```text
Use the Codebase Atlas skill for this repo.
Before scanning, ask me:
1. Should the output be English or Traditional Chinese?
2. Should this be standalone or reference-assisted?
3. After each generated workflow finishes, should it do no commit, commit only, or commit and push?
```

For reference-assisted mode, provide the reference path, URL, or artifact before
the agent starts the full scan.

## Choosing A Mode

Use **standalone** when the repository is the only source of truth.

Use **reference-assisted** when the repository should be understood alongside:

- another codebase
- a previous implementation
- design or product docs
- API documentation
- screenshots or behavior notes
- migration or compatibility material

By default, reference-assisted mode uses the reference for architecture,
responsibility boundaries, flow design, stability patterns, and diagnostics. It
does not assume that missing features in the target project are bugs.

## Normal Follow-Up Work

After the atlas exists, do not run Codebase Atlas again for ordinary
development. Use the generated workflow docs instead:

```text
Read docs/<project>_bug_workflow.md and follow it to fix this bug: ...
Read docs/<project>_feature_workflow.md and follow it to implement this feature: ...
Read docs/<project>_optimization_workflow.md and follow it to optimize this area: ...
```

Run Codebase Atlas again only when you want a full rebuild:

```text
Use the Codebase Atlas skill to rescan the full repo and rebuild the atlas from current code.
```

## How It Is Different

Codebase Atlas is not a live code search engine, IDE rule file, or one-off
documentation prompt.

It is designed to create durable project context:

- Repo maps are usually temporary context for a model. Codebase Atlas writes
  docs that can be committed and reused.
- Project rules usually tell an agent how to behave. Codebase Atlas first maps
  the actual repo, then creates workflows tied to that map.
- Documentation prompts often stop after generating docs. Codebase Atlas also
  creates the follow-up workflows future agents should use.

## Package Contents

- `SKILL.md`: main agent instructions.
- `references/`: mode guides and output contract.
- `assets/templates/`: Markdown templates for generated atlas docs.

The package is not tied to a specific agent runtime. Any coding agent can use it
by reading `SKILL.md`, the relevant reference files, and the templates.

## License

MIT
