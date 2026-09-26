---
name: appraise-code
description: Review uncommitted code changes and produce an ML-significance-ordered change summary, a commit message, and tightly related next steps.
---

# Appraise Code

Inspect the current working tree and explain what a cohesive commit should contain. Do not modify files, stage changes, create commits, or run tests unless separately asked.

## Review Workflow

1. Inspect `git status --short`, then inspect both unstaged and staged diffs with `git diff` and `git diff --cached`. Use diff statistics to understand the complete scope before interpreting individual files.
2. Include untracked source and configuration files. Read their contents when they plausibly belong to the change; list unrelated, generated, binary, or large artifacts separately without treating them as reviewed code.
3. Group related files into scopes of change. Interpret behavior from the diff and relevant nearby code rather than merely restating line edits. Note important uncertainty or missing context.
4. Order scopes from greatest machine-learning significance to least: model, objective, data, or experiment semantics first; then training or evaluation behavior; infrastructure or interfaces; and finally refactors, tests, formatting, or documentation. Do not force a category the changes do not support.
5. Suggest only highly relevant tasks within the changed scope that would make this particular commit more cohesive. Examples include a relevant change on similar files based on existing changes. Exclude broad future ideas and unrelated cleanup.

## Response Format

Return these sections in order:

1. **Change summary** — Provide one ordered entry per scope. State the ML or engineering significance, concise behavior change, and every affected file; abbreviate the file list if it is long.
2. **Suggested commit message** — Provide exactly one plain-text commit-message line wrapped with quotation marks. Each chunk is separated by `;`. Do not use Markdown, bullets, code fences, prefixes, or conventional-commit syntax. For example: "Implemented bounded learnable Box-Cox lambdas; removed unused row attention; modularized icad.py".
3. **What else could be included in this commit** — List the relevant, useful follow-ups that should belong in this commit. Explain why each is tightly coupled; say "None identified" when appropriate.

If the working tree has no relevant uncommitted changes, say so plainly and omit speculative summaries or follow-ups.
