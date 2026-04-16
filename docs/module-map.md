# Module map

This kit pairs with the four-module course "Advanced prompt engineering for journalists." The course has 10 teaching videos plus 2 bonus interviews and 1 final project. Watch the videos at [mooc.amditis.tech](https://mooc.amditis.tech). This file tells you which files in the repo line up with which video, so you can jump straight to the thing you're trying to learn.

If you're new, start with Module 1, fork the repo, and work through the files in order. If you're already deep in a module, search this table for the file you need.

## Modules at a glance

- **Module 1** — Context engineering basics (videos A1, A2)
- **Module 2** — Skills, commands, hooks, plugins (videos B1, B2)
- **Module 3** — Pipelines, scripts, GitHub Actions (videos C1, C2)
- **Module 4** — Context management, sub-agents, cross-model review, tool selection (videos D1, D2, D3, D4)
- **Final project** — Build something on your beat using anything from the kit

## File and folder index

| File / folder | Module | Video | What it's for |
|---|---|---|---|
| `CLAUDE.md` | 1 | A1 | The project context scaffold. Edit this first. |
| `examples/worked-claude-md/CLAUDE.md` | 1 | A1 | A filled-in CLAUDE.md for a fictional Greenfield city council beat. Use it as a model. |
| `MEMORY.md` | 1 | A2 | Index of the four memory types (user, feedback, project, reference). |
| `LESSONS.md` | 1 | A2 | Rolling log where corrections become rules. The "remove a line" pattern. |
| `AGENTS.md` | 1 | A1 | Same idea as CLAUDE.md, for OpenAI Codex users. |
| `GEMINI.md` | 1 | A1 | Same idea, for Gemini CLI users. |
| `sample-docs/` | 1 | A1, A2 | The Greenfield beat sample documents. Used in exercises across modules. |
| `skills/` | 2 | B1 | Real Claude Code skills with YAML frontmatter, not markdown docs. |
| `skills/newsroom-style/SKILL.md` | 2 | B1 | A full skill: AP style enforcement on draft writing. |
| `skills/first-skill/SKILL.md` | 2 | B1 | Minimal "build your first skill" template. |
| `.claude/commands/` | 2 | B1 | Slash commands you can run inside Claude Code. |
| `.claude/commands/beat-brief.md` | 2 | B1 | `/beat-brief` — drafts a daily briefing from `sample-docs/`. |
| `.claude/commands/cross-review.md` | 2, 4 | B1, D3 | `/cross-review` — runs Copilot CLI and Codex against your current diff. |
| `.claude/commands/verify-claim.md` | 2 | B1 | `/verify-claim` — walks the SIFT method on a claim. |
| `.claude/hooks.json` | 2 | B1 | One-way-door guardrail. Warns before destructive actions. |
| `plugin/` | 2 | B2 | Minimal plugin skeleton showing the plugin-vs-project shape. |
| `plugin/plugin.json` | 2 | B2 | Plugin manifest. |
| `plugin/skills/beat-brief/SKILL.md` | 2 | B2 | A skill packaged inside a plugin. |
| `scripts/pipeline/` | 3 | C1 | The fetch → clean → process → save pattern, one stage per file. |
| `scripts/pipeline/01-fetch.sh` | 3 | C1 | Stage 1. Owns input. Hands clean text to stage 2. |
| `scripts/pipeline/02-clean.sh` | 3 | C1 | Stage 2. Strips HTML, normalizes whitespace. |
| `scripts/pipeline/03-process.sh` | 3 | C1 | Stage 3. Calls `claude -p` with a beat-specific prompt. |
| `scripts/pipeline/04-save.sh` | 3 | C1 | Stage 4. Writes timestamped output. |
| `scripts/legacy/` | 3 | C1 | The "before" versions of the scripts, kept for reference. |
| `.github/workflows/weekly-digest.yml` | 3 | C2 | Hybrid cloud-detect / local-process GitHub Action. |
| `examples/mamdani-mini/` | 3 | C1 | The shape of video B1's pipeline demo, with synthetic data. |
| `docs/module-map.md` | — | — | This file. |
| `docs/context-management.md` | 4 | D1, D2 | `/effort`, `/context`, `/compact`, the 40% rule, sub-agents, rewind. |
| `docs/cross-model-review.md` | 4 | D3 | Calling Copilot CLI and Codex from inside Claude Code with `-p`. |
| `docs/four-questions.md` | 4 | D4 | The tool-selection framework. |
| `examples/rag-archive/` | — | — | Optional advanced. Local RAG over your own docs if you want to try it. |
| `mcp-configs/` | — | — | Optional advanced. MCP is still useful but no longer the spine of Module 4. |
| `docs/superpowers/specs/` | — | — | Design docs for the kit itself. Not student-facing. |

## How to use this map

If you're stuck on a video, pull up the corresponding row, open that file, and read it alongside the video. Every file has a header comment or README explaining what it owns.

If you're hunting for a specific feature ("where does Joe show hooks?"), search the table for the keyword. Every video has at least one file in the repo that goes with it.
