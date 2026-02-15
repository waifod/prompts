---
name: research-bug-investigation
description: Debugging, diagnosing, troubleshooting, or investigating bugs and unexpected behavior. Covers reproduction, isolation, evidence gathering, hypothesis testing, and verification.
---

# Bug Investigation

Process for systematically investigating a bug or unexpected behavior. Activate the `research-methodology` skill and follow it during the investigation.

## When to Use

When something is broken and the cause is not obvious. Not for typos or simple fixes where you can see the problem immediately.

## Scope Definition

Before investigating, write down:

1. What is the expected behavior?
2. What is the actual behavior?
3. When did it start? (if known)
4. Is it reproducible? Always / sometimes / once?
5. What changed recently? (deploys, config changes, dependency updates)

## Investigation Process

### 1. Reproduce

Get a reliable reproduction first. Everything else is guessing without one.

- Identify the minimal steps to trigger the bug.
- Note the environment: OS, runtime version, configuration, input data.
- If intermittent, run it multiple times and record the failure rate.

### 2. Isolate

Narrow the problem space systematically.

- Binary search through recent changes (git bisect or manual).
- Remove components until the bug disappears, then add them back.
- Check if the bug exists in other environments (local, staging, production).
- Check if the bug exists with different inputs.

### 3. Gather Evidence

Record in the research folder (`thoughts/local/research/<topic>/`), using per-source files (`notes_<source>.md`):

- Error messages (exact text, not paraphrased)
- Stack traces
- Log output around the time of failure
- Relevant configuration
- Dependency versions

### 4. Form Hypotheses

List possible causes, ranked by likelihood. For each:

- What evidence supports it?
- What evidence contradicts it?
- How would you confirm or rule it out?

Test the most likely hypothesis first. If it does not pan out, move to the next. Do not pursue multiple hypotheses simultaneously.

### 5. Fix and Verify

- Fix the root cause, not the symptom.
- Write a test that fails before the fix and passes after.
- Verify the fix does not break other things.
- Check if the same bug pattern exists elsewhere in the codebase.

## Common Pitfalls

- Fixing the first thing that looks wrong without confirming it is the cause.
- Changing multiple things at once, making it unclear which change fixed it.
- Stopping at "it works now" without understanding why it was broken.
- Not checking whether the bug was introduced by a dependency update.
