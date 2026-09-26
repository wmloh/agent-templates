# Agent templates

This repository contains provider-agnostic templates for agent skills and project instructions. Have the agent in your target environment install and adapt them before using them in a project. The files here are source templates; they are not ready-to-use project instructions or an installation package for a particular provider.

## Contents

| Template | Purpose | Automatic invocation |
| --- | --- | --- |
| [appraise-code](skills/appraise-code.md) | Review code before a commit, summarize changes, suggest a commit message, and identify related omissions. | No; explicit request required. |
| [decision](skills/decision.md) | Record, apply, and update persistent project decisions. | `use` only, when the task or project instructions indicate relevance. `make` and `update` require an explicit request. |
| [incidental-findings](skills/incidental-findings.md) | Report unrelated issues observed during required work without expanding the task. | No; explicit request required. |
| [probe-me](skills/probe-me.md) | Inspect and question an implementation request before changing files. | Yes, for complex or consequential implementation requests; also available explicitly. |
| [INIT_AGENT.md](INIT_AGENT.md) | Interview the user and generate or merge project instructions, workflow files, and a project map. | Run when explicitly asked to initialize or update project instructions. |

## Installation and adaptation

Ask the agent in the target environment to read these templates and install the skills using that environment's supported locations, file structure, metadata, and invocation syntax. Install or adapt `INIT_AGENT.md` as a reusable initialization procedure, then invoke it when setting up or updating a project. Its interview produces project-specific instructions; do not copy the procedure wholesale into the project's instruction file.

Keep the contents almost exactly the same. Make changes only for a specific compatibility requirement or an explicit user request, and preserve the workflows, invocation rules, and unanswered-question rule.

For example, if `request_user_input` does not exist, replace it with an available tool that serves the same purpose and use only parameters that tool supports. If no suitable tool exists, ask the questions in conversation. Preserve the requirement to wait for answers. If the environment cannot honor a required behavior, explain the incompatibility and consult the user before changing that behavior.

Use native discovery or invocation settings where available, while preserving the rules written in each skill. Adapt project instruction filenames or references only where the target environment requires it. Check that installed skills are discoverable, references resolve, and the initialization procedure can access its required `probe-me` and `decision` skills. Report where the templates were installed and any adaptations made.

An example installation request:

> Install the skills from this repository and adapt INIT_AGENT.md for this environment. Preserve their content and behavior, making only necessary compatibility changes. Report the installed locations and explain each adaptation.
