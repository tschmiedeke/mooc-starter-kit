---
name: beat-brief
description: Draft a short daily beat briefing from a folder of incoming source documents. Use when the reporter wants a five-bullet summary of the day's material with attribution flags and follow-up actions.
---

# Beat brief

Reads a folder of incoming source material on a beat and produces a short daily briefing for the reporter covering it.

## When to use

- The reporter has a folder of fresh material — minutes, press releases, interview notes, tips — and wants a quick read on what's in it
- A briefing needs to land in the reporter's hands at the start of a shift
- A new reporter is filling in on a beat and needs a one-page orientation to today's material

## What it does

When this skill is loaded, Claude will:

1. Read every file in the source folder the user names (default: `sample-docs/`)
2. Draft a five-bullet briefing in plain news voice. One sentence per bullet. Each bullet cites the file it's drawn from in parentheses.
3. Flag any claim presented as fact that is not attributed to a named source or a primary document
4. End with a "what to follow up" list of concrete reporter actions, each one doable in under 30 minutes

## Output rules

- Sentence case throughout. No Title Case.
- No exclamation points
- Plain news voice — no editorializing, no adjectives like "important" or "critical"
- Five bullets, no more, no fewer
- The follow-up list is concrete: a number to call, a record to pull, a person to find

## Plugin vs project skill

This skill is the plugin-bundled version of the same idea that lives at `.claude/commands/beat-brief.md` in the MOOC starter kit. The two have different shapes on purpose:

- **The slash command** (`.claude/commands/beat-brief.md`) is a one-shot prompt the student runs by typing `/beat-brief`. It only exists inside the starter kit repo.
- **This plugin skill** is loaded automatically whenever the plugin is installed in any project. The student does not have to type a command — Claude picks it up when the description matches what the user is asking for.

The skill format is the right shape when the behavior should travel across projects. The slash command is the right shape when the behavior is tied to one repo's file layout. Use both together: ship the slash command in the project where the file paths are known, ship the skill in a plugin when the behavior is general.

See video B2 in the course for more on the plugin-vs-project-skill distinction.
