# Agent templates

This repository contains provider-agnostic templates for agent skills and project instructions. Install the skills once in your target environment. For each project, use `INIT_AGENT.md` to initialize its instructions. The files here are source templates; they are not ready-to-use project instructions or an installation package for a particular provider.

This README is for humans browsing and using this repository. During project initialization, the agent receives only [INIT_AGENT.md](INIT_AGENT.md); this README is not supplied. Keep all initialization requirements in `INIT_AGENT.md`, with ongoing rules carried into the generated project instructions, so no agent behavior depends on this README.

## Contents

| Template | Purpose | Automatic invocation |
| --- | --- | --- |
| [appraise-code](skills/appraise-code.md) | Review code before a commit, summarize changes, suggest a commit message, and identify related omissions. | No; explicit request required. |
| [decision](skills/decision.md) | Record, apply, and update persistent project decisions. | `use` only, when the task or project instructions indicate relevance. `make` and `update` require an explicit request. |
| [incidental-findings](skills/incidental-findings.md) | Report unrelated issues observed during required work without expanding the task. | No; explicit request required. |
| [probe-me](skills/probe-me.md) | Inspect and question an implementation request before changing files. | Yes, for complex or consequential implementation requests; also available explicitly. |
| [INIT_AGENT.md](INIT_AGENT.md) | Interview the user and generate or merge initial project instructions, workflow files, and a project map. | Run when explicitly asked to initialize project instructions; subsequent template updates use the generated `UPDATE_WORKFLOW.md` on explicit request. |

## Install skills

Do this once per system or agent environment. Ask the agent to install the templates in `skills/` using that environment's supported locations, file structure, metadata, and invocation syntax. `INIT_AGENT.md` is not part of the skill installation.

Keep the skill contents almost exactly the same. Make changes only for a specific compatibility requirement, agent provider Markdown formatting requirements, or an explicit user request, and preserve the workflows, invocation rules, and unanswered-question rule.

For example, if `request_user_input` does not exist, replace it with an available tool that serves the same purpose and use only parameters that tool supports. If no suitable tool exists, ask the questions in conversation. Preserve the requirement to wait for answers. If the environment cannot honor a required behavior, explain the incompatibility and consult the user before changing that behavior.

Use native discovery or invocation settings where available, while preserving the rules written in each skill. Adjust references in the skills only where the target environment requires it. Check that the installed skills are discoverable and their references resolve. Report where the skills were installed and any adaptations made.

An example installation request:

> Install the skills from this repository globally for this agent environment. Preserve their content and behavior, making only necessary compatibility changes. Check that they are discoverable, then report their installed locations and any adaptations.

## Initialize instructions for each project

For each new or existing project, copy and paste the contents of [INIT_AGENT.md](INIT_AGENT.md) into an agent conversation in that project, then ask the agent to follow those instructions. Install the `probe-me` and `decision` skills in that environment beforehand.

The interview produces or merges root `AGENTS.md`, root `PROJECT_MAP.yaml`, and workflows under `workflows/`. Every project receives `UPDATE_WORKFLOW.md`; optional workflows cover code, tasks, review, paper, memory, and tools. After initialization and checks, the supplied template is moved to `workflows/INIT_AGENT.md` as an unmodified comparison baseline. If you supplied only pasted contents, the agent saves those contents there instead. The project map is tracked with the main project; workflow instructions, the template baseline, and support files use a separate Git repository under `workflows/`. Root `AGENTS.md` remains outside both repositories.

For cross-device use, synchronize and restore the workflow repository separately from the main project, and establish the local exclusions and root `AGENTS.md` on each device using the initialization procedure.

An example request to send after pasting `INIT_AGENT.md` in the project conversation:

> Follow the INIT_AGENT.md instructions I just pasted to initialize this project's AGENTS.md and related instruction files. Inspect the project, ask the required questions, and preserve existing project-specific instructions.

## Update an initialized project

Explicitly ask the agent to follow `workflows/UPDATE_WORKFLOW.md` to update project instructions. It fetches the latest public template from the fixed raw GitHub URL, diffs it against `workflows/INIT_AGENT.md`, and reconciles upstream changes with project customizations. If the template is unchanged, no instruction update is needed. Otherwise, the agent interviews you with `probe-me`, presents a table of proposed changes, and waits for your approval before editing `AGENTS.md` and the approved workflow instruction files. After the approved update and verification are complete, it replaces the saved baseline with the exact reviewed template copy. Other project files remain untouched.

You can also request updates to named skills, alongside instructions or on their own. The agent compares their public sources with the confirmed installed files, preserves local and provider adaptations, and uses the same interview and approval process. Skill comparisons proceed independently when the project template is unchanged; skills-only updates leave the template baseline unchanged. Confirmed skill installations may be outside the project, and updating a shared installation affects other projects using it.

Example requests:

> Follow UPDATE_WORKFLOW.md to update this project's instructions from the latest template while preserving its customizations.

> Follow UPDATE_WORKFLOW.md to update only the installed probe-me and decision skills. Leave project instructions unchanged.
