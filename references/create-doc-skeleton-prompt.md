# Create Doc Skeleton Prompt

Use this prompt as the reusable procedure for creating or extending Codebase
Atlas docs. Do not run code generation for this task; create or update Markdown
files directly from the templates and project context.

This is a one-time initialization prompt unless the user explicitly asks to
rebuild or rescan the atlas. For normal follow-up development, use the generated
workflow docs instead of running this prompt again.

## Prompt

You are creating a Codebase Atlas for a target repository.

Inputs to resolve from the user request and repo context:

- `project_name`: the target project name.
- `mode`: `standalone` or `reference-assisted`.
- `reference_name`: required only for reference-assisted mode.
- `output_dir`: default to `docs/`.
- `modules`: 6-20 stable module slugs derived from the target repo.
- `feature_parity`: true only when the user explicitly asks to align features
  with the reference.
- `rebuild`: true only when the user explicitly asks to rebuild, refresh,
  regenerate, or rescan the atlas.
- `output_language`: `English` or `Traditional Chinese`.

Before scanning the full repo, resolve `mode`:

- If the user already specified standalone or reference-assisted mode, continue.
- If the mode is missing, ask whether this is a standalone project or whether
  reference material should be used.
- If reference-assisted mode is selected, ask for the reference path, URL, or
  artifact before proceeding.
- If standalone mode is selected, continue without reference material.

Also resolve `output_language`:

- If the user or project rules specify English or Traditional Chinese, use it.
- If the language is unclear, ask whether generated docs should be written in
  English or Traditional Chinese.
- Keep code identifiers, file paths, command names, API names, and product names
  unchanged.

Follow this process:

1. Resolve the atlas mode, output language, and any required reference material.
2. Inspect the target repo before creating files. Use manifests, entrypoints,
   source roots, tests, build/config files, and existing docs to infer modules.
3. If `mode` is reference-assisted, inspect the reference after understanding the
   target. Keep the target as the primary subject.
4. Read `references/doc-output-contract.md` and the correct mode guide.
5. Decide the output tree:
   - Standalone:
     - `docs/<project>_index.md`
     - `docs/<project>/<module>.md`
     - `docs/<project>_bug_workflow.md`
     - `docs/<project>_feature_workflow.md`
     - `docs/<project>_optimization_workflow.md`
   - Reference-assisted:
     - `docs/<project>_<reference>_index.md`
     - `docs/<project>_<reference>/<module>.md`
     - `docs/<project>_<reference>_bug_workflow.md`
     - `docs/<project>_<reference>_optimization_workflow.md`
     - Add `docs/<project>_<reference>_feature_workflow.md` only when
       `feature_parity` is true.
6. Use the bundled templates in `assets/templates/` as starting shapes:
   - `index.md`
   - `standalone_module.md`
   - `reference_module.md`
   - `bug_workflow.md`
   - `feature_workflow.md`
   - `optimization_workflow.md`
7. Replace template placeholders with concrete names, module links, summaries,
   workflow filenames, and reference-boundary language. Translate template
   headings and prose when `output_language` is Traditional Chinese.
8. Before writing each file, check whether it already exists:
   - If missing, create it.
   - If present, preserve useful content and update only what the atlas needs.
   - Do not erase existing project-specific notes just to match the template.
   - If `rebuild` is true, perform a full repo scan and rebuild module
     boundaries from current code reality. Keep accurate existing notes, remove
     stale boundaries, and clearly update the index.
9. Fill docs with concise, inspected facts. Use TODO only where the repo or
   reference genuinely does not contain enough information.

Output requirements:

- Keep docs generic to the project; do not add framework assumptions that are not
  visible in the repo.
- Prefer relative links for new docs.
- Use the selected output language and the target project's terminology.
- In reference-assisted mode, state that the reference is guidance, not a feature
  backlog, unless feature parity was explicitly requested.
- State in the generated index that Codebase Atlas is normally run once;
  future work should follow the generated workflows, and running it again means a
  full codebase rescan and atlas rebuild.
- After writing, summarize created and updated files plus any remaining TODOs.
