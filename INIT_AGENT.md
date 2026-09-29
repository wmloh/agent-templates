# Initialize project instructions

Use this file to initialize or update repository instructions for a new or existing project. Produce a concise root `AGENTS.md`, four modular workflow files, and a compact `PROJECT_MAP.md`. This file is the initialization procedure; do not copy the entire procedure into `AGENTS.md`.

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
4. **Workflows:** Which workflows are active: code, task tracking, review, or paper writing? All four workflow files will exist, but irrelevant workflows will be marked inactive. Identify any additional workflow that needs its own file.
5. **Execution and artifacts:** Which commands, resource budgets, and artifact locations matter? Establish whether training, evaluation, data processing, network access, or other substantial runs are authorized. Preserve the explicit restrictions on installations, environment changes, destructive commands, and artifact overwrites unless the user revises them.
6. **Collaboration and decisions:** How should tasks, unresolved decisions, and user requests be tracked? Confirm the task and paper conventions below, the review audience, and whether any existing policy needs reconciliation. Confirm the compact project map and its feature-change maintenance rule.

Challenge proposals constructively where evidence reveals a practical problem. Keep the interview relevant to the project's domain; add scientific, deployment, or evaluation policies only when the user requests or confirms them.

Summarize decisions, remaining assumptions, and consequences before editing. If the interview receives no response, leave initialization unfinished and resume the unanswered questions on continuation, subject to the available tool's governing instructions. For an individually skipped optional detail, state a conservative assumption. Never treat silence as authorization for restricted actions.

## 3. Generate or merge the files

State the intended edits first. Create or update the following files at the repository root using repository-relative Markdown links. Preserve unrelated content and edits. Existing equivalent workflow files may be consolidated into this structure only after resolving meaningful conflicts; avoid leaving contradictory duplicate instructions.

### AGENTS.md: shared operating rules and routing

Keep this file lean. Include a short project description, confirmed environment facts, the shared rules below, and the routing table. Put workflow-specific detail in the linked files. Record durable decisions, not the interview transcript.

Preserve these core rules:

- Do not read, search, or modify files outside this repository unless the user explicitly asks.
- Before editing files, state the intended edits.
- Preserve changes from the user and other agents. Do not revert, overwrite, or clean up unrelated files unless explicitly asked.
- Do not run destructive commands such as `rm`, `git reset`, `git checkout`, broad `mv`, or cleanup scripts unless the user explicitly approves the exact action.
- Do not install packages, download dependencies, or change environments unless explicitly asked. Notify the user of missing environment components or packages before proceeding with dependent work.
- Lightweight read-only inspection and small, relevant syntax/import checks are acceptable when they do not touch large data or model artifacts. Follow confirmed project limits for other execution.
- For substantial features or experimental changes whose intended behavior is unclear, ask clarifying questions before editing and use `probe-me` as appropriate. Always honor an explicit invocation of that skill. Prefer multiple-choice questions and challenge proposals constructively.
- Do not overwrite result files, checkpoints, Parquet data, experiment caches, or plots. Use new output locations for authorized runs.
- Read workflow files only when their triggers apply. For a task spanning workflows, read each applicable file; do not load all files merely because they are linked.
- Consult [PROJECT_MAP.md](PROJECT_MAP.md) when locating work or understanding repository structure. Update it in the same change when a feature is added or removed; also correct affected entries when features or entry points move.

Include a routing table of this form, adapted to confirmed project status:

| File | Read when |
| --- | --- |
| [CODE_WORKFLOW.md](CODE_WORKFLOW.md) | Implementing, modifying, debugging, or validating code. |
| [TASK_WORKFLOW.md](TASK_WORKFLOW.md) | The user explicitly asks to create, track, or complete a task. |
| [REVIEW_WORKFLOW.md](REVIEW_WORKFLOW.md) | Reviewing code, designs, experiments, or written work. |
| [PAPER_WORKFLOW.md](PAPER_WORKFLOW.md) | Writing or editing a research paper or managing its requests. |

Mark inactive workflows in the table so agents need not open them. A later request that activates an inactive workflow should trigger a targeted clarification and update of its status. Link `PROJECT_MAP.md` separately as a navigation resource, not as mandatory reading for every task.

### Workflow file structure

Generate **all four** workflow files above, even when some are inactive. Each should state its status, activation trigger, and concise actionable rules. For an inactive workflow, retain a short applicable baseline and identify what must be confirmed before activation. Do not invent tools, paths, commands, or domain requirements. Do not duplicate shared operating rules or require reading unrelated workflows.

**CODE_WORKFLOW.md**

- Follow nearby code style and the confirmed language conventions. For Python, use Google-style docstrings for public functions/classes and nontrivial private helpers. Keep comments concise and focused on non-obvious logic.
- Avoid routine logging or printing in library functions. Warnings are acceptable for unusual or incorrect states. Python driver scripts should report progress with the project's existing `accelerate` logger or `tqdm` convention where available; confirm a suitable existing alternative for other stacks. This rule does not authorize installing either dependency.
- Do not create test cases in `tests/` or `README.md` files in subdirectories unless explicitly told to do so. Do not consider backward compatibility unless explicitly told to do so.
- Document confirmed lightweight validation commands and their prerequisites. Run checks appropriate to the change within the authorized scope; report what was checked and any limitations. Do not claim unrun tests passed.
- After implementation and validation, if a concrete cleanup, organization improvement, fix, or modularization opportunity was encountered, propose it in one sentence in the conversation without executing it. Base it only on files already read; do not inspect unrelated files to find a suggestion.

**TASK_WORKFLOW.md**

- Activate only when the user asks to create, track, or complete a task. Ordinary code edits and initialization alone do not require a task ledger.
- If `TASKS.md` is absent when this workflow is activated, create it. Preserve existing IDs and content; assign unused IDs for new entries.
- Use exactly two sections in `TASKS.md`, in this order: `Completed` and `Pending`.
- List completed tasks under `Completed` as one-sentence bullet points, preserving their task IDs and relative order. When the user asks to condense or compact `TASKS.md`, summarize each fully completed task and its subtasks in one concise, broad sentence, then remove those subtasks.
- Under `Pending`, use exactly two tiers of checkboxes. Outer items describe high-level tasks and start with IDs such as `T-01`; inner items describe one narrow local subtask per sentence and start with IDs such as `T-01.1`. An optional tag follows the ID.

  ```markdown
  ## Completed

  - T-01 Implement the agreed feature and complete its lightweight validation.

  ## Pending

  - [ ] T-02 Implement the agreed feature.
    - [ ] T-02.1 #code Add the entry point.
    - [ ] T-02.2 #check Run the agreed lightweight validation.
  ```

- Mark work complete only when its stated outcome is achieved; do not check off blocked or merely proposed work.

**REVIEW_WORKFLOW.md**

- Be critical about design, implementation, organization, and correctness while respecting time and compute constraints.
- For scientific work, apply the scrutiny of a reviewer at a top-tier scientific conference. For other domains, adapt the review criteria to the intended users and project purpose.
- Report issues in descending priority. Tag each with an aspect such as `Code` or `ML design` and confidence such as high, medium, or low. Explain the evidence, consequence, and a practical improvement; distinguish confirmed defects from open questions.
- Identify discrepancies among code, comments, documentation, and papers when those materials exist.

**PAPER_WORKFLOW.md**

- BibTeX management belongs to the user. Agents may read and use existing references for citations, but should request missing reference keys rather than invent or manage entries.
- Write clearly and naturally. Keep the introduction and abstract understandable to an undergraduate student, minimize unnecessary jargon, and avoid stock AI phrasing and em dashes.
- Put significant decisions that `probe-me` cannot settle, citation requests, or user work that takes time in `REQUESTS.md`. Use unique IDs and this format:

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

### PROJECT_MAP.md: compact repository navigation

- Describe the repository's purpose and the principal directories, features, entry points, and relevant workflows. Link important source/configuration/documentation paths that actually exist.
- Prefer a compact table mapping each feature or area to its location, role, and relevant workflow. Identify artifact directories without listing or loading their contents.
- For directories with many files, map the directory or relevant groups of files rather than listing every file individually.
- For a new repository, distinguish planned structure from existing files. Do not fabricate modules, commands, or completed features.
- Avoid exhaustive file inventories, copied code, and implementation detail that will quickly go stale.
- Require updates when features are added or removed, and when mapped locations change. Keep this maintenance instruction in `AGENTS.md` so it applies across workflows.

## 4. Check and hand off

- Verify that `AGENTS.md`, all four workflow files, and `PROJECT_MAP.md` exist; generated relative links resolve; status and routing agree; and the files do not contradict each other or unresolved existing policies.
- Check that the interview included at least six questions, explicitly including domain and environment; remove unsupported environment assumptions and unconfirmed commands.
- Ensure `AGENTS.md` stays concise and workflow detail remains in the relevant file. Do not create `TASKS.md`, `REQUESTS.md`, tests, or other support files merely to demonstrate the format.
- Report files created or updated, important confirmed choices, and any unresolved limitations. Initialization authorizes instruction-file work, not implementation, experiments, dependency changes, or unrelated cleanup.
