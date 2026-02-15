# AI Agent Prompts

Reusable prompt documents for AI coding agents. Agent-agnostic: works with Kiro, opencode, Claude Code, Cursor, or anything that accepts markdown context.

## Structure

```
├── core/
│   ├── context.md                # Context window hygiene, compaction, session management
│   ├── amazon-builder.md         # Amazon development context (Brazil, CRUX, etc.)
│   ├── tools.md                  # CLI tool preferences by platform
│   └── style.md                  # Writing style guide
├── research/
│   ├── methodology.md           # Core research methodology: how to gather and synthesize
│   ├── technology-evaluation.md # Evaluating libraries, frameworks, tools
│   ├── bug-investigation.md     # Systematic bug investigation
│   └── design.md                # Research for design docs and architecture proposals
├── tasks/
│   ├── coding.md                # Coding workflow: plan, execute, verify, quality standards
│   ├── cv-update.md             # CV maintenance workflow
│   ├── code-review.md           # Preparing and conducting code reviews
│   ├── document-writing.md      # Writing documents: design docs, proposals, guides
│   ├── mcm-writing.md           # Manual Change Management documents
│   ├── orr-writing.md           # Operational Readiness Reviews
│   └── problem-resolution.md    # Ambiguous problems: research, narrative, plan, agent handoff
└── skills/                      # Agent Skills (SKILL.md) format
    ├── coding/
    ├── research-bug-investigation/
    ├── code-review/
    ├── cv-update/
    ├── research-design/
    ├── document-writing/
    ├── mcm-writing/
    ├── orr-writing/
    ├── problem-resolution/
    ├── research-methodology/
    └── research-technology-evaluation/
```

## How to Use

The plain markdown files in `research/` and `tasks/` are the source of truth. The `skills/` folder packages the same content in the [Agent Skills](https://github.com/agentskills/agentskills) format for tools that support on-demand skill discovery.

### As always-on context

For files you want in every conversation (everything in `core/`), use your tool's always-loaded mechanism:

- **Kiro**: Copy into `.kiro/steering/` (default inclusion mode is always-on)
- **opencode**: Reference in the `instructions` field of `opencode.json`, or paste into `AGENTS.md`
- **Other tools**: Add to system prompt, custom instructions, or equivalent

### As on-demand skills

For task and research files, copy the relevant folders from `skills/` into your tool's skills directory:

- **Kiro**: `~/.kiro/skills/` (global) or `.kiro/skills/` (workspace)
- **opencode**: `~/.config/opencode/skills/` (global) or `.opencode/skills/` (project)
- **Claude Code**: `~/.claude/skills/` (global) or `.claude/skills/` (project)

The agent sees each skill's name and description, then loads the full content when the task is relevant.

### Other options

- **Session context**: Reference files with `@file` or `#file` syntax in chat
- **CLI resources**: Add as `file://` resources in agent config

## Categories

**core/** contains general-purpose files. Load them in most sessions.

**research/** contains the methodology for structured information gathering, plus topic-specific guides. The methodology file is the core; topic files extend it for specific scenarios.

**tasks/** contains workflow guides for specific recurring tasks. Load them when doing that task.

**skills/** contains the same content as `research/` and `tasks/`, packaged as Agent Skills (`SKILL.md` with YAML frontmatter).

## Working Directory

Agents write working artifacts to a `thoughts/` directory in the project root. It has two subdivisions:

- `thoughts/local/` is session-local scratch space: in-progress research, handoff documents, draft plans. Gitignore it.
- `thoughts/shared/` is the permanent record: finalized research, approved plans, execution logs, decision records. Commit it to the repo.

Add to your project's `.gitignore`:

```
thoughts/local/
```

Work starts in `local/` and moves to `shared/` when reviewed or finalized. See `core/context.md` for the full convention, including promotion criteria, handoff procedures, and decision record format.

## Sub-Agents

`core/context.md` defines six specialized sub-agent roles for keeping the main agent's context clean during research-heavy tasks:

| Agent | Purpose |
|---|---|
| code-finder | Locate files and components relevant to a feature |
| code-analyzer | Trace implementation details and data flow |
| pattern-finder | Find similar implementations and conventions |
| knowledge-finder | Discover relevant documents in `thoughts/` and project docs |
| knowledge-analyzer | Deep-read research documents for actionable findings |
| web-researcher | Search the web for external documentation and current data |

These are role descriptions, not tool-specific configurations. Map them to your agent tool's sub-agent mechanism:

- **Kiro**: Use `invokeSubAgent` with a prompt that includes the role name, scope constraints, and allowed operations from the table.
- **Claude Code**: Create agent files in `.claude/agents/` (e.g., `code-finder.md`) containing the role description and tool allowlist.
- **opencode**: Configure sub-agents in `.opencode/agents/` or equivalent, referencing the role constraints.
- **Other tools**: Include the role description in the sub-agent's system prompt or instructions.

## Influences

- [Advanced Context Engineering for Coding Agents](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents) by HumanLayer. The context management and research/plan/implement workflow ideas draw heavily from this.

## Conventions

- All filenames use `kebab-case`
- Documents are agent-agnostic: no tool-specific references
- Each document is self-contained but may reference siblings
