---
name: research-methodology
description: Researching, investigating, or gathering information from multiple sources. Core methodology covering file structure, progress tracking, source-by-source gathering, synthesis, and context drift prevention.
---

# Research Methodology

Rules for conducting research tasks. Designed to prevent information loss, context drift, and hallucination during multi-source investigations.

## Core Principle

Write as you go. Do not accumulate findings in memory across multiple sources. Record each finding before moving to the next source.

## File Structure

All research artifacts start in `thoughts/local/research/` during active investigation, then move to `thoughts/shared/research/` once finalized (see `core/context.md` for the `thoughts/` directory convention). At the start of every research task, create a dedicated folder:

```
thoughts/local/research/<topic>/
  progress.md           # Task tracking: goal, source checklist, decision log
  notes_<source>.md     # One file per source consulted (e.g., notes_aws_docs.md)
  synthesis.md          # Final synthesis, created in Phase 3
```

After synthesis is complete and reviewed, move the folder to `thoughts/shared/research/<topic>/`.

Use descriptive source names in filenames: `notes_dynamodb_docs.md`, `notes_team_wiki.md`, `notes_github_issues.md`. This keeps findings separated and easy to revisit.

## Progress Tracking

At the start of any research task, create `progress.md` in the research folder with:

1. A summary of the research goal.
2. A checklist of sources to consult.
3. A log section for decisions, surprises, and open questions.

Update the checklist as you go. Check items off when done. Before moving to the next source, reread the checklist to confirm nothing was skipped.

## Phase 1: Define Scope

Before consulting any source:

1. State the research question clearly. One sentence if possible.
2. Identify what a good answer looks like: what format, what level of detail, what would make it actionable.
3. List known sources to consult. Add each as a checklist item in `progress.md`.
4. Identify what you already know vs. what you need to verify.

## Phase 2: Gather

1. Consult one source at a time.
2. After each source, immediately record findings in a dedicated `notes_<source>.md` file in the research folder. Include:
   - Source name/URL/reference
   - Date consulted (if relevant to freshness)
   - Key findings, paraphrased
   - Direct quotes only when precision matters
   - Confidence level: high, medium, low
3. Check off the source in `progress.md` before moving on.
4. If a source contradicts existing findings, flag the discrepancy explicitly. Do not silently pick a winner.
5. If a source leads to new sources, add them to the checklist before continuing.

## Phase 3: Synthesize

1. Reread all notes files in the research folder before drawing conclusions.
2. Identify patterns, contradictions, and gaps.
3. For contradictions: state both positions, note which sources support each, and recommend a resolution with reasoning.
4. For gaps: explicitly list what remains unknown and whether it matters for the task at hand.
5. Write the synthesis to `synthesis.md` in the research folder.
6. Present findings to the user before taking action on them.

## Constraints

- Do not guess. If unsure about a fact, say so. "I do not know" is a valid finding.
- Do not merge information from multiple sources in your head. Write it down, then synthesize from the written record.
- Do not trust a single source for critical claims. Look for corroboration.
- Prefer primary sources over summaries. Documentation over blog posts. Official over unofficial.
- Note when information may be stale. Include dates where available.

## Context Drift Prevention

During any research task longer than a few steps:

1. Reread this file after every 5-6 tool calls.
2. Reread the notes files if you are unsure about a fact. Do not reconstruct from memory.
3. If you notice yourself making claims not grounded in the research folder, stop and verify.

## Sub-Agent Research

When research involves reading many files, searching a large codebase, or consulting multiple sources, delegate gathering to sub-agents. The main agent's context stays clean; only synthesized findings return.

### How to Structure It

1. Define the research question clearly before spawning sub-agents.
2. Give each sub-agent a focused scope: one component, one source, one question.
3. Instruct sub-agents to return:
   - A direct answer to the question.
   - File paths and line numbers for code references.
   - Confidence level (certain, likely, uncertain).
   - What they could not determine.
4. Write sub-agent findings to the appropriate `notes_<source>.md` file before moving on.
5. Do not trust sub-agent findings blindly. Verify key claims against the files if something looks off.

### When Not to Use Sub-Agents

- The research is small enough that a few file reads answer the question.
- The question requires conversational context the sub-agent would not have.
- File changes are needed (sub-agents should be read-only).

See `core/context.md` for broader guidance on context isolation and compaction.
