# Code Review

Rules for preparing and conducting code reviews.

## Preparing a Code Review

Before submitting:

1. Build and test. The code review should not be the first time anyone runs the code.
2. Self-review the diff. Read it as if someone else wrote it. Catch the obvious stuff yourself.
3. Keep it small. One logical change per review. If you find yourself writing "also" in the description, consider splitting.
4. Write a useful description:
   - What changed and why (not how; the diff shows how)
   - Link to the relevant task or ticket
   - Call out anything non-obvious or risky
   - Note if any part is mechanical/generated vs. hand-written
5. If the change is large or architectural, consider a pre-review conversation. A code review is not the place to discover fundamental disagreement.

## Reviewing

### What to Look For

In priority order:

1. Correctness: Does it do what it claims? Are there edge cases?
2. Safety: Could this break production? Data loss? Security issues?
3. Design: Is the approach reasonable? Is there a simpler way?
4. Maintainability: Will someone understand this in six months?
5. Testing: Are the tests meaningful? Do they test behavior, not implementation?
6. Style: Only if it meaningfully affects readability. Do not bikeshed.

### How to Comment

- Be specific. "This might have a race condition when X happens" beats "looks risky."
- Prefix every comment with a gravity label so the author knows what matters:

  | Label | Meaning | Blocks approval |
  |---|---|---|
  | `[blocker]` | Non-negotiable concern | Yes |
  | `[critical]` | Strong concern | Yes |
  | `[major]` | Concern worth addressing | No |
  | `[minor]` | Recommendation | No |
  | `[nitpicky]` | Mild recommendation | No |

  Mark `[blocker]` and `[critical]` comments as blocking in the review tool. `[major]` should be flagged as blocking to ensure visibility, but does not block approval.
- Ask questions when you do not understand, rather than assuming it is wrong.
- If you suggest a change, explain why. "Use X instead of Y because Z" is useful. "Use X instead of Y" is not.
- Acknowledge good work when appropriate. A simple "nice approach" is sufficient.

### What Not to Do

- Do not rewrite the author's code in comments. Suggest the direction, not the implementation.
- Do not block on style preferences not in the team's style guide.
- Do not approve without reading.
- Do not let a review sit. Review within one business day, or say when you will.

## Responding to Review Feedback

- Address every comment, even if just to acknowledge it.
- If you disagree, explain your reasoning.
- If a discussion stalls, take it offline. The comment thread is not a debate forum. After resolving offline, summarize the outcome back on the review so the decision is recorded.
- After addressing feedback, rebuild and retest before updating the review.
