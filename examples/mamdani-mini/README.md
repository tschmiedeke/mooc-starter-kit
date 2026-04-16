# mamdani-mini — pedagogical pipeline example

This folder is a scaled-down, no-scrape version of the social media pipeline Joe demos in video B1 of the MOOC.

In the live demo, the pipeline pulls the 15 most recent videos from a public figure's Twitter, TikTok, YouTube, Instagram, and Facebook accounts; transcribes them with Whisper turbo; runs OCR on extracted frames; and builds an interactive dashboard for cross-platform content analysis.

This folder strips that down to its shape. Everything here is synthetic:

- The "videos" are five fake entries about a fictional local council member
- The transcripts were hand-written, not produced from real audio
- The dashboard is a static HTML skeleton, not a generated page
- No URL in `videos.json` resolves to anything real
- No API keys or scraping tools are needed to read this folder

The point is to see the SHAPE of a fetch → clean → process → save pipeline without any live scraping or any real person's content. For the runnable version with real data, see video B1.

## The fictional subject

Councilmember Yvonne Reyes represents District 4 on the Greenfield City Council. She's running for reelection and posts regularly about the Riverside Park project, the city budget, public safety, and transit. She ties into the same Greenfield beat as `sample-docs/` — same city, same park closure, same contractor.

## Folder structure

```
mamdani-mini/
├── README.md                  # this file
├── sample-data/
│   ├── videos.json            # 5 synthetic video entries (the input)
│   └── transcripts/
│       ├── video-01.txt       # budget priorities
│       ├── video-02.txt       # Riverside Park closure
│       ├── video-03.txt       # contractor selection
│       ├── video-04.txt       # transit and the park
│       └── video-05.txt       # town hall Q&A clip
├── prompts/
│   ├── 01-discover.md         # stage 1: find the videos
│   ├── 02-transcribe.md       # stage 2: transcribe them
│   ├── 03-analyze.md          # stage 3: extract themes + claims
│   └── 04-dashboard.md        # stage 4: build the dashboard
└── dashboard-skeleton.html    # what the output target looks like
```

## How to use this folder

1. Read `sample-data/videos.json` to see what the fake input looks like.
2. Read `prompts/01-discover.md` through `prompts/04-dashboard.md` in order. Each prompt is one stage of the pipeline. They build on each other.
3. Try running stage 3 against a transcript — it works without any scraping setup:

   ```bash
   claude -p "$(cat prompts/03-analyze.md)" < sample-data/transcripts/video-01.txt
   ```

   You should get back structured JSON with themes, entities, sentiment, and claims to verify.

4. Open `dashboard-skeleton.html` in a browser to see what the target output looks like once the pipeline has run on all five transcripts.

## What to swap when you go live

If you want to run the real version, replace:

- `sample-data/videos.json` with the output of a real discovery script (`yt-dlp`, Playwright, or platform APIs)
- `sample-data/transcripts/*.txt` with Whisper turbo output
- `dashboard-skeleton.html` with whatever the dashboard prompt generates

The four prompts in `prompts/` should keep working with minimal changes — that's the point of staging the pipeline this way.

## Why no real scraping in this folder

Public starter kits should not ship code that targets real people's social accounts, even public ones. The synthetic version keeps the teaching value without the risk.
