# GitHub Actions workflows

This folder has the cloud side of the hybrid cloud-detect / local-process pattern from video C2.

## What's here

- `weekly-digest.yml` — runs the `scripts/pipeline/` stages against `sample-docs/` every Monday at 09:00 UTC and commits the digest back to the repo.

## The hybrid pattern

The idea from video C2 is to split work between the cloud and your local machine based on what each is good at.

**Cloud (GitHub Actions) is good for:**
- Scheduled checks (every hour, every day, every week)
- Lightweight text processing
- Anything that has to run when your laptop is closed
- Triggering on git events (push, PR, issue)

**Local (your laptop or a Pi) is good for:**
- GPU-heavy work (Whisper transcription, image generation, big batch inference)
- Long-running jobs that would burn through GitHub minutes
- Anything touching files you don't want to upload to a runner
- Interactive debugging

The weekly-digest workflow lives on the cloud side because it's text-only, scheduled, and small. If you wanted to add Whisper transcription to it, you'd move that step to a local runner instead.

## Adding your API key

The workflow needs `ANTHROPIC_API_KEY` to actually call Claude. To set it in your fork:

1. Go to your repo on GitHub
2. Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Name: `ANTHROPIC_API_KEY`
5. Value: your key from console.anthropic.com
6. Save

Without the secret, the workflow still runs — it just writes a stub digest explaining what's missing. That's deliberate: we don't want students who fork the repo to get failing-build emails on day one.

## Secret hygiene

- Never paste a key into the workflow file itself. Always use the `secrets` context.
- Never `echo` a secret in a step. GitHub masks them in logs but the masking isn't bulletproof.
- Don't add secrets to repo files, even commented out, even temporarily.
- If you think you leaked a key, rotate it immediately at console.anthropic.com.

## The commit-loop trap

Video C2 mentions this: a workflow that commits to its own branch can re-trigger itself and run forever. We avoid it two ways:

1. The stub digest is byte-stable — same content every run — so when the secret is missing, `git diff --staged --quiet` short-circuits the commit step.
2. The schedule trigger doesn't fire on bot-author commits by default in GitHub Actions, so even a real diff won't loop.

If you change the digest content to include a timestamp or random ID, you'll need to add a path filter or guard yourself.
