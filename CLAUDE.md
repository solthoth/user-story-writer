# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repo contains a Claude Code skill that generates user stories in the **3Cs format** (Card, Conversation, Confirmation). When installed, it registers a skill that Claude Code loads and triggers on user-invocable commands.

## Skill Architecture

Claude Code skills follow a standard layout:

```
3cs-story-skill/
└── SKILL.md          ← required entry point (YAML frontmatter + Markdown instructions)
```

`SKILL.md` has two parts:
- **YAML frontmatter** — `name`, `description` (drives trigger matching), and optional `trigger` (slash command alias).
- **Markdown body** — instructions Claude follows when the skill is invoked. This is where the 3Cs logic lives.

The `description` field is the primary trigger mechanism. It must clearly state when to use the skill so Claude recognizes relevant user prompts. Err on the side of being "pushy" — list synonyms and related contexts so the skill doesn't undertrigger.

## 3Cs Format Reference

- **Card** — one-sentence story in the form: _"As a [persona], I want [goal] so that [benefit]."_
- **Conversation** — the discussion/context behind the story: acceptance criteria, edge cases, notes.
- **Confirmation** — testable conditions that prove the story is done (Given/When/Then or a checklist).

## Development Workflow

No build step is required — `SKILL.md` is plain Markdown. To iterate:

1. Edit `SKILL.md`.
2. Install/reload the skill in Claude Code (`/skills install` or by symlinking into `~/.claude/skills/`).
3. Test by invoking the trigger phrase in a Claude Code session.
4. Use the `skill-creator` skill (`~/.claude/skills/skill-creator/SKILL.md`) for guided iteration, eval generation, and description optimization.

## Installation

Skills are loaded from `~/.claude/skills/`. To make this skill available locally, symlink or copy this directory there:

```bash
ln -s /path/to/3cs-story-skill ~/.claude/skills/3cs-story-skill
```
