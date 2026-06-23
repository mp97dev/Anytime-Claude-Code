# Anytime-Claude-Code 🤖⏰

A GitHub Action that pokes Claude Code at 7am so the 5h usage reset happens before I get to work.

> ⚠️ I have no idea if this violates any ToS. Probably fine. Maybe not. Use at your own risk.

## What it does

1. Sends `"Respond with exactly: ok"` to Claude Code CLI at 7:00 CEST (5:00 UTC)
2. Starts the 5h countdown
3. By 9am when I sit down, I still have ~3h of fresh usage ahead
4. Writes the current date to `.last-ping` so GitHub doesn't disable the workflow after 60 days of "inactivity"

## Setup

1. Fork or clone this repo (or just copy the workflow file, honestly)
2. Get your Anthropic API key from [console.anthropic.com](https://console.anthropic.com) → *API Keys*
3. Add it as a GitHub secret:
   `Settings → Secrets and variables → Actions → New repository secret`
   Name it `ANTHROPIC_API_KEY`
4. Enable write permissions: `Settings → Actions → General → Workflow permissions → Read and write permissions`
5. Push and forget

> Claude Code uses the `ANTHROPIC_API_KEY` env variable automatically — no OAuth login needed in CI.

## Cost

Each ping sends one minimal prompt and forces a one-word reply. Basically free.

## Caveats

- Cron runs in UTC. Adjust the schedule if you're not in CEST.
- Works with **Claude Code subscription** (5h rolling window). Doesn't do anything for claude.ai sessions.
- The `.last-ping` commit trick is a bit silly but it works.
- If GitHub ever changes how they handle inactive workflows, this whole thing breaks silently and I'll have no idea until I show up at work and Claude is throttled.

## Files

```
.github/workflows/claude-ping.yml   # the actual thing
.last-ping                          # auto-updated, ignore it
README.md                           # this file
```

---

*Built out of mild frustration and a healthy distrust of manually remembering to do things.*
