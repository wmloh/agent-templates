---
name: probe-me
description: Clarify and critique an implementation instruction before changing files by inspecting the request and relevant project state, then asking targeted questions about assumptions, flaws, alternatives, scope, and consequences.
---

# Probe Me

Turn an underspecified or consequential implementation request into a shared, informed decision before changing files.

## Workflow

1. Before asking, understand the request and inspect the relevant project state. Read applicable code, configuration, and recent local context needed to identify real constraints.
2. Decide whether probing is warranted. Always probe after an explicit "probe me" request. For implementation requests, probe when the feature is complex or the change is profound. Do not impose a probe on a clearly local, simple task.
3. Use a multiple choice question tool (e.g.`request_user_input`) to ask concise, decision-oriented questions. Ask at least two questions per call. Start with the highest-impact unknowns; use multiple calls if the previous answers reveal unresolved choices. If the user does not respond, stop the conversation **immediately**. Upon continuation, ask the same unresponded questions again.
4. Challenge assumptions extensively but constructively. Prefer questions that critique design grounded on established theory and conventions, expose alternatives, and make trade-offs or failure modes explicit.
5. Summarize the resulting decisions, remaining assumptions, and implications, then continue with the agreed task.
## Question Design

Ask about uncertainties, prioritizing design, evaluation procedures, code, and data. Examples include:

- The user outcome and how success will be evaluated.
- Whether the proposed feature fits the existing architecture and workflows.
- Research, performance, or backwards-compatibility consequences.
- Scope boundaries, assumptions, data, and interfaces
- Viable alternatives and the trade-off the user prefers.

For each tool question, provide enough choices to state the trade-off. Use the tool's free-form response path when no choice fits. Keep the tone curious and direct.
