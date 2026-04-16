<!--
Stage 2 of 4 — transcription.

What this stage owns: turning a video file into a plain-text transcript saved to sample-data/transcripts/<video-id>.txt.

What it hands off: one .txt file per video, matching the shape of the existing transcript files in sample-data/transcripts/. Stage 3 reads those text files directly.

In video B1 of the MOOC, this stage uses Whisper turbo running locally. The prompt below shows how you'd frame the work for Claude. The transcripts already in this folder were hand-written for teaching, not produced by Whisper.
-->

# Transcription prompt

You are the transcription stage of a content analysis pipeline. You take a video file and produce a clean plain-text transcript.

## Inputs

- Path to a video file: `$VIDEO_PATH`
- Video id from `videos.json`: `$VIDEO_ID`
- Output path: `sample-data/transcripts/$VIDEO_ID.txt`

## Preferred path: Whisper turbo locally

Whisper turbo is the model Joe demos in B1. It runs on a laptop CPU in roughly real time and costs nothing per video.

```bash
# install once
pip install -U openai-whisper
# transcribe
whisper "$VIDEO_PATH" --model turbo --output_format txt --output_dir sample-data/transcripts/
# rename to match the video id
mv "sample-data/transcripts/$(basename "${VIDEO_PATH%.*}").txt" "sample-data/transcripts/$VIDEO_ID.txt"
```

If Whisper turbo isn't installed and the user can't install it, fall back to the OpenAI API:

```bash
curl https://api.openai.com/v1/audio/transcriptions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F "file=@$VIDEO_PATH" \
  -F "model=whisper-1" \
  -F "response_format=text" \
  > "sample-data/transcripts/$VIDEO_ID.txt"
```

## Cleanup the output

After Whisper writes the file:

1. Strip any speaker labels Whisper added (e.g. `Speaker 1:`)
2. Strip timestamps if they snuck into the txt format
3. Collapse runs of more than two newlines into two
4. Do not paraphrase or summarize. The whole point is the speaker's words.

## Local vs. cloud tradeoffs

| Path | Speed | Cost | Privacy | Quality |
|------|-------|------|---------|---------|
| Whisper turbo (local) | ~real time on CPU, faster on GPU | free | data never leaves your machine | excellent for clean audio |
| OpenAI Whisper API | faster than local CPU | paid per minute | data goes to OpenAI | excellent |

Default to local. Use the API only when local install isn't possible.

## Output shape

A single .txt file per video. Plain spoken-word text. No timestamps, no speaker labels, no metadata. See `sample-data/transcripts/video-01.txt` for the target shape.
