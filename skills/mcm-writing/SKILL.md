---
name: mcm-writing
description: Writing, reviewing, checking, or updating a Manual Change Management (MCM) document. Covers research, drafting, and review process.
---

# MCM Writing

Process for preparing a Manual Change Management (MCM) document. MCM templates evolve; this file covers the process, not the template.

## Before Writing

1. Activate the `research-methodology` skill and follow it to understand the change: what is being modified, why, what could go wrong.
2. Fetch the current MCM template and documentation. Start with the [MCM User Guide](https://w.amazon.com/bin/view/ChangeManagement/MCM/Website/UserGuides/UserGuide) and the [MCM tool](https://mcm.amazon.com). Do not rely on memory or cached versions.
3. Review recent MCMs for the same service or team to understand local conventions.

## Writing

Reread this file before starting the draft. The research phase may have pushed these guidelines out of your working context.

Activate the `document-writing` skill and follow it for general drafting discipline. In addition:

- Fill in every section of the template. If a section does not apply, say so explicitly rather than leaving it blank.
- The rollback plan must be concrete and tested. "Revert the change" is not a rollback plan unless you specify exactly how.
- Validation steps should be verifiable by someone who did not write the MCM.
- Be honest about blast radius. Understating risk does not reduce it.

## Review

- Have someone who will be oncall during the change review the MCM.
- Verify the rollback plan is actually executable, not just plausible.
- Confirm approval requirements for the change's risk level.
