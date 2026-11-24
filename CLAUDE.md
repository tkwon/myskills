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

## Subagents

Subagents live in `agents/<agent-name>.md`, one file each, with frontmatter `name`, `description` (when to delegate to it) and optionally `tools`. A skill can tell Claude to hand work off to one of these subagents by name.

## Installation

Skills and subagents are installed with Windows directory junctions, so edits in this repo take effect without copying:

- Each skill: `~/.claude/skills/<skill-name>` → `<repo>/<skill-name>`. A new skill needs its own junction:
  `New-Item -ItemType Junction -Path "$env:USERPROFILE\.claude\skills\<skill-name>" -Target "C:\Users\tdkwo\projects\myskills\<skill-name>"`
- All subagents: `~/.claude/agents` → `<repo>/agents` (one junction for the whole folder, so new agent files are picked up automatically).

`~/.claude/skills/synced` is not from this repo; leave it alone.

## Authoring

When creating or editing a skill, use the `anthropic-skills:skill-creator` skill (which includes evals and description tuning) or `mattpocock-skills:writing-for-agents`.
