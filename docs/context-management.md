# Context management

This is the Module 4 walkthrough for videos D1 and D2. It covers the things you need to do to keep Claude Code sharp on long tasks: watching your context window, setting reasoning effort, compacting on purpose, the 40% rule, sub-agents, and the rewind escape hatch.

If you only remember one thing from this page: **context isn't infinite, and quality drops long before the window is full.**

## Why context management matters

Claude's context window for Sonnet and Opus 4.6 sits at one million tokens. That's an enormous amount of room. It's also a trap.

Quality starts to slip somewhere around 20-30% context usage. Not at 90%. Not at "context full." A conversation that's a quarter of the way through its window can already start repeating itself, dragging in stale facts, or wandering off task. The window is bigger than it used to be, but the useful zone inside that window hasn't really grown.

That's the framing for everything else on this page. You're not managing "running out of room." You're managing "staying in the sharp part of the window."

## `/context` — see what's in your window

The `/context` command shows you a breakdown of what's currently loaded:

- System prompt
- Custom agents
- Memory files (`CLAUDE.md`, `MEMORY.md`, `LESSONS.md`, anything else you've pointed at)
- Skills the model has loaded
- Accumulated message history
- Free space
- Auto-compact buffer (Claude reserves space at the top of the window for the eventual auto-compaction)

Run it any time you want a sanity check. If your CLAUDE.md is eating 40k tokens before you've sent a single message, that's worth knowing.

[screenshot: /context output showing the breakdown]

You can also put a live context percentage indicator in your status line so you don't have to keep running the command. Mine shows the current percent at the bottom of the terminal at all times. When it ticks past 30%, I start thinking about whether to compact or start fresh.

## `/effort` — set reasoning depth

Claude can spend more or less effort on each turn. The `/effort` command sets it for the current session:

- `low` — fast, minimal reasoning
- `medium` — default
- `high` — more thinking
- `max` — heavy reasoning, longer waits, more tokens
- `auto` — let the model decide

Higher effort burns more tokens. A lot more, sometimes. Don't park it on `max` and forget. Set it intentionally for the task: `max` for a tricky architectural decision, `low` for "rename this variable everywhere."

This setting only applies to the current session. New session = back to default.

[screenshot: /effort menu]

## `/compact` — make it proactive, not reactive

`/compact` clears your conversation history but keeps a summary. The model still remembers what it was doing — it just no longer carries every word of the back-and-forth that got it there. A conversation sitting at 5% context usage will typically drop to around 3% after a compact. That doesn't sound like much. The point is the **shape** of what's left: a clean summary instead of a mountain of raw turns.

The default trigger for compaction is auto-compact: Claude runs it for you when the window is nearly full. By that point you're already in the degraded zone. Don't wait. Compact on purpose, before the model starts struggling.

### Custom compaction with a hint

You can tell `/compact` what to preserve in the summary:

```
/compact VLC information and streaming configuration
```

That hint biases the summary toward the topic you care about. If you've spent the last hour debugging a streaming setup and you don't want the summary to forget the port numbers and config flags, say so. Without the hint, the model picks what it thinks is important. With the hint, you get to weigh in.

[screenshot: /compact in progress with custom hint]

## The 40% rule

Cap your conversations at 40% of context window. Once you hit that, you have three choices:

1. **Compact.** Summarize what's there and keep going.
2. **Dump.** Save the conversation transcript somewhere and start fresh.
3. **Start fresh.** Open a new session in the same project.

I prefer option 3 most of the time. Compaction is a tool, not a save point. Every compaction loses something. The cleanest reset is a fresh session.

The 40% number isn't a law of nature. It's a heuristic. What it really says is: "Don't push it. Long before the window is full, your output quality will be."

### Signs you're in the degradation zone (30-40%)

- Claude repeats itself across turns
- Pulls threads from unrelated parts of the conversation
- References stale info (e.g., a file you already deleted)
- Drifts off the current task
- Suggests things you already explicitly ruled out three messages ago

If you see any of these, stop adding to the conversation. Compact or restart.

## One conversation per task as a diagnostic

This one's the meta-rule. Treat every task as its own conversation. If you can't go from the end of one conversation to a clean new conversation in the same project and get the same quality of work, **something is missing from your project context.**

Maybe your CLAUDE.md is underspecified. Maybe you've been making decisions in chat that should have been written into a memory file. Maybe a piece of state lives only in the session and not in any committed file.

Starting fresh is a test of your context hygiene. If it passes, your project is well-structured. If it fails, you have homework: figure out what the new session is missing and write it down so the next fresh session starts at full speed.

This is the most useful framing in Module 4 and the easiest to skip. Don't skip it.

## Sub-agents — fresh windows on tap

Sub-agents (the Task tool) get **fresh context windows** every time you spin one up. Brand new. That's the killer feature.

You can run an expensive research task — "read these 80 files and summarize the patterns" — against a fresh 1M token window without spending a single token on your main conversation. The sub-agent does the work in its own sandbox and reports back with a summary. Your main conversation stays sharp.

Two rules for working with sub-agents:

### 1. Narrow tasks only

A sub-agent only knows what you tell it. It doesn't have access to your CLAUDE.md, your memory files, or your conversation history (unless you pass them in explicitly). Give it exactly one job, with all the context it needs to do that job, and nothing else.

"Summarize this folder" is a fine sub-agent task.

"Refactor my codebase to use the new pattern we were just discussing" is a terrible sub-agent task. The sub-agent doesn't know what pattern you were just discussing. It will guess, badly.

### 2. Watch out for agent telephone

Even when a sub-agent does its job well, the report back can mishandle small details. The main agent then accepts the summary without realizing those details got mangled. This is the "agent telephone" risk.

Don't auto-trust sub-agent results. Spot-check. If the sub-agent says "I found 12 files matching the pattern," and the answer matters, run a quick check yourself before building on it.

[screenshot: sub-agent kicking off a research task]

## Double-escape rewind

Hit Escape twice in Claude Code and you'll get a rewind menu. You can jump back to any earlier point in the current conversation. Useful when you realize you took a wrong turn ten messages ago and want to undo without losing everything in between.

**Catch:** once you've compacted, you can't rewind past the compaction point. The original messages are gone — only the summary remains. So if you're about to make a risky move and you might want to undo it, don't compact right before.

## Transcripts are persisted

Every conversation in Claude Code is saved as a JSONL file on your local machine. The transcripts persist after the session ends. You can open `Ctrl+O` to view the full transcript of the current conversation, including any compaction summaries.

This is convenient for going back and finding "what was that command Claude suggested yesterday?" It's also a security note: **don't dump secrets in your terminal.** API keys, passwords, access tokens — if you paste them into Claude Code, they end up in a file on your disk. Use environment variables. Use `pass` or another secret manager. Don't paste raw secrets.

## Try it yourself

1. Open a project of yours and run `claude` from the project root.
2. Run `/context` and read the breakdown. Screenshot it. Notice how much your CLAUDE.md, memory files, and skills are using before you've done anything.
3. Send a few messages — ask Claude to explore a few files, summarize them, propose a change.
4. Run `/context` again. See how much the conversation has added.
5. Run `/compact` with a hint about what to preserve. Run `/context` once more. Notice the drop.
6. Hit Escape twice. Look at the rewind menu. Pick an earlier point and jump back.
7. Now close the session and start a new one in the same project. Try to pick up where you left off using only what's in the project files. Where does the new session struggle? That gap is what should go into your CLAUDE.md, MEMORY.md, or LESSONS.md.

That last step is the whole module in one exercise. Do it once and you'll feel the difference.
