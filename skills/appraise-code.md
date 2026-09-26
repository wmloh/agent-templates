---
name: appraise-code
description: Review uncommitted code before a commit, report findings, summarize changes by significance, suggest a commit message, and identify closely related omissions. Use only when explicitly invoked.
---

# Appraise Code

Review the current working tree and explain what a cohesive commit should contain. Cover code review findings, a summary of changes, a suggested commit message, and anything closely related that may have been missed. Do not modify files, stage changes, create commits, or run tests unless separately asked.

## Invocation

Invoke only when the user explicitly requests this skill. Do not invoke automatically during ordinary code edits, reviews, or commit preparation.

## Review Workflow

1. Inspect `git status --short`, then inspect diffs to identify changes. Use diff statistics to understand the complete scope before interpreting individual files.
2. Include untracked source and configuration files. Read their contents when they plausibly belong to the change; list unrelated, generated, binary, or large artifacts separately without treating them as reviewed code.
3. Review the changes and relevant nearby code for correctness, design problems, regressions, and omissions. Ground findings in concrete evidence, explain their consequences, and distinguish confirmed issues from uncertainty or missing context.
4. Group related files into scopes of change. Explain the behavior change rather than merely restating line edits.
5. Order scopes from greatest significance to least: design, processes, objectives, data, or experiment semantics first; then infrastructure or interfaces; and finally refactors, tests, formatting, or documentation. Do not force a category the changes do not support.
6. Suggest only closely related tasks within the changed scope that would make this commit more cohesive, such as applying the same necessary change to similar files. Exclude broad future ideas and unrelated cleanup.

## Response Format

Return these sections in order:

1. **Code review findings** — List issues in descending priority. For each, give the location, evidence, likely impact, and a practical fix. Note uncertainty where relevant. Say "None identified" when appropriate, and state any material review limitations.
2. **Change summary** — Provide one ordered entry per scope. State its significance, the behavior change, and the affected files; group or abbreviate paths when the list is long.
3. **Suggested commit message** — Provide exactly one plain-text commit-message line wrapped in quotation marks, with clauses separated by `;`. Within that line, do not use Markdown, bullets, code fences, prefixes, or conventional-commit syntax. For example: "Implemented bounded learnable Box-Cox lambdas; removed unused row attention; modularized icad.py".
4. **What else could be included in this commit** — List useful follow-ups that belong in this commit and explain why each is closely related. Say "None identified" when appropriate.

If the working tree has no relevant uncommitted changes, say so plainly and omit speculative summaries or follow-ups.
