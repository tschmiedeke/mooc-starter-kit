<!--
Stage 1 of 4 — discovery.

What this stage owns: finding the N most recent videos for a given subject across one or more platforms, and writing the metadata (title, URL, duration, posted_at, views, description, thumbnail) to videos.json.

What it hands off: a videos.json file matching the shape in sample-data/videos.json. Stages 2-4 expect that shape.

In video B1 of the MOOC, this stage is wired up to yt-dlp and Playwright for actual scraping. In this folder there's no real scraping — the prompt below shows the SHAPE you'd hand to Claude if you were going live. Read it, but don't expect it to run end-to-end without those tools installed and configured.
-->

# Discovery prompt

You are helping a journalist build a content analysis pipeline. The first stage is discovery: finding the most recent videos posted by a public figure on social platforms.

## Inputs

- Subject name (e.g. "Yvonne Reyes")
- A list of platform handles, one per platform: `youtube=@yvonnereyes`, `tiktok=@yvonnereyes`, `twitter=@yvonnereyes`
- Number of videos per platform (default: 15)
- Output path for the metadata JSON (default: `sample-data/videos.json`)

## What to do

1. For each platform, use the appropriate tool to list the N most recent videos. Suggested tools:
   - YouTube: `yt-dlp --flat-playlist --dump-json "https://www.youtube.com/@HANDLE/videos"`
   - TikTok: Playwright session against the user's profile page; scroll, capture video tiles
   - Twitter: Playwright session against the user's media tab
2. For each video found, extract: id, title, platform, url, duration_seconds, posted_at (ISO date), views (best estimate), description (first 1-2 sentences), thumbnail_url
3. Merge results from all platforms into a single array
4. Sort newest first
5. Write the array to the output path as valid JSON, one object per video
6. Do not invent fields. If a platform doesn't expose views, set views to null and note it in stage 3 instead of guessing.

## Output shape

Match `sample-data/videos.json` exactly. If you add fields, add them to every entry so the downstream stages don't break on missing keys.

## Failure modes to handle

- Platform changed its DOM. Don't keep retrying — log and skip the platform.
- Rate limit hit. Stop, save partial results, exit with a clear message.
- Video has no public duration (some live replays). Set `duration_seconds: null`.

## Notes

- Real scraping pulls from real people. Get permission and read each platform's terms of service before pointing this at a live account.
- The pedagogical version of this folder uses synthetic data — see `sample-data/videos.json`. That file was hand-written, not scraped.
