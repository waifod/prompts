# Context Management

Rules for managing the context window during agent sessions.

## Priority

Context windows are finite. As they fill, signal degrades. Failure modes, ranked by severity:

1. Incorrect information in context (actively misleading)
2. Missing information (needed facts absent)
3. Noise (correct but irrelevant information diluting signal)

Keep context correct, complete, and compact. When these conflict, correctness wins.

## Compaction

Compaction distills accumulated context into a structured artifact so a fresh session can continue without loss.

### When to Compact

- Context utilization exceeds 50-60% and the task is not nearly done.
- Accumulated findings, decisions, or progress would be expensive to reconstruct.
- Transitioning between work phases (research to planning, planning to implementation).
- Uncertainty about whether earlier context is still accurate.

### How to Compact

Write a progress file containing:

- The goal (what you are trying to achieve).
- The approach (what strategy you are following).
- What has been done so far, with outcomes.
- What remains to be done.
- The current problem or blocker, if any.
- Key decisions made and why.
- File paths and references needed to resume.

The file must be self-contained: a fresh session reading only this file and the referenced artifacts continues the work without loss.

### Where to Write It

Write to `thoughts/` in the project root. The directory has two subdivisions:

```
thoughts/
  local/                   # Session-local, not shared across teams
    research/              # In-progress research (per-topic subfolders)
    scratch/               # Scratch notes, handoffs, session context
  shared/                  # Committed to repo, available to the team
    research/              # Finalized research artifacts
    plans/                 # Execution plans
    logs/                  # Execution logs
    decisions/             # Architectural decision records
```

`local/` is working space. Handoff documents, in-progress research, and scratch notes go here. Add `thoughts/local/` to the project's `.gitignore`.

`shared/` is the permanent record. Finalized research, approved plans, execution logs, and decision records go here. Commit these to the repo.

### Promotion

Work starts in `local/`, moves to `shared/` when it meets the finalization criteria for its type:

| Artifact | Starts in | Moves to | Finalized when |
|---|---|---|---|
| Research | `local/research/<topic>/` | `shared/research/<topic>/` | Synthesis written, user has reviewed findings |
| Plan | `local/plans/` | `shared/plans/` | User approves the plan |
| Log | `shared/logs/` (directly) | n/a | Logs are append-only; they start in shared |
| Decision | `shared/decisions/` (directly) | n/a | Decision is made and recorded |
| Handoff | `local/scratch/handoffs/` | n/a | Consumed by the resuming session, then archived or deleted |

Create the directory if it does not exist. For implementation work where the code itself is the artifact, commit messages can serve as the compaction record.

Write the progress file before you need it, not after.

## Session Boundaries

### Starting a Session

1. Read project documentation (if it exists).
2. Look for handoff files in `thoughts/local/scratch/handoffs/`. If any exist, read the most recent one (by filename timestamp).
3. Look for progress files in `thoughts/local/`. If resuming work, read the relevant progress file.
4. Read relevant steering files (core files, task-specific files).
5. If resuming from a handoff, verify assumptions: check branch state, reread referenced artifacts, confirm nothing has changed since the handoff was written. Do not trust the handoff blindly if time has passed.
6. Orient before acting. Understand current state before making changes.

### Ending a Session

1. Write a progress file if work is incomplete.
2. Commit code changes (do not leave uncommitted work as the only record).
3. Update task tracking if applicable.

A session without a written record of its progress is wasted context.

### Handoffs

A handoff is a structured compaction for session transfer: to a future session or a different agent.

Write handoff files to `thoughts/local/scratch/handoffs/<timestamp>-<description>.md`. Use ISO 8601 date prefix for sorting (e.g., `2025-02-17-migrate-auth-service.md`).

A handoff file contains:

- **Goal**: One sentence stating what the work is trying to achieve.
- **Status**: What is done, what is in progress, what is blocked.
- **Key decisions**: Decisions made during the session and why.
- **Artifacts**: Files the resuming session should read, in order.
- **Next steps**: Concrete actions to take. No vague intentions.
- **Open questions**: Unresolved issues requiring human input or further research.

Write a handoff when:

- Context utilization reaches 60-70% and work is not nearly done.
- Switching to a different task with intent to return.
- Transferring work to another agent or session.

A handoff differs from a progress file in specificity: a progress file tracks state; a handoff orients a reader with no prior context. When in doubt, write a handoff. It is strictly more useful than a progress file.

## Sub-Agent Context Isolation

Sub-agents run in isolated context windows. Use them to keep the main context clean.

### When to Use

- Searching, grepping, or reading many files to answer a question. Search noise stays in the sub-agent's context; only the answer returns.
- Investigating a tangent that may or may not be relevant.
- Gathering information from multiple sources in parallel.

### When Not to Use

- Making file changes (the main agent owns all mutations).
- Tasks requiring full conversation history.
- Simple operations where sub-agent overhead exceeds context savings.

### Specialized Agents

Use focused sub-agents rather than general-purpose ones. Each agent has a narrow scope and returns structured output. The main agent synthesizes their findings.

| Agent | Purpose | Allowed operations |
|---|---|---|
| code-finder | Locate files and components relevant to a feature or question | Search (grep, glob, file listing), LSP lookups |
| code-analyzer | Trace implementation details, data flow, and call chains | File reading, search, LSP lookups |
| pattern-finder | Find similar implementations, reusable patterns, and conventions | Search, file reading, LSP lookups |
| knowledge-finder | Discover relevant documents in `thoughts/` and project docs | Search, file listing |
| knowledge-analyzer | Deep-read research documents and extract actionable findings | File reading, search |
| web-researcher | Search the web for external documentation, library info, and current data | Web search, web fetch, file reading |

All code-focused agents (code-finder, code-analyzer, pattern-finder) document what exists as-is. They do not suggest improvements or generate solutions. They report facts.

When spawning a sub-agent, provide:

1. A clear, specific question.
2. The scope (which directories, which files, which topic).
3. What format the answer should take.

### Expected Sub-Agent Output

A sub-agent response must include:

- A direct answer to the question asked.
- File paths and line numbers for any code references.
- Confidence level (certain, likely, uncertain).
- What it could not determine, if anything.

If a sub-agent returns vague or incomplete results, do not fill in gaps from memory. Ask again with more specific instructions, or investigate directly.

## Context Drift

Context drift: the agent's working assumptions diverge from reality. It happens gradually and is hard to detect from inside the session.

Causes:

- Accumulated assumptions from earlier in the session that are no longer true.
- Files changed since last read.
- Findings from one source silently overridden by findings from another.
- Inaccurate recall of content read many tool calls ago.

Prevention:

- Reread source files before making claims about their contents.
- Reread steering files (core files, task-specific files) every 5-6 tool calls during long tasks.
- Write findings to files rather than holding them in context. The file is the source of truth, not memory.
- When referencing earlier findings, verify against the written record.

## Phased Work

For tasks spanning multiple phases (research, planning, implementation), each phase transition is a compaction point.

- Complete one phase fully before starting the next.
- Write phase output to a file (research notes, plan document).
- The next phase reads the artifact from the previous phase, not the raw context that produced it.

This is the core idea behind the research/plan/implement workflow in `tasks/problem-resolution.md`. It applies to any multi-phase task.

## Decision Records

Record significant technical decisions (architecture, technology choice, approach selection) in `thoughts/shared/decisions/`. Use a lightweight ADR (Architecture Decision Record) format.

Filename: `<number>-<description>.md`, zero-padded to three digits (e.g., `001-use-dynamodb-for-sessions.md`). Number sequentially.

Format:

```markdown
# <Number>. <Title>

- Status: [proposed | accepted | deprecated | superseded by <number>]
- Date: YYYY-MM-DD

## Context

What is the situation. What forces are at play. One to three paragraphs.

## Decision

What was decided. State it directly.

## Consequences

What follows from this decision. Include both positive and negative consequences. State tradeoffs plainly.
```

Record a decision when:

- Choosing between competing approaches (the options from a problem resolution narrative).
- Adopting or rejecting a technology, library, or pattern.
- Changing an existing architectural convention.
- The choice would be non-obvious to a future reader of the codebase.

Do not record trivial implementation choices. The threshold: would this context be needed six months from now.

## Prohibited Patterns

- Accumulating findings across many tool calls without writing them down. See `research/methodology.md`.
- Starting a new phase while carrying unwritten context from the previous phase.
- Assuming sub-agent findings are correct without checking key claims.
- Treating the context window as unlimited.
