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
- `delivery_policy`: `no commit`, `commit only`, or `commit and push`.

Resolve `mode`, `output_language`, and `delivery_policy` using
`references/doc-output-contract.md`. If `mode` is `reference-assisted`, get the
reference path, URL, or artifact before scanning the full repo.

Follow this process:

1. Resolve the atlas mode, output language, delivery policy, and any required
   reference material.
2. Inspect the target repo before creating files. Use manifests, entrypoints,
   source roots, tests, build/config files, and existing docs to infer modules.
   Apply the scan boundaries in `references/doc-output-contract.md`.
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
     - `docs/<project>_investigation_workflow.md`
     - `docs/<project>_refactor_workflow.md`
     - `docs/<project>_validation_workflow.md`
   - Reference-assisted:
     - `docs/<project>_<reference>_index.md`
     - `docs/<project>_<reference>/<module>.md`
     - `docs/<project>_<reference>_bug_workflow.md`
     - `docs/<project>_<reference>_optimization_workflow.md`
     - `docs/<project>_<reference>_investigation_workflow.md`
     - `docs/<project>_<reference>_refactor_workflow.md`
     - `docs/<project>_<reference>_validation_workflow.md`
     - Add `docs/<project>_<reference>_feature_workflow.md` only when
       `feature_parity` is true.
6. Use the bundled templates in `assets/templates/` as starting shapes:
   - `index.md`
   - `standalone_module.md`
   - `reference_module.md`
   - `bug_workflow.md`
   - `feature_workflow.md`
   - `optimization_workflow.md`
   - `investigation_workflow.md`
   - `refactor_workflow.md`
   - `validation_workflow.md`
7. Replace template placeholders with concrete names, module links, module
   summaries, workflow links, workflow filenames, and reference-boundary
   language. Translate template headings and prose when `output_language` is
   Traditional Chinese. Replace `{{DELIVERY_POLICY}}` with the selected
   completion rule. For optimization workflow docs, replace `{{REFERENCE_STEP}}`
   with either a Markdown numbered step that compares useful reference patterns
   before choosing an optimization direction, including its trailing newline, or
   an empty string.
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
- Write routing-oriented module summaries in the index. Each module summary
  should help a future agent decide when to start there based on symptoms, task
  types, or entry conditions.
- State the selected delivery policy in the generated index and every workflow
  doc.
- In reference-assisted mode, generate investigation, refactor, validation, bug,
  and optimization workflows by default. Generate the feature workflow only when
  `feature_parity` is true.
- Apply the final validation checklist in `references/doc-output-contract.md`.
- After writing, summarize created and updated files plus any remaining TODOs.
