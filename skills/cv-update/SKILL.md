---
name: cv-update
description: Writing, updating, editing, or maintaining a one-page CV or resume. Covers research, content curation, and formatting constraints.
---

# CV Update

Rules for researching, updating, and maintaining a CV. For the research process itself (progress tracking, source-by-source gathering, write-as-you-go discipline), activate the `research-methodology` skill and follow it. This file covers only what is specific to CV tasks.

## Files

A CV project typically contains:

- A data file (e.g., `cv_data.md`): Raw information dump. All facts, transcripts, links, context, and notes live here. This is the source of truth.
- A source file (e.g., `.typ`, `.tex`, `.html`): The actual one-page CV. Only curated, concise content goes here.
- A compiled output (e.g., `.pdf`): Regenerate using the appropriate tool for the source format.

The exact filenames and formats depend on the project. Check the working directory before assuming anything.

## Phase 1: Research

Activate the `research-methodology` skill and follow it. Sources typically include personal website, GitHub repos, LinkedIn, and similar. Record findings in the data file under the relevant section (in addition to the per-source notes in the research folder).

If a source contradicts existing data, flag the discrepancy and ask the user.

## Phase 2: CV Editing

Reread this file before starting edits. The research phase may have pushed these guidelines out of your working context.

1. Read the data file for the full context.
2. Read the source file for the current state.
3. Propose changes to the user before applying them. Explain the reasoning.
4. The CV must remain one page. If adding content, identify what to cut or compress.
5. After editing, update the data file if the editorial rationale has changed.

## Constraints

These are defaults. The user or the project may override them.

- One page, always. No exceptions.
- Keep alphabetical ordering for lists (skills, focus areas) unless the user specifies otherwise.
- Formatting details (font, margins, paper size, colors) are defined in the source file. Respect what is already there; ask before changing.
