# Agent templates

This repository contains provider-agnostic templates for agent skills and project instructions. Install the skills once in your target environment. For each project, use `INIT_AGENT.md` to initialize its instructions. The files here are source templates; they are not ready-to-use project instructions or an installation package for a particular provider.

## Contents

| Template | Purpose | Automatic invocation |
| --- | --- | --- |
| [appraise-code](skills/appraise-code.md) | Review code before a commit, summarize changes, suggest a commit message, and identify related omissions. | No; explicit request required. |
| [decision](skills/decision.md) | Record, apply, and update persistent project decisions. | `use` only, when the task or project instructions indicate relevance. `make` and `update` require an explicit request. |
| [incidental-findings](skills/incidental-findings.md) | Report unrelated issues observed during required work without expanding the task. | No; explicit request required. |
| [probe-me](skills/probe-me.md) | Inspect and question an implementation request before changing files. | Yes, for complex or consequential implementation requests; also available explicitly. |
| [INIT_AGENT.md](INIT_AGENT.md) | Interview the user and generate or merge project instructions, workflow files, and a project map. | Run when explicitly asked to initialize or update project instructions. |

## Install skills

Do this once per system or agent environment. Ask the agent to install the templates in `skills/` using that environment's supported locations, file structure, metadata, and invocation syntax. `INIT_AGENT.md` is not part of the skill installation.

Keep the skill contents almost exactly the same. Make changes only for a specific compatibility requirement, agent provider Markdown formatting requirements, or an explicit user request, and preserve the workflows, invocation rules, and unanswered-question rule.

For example, if `request_user_input` does not exist, replace it with an available tool that serves the same purpose and use only parameters that tool supports. If no suitable tool exists, ask the questions in conversation. Preserve the requirement to wait for answers. If the environment cannot honor a required behavior, explain the incompatibility and consult the user before changing that behavior.

Use native discovery or invocation settings where available, while preserving the rules written in each skill. Adjust references in the skills only where the target environment requires it. Check that the installed skills are discoverable and their references resolve. Report where the skills were installed and any adaptations made.

An example installation request:

> Install the skills from this repository globally for this agent environment. Preserve their content and behavior, making only necessary compatibility changes. Check that they are discoverable, then report their installed locations and any adaptations.

## Initialize instructions for each project

For each new or existing project, copy and paste the contents of [INIT_AGENT.md](INIT_AGENT.md) into an agent conversation in that project, then ask the agent to follow those instructions. The interview produces or updates that project's `AGENTS.md`, workflow files, and `PROJECT_MAP.md`. Do not copy the procedure wholesale into `AGENTS.md`. The globally installed `probe-me` and `decision` skills must be available to the agent.

An example request to send after pasting `INIT_AGENT.md` in the project conversation:

> Follow the INIT_AGENT.md instructions I just pasted to initialize or update this project's AGENTS.md and related instruction files. Inspect the project, ask the required questions, and preserve existing project-specific instructions.
