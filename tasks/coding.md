# Coding

Rules for performing coding tasks.

## Core Principles

- Do what is asked. Not more, not less.
- Implement the simplest solution that meets all requirements.
- Write clean, idiomatic code following existing conventions.
- Default to immutability. Use mutable state only when it provides a clear benefit.
- Favor functional patterns (pure functions, composition) where they improve clarity. Do not force them where they do not.
- If uncertain about requirements, ask.

## Workflow

### Complexity Check

Before starting, assess the task:

- Simple (single file, clear change, no ambiguity): proceed directly to Plan, Execute, Verify.
- Moderate (multiple files, some unknowns): add a brief research step. Read the relevant code, note findings, then plan.
- Complex (many files, unclear approach, unfamiliar codebase, architectural implications): use the full research/plan/implement workflow from `tasks/problem-resolution.md`. Write artifacts at each phase. Do not skip research.

Skipping research on a complex task leads to wrong approaches, wasted context, and rework. Light research on a simple task costs little. When in doubt, research.

### 1. Plan

- Read relevant files and understand the current implementation.
- Search the codebase for similar patterns.
- Identify all files that need modification.
- Plan the sequence of changes.
- For moderate and complex tasks, write the plan to a file. A plan that exists only in the context window will drift.

### 2. Execute

- Make changes incrementally.
- Run tests after every significant change.
- Check the build before moving on.
- When on macOS, prefer building on the Cloud Desktop via `remote-build`. The Cloud Desktop has more CPU and memory. To detect the platform, check `uname`: `Darwin` means macOS, `Linux` means Cloud Desktop or a personal Linux machine. See `core/tools.md` for `remote-build` usage.

### 3. Verify

- Read command output. Do not assume success.
- Check for unintended side effects.
- Confirm the build is clean, tests pass, and types check.

### 4. Finish

A task is done when:

- All tests pass.
- Build completes without warnings.
- Type checking passes.
- No error suppression patterns introduced.
- Documentation updated.

## Quality

- Treat warnings as errors.
- Never suppress errors without fixing root causes. Forbidden patterns:
  - `@ts-ignore`, `@ts-expect-error`, `eslint-disable`
  - `# type: ignore`, `# noqa`, `# pylint: disable`
  - `@SuppressWarnings`, `#pragma warning disable`
- Prefer composition over inheritance.
- Use language built-ins before reaching for abstractions.
- No speculative generalization. Solve the current problem.

## File Management

- Name files by what they do, not by development state.
- Forbidden suffixes: `-v2`, `-new`, `-old`, `-legacy`, `-temp`, `-backup`, `-enhanced`, `-improved`.
- Search for existing implementations before creating new files.

## Documentation

- Maintain project docs (roadmap, current task, tech stack, codebase summary) in a location appropriate to the project.
- Create them if they do not exist.
- Read them before starting work.
- Update them when things change.

## Testing

- Unit tests (most): fast, focused, 80%+ coverage target.
- Integration tests (some): real dependencies, component interactions.
- E2E tests (few): complete user journeys.
- Each test file runs in isolation.
- Flaky tests get fixed, not ignored.

## Error Messages

Every error message must include:

1. What went wrong.
2. The value that caused it.
3. What was expected.
4. How to fix it.

## Context Drift Prevention

During long tasks, assumptions accumulate and details get lost. To counter this:

- Reread this file after every 5-6 tool calls.
- Reread project documentation before making decisions based on memory.
- If you catch yourself making claims not grounded in the files, stop and verify.

See `core/context.md` for the full treatment: compaction, session boundaries, sub-agent isolation, and phased work.

## Tools

See `core/tools.md` for platform-specific CLI tool preferences.
