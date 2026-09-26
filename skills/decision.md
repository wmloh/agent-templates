---
name: decision
description: Manage persistent project-wide decisions only when explicitly invoked with $decision, make decision, use decision, or update decision. 
---

# Decision

Keep concise project-wide constraints in a local, untracked `decisions/` directory. This skill is explicit-only; do not invoke automatically for ordinary tasks or mentions of decisions. If invoked without a clear mode, ask whether the user wants `make`, `use`, or `update`.

## Project and storage

- Resolve the project root with `git rev-parse --show-toplevel` from the task's working directory. If there is no Git repository, explain that this workflow requires one and ask for the intended repository; do not initialize Git or create a store there.
- Store aspect files at `<root>/decisions/<aspect>.txt`, using short, descriptive lowercase hyphenated names. Each file contains plain text bullets, one concise decision per bullet, without metadata or narrative.
- Keep `decisions/DECISION_MAP.json` as a JSON object mapping each aspect filename without `.txt` to a brief, one-sentence description. Avoid redundant phrases such as "decisions about". Each key must correspond to one aspect file and every aspect file must have a key.
- Give each aspect a distinct scope and keep each decision in exactly one file. For example, `training.txt` could contain `- Do not use Adam optimizer; use SGD instead.` The map describes the aspect, not a second copy of its decisions.
- Only `make` initializes a missing store. Resolve the local exclude file using `git rev-parse --git-path info/exclude`, including when `.git` is a worktree pointer. Preserve its contents and add `/decisions/` once before writing decision files. Never use tracked `.gitignore` for this purpose.
- Check whether anything in `decisions/` is already tracked before mutations. If so, stop and explain that local excludes cannot hide tracked files; ask how the user wants to handle them. Do not untrack files automatically. Verify the store is ignored with `git check-ignore` after initialization.
- Local exclusion keeps the store out of ordinary Git status and commits; it does not make the files secret or inaccessible to filesystem tools. Never stage or commit the store.

## Make decision

1. Identify the explicit constraint the user wants persisted. Ask if its meaning or scope is ambiguous; do not turn examples or tentative discussion into new rules.
2. Read the existing map and aspect files, if present, to find duplicates, overlaps, and conflicts. Initialize an absent store as described above.
3. Reuse the appropriate aspect or create a distinct one. If the proposed decision conflicts with an existing rule, clarify whether the user intends replacement or a narrower exception before editing. Do not silently supersede decisions.
4. State the intended edits, then write the decision and synchronize the map. Reorganize or compact when useful under the preservation rules below.
5. Verify the resulting store and briefly report what was recorded and where.

## Use decision

1. Read the map and the files relevant to the task. Search the remaining decision files when the map alone cannot resolve relevance or a requested rule cannot be found.
2. If the store is absent, report that no decisions have been recorded; do not create it. If a requested decision is missing or ambiguous, report that and ask for clarification rather than inventing a rule.
3. Briefly explain the relevant constraints and their concrete implications for the current task, citing aspect files. Apply them during the task; do not treat this invocation as permission to rewrite the store.
4. If a task instruction conflicts with a stored decision, explain the conflict and ask before affected edits whether the user wants a one-time exception or a persistent update. An exception leaves storage unchanged; an explicit persistent change follows `update`. Continue independent work when possible.

## Update decision

1. Read the map, locate candidate files, and read the corresponding decisions. Search all aspect files if needed, including wording variants.
2. If the store or target decision cannot be found, or the target is uncertain, stop this operation, warn that the decision could not be identified, and ask for clarification. Do not create a replacement decision or initialize a store as a fallback.
3. Apply the user's requested modification or deletion only to the identified decision. Clarify conflicts with other active decisions before writing.
4. State the intended edits, then update the files and map together. Reorganization and compaction are encouraged when useful, subject to the preservation rules below. Remove empty aspect files and their map entries only when file deletion is authorized under the project's rules; otherwise leave an empty mapped file and explain the pending cleanup.
5. Verify and briefly report what changed or was removed.

## Preservation and verification

- Preserve the meaning of every active decision, including scope, conditions, exceptions, and prohibitions. Historical wording need not be archived. Remove meaning only when the user explicitly requests its removal or replacement.
- Before compacting or moving decisions, account for each original constraint in the proposed result. Merge only when the replacement is semantically equivalent; do not generalize into a stronger or weaker rule. Prefer separate precise bullets when equivalence is uncertain.
- Read all affected files before edits and preserve unrelated or concurrent changes. Write destination content before removing source content when reorganizing. Keep each file focused and concise; split by distinct aspects when needed rather than imposing an arbitrary size limit.
- Treat a missing or invalid map in a nonempty store as an inconsistency, not an empty store. Inspect existing text files and repair the map during an authorized `make` or `update` only when their scopes are clear; otherwise ask. `use` may read existing files and report the inconsistency without repairing it.
- After mutations, parse the map as JSON, verify the one-to-one correspondence with aspect files, and review affected content for duplicated or contradictory rules and lost constraints. Confirm that the store remains locally excluded and untracked.
