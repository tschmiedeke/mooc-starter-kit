# The four questions

This is the Module 4 walkthrough for video D4. It's a tool-selection framework for picking which AI agent or model to throw at a given task. Use it instead of the usual feature comparison.

## Why feature comparisons go stale

Anything I write about "Claude vs. ChatGPT vs. Gemini in 2026" will be wrong by the time you read it. Models change in months. Pricing changes. Context windows change. The chart you bookmarked last quarter is already misleading.

What doesn't change is the questions you should ask before picking a tool. The questions outlast any specific model. That's what this page is for.

There are four of them.

## Question 1: What is the task, and what does a good outcome look like?

Start here. Not with the tool. With the work.

What are you actually trying to do? "Write a story" isn't enough. Are you summarizing a 90-minute meeting transcript into three paragraphs? Are you drafting a 1,200-word feature from scratch? Are you fact-checking 40 quotes against source documents? Each of those is a different job and a different model fits each one differently.

Then: what does "done well" look like? Be concrete. "A clean draft" is not concrete. "A 700-word piece in AP style with three named sources, no quotes from billionaires, and a clear nut graf in the second paragraph" is concrete. If you can't describe the good outcome, you can't pick a tool to produce it, and you can't tell whether the tool succeeded.

This question alone kills half of the bad tool choices. You'd be surprised how often "I need an AI for this" turns out to mean "I haven't decided what I'm trying to do yet."

## Question 2: How much context does it need?

Think of the model like a new coworker you're onboarding for one specific task. How much does a smart-but-fresh person need to know to do this job well? That's how much context you need to give the model.

Three categories:

- **Almost none.** "Translate this paragraph into Spanish." The model brings everything it needs. You hand it the paragraph and walk away.
- **Some.** "Draft a story from these notes in our house style." The model needs the notes, the style guide, and maybe two or three example stories. A small amount of project context.
- **A lot.** "Take this beat I've been covering for three years and find me three angles I haven't written yet." The model needs the institutional knowledge, the pattern of what you've already published, and the map of who matters on this beat. That's a meaningful chunk of context.

Why this matters for tool choice: some tools are better at carrying lots of context than others. Claude Code with a CLAUDE.md and committed memory files holds project context across sessions. A bare ChatGPT window doesn't. If your task is in the "a lot" category, you want a tool that can hold the context without you reloading it every conversation.

You can also fail in the other direction. Drowning a fresh model in 80 pages of background it doesn't need will degrade the answer. Too much context is its own bug. Pick what's needed, no more.

## Question 3: Does the agent need access to tools?

By "tools" I mean the things the agent can do beyond reading and writing text:

- Web scraping (Firecrawl, Playwright)
- Spreadsheets (Airtable, Google Sheets)
- Video and audio (yt-dlp, ffmpeg, Whisper)
- Databases (SQLite, Postgres)
- The shell itself

If your task is "summarize this PDF I'm pasting in," no tools needed. Any chat interface works.

If your task is "find every council meeting video from the last six months, transcribe them, and pull out budget mentions," you need yt-dlp, you need a transcription model, you probably need a spreadsheet to track results. You need a tool that can actually call those tools — Claude Code, OpenAI Codex CLI, or similar. A ChatGPT browser tab isn't going to cut it.

The split is roughly:

- **No tools needed** → any text interface works. Cheapest tool wins.
- **A few tools needed** → use a CLI agent that can run shell commands.
- **Many tools needed** → use a CLI agent with skills, plugins, or MCP servers configured for the specific tools you need.

This question is where MCP comes back into the picture. MCP is no longer the spine of Module 4, but it's still the right answer when you need a specific external service wired in cleanly. Use it where it earns its place.

## Question 4: How cost-sensitive are you?

Two kinds of cost:

- **Token budget.** Big context windows and high-effort reasoning burn tokens. If you're running the same task 200 times in a loop, the per-run cost matters.
- **Real-money budget.** Subscriptions vs. per-call API billing. Are you on Claude Pro for $20/month or paying API rates per token? Are you using GitHub Copilot included with your education plan or paying out of pocket?

A task that's free under one pricing model might cost real money under another. A long-running pipeline that's fine on a Claude Pro subscription might run you a hundred dollars on metered API calls.

Sometimes "cost-sensitive" means "I will pay anything for the right answer, this is for an important investigation." Sometimes it means "I want to do this 50 times this week and it has to be cheap." The question isn't only "how much does it cost?" — it's "how much does it cost relative to how much I care about the result?"

## Worked example: summarize 40 council meeting transcripts

1. **Task:** Read 40 transcripts (each ~10k words) and produce a one-paragraph summary of each that captures votes taken, dollar amounts mentioned, and any sharp disagreements.
2. **Context needed:** Some. The model needs to know what to extract (your spec) and the format you want back. It does not need years of beat history.
3. **Tools needed:** A few. File reading, maybe a spreadsheet to collect results. No web scraping, no audio.
4. **Cost:** 40 runs is enough that token cost matters. A subscription plan is much better than per-call API billing.

Tool fit: a CLI agent on a subscription plan, with a small skill or slash command that defines the extraction spec, looped over the 40 files. Claude Code with a `/extract-summary` command would fit. So would Codex CLI. Don't pay API rates if you don't have to.

## Worked example: find all mentions of my beat in a year of news archives

1. **Task:** Search a year of online news (your own archive plus competitors) for every mention of three named people on your beat. Output a list of dates, headlines, and links.
2. **Context needed:** Some. The model needs to know who the three people are, what counts as a real mention vs. a passing reference, and what beat you cover.
3. **Tools needed:** Many. Web search, web scraping, maybe an archive search API. This is not a "drop a PDF in chat" task.
4. **Cost:** Probably a one-shot job, not a loop. Real-money cost is fine if it's small. Token cost is small.

Tool fit: a CLI agent with web tools wired in. Claude Code with Firecrawl plus a search MCP server. Or a standalone agent like Perplexity for the search step plus Claude Code for the synthesis. The key is "many tools needed" — a chat interface alone won't do it.

## Minimum viable effectiveness

You should have at least one tool you trust for any category of task you do regularly. Maybe two. Not eight.

The point isn't to chase every new tool. The point is that when something really matters, you have a fallback. If your usual tool is down, or it's the wrong fit for this particular task, or the answer it gave you smells wrong, you have somewhere else to go. That's "minimum viable effectiveness": one trusted primary, one trusted backup, per task category.

Try more than one tool when picking your primary. Don't get loyal. You picked the first one because you'd heard of it, not because you'd compared it to anything. Spend a week testing two or three on the same task and you'll often find the loyalty was misplaced.

## The editorial judgment note

Joe says it this way in the video, and it bears repeating in plain English:

When anyone can produce passable text at scale for $20 a month, the thing that separates good work from slop is human judgment. The decisions about what to include, what to leave out, what to verify, what to push back on, what to actually publish — those don't come from the tool. They come from you.

If you don't care enough to make the work yourself, or at least to read it carefully and shape it before it goes out, nobody on the receiving end is going to care enough to take it seriously. That's true for stories, emails, code, and everything in between.

The four questions help you pick a tool. They don't replace the judgment about whether the work is any good. That part is still your job.
