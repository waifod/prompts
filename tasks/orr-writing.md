# ORR Writing

Process for preparing an Operational Readiness Review (ORR). ORR checklists evolve; this file covers the process, not the checklist.

## Before Writing

1. Follow `research/methodology.md` to understand the service's operational posture: what is in place, what is missing, what changed since the last review.
2. Fetch the current ORR checklist and documentation. Start with the [ORR wiki](https://w.amazon.com/bin/view/AWS/OperationalReadiness/OperationalReadinessReview) and the [ORR tool](https://orr.reflect.aws.dev/). Do not rely on memory or cached versions.
3. Review recent ORRs for the same service or team to understand what was flagged and what was resolved.

## Writing

Reread this file before starting the draft. The research phase may have pushed these guidelines out of your working context.

Follow `tasks/document-writing.md` for general drafting discipline. In addition:

- Address every item in the checklist. If something is not applicable, explain why.
- For each gap, provide a remediation plan with an owner and a timeline.
- Be specific about operational evidence: link to dashboards, alarms, runbooks, and load test results rather than asserting they exist.
- If a requirement is partially met, say so. "We have alarms but no runbook for this failure mode" is more useful than "monitoring: done."

## Review

- Walk through the ORR with the oncall team, not just the development team.
- Verify that linked resources (dashboards, runbooks, alarms) actually exist and are current.
- Confirm that remediation items have owners who have acknowledged them.
