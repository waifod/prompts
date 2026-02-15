# Contributing

Rules for modifying files in this repo. Read `README.md` for structure, installation, and conventions.

## Audience

All markdown files except `README.md` are written for LLM consumption. Use imperative instructions directed at an agent. No human-flavored asides, no metaphors, no second-person narrative framing. `README.md` is the only human-facing file.

## Organization

Each instruction lives in exactly one file. Other files reference it by path. Before adding content, check whether it belongs in the current file or is already covered elsewhere (e.g., research methodology belongs in `research/methodology.md`, not in a task file). If it exists elsewhere, add a cross-reference.

## Source of Truth

Files in `core/`, `research/`, and `tasks/` are canonical. The `skills/` folder contains copies wrapped in YAML frontmatter. Edit the source first, then propagate to the skill copy. Do not edit skill copies directly.

Files in `core/` have no skill copies.

## Editing a File

1. Edit the source file in `core/`, `research/`, or `tasks/`.
2. If the file has a skill copy, replace the content in `skills/<name>/SKILL.md` below the YAML frontmatter (first 4 lines). Do not modify the frontmatter unless the description has changed.
3. Verify the skill copy matches. Skill copies may differ from source files in cross-references (file paths converted to skill activation names); this is expected. Check for unintended differences:

```bash
diff <(tail -n +5 skills/<name>/SKILL.md) <source-file>
```

Acceptable differences: blank line after frontmatter, skill activation references replacing file-path references.

## Adding a File

1. Create the source file in the appropriate folder (`core/`, `research/`, or `tasks/`).
2. If the file belongs to `research/` or `tasks/`, create a skill copy at `skills/<name>/SKILL.md`:

```yaml
---
name: <kebab-case-name>
description: <One sentence. What the skill covers.>
---
```

3. Paste the full source content below the frontmatter.
4. Skill naming convention: research files use a `research-` prefix (e.g., `research-methodology`). Task files use the filename as-is (e.g., `code-review`).
5. Update the structure tree in `README.md`.

## Removing a File

1. Delete the source file.
2. Delete the corresponding `skills/<name>/` folder if it exists.
3. Update `README.md`.
4. Search for stale cross-references and update them:

```bash
grep -rn "<deleted-filename>" --include="*.md"
```

## Renaming a File

1. Rename the source file.
2. Rename the `skills/<name>/` folder. Update the `name` field in the YAML frontmatter to match.
3. Search for the old filename across all `.md` files (source and skill copies) and update every reference.
4. Update `README.md`.

## Cross-References

Source files in `core/`, `research/`, and `tasks/` reference each other by relative path from the repo root (e.g., `research/methodology.md`, `tasks/document-writing.md`).

Skill copies must reference other skills by activation name, not by file path. Use the phrasing "activate the `skill-name` skill" with the exact `name` from the target skill's YAML frontmatter. This ensures the agent activates the skill (loading its full instructions) rather than just reading a file.

When propagating a source file to its skill copy, convert any file-path cross-references to skill activation references. This is an expected difference between source and skill copy.

## Propagating to Installed Copies

After any change, re-copy to the tool's directories. Target paths are documented in `README.md`. For Kiro:

```bash
cp core/*.md ~/.kiro/steering/
cp -r skills/* ~/.kiro/skills/
```

If a file or skill was removed, delete the corresponding installed copy manually.
