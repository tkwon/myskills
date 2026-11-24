# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repo is a personal collection of Claude Code skills. There is no build, lint or test tooling.

## Skill layout

Each skill is its own top-level directory containing a `SKILL.md`:

```
<skill-name>/
  SKILL.md        # required: YAML frontmatter + instructions
  scripts/        # optional: helper scripts the skill tells Claude to run
  references/     # optional: longer docs loaded only when the skill needs them
  assets/         # optional: templates or other files the skill uses as output
```

`SKILL.md` frontmatter:

```yaml
---
name: <skill-name>          # kebab-case, matches the directory name
description: <what it does and when to use it>
---
```

The `description` is the only part Claude sees before deciding to load a skill. Put the trigger conditions there (what the user says or is doing), not in the body.

Keep `SKILL.md` focused and move long reference material into `references/`. Files there are read on demand, so they don't take up context until needed.

## Authoring

When creating or editing a skill, use the `anthropic-skills:skill-creator` skill (which includes evals and description tuning) or `mattpocock-skills:writing-for-agents`.
