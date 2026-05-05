Skills live as self-contained markdown files under `commands/`. Each file is one Claude Code slash command.

## File format

Every skill file must have YAML frontmatter:

```md
---
name: skill-name
description: One-line description shown in the skill picker. Describe what it does and when to trigger it.
---

Skill content here.
```

Optional frontmatter field:
- `disable-model-invocation: true` — the skill's content is injected as a user message rather than invoking the model directly. Use for skills that set up context or configure other skills.

## Deploying skills

Copy the files from `commands/` to `~/.claude/commands/` to make them available globally across all projects:

```bash
cp commands/*.md ~/.claude/commands/
```

Or symlink the folder for automatic sync:

```bash
ln -s /path/to/AI-engineering/commands ~/.claude/commands
```

## Adding or editing a skill

1. Edit or create the `.md` file in `commands/`
2. Copy to `~/.claude/commands/` (or rely on the symlink)
3. Restart Claude Code if the skill doesn't appear

## Rules

- Each skill is a **single self-contained file** — no references to other local files. Inline any supporting content at the bottom of the skill file.
- The `name` field in frontmatter determines the slash command: `name: grill-me` → `/grill-me`
- Keep descriptions specific enough that Claude knows when to auto-trigger the skill
