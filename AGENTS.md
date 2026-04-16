<!--
This file is for students using OpenAI's Codex CLI instead of (or alongside)
Claude Code. The MOOC is taught with Claude Code, but the patterns in this
repo work with any agentic CLI that reads a project context file.
-->

# AGENTS.md

This repo works with OpenAI Codex CLI too.

Codex reads `AGENTS.md` the same way Claude Code reads `CLAUDE.md`. If you
want to use Codex on this repo, you have two options:

1. Symlink it: `ln -s CLAUDE.md AGENTS.md` (then delete this file)
2. Copy it: keep both files in sync by hand

Either works. The symlink is less effort. The copy lets you keep two
slightly different briefings if you want one tone for Claude and another
for Codex.

## One-shot runs

Codex supports a `-p` flag for non-interactive prompts, the same way
Claude Code does:

```
codex exec -p "draft a short brief from the docs in sample-docs/"
```

That's the pattern Module 4 uses for cross-model review — fire the same
prompt at Claude, Codex, and Copilot CLI in parallel and compare what
each one catches.

## Worked example

See `examples/worked-claude-md/CLAUDE.md` for a fully filled-in context
file. The same content drops into `AGENTS.md` without changes.

## More

- Course site: https://mooc.amditis.tech
- Cross-model review walkthrough: `docs/cross-model-review.md`
