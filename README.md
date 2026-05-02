# Codebase Atlas

Codebase Atlas is an agent-neutral skill for turning a repository into a
navigable engineering map. It creates project docs, module summaries,
dependency and impact notes, and follow-up workflows for bugs, features, and
optimizations.

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

## Usage

Ask the agent to read this skill and choose the setup options first:

```text
Use the Codebase Atlas skill for this repo.
Before scanning, ask me:
1. Should the output be English or Traditional Chinese?
2. Should this be standalone or reference-assisted?
3. After each generated workflow finishes, should it do no commit, commit only, or commit and push?
```

For reference-assisted mode, provide the reference path, URL, or artifact before
the agent starts the full scan.

Run it again only for a rebuild:

```text
Use the Codebase Atlas skill to rescan the full repo and rebuild the atlas from current code.
```

## Normal Follow-Up Work

After the atlas exists, do not run Codebase Atlas again for ordinary
development. Use the generated workflow docs instead:

```text
Read docs/<project>_bug_workflow.md and follow it to fix this bug: ...
Read docs/<project>_feature_workflow.md and follow it to implement this feature: ...
Read docs/<project>_optimization_workflow.md and follow it to optimize this area: ...
```

## Package Contents

- `SKILL.md`: main agent instructions.
- `references/`: mode guides and output contract.
- `assets/templates/`: Markdown templates for generated atlas docs.

The package is not tied to a specific agent runtime. Any coding agent can use it
by reading `SKILL.md`, the relevant reference files, and the templates.

## License

MIT
