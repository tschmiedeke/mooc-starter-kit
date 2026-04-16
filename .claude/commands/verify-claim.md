---
description: Walk a claim through the SIFT method (Stop, Investigate, Find better coverage, Trace)
argument-hint: <the claim to verify>
---

<!--
This command runs the SIFT method on a claim the user passes in.

  Usage: /verify-claim The mayor said the new park will cost $2 million.

SIFT is Mike Caulfield's four-move framework for evaluating a claim:
  S — Stop
  I — Investigate the source
  F — Find better coverage
  T — Trace the claim back to the original context

For a worked example, the file sample-docs/viral-claim-example.md in this
repo is a good test fixture. Try running this command against a claim from
that file.
-->

# Verify claim

The claim to verify is: **$ARGUMENTS**

If `$ARGUMENTS` is empty, ask the user to paste the claim and stop. Otherwise, walk through the SIFT method on it.

## Step 1: Stop

Before doing anything, name your initial reaction to the claim in one sentence. Are you inclined to believe it? Why? Flag any emotional pull. The point of this step is to slow down before doing the work.

## Step 2: Break the claim into testable sub-assertions

Most claims that look simple are actually three or four claims stacked together. Split this one into its smallest checkable parts. Number them.

Example: "The mayor said the new park will cost $2 million" contains at least:
1. There is a new park (or proposal for one)
2. The mayor made a public statement about it
3. The dollar figure attributed is $2 million
4. That figure is the project's actual cost

## Step 3: Investigate the source

For each sub-assertion, identify what the original source would be. A government budget document? A council vote record? A press release? A reporter's quote? Note the type of source and whether it is a primary document or someone's summary of one.

## Step 4: Find better coverage

For each sub-assertion, search for independent reporting or primary documents that confirm or contradict it. Note any sources that disagree with each other — disagreement is a signal to dig deeper.

## Step 5: Trace

Trace each sub-assertion back to its earliest verifiable origin. Quotes get distorted as they travel. Numbers get rounded. Context gets stripped. Where did this claim actually start, and does the original say what later versions say it says?

## Step 6: Confidence scoring

For each numbered sub-assertion, rate confidence on a 1 to 5 scale:

- **5** — Confirmed by primary document or multiple independent sources
- **4** — Confirmed by one reliable secondary source
- **3** — Plausible but not yet confirmed
- **2** — Contradicted by at least one source
- **1** — Likely false or fabricated

## Step 7: Verdict

End with a one-paragraph verdict. Options:

- **Verified** — all sub-assertions scored 4 or 5
- **Partially verified** — some sub-assertions hold, others do not (specify which)
- **Unverified** — not enough evidence either way
- **False** — at least one sub-assertion contradicted by a reliable source

If the claim is unverified or false, suggest the next concrete reporting step the user could take.

For a test fixture to try this on, see `sample-docs/viral-claim-example.md`.
