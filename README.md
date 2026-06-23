# Anytime-Claude-Code 🤖⏰

A GitHub Action that pokes Claude at 7am so the 5h usage reset happens before I get to work.

> ⚠️ I have no idea if this violates any ToS. Probably fine. Maybe not. Use at your own risk.

## What it does

1. Sends a "hi" to the Claude API at 7:00 CEST (5:00 UTC)
2. Starts the 5h countdown
3. By 9am when I sit down, I still have ~3h of fresh usage ahead
4. Writes the current date to `.last-ping` so GitHub doesn't disable the workflow after 60 days of "inactivity"

## Setup

1. Fork or clone this repo (or just copy the workflow file, honestly)
2. Add your Anthropic API key as a GitHub secret:
   `Settings → Secrets and variables → Actions → New repository secret`
   Name it `ANTHROPIC_API_KEY`
3. Push and forget

## Cost

Uses `claude-haiku` with `max_tokens: 1`. Each ping costs roughly **$0.000001**. You'll burn through a dollar in approximately the heat death of the universe.

## Caveats

- Cron runs in UTC. Adjust the schedule if you're not in CEST.
- Only useful if your Claude usage is tied to the **API**. Doesn't do anything for claude.ai sessions.
- The `.last-ping` commit trick is a bit silly but it works.
- If GitHub ever changes how they handle inactive workflows, this whole thing breaks silently and I'll have no idea until I show up at work and Claude is throttled.

## Files

```
.github/workflows/claude-ping.yml   # the actual thing
.last-ping                          # auto-updated, ignore it
```

---

*Built out of mild frustration and a healthy distrust of manually remembering to do things.*
