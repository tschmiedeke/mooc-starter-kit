# Hooks

Hooks let Claude Code run a shell command at specific points in a session — before a tool runs, after a tool runs, when the session starts, when it stops. The hook can warn, log, or block.

This folder ships with one example hook in `hooks.json`: a `PreToolUse` guardrail that fires whenever Claude is about to run a Bash command. If the command contains `rm -rf /`, `DROP TABLE`, or `git push --force`, the hook prints a warning to stderr and lets the command continue.

## The one-way door pattern

This is the "one-way door" pattern Joe walks through in video B1. The idea: most commands are reversible. You can `git revert`, restore from a backup, undo a typo. A few commands are not. Once you `rm -rf` the wrong directory or force-push over someone elses work, there is no undo. Those are one-way doors.

The hook does not block. It just makes you stop and read the command before pressing enter. That is usually enough.

## How to extend it

Add more patterns to the regex in `hooks.json`. Common candidates:

- `truncate table` — destructive SQL
- `DELETE FROM .* WHERE 1=1` — unbounded delete
- `chmod -R 777` — broad permission change
- `aws s3 rb` — bucket removal

You can also add new hook entries for other events. The full event list is in the Claude Code docs:

- `PreToolUse` — fires before a tool runs (can block)
- `PostToolUse` — fires after a tool runs
- `SessionStart` — fires when a session opens
- `Stop` — fires when the session ends
- `UserPromptSubmit` — fires when the user submits a prompt

## See also

- Video B1 in the course covers the one-way door concept in more depth
- `docs/context-management.md` covers related guardrails like `/effort` and the 40% rule
