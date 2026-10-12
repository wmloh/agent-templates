# Initialize project instructions

Use this file to initialize or update repository instructions for a new or existing project. Produce a concise root `AGENTS.md`, five modular workflow files under `workflows/`, and a compact root `PROJECT_MAP.yaml` tracked by the main project repository. This file is the initialization procedure; do not copy the entire procedure into `AGENTS.md`.

`INIT_AGENT.md` will be deleted after `AGENTS.md` is created. Ensure all information needed for ongoing work is propagated into the resultant `AGENTS.md`, with workflow-specific details retained in the linked workflow files. No durable instruction or project information may depend on this initialization file remaining available.

Assume the `probe-me` and `decision` skills are available. Read their actual instructions when using them; do not invent their interfaces.

## 1. Inspect before interviewing

- Read existing applicable `AGENTS.md` files and relevant instruction files. Inspect a small amount of repository structure, manifests, entry points, and documentation to ground the interview. For an empty repository, establish the intended structure through questions.
- Stay within the repository unless the user explicitly authorizes access elsewhere. Access to an externally stored skill must also follow applicable access rules; ask for access or its supplied contents if necessary.
- Preserve user changes and project-specific instructions. Do not overwrite artifacts, install packages, download dependencies, change environments, or run expensive workloads during initialization.
- Treat existing instructions as evidence of intent. Merge compatible rules. Surface conflicts with a proposed resolution and ask when intent remains unclear; do not silently replace local policies with these defaults.

## 2. Interview with probe-me

Invoke `probe-me` before editing. Ask the user at least **six distinct, relevant questions**, in manageable rounds of two or three questions. Prefer the multiple-choice interface with concrete trade-offs and a free-text alternative. If that interface is unavailable, ask numbered questions in conversation. Use only parameters the available tool supports.

Always ask about **project domain** and **execution environment**, even if repository evidence suggests the answers. For other topics, use inspected evidence to offer informed choices rather than making the user repeat documentation. Cover all six topics below; follow up on consequential gaps or conflicts.

1. **Domain and outcome:** What does this project do, who uses its outputs, and what constitutes success? Offer relevant choices such as ML research, ML applications, general Python software, or another domain. Do not impose ML research standards on unrelated projects.
2. **Environment:** Where will work run: WSL 2, native Linux, macOS, Windows, a container, a remote cluster, or another environment? Establish the relevant local/remote distinction, environment manager, and any hardware constraints. Ask explicitly whether WSL 2 applies.
3. **Language and validation:** Confirm languages, framework/tooling conventions, and acceptable lightweight checks. Confirm the default restriction against adding tests under `tests/` or subdirectory `README.md` files unless explicitly requested. Adapt Python-specific style rules only where relevant.
4. **Workflows:** Which workflows are active: code, task tracking, review, or paper writing? All five workflow files will exist, but irrelevant workflows will be marked inactive. Identify any additional workflow that needs its own file.
5. **Execution and artifacts:** Which commands, resource budgets, and artifact locations matter? Establish whether training, evaluation, data processing, network access, or other substantial runs are authorized. Preserve the explicit restrictions on installations, environment changes, destructive commands, and artifact overwrites unless the user revises them.
6. **Collaboration and decisions:** How should tasks, unresolved decisions, and user requests be tracked? Confirm the task and paper conventions below, the review audience, and whether any existing policy needs reconciliation. Confirm the compact project map and its feature-change maintenance rule. Establish whether a separate workflow Git repository and remote already exist, which remote and branch to use for cross-device synchronization, and whether workflow commits and network synchronization are authorized. Do not invent a remote or treat local Git initialization as completed synchronization.

Challenge proposals constructively where evidence reveals a practical problem. Keep the interview relevant to the project's domain; add scientific, deployment, or evaluation policies only when the user requests or confirms them.

Summarize decisions, remaining assumptions, and consequences before editing. If the interview receives no response, leave initialization unfinished and resume the unanswered questions on continuation, subject to the available tool's governing instructions. For an individually skipped optional detail, state a conservative assumption. Never treat silence as authorization for restricted actions.

## 3. Generate or merge the files

State the intended edits first. Keep `AGENTS.md` and `PROJECT_MAP.yaml` at the project root. The map is the only generated workflow item tracked by the main project repository. Create or update the remaining generated support files in `workflows/`: every `workflows/*_WORKFLOW.md` and, when activated, `workflows/TASKS.md`, `workflows/REQUESTS.md`, and `workflows/memory/`. Additional personal workflow files also belong there. Use Markdown links relative to the file containing the link: root `AGENTS.md` links into `workflows/`, while files inside `workflows/` link to siblings or use `../` for project files. All paths below are relative to the project root unless explicitly stated otherwise. Preserve unrelated content and edits. Existing equivalent workflow files may be consolidated into this structure only after resolving meaningful conflicts; avoid leaving contradictory duplicate instructions.

### AGENTS.md: shared operating rules and routing

Keep this file lean. Include a short project description, confirmed environment facts, the shared rules below, and the routing table. Put workflow-specific detail in the linked files. Record durable decisions, not the interview transcript.

Preserve these core rules:

- Do not read, search, or modify files outside this repository unless the user explicitly asks.
- Before editing files, state the intended edits.
- Preserve changes from the user and other agents. Do not revert, overwrite, or clean up unrelated files unless explicitly asked.
- Do not run destructive commands such as `rm`, `git reset`, `git checkout`, broad `mv`, or cleanup scripts unless the user explicitly approves the exact action. The only workflow exception is narrowly scoped removal of obsolete notes under `workflows/memory/`, as authorized by `workflows/MEMORY_WORKFLOW.md`.
- Do not install packages, download dependencies, or change environments unless explicitly asked. Notify the user of missing environment components or packages before proceeding with dependent work.
- Lightweight read-only inspection and small, relevant syntax/import checks are acceptable when they do not touch large data or model artifacts. Follow confirmed project limits for other execution.
- For substantial features or experimental changes whose intended behavior is unclear, ask clarifying questions before editing and use `probe-me` as appropriate. Always honor an explicit invocation of that skill. Prefer multiple-choice questions and challenge proposals constructively.
- Do not overwrite result files, checkpoints, Parquet data, experiment caches, or plots. Use new output locations for authorized runs.
- Read workflow files only when their triggers apply. Open their explicit paths because parent Git listings and ignore-aware searches may omit `workflows/`. For a task spanning workflows, read each applicable file; do not load all files merely because they are linked.
- Keep transient development notes only in `workflows/memory/` through [MEMORY_WORKFLOW.md](workflows/MEMORY_WORKFLOW.md), never in `workflows/TASKS.md` or unsolicited documents elsewhere. Keep `AGENTS.md` and `workflows/` locally excluded from the parent project Git repository. Track the contents of `workflows/`, including memory notes, in its separate Git repository. Run project Git commands from the project root and workflow Git commands with `git -C workflows ...` from that root; verify the repository boundary before staging or committing. Keep durable project documentation in established locations.
- `workflows/TASKS.md` may contain only `# History` with historical bullets and `# Current` with checklists, plus blank lines. Do not add paragraphs or development notes, including at the start of `Current`. Follow [TASK_WORKFLOW.md](workflows/TASK_WORKFLOW.md) whenever editing the ledger.
- Use task IDs only in `workflows/TASKS.md` and files under `workflows/memory/`, not in other files or communications. Refer to tasks by descriptive names elsewhere. Task IDs may change when historical tasks are removed or compressed in `workflows/TASKS.md`; keep affected memory references current.
- The project map is in root [PROJECT_MAP.yaml](PROJECT_MAP.yaml), tracked by the main project repository rather than workflow Git. Consult it when locating work or understanding repository structure. It is a concise YAML map that roughly follows the directory tree; it need not describe every file. Group related files or summarize whole directories, especially as the project grows. Update it in the same change when a feature is added or removed; also correct affected entries when features or entry points move.

Include a routing table of this form, adapted to confirmed project status:

| File | Read when |
| --- | --- |
| [CODE_WORKFLOW.md](workflows/CODE_WORKFLOW.md) | Implementing, modifying, debugging, or validating code. |
| [TASK_WORKFLOW.md](workflows/TASK_WORKFLOW.md) | The user explicitly asks to create, track, or complete a task, condense completed current tasks, or compress historical tasks. |
| [REVIEW_WORKFLOW.md](workflows/REVIEW_WORKFLOW.md) | Reviewing code, designs, experiments, or written work. |
| [PAPER_WORKFLOW.md](workflows/PAPER_WORKFLOW.md) | Writing or editing a research paper or managing its requests. |
| [MEMORY_WORKFLOW.md](workflows/MEMORY_WORKFLOW.md) | The agent needs to document or communicate transient development state for continuity between sessions. |

Mark inactive workflows in the table so agents need not open them. A later request that activates an inactive workflow should trigger a targeted clarification and update of its status. Link `PROJECT_MAP.yaml` separately as a navigation resource, not as mandatory reading for every task.

### Workflow file structure

Generate **all five** workflow files above, even when some are inactive. Each should state its status, activation trigger, and concise actionable rules. For an inactive workflow, retain a short applicable baseline and identify what must be confirmed before activation. Do not invent tools, paths, commands, or domain requirements. Do not duplicate shared operating rules or require reading unrelated workflows.

**workflows/CODE_WORKFLOW.md**

- Follow nearby code style and the confirmed language conventions. For Python, use Google-style docstrings for public functions/classes and nontrivial private helpers. Keep comments concise and focused on non-obvious logic.
- Avoid routine logging or printing in library functions. Warnings are acceptable for unusual or incorrect states. Python driver scripts should report progress with the project's existing `accelerate` logger or `tqdm` convention where available; confirm a suitable existing alternative for other stacks. This rule does not authorize installing either dependency.
- Do not create test cases in `tests/` or `README.md` files in subdirectories unless explicitly told to do so. Do not consider backward compatibility unless explicitly told to do so.
- Document confirmed lightweight validation commands and their prerequisites. Run checks appropriate to the change within the authorized scope; report what was checked and any limitations. Do not claim unrun tests passed.
- After implementation and validation, if a concrete cleanup, organization improvement, fix, or modularization opportunity was encountered, propose it in one sentence in the conversation without executing it. Base it only on files already read; do not inspect unrelated files to find a suggestion.

**workflows/TASK_WORKFLOW.md**

- Activate only when the user asks to create, track, or complete a task, condense completed current tasks, or compress historical tasks. Ordinary code edits and initialization alone do not require a task ledger.
- If `workflows/TASKS.md` is absent when this workflow is activated to create, track, or complete a task, create it. If it is absent for a condensation or compression request, report that there are no tasks to process. Preserve existing IDs and content except during explicitly requested condensation or historical compression; assign unused IDs for new entries.
- Use exactly two section headers in `workflows/TASKS.md`, in this order: `# History` and `# Current`. All other nonblank lines must be historical bullets or current checklist entries. Do not add a separate title, paragraphs, development notes, tables, or code blocks.
- In `History`, use a single tier of plain bullet points without checkboxes, each describing a completed outcome in one sentence.
- For detailed task entries in `Current`, use exactly two tiers of checkboxes. Outer items describe high-level tasks and start with IDs such as `T-01`; inner items describe one narrow local subtask per sentence and start with IDs such as `T-01.1`. An optional tag follows the ID.
- When a task is completed, check its boxes in-place. Keep the detailed entries available so the user can review or uncheck them. **Condense completed current tasks:** Only perform this function when the user explicitly asks to condense or compact completed current tasks or `workflows/TASKS.md`; then summarize each fully completed task as a one-sentence bullet in `History`, preserving task IDs and their relative order, broadly integrating the subtask outcomes, and removing those subtasks. Keep incomplete tasks under `Current`. This function does not merge existing historical entries.

  Example after an explicit compaction:

  ```markdown
  # History

  - T-01 Implemented the agreed feature and validated its entry point.

  # Current

  - [ ] T-02 Implement the next agreed feature.
    - [ ] T-02.1 #code Add its entry point.
  ```

- **Compress historical tasks:** Only perform this function when the user explicitly asks to compress historical tasks. Group similar entries in `History` by shared feature, purpose, or outcome, and replace each group with fewer one-sentence historical task bullets. Retain higher-level accomplishments, significant decisions, and material outcomes while intentionally discarding low-level implementation steps and per-task granularity. Do not merge unrelated work or invent accomplishments; keep unmatched entries. Place each merged summary at the position of its earliest source entry, preserving the relative order of the remaining entries. If no entries can meaningfully be combined, report that and leave the ledger unchanged.
- After historical compression, update all task IDs in `workflows/TASKS.md`: renumber every top-level entry sequentially in document order, starting with `History` and continuing through `Current`; regenerate every current subtask ID from its new parent ID and sequential position. Update any references within `workflows/TASKS.md` and affected files under `workflows/memory/` to the corresponding new IDs, including references to source entries now represented by a merged summary. Preserve current task descriptions, tags, checkbox states, and subtask structure. Verify that IDs are unique, subtask IDs match their parents, and no stale references remain. Do not retain an old-ID mapping or write IDs outside `workflows/TASKS.md` and `workflows/memory/`.

- Mark work complete only when its stated outcome is achieved; do not check off blocked or merely proposed work.

**workflows/REVIEW_WORKFLOW.md**

- Be critical about design, implementation, organization, and correctness while respecting time and compute constraints.
- For scientific work, apply the scrutiny of a reviewer at a top-tier scientific conference. For other domains, adapt the review criteria to the intended users and project purpose.
- Report issues in descending priority. Tag each with an aspect such as `Code` or `ML design` and confidence such as high, medium, or low. Explain the evidence, consequence, and a practical improvement; distinguish confirmed defects from open questions.
- Identify discrepancies among code, comments, documentation, and papers when those materials exist.

**workflows/PAPER_WORKFLOW.md**

- BibTeX management belongs to the user. Agents may read and use existing references for citations, but should request missing reference keys rather than invent or manage entries.
- Write clearly and naturally. Keep the introduction and abstract understandable to an undergraduate student, minimize unnecessary jargon, and avoid stock AI phrasing and em dashes.
- Put significant decisions that `probe-me` cannot settle, citation requests, or user work that takes time in `workflows/REQUESTS.md`. Use unique IDs and this format:

  ```markdown
  ## REQ-014 — Decision

  **Need:** Decide whether the paper claims scalability in vocabulary size or computational complexity.

  **Context:** The implementation removes the vocabulary-sized output layer, but temporal attention still scales with sequence length.

  ## REQ-015 — Citation

  **Need:** Find prior work supporting candidate-based prediction over large discrete spaces.

  **Claim:** Candidate-based prediction avoids a global vocabulary-sized output layer.
  ```

- Place a matching TODO comment, such as `%TODO REQ-014`, at the relevant `.tex` location. Adapt comment syntax for other confirmed authoring formats.
- When the user invokes the `decision` skill and the corresponding decision is found, or supplies the requested BibTeX key, apply the resolution and remove the resolved request and matching TODO. Preserve unrelated requests. Follow the actual skill instructions.

**workflows/MEMORY_WORKFLOW.md**

- Available on demand. Invoke only when the agent needs to document or communicate transient development state between sessions; consult relevant existing notes when invoked.
- Save notes only in `workflows/memory/`, excluded from the parent project repository but tracked in the workflow repository. Verify the parent exclusion and independent workflow Git root before writing; do not exclude memory from the workflow repository. Create the directory only when needed, and organize concise notes by topic or feature using descriptive names. Task IDs are allowed in these files; keep them aligned with `workflows/TASKS.md`. Update relevant notes rather than duplicating them.
- Record only useful resume context: current state, relevant paths, blockers, validation performed, and next steps. Keep durable documentation and decisions in their established locations; avoid transcripts and running diaries.
- Update stale notes and remove obsolete notes for the work being handled. This authorizes narrowly scoped cleanup within `workflows/memory/`, including tracked obsolete notes; inspect their workflow Git changes first and preserve unrelated notes and user or other-agent changes. Workflow commits and synchronization remain subject to the confirmed authorization.

### PROJECT_MAP.yaml: compact repository navigation

- Interpret map path keys relative to the parent project root, where `PROJECT_MAP.yaml` also lives. Write valid YAML that roughly follows the repository's directory tree. Describe its purpose and the principal directories, features, entry points, and relevant workflows using concise descriptions beside path keys. Include important source, configuration, and documentation paths that actually exist.
- Never include workflow or instruction files in the project map, including root `AGENTS.md` and any files under `workflows/`.
- The map need not describe every file. Summarize whole directories or group related file keys under a shared description; for example, `"{util.py, io.py}": general utils`. Grouping is generally encouraged as the project grows. Identify artifact directories without listing or loading their contents.
- For a new repository, distinguish planned structure from existing files. Do not fabricate modules, commands, or completed features.
- Avoid exhaustive file inventories, copied code, and implementation detail that will quickly go stale.
- Require updates when features are added or removed, and when mapped locations change. Keep this maintenance instruction in `AGENTS.md` so it applies across workflows.

### Parent Git exclusions and separate workflow repository

- Resolve the parent project root before creating the nested repository. Run parent Git commands from that root, using `git -C <project-root> ...` when needed. Resolve its local exclude file with `git rev-parse --git-path info/exclude` so worktrees are handled correctly. Preserve existing contents and add only `/AGENTS.md` and `/workflows/`, once each, for these generated instructions. Never use the parent project's tracked `.gitignore` or register `workflows/` as a submodule.
- Check the parent index for already tracked `AGENTS.md`, `workflows/`, and legacy root support files before migration; exclusions cannot hide tracked files. Report conflicts and ask how to handle them without automatically untracking anything. For an existing setup, inspect legacy root workflow files, `TASKS.md`, `REQUESTS.md`, and `memory/`. Preserve their contents, resolve meaningful conflicts, and migrate them to `workflows/` under the confirmed migration authorization. Update all affected links and paths. Do not leave contradictory duplicate instructions. Remove only obsolete exclusion entries owned by this setup after migration is complete; preserve unrelated exclusions and ask when ownership is unclear.
- If the user supplies an existing workflow remote for another device, restore it with `git clone <confirmed-remote> workflows` before generating or merging files, provided network access is authorized and the destination is absent or empty. Never clone over an existing nonempty directory; inspect and reconcile existing contents first. Otherwise create `workflows/` and run `git init workflows` from the project root if it has no repository of its own. Initialization authorizes this local nested Git setup, but not creation of a remote hosting repository.
- Verify `git -C workflows rev-parse --show-toplevel` resolves exactly to `<project-root>/workflows`. Git may find the parent repository if the nested repository is missing, so merely checking that the command succeeds is insufficient. Preserve an existing workflow repository's history, remotes, branch, staged changes, and user edits; inspect before making changes.
- Track all regular files within `workflows/`, including every workflow, ledger, request file, and memory note, in that independent repository; `.git/` is Git metadata. Do not add ignore rules for these files inside the workflow repository. Check for existing or global ignore rules that prevent tracking them and report conflicts. Review its contents and stage the generated or migrated files with `git -C workflows add -- <reviewed-paths-relative-to-workflows>`; do not stage unrelated user changes. Verify those files appear in `git -C workflows ls-files`. Future notes and other support files must also be tracked there when created; never force-add `workflows/` to the parent repository.
- Keep root `PROJECT_MAP.yaml` out of local exclusions and track it in the main project repository. Review and stage its generated or updated contents from the project root with `git add -- PROJECT_MAP.yaml`; verify it appears in the parent `git ls-files` and is not ignored. If a legacy `PROJECT_MAP.yml` at the root or a map under `workflows/` exists, preserve its contents and migrate it to root `PROJECT_MAP.yaml` under the confirmed migration authorization, resolving conflicts before replacing anything. Update affected links and remove the obsolete copy only when authorized; preserve unrelated staged changes and history in both repositories. Do not create a second map in workflow Git.
- Before saving notes, verify from the project root with `git check-ignore` that `AGENTS.md`, workflow files, and intended memory paths are ignored by the parent, and verify the nested Git boundary. If Git is unavailable or the parent project is not initialized, report the limitation and defer nested setup and memory writes until parent exclusion can be established; do not initialize the parent project implicitly.
- A local nested repository alone does not synchronize devices. Use the user-confirmed remote and branch for authorized workflow commits, pushes, and pulls; inspect local changes before synchronization and preserve them when reconciling conflicts. If remote configuration or synchronization authorization is missing, report that cross-device setup is pending. On each device, establish the parent exclusions and restore `workflows/` separately from the project clone. Root `AGENTS.md` remains outside workflow Git and must be generated or maintained on each device; keep its routing and shared rules consistent with the restored workflows.
- Retain the storage paths, repository-boundary rules, and cross-device setup guidance in generated `AGENTS.md` and the relevant workflow files so they survive deletion of this initialization file.

## 4. Check and hand off

- Verify that `AGENTS.md`, all five workflow files under `workflows/`, and `PROJECT_MAP.yaml` exist; the YAML is valid; generated relative links resolve; status and routing agree; and the files do not contradict each other or unresolved existing policies.
- Check that the interview included at least six questions, explicitly including domain and environment; remove unsupported environment assumptions and unconfirmed commands.
- Ensure `AGENTS.md` stays concise and workflow detail remains in the relevant file. Do not create `workflows/TASKS.md`, `workflows/REQUESTS.md`, `workflows/memory/`, tests, or other support files merely to demonstrate the format.
- Verify that all durable information survives deletion of `INIT_AGENT.md` and that `AGENTS.md` includes the rule restricting task IDs to `workflows/TASKS.md` and files under `workflows/memory/`. Use descriptive placeholders instead of literal task IDs in generated workflow examples.
- Verify that task-workflow routing and activation cover both condensation and historical compression, and that `workflows/TASK_WORKFLOW.md` retains both functions and the full-ledger ID update rules after historical compression.
- Check task examples and any edited ledger for `# History` with plain bullets and `# Current` with checklists, without prose notes. Verify the parent excludes `/AGENTS.md` and `/workflows/`, the nested Git root is `workflows/`, and support files inside `workflows/` and existing memory notes are tracked only in that nested repository. Verify root `PROJECT_MAP.yaml` is tracked by the parent and is not ignored or duplicated under `workflows/`. Report any parent tracked-file conflicts and pending workflow commits or remote synchronization.
- Report files created or updated, important confirmed choices, and any unresolved limitations. Initialization authorizes instruction-file work, not implementation, experiments, dependency changes, or unrelated cleanup.
