# Technology Evaluation

Process for researching and evaluating a technology, library, framework, or tool. Follows the methodology in `methodology.md`.

## When to Use

When deciding between competing options (libraries, frameworks, cloud services, architectural patterns) or evaluating whether to adopt something new.

## Scope Definition

Before researching, answer:

1. What problem does this solve? One sentence.
2. What are the alternatives, including "do nothing" or "build it ourselves"?
3. What are the decision criteria? Common ones:
   - Maturity and stability
   - Community size and activity
   - Documentation quality
   - Performance characteristics
   - Licensing
   - Maintenance burden
   - Team familiarity
   - Integration with existing stack
4. Are there hard constraints? (e.g., must be open source, must run on X, must support Y language)

## Sources to Consult

In rough priority order:

1. Official documentation and changelogs
2. GitHub/repo: stars, issues, commit frequency, last release date
3. Existing usage in your codebase or organization (search internal repos first)
4. Benchmark comparisons (prefer reproducible ones with methodology described)
5. Migration guides and breaking change history
6. Community forums, Stack Overflow, Reddit (for pain points, not endorsements)

## Evaluation Template

For each candidate, record in a dedicated `notes_<candidate>.md` file in the research folder (`thoughts/local/research/<topic>/`):

```
## [Technology Name]

- **What it does**: one sentence
- **Latest version**: X.Y.Z (released YYYY-MM-DD)
- **License**: MIT / Apache 2.0 / etc.
- **Maturity**: experimental / stable / mature / declining
- **Pros**: (list)
- **Cons**: (list)
- **Risks**: (list)
- **Existing usage**: where it is already used, if anywhere
- **Migration cost**: low / medium / high
- **Sources consulted**: (list with links)
```

## Synthesis

After evaluating all candidates:

1. Create a comparison table with the decision criteria as rows.
2. State your recommendation with reasoning.
3. Explicitly state what you are giving up by not choosing the alternatives.
4. Note any reversibility: is this a one-way door or a two-way door?
