# Problem Resolution

Process for approaching ambiguous or complex problems. Four phases: research, narrative, execution plan, and (optionally) agent-ready handoff.

This is not for fixing a known bug (see `research/bug-investigation.md`). This is for taking a messy, underspecified problem and turning it into something actionable.

## Core Principle

Write every finding, decision, and action to a file before moving to the next step. Do not rely on context window memory; files are the only reliable record.

## Phase 1: Research

Follow `research/methodology.md`. The research question is: what is the actual problem, and what are the options for resolving it?

Do not generate solutions during research. Complete the research phase first.

## Phase 2: Narrative Document

Write a document explaining the problem for the user. Follow `tasks/document-writing.md` for structure and drafting discipline.

The narrative should cover:

1. **Problem statement**: What is wrong, in plain language. One or two paragraphs.
2. **Context**: How this happened. Relevant history, prior attempts, contributing factors.
3. **Findings**: What the research revealed. Organized by theme, not by source.
4. **Options**: Possible approaches to resolution, with tradeoffs for each.
5. **Recommendation**: Which option to pursue and why.

Present this to the user before moving on. Do not proceed to Phase 3 without user approval.

## Phase 3: Execution Plan

Once the user approves a direction, translate the recommendation into a concrete plan.

The execution plan should be:

- **Sequential**: Ordered steps, each with a clear completion criterion.
- **Granular**: Small enough that each step can be verified independently.
- **Reversible where possible**: Note which steps are hard to undo.
- **Risk-aware**: Flag steps that could cause side effects or require elevated access.

Format:

```markdown
## Execution Plan

### Step 1: [Description]
- Status: [pending | in-progress | done | paused | blocked | skipped]
- Action: What to do.
- Verify: How to confirm it worked.
- Rollback: How to undo if needed.
- Outcome: One-line summary of what happened. Detail goes in the execution log.

### Step 2: [Description]
...
```

Write the execution plan to `thoughts/local/plans/<description>.md`. Once approved by the user, move it to `thoughts/shared/plans/`.

### Execution Log

Keep a separate file in `thoughts/shared/logs/<description>.md`. The plan stays clean as a reference; the log captures what actually happened.

The log is append-only. Each entry records the step number, what was done, what the output was, and any deviations from the plan. Format:

```markdown
## Execution Log

### Step 1: [Description]
- Timestamp: [when]
- What happened: [detail]
- Deviation from plan: [if any, otherwise "none"]
- Notes: [anything relevant for later steps]

### Step 2: [Description]
...
```

### Execution Tracking

During execution (whether by the same agent, another agent, or with user assistance):

- Update each step's status in the execution plan as work progresses.
- Write detailed records to the execution log, especially when things diverge from the plan.
- If a step is blocked or paused, note the reason in both the plan (status) and the log (detail).
- If a step is skipped, explain why in the log.
- The execution plan and log are both living documents during this phase.

## Phase 4: Agent-Ready Handoff (Optional)

If the execution will be performed by another agent (or a future session), produce a handoff document following the convention in `core/context.md` (see Handoffs). Write it to `thoughts/local/scratch/handoffs/<timestamp>-<description>.md`.

The research folder, narrative, and execution plan are passed along as artifacts, so the handoff does not need to restate them. In addition to the standard handoff fields, include:

1. **Guidelines**: List the steering and convention files the agent should follow (e.g., `coding.md`, `tools.md`, project-specific standards). The receiving agent has no memory of your conventions; if you do not point it at them, it will invent its own.
2. **Constraints**: What the agent must not do. Boundaries, protected files, systems to avoid.
3. **Verification**: How the agent should confirm success after each step and at the end.
4. **Escalation**: When to stop and ask a human. Define the conditions explicitly.

Guidelines for the handoff:

- The executing agent has the artifacts but no memory of the conversation that produced them. The handoff must provide sufficient orientation without duplicating artifact content.
- Be explicit about what "done" looks like.
- Do not assume the executing agent will exercise judgment on ambiguous steps. Remove the ambiguity or flag it as a decision point requiring human input.
- Keep it concise. Point to the artifacts rather than duplicating their content.

## Context Drift Prevention

This process can span many steps. Reread this file after every 5-6 tool calls. Reread the research notes and narrative before making decisions from memory. See `core/context.md` for the full treatment.
