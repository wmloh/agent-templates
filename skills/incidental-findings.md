---
name: incidental-findings
description: Record concrete issues unrelated to the requested task that surface during required work, then report them afterward with evidence and confidence; do not investigate beyond the task or fix them. Use only when explicitly invoked as $incidental-findings.
---

# Incidental Findings

Track concrete, unrelated issues that become visible while completing the user's requested task. This skill supplements the task; it must not expand, delay, or replace it.

## Invocation

Invoke only when the user explicitly requests this skill. Do not invoke automatically when an unrelated issue appears during another task.

## Boundaries

- Use only observations surfaced by work already required for the task: relevant file inspection, commands, tests, builds, runtime checks, tool responses, or user-provided evidence.
- Do not search, test, reproduce, inspect adjacent areas, or run any other check solely to discover unrelated issues. Do not use a finding as a reason to broaden the task.
- Do not implement, suppress, reformat, work around, or otherwise remediate an unrelated finding. Preserve it for the final report. If it blocks or makes the requested work unsafe, identify it as a blocker and ask the user how to proceed rather than silently expanding scope.
- Do not report expected behavior, intentional limitations, transient tool noise, or issues already resolved by the requested change. If a problem directly affects the requested outcome, handle or report it as part of that task instead of treating it as incidental.

## Capture

When an incidental issue appears, record enough evidence to report it later without additional investigation:

- a precise location or command/test that exposed it;
- the observed behavior or failure, separated from interpretation;
- the likely impact; and
- confidence: `high` for direct or reproducible evidence, `medium` for a well-supported but unconfirmed defect, or `low` for a plausible signal with limited evidence.

Continue the requested task after capturing the finding. Do not interrupt the task to improve confidence unless the issue is a safety or completion blocker.

## Completion report

After delivering the requested task result, add a concise `Incidental findings` section. List each finding with its confidence, location or exposing command, evidence, and impact. State `None observed` when there are no findings. Do not claim to have investigated or fixed any finding; any suggested follow-up is for the user to decide and perform separately.
