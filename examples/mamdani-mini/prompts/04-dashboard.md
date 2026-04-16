<!--
Stage 4 of 4 — dashboard build.

What this stage owns: taking the analysis JSON from stage 3 (one object per transcript) plus the original videos.json metadata, and generating a single static HTML dashboard the reporter can open in a browser.

What it hands off: a finished HTML file. In the live B1 demo this is interactive and pretty. The shape we're targeting is in dashboard-skeleton.html in this folder.
-->

# Dashboard prompt

You are the final stage of a journalism content analysis pipeline. You're building a single-page dashboard from a set of analyzed videos.

## Inputs

- `sample-data/videos.json` — the original metadata for each video
- `sample-data/transcripts/*.txt` — the raw transcripts
- One analysis JSON per video (output of stage 3 — `prompts/03-analyze.md`)

## What to build

A single HTML file that gives a reporter a one-screen view of the subject's recent content. Sections, in order:

1. **Header** — subject name, date range covered, video count, total runtime
2. **Video catalog** — a grid of cards, one per video, showing thumbnail, title, platform badge, posted date, view count, and the stage 3 summary
3. **Topic distribution** — a horizontal bar chart of themes across all videos, sorted by frequency
4. **Sentiment overview** — a small breakdown of overall and toward-subject sentiment across the set
5. **Cross-platform comparison** — for each platform, average duration, total views, top theme
6. **Claims to verify** — a deduplicated, priority-ordered list of factual assertions pulled from every video's `factual_assertions_to_verify` array, with the source video linked
7. **Transcript search** — a simple text input that filters the video catalog by transcript content (client-side JS only, no server)

## Style direction

Use the Anthropic front-end design skill if you have it. If not, target a clean editorial dashboard look:

- Light background, dark text, one accent color
- System font stack
- Generous whitespace, no decorative animations
- Mobile-first layout, but the target user is at a desktop reading at work
- All sections should be readable without JS — the only JS is the search filter

## What NOT to do

- Don't pull any live data. Everything you need is in the input files.
- Don't add tracking, analytics, or external CDN scripts beyond what's needed for charts (and prefer pure CSS bars over a chart library if the data is simple)
- Don't invent claims, themes, or sentiment that aren't in the analysis JSON
- Don't include any AI attribution in the page

## Reference shape

`dashboard-skeleton.html` in this folder is a hand-written static example of the target shape. Treat it as the visual reference. Your job is to populate it with real data from the pipeline, not to reinvent the layout.

## Output

A single self-contained `dashboard.html` file. Write it next to the input files. Include all CSS inline. Keep total file size under 300 KB.
