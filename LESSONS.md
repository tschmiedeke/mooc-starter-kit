<!--
This is your lessons log. It's a Joe-specific pattern from video A2 —
not a built-in Claude Code feature, just a discipline that pays off.

The idea:

  Every time you correct Claude on something, write the correction
  down here as a rule. Date it. Add a one-line context note so future-
  you remembers why the rule exists.

  Then reference this file from CLAUDE.md so it gets pulled in every
  session:

    "Before drafting any schedule or dated content, check LESSONS.md."

  Over time this file becomes the most opinionated, most specific
  document in your repo. It's where Claude learns your taste — not
  from a generic style guide, but from the specific places it has
  burned you.

Format for each entry:

  ## YYYY-MM-DD — short rule title

  **Context:** one or two sentences about what happened.

  **Rule:** the actual rule, written so a fresh agent could follow it
  without having been there for the original mistake.

  **Why this matters:** optional, but useful when the rule is non-
  obvious. Future-you will thank you.

Keep it tight. If a lesson stops applying, delete it. This file is a
working document, not an archive.
-->

# LESSONS.md

## 2026-03-10 — Always double-check dates against a real calendar

**Context:** I asked Claude to build a weekly schedule and it assumed March 10 was a Monday. It was a Tuesday.

**Rule:** Before committing any date to a published schedule, run `python3 -c "import datetime; print(datetime.date(YEAR, MONTH, DAY).strftime('%A'))"` to verify the day of the week.

**Why this matters:** Model training data is biased toward certain calendar years and will confidently produce wrong weekdays. The model never says "I'm not sure" about a date — it just guesses.

<!--
Your lessons go below this line. Add a new section every time the desk
catches something or you spot the model making the same mistake twice.
-->
