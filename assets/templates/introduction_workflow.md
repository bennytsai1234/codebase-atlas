# {{ATLAS_TITLE}} Introduction Workflow

## Purpose

- Use this workflow when the user wants to understand what the project does.
- Keep the output plain-language and user-facing.
- Do not turn the answer into an architecture report, file inventory, or module
  checklist unless the user asks for those details.
- Do not edit code during this workflow.
- Do not run Codebase Atlas again for ordinary project explanation; use this
  workflow and the existing atlas docs.

## Workflow

1. Open `{{INDEX_FILE}}` and read the project purpose, module summaries, and
   workflow list.
1. Read only the module docs needed to explain the project clearly.
1. Inspect code only when the atlas does not contain enough context to explain
   user-visible behavior.
1. Explain the project in plain language:
   - what it is
   - who or what it serves
   - what main jobs it performs
   - where the important boundaries are, only when that helps understanding
1. Avoid listing every module, dependency, file, or technical detail.
1. If the user asks for deeper technical context, recommend the investigation
   workflow.
1. Finish according to this delivery policy when files changed; otherwise
   summarize the explanation and state that no commit is needed:
   {{DELIVERY_POLICY}}

## Plain-Language Introduction

Write the final explanation as if the user wants to quickly understand the
project, not audit the implementation. Prefer a few clear paragraphs over a
long checklist.

If the project is complex, start with the simplest useful explanation first,
then add one short paragraph for the main moving parts.

## Delivery Policy

{{DELIVERY_POLICY}}
