# Document Writing

Rules for producing written documents: design docs, proposals, runbooks, guides, postmortems.

## Before Writing

### 1. Clarify the Purpose

Before opening a blank file, answer:

- Who is the audience?
- What do they need to take away?
- What decisions should this document enable?
- What's the expected format and length?

If any of these are unclear, ask the user.

### 2. Research

Follow `research/methodology.md`. Gather information from the starting pointers the user provides, then expand outward to related sources. Record findings before moving on. Do not start drafting until the research phase is complete and findings are synthesized.

If the document is short or the topic is well-understood, a lightweight pass is sufficient. The point is to ground writing in verified information.

## Writing

### 3. Outline First

Reread this file before starting the outline. The research phase may have pushed these guidelines out of your working context.

Write a structural outline before drafting prose. Share it with the user for feedback. An outline is cheap to change; a full draft is not.

The outline should cover:

- Section headings
- Key points per section (one line each)
- Open questions or sections that need user input

### 4. Draft

- Write for the audience, not for the agent. Assume the audience is knowledgeable but lacks the specific context.
- Lead with the conclusion or recommendation. Supporting detail follows.
- One idea per paragraph. If a paragraph covers two things, split it.
- Use concrete examples over abstract descriptions.
- Prefer short sentences. A long sentence that could be two sentences should be two sentences.
- Use bullet points and tables when they are clearer than prose. Do not use them for everything.

### 5. Structure Conventions

- Use markdown headers to create scannable hierarchy.
- Keep heading levels consistent (do not jump from `##` to `####`).
- Front-load the document: the most important information goes first.
- Include a summary or TL;DR at the top for longer documents.
- If the document has prerequisites or assumptions, state them early.

## After Writing

### 6. Review and Tighten

After the first draft:

- Cut anything that does not serve the reader.
- Remove hedging language ("it might be worth considering" → state the recommendation).
- Check that every section earns its place. If a section is one sentence, it probably belongs elsewhere.
- Verify all claims against the research notes. Do not introduce facts that are not in the sources.

### 7. Present to the User

- Share the draft and explain the structure.
- Flag sections where you made judgment calls.
- Highlight open questions or areas where user input is needed.
- Be ready to iterate.

## Principles

- Accuracy over speed. A wrong document is worse than a late one.
- Clarity over completeness. A focused document covering the essentials beats an exhaustive one nobody reads.
- Respect the format. If the user asked for a one-pager, do not write five pages. If they asked for a design doc, do not write a blog post.
- When in doubt about tone, scope, or depth, ask.

## Context Drift Prevention

Writing a document is a multi-step process. Reread this file after every 5-6 tool calls. Reread the research notes before making claims in the draft. See `core/context.md` for the full treatment.
