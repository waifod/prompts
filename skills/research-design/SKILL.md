---
name: research-design
description: Researching, planning, or scoping design documents, architecture proposals, and technical RFCs. Covers scope definition, sources, recording findings, and synthesis.
---

# Design Research

Process for researching prior to writing a design document, architecture proposal, or technical RFC. Activate the `research-methodology` skill and follow it during the research phase.

## When to Use

When you need to understand the problem space, existing solutions, and constraints before proposing a design. Not for implementation details; those come after the design is accepted.

## Scope Definition

Before researching, answer:

1. What problem are we solving? One paragraph max.
2. Who are the stakeholders? (users, dependent teams, oncall, etc.)
3. What are the known constraints? (latency, cost, compliance, team size, timeline)
4. What existing systems does this interact with?
5. Is there prior art? Previous attempts, related designs, rejected proposals.

## Sources to Consult

In rough priority order:

1. Existing design documents for the system being modified
2. Architecture diagrams and data flow documentation
3. Related tickets, post-mortems, and COEs
4. API contracts and interface definitions
5. Operational runbooks (they reveal what actually breaks)
6. Similar designs from other teams or open-source projects
7. Relevant academic papers or industry blog posts (for novel problems only)

## What to Record

For each source, create a `notes_<source>.md` in the research folder (`thoughts/local/research/<topic>/`) with:

- How the current system works (not how it is supposed to work; check the code)
- Assumptions baked into the current design
- Known pain points and limitations
- Scale characteristics: current load, growth trajectory, bottlenecks
- Dependencies: what breaks if this changes

## Synthesis

After gathering, write `synthesis.md` covering:

1. Problem statement (refined from initial scope)
2. Current state: how things work today, with evidence
3. Constraints: hard (non-negotiable) vs. soft (preferences)
4. Options considered: at least two, including "do nothing"
5. For each option:
   - How it works
   - What it costs (engineering time, operational burden, infrastructure)
   - What it risks
   - What it gives up
6. Recommended approach with reasoning
7. Open questions that need answers before committing

## Common Pitfalls

- Researching the solution before understanding the problem.
- Ignoring operational concerns (who pages at 2am when this breaks?).
- Treating the current system as wrong rather than understanding why it was built that way.
- Skipping the "do nothing" option. Sometimes the answer is to not build the thing.
