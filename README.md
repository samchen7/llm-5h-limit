# llm-5h-limit

A single-page timeline calculator for squeezing the most out of $20 Claude and ChatGPT (Codex) plans during a 48-hour hackathon.

**Live:** https://samchen7.github.io/llm-5h-limit/

## Idea

Both plans use a rolling 5-hour usage window, and the weekly cap is roughly 7.7 of those windows. A 5-hour window starts at your first message, so:

1. A scheduled job sends a tiny prompt to open the window early.
2. You start heavy use near the end of that window and burn through it.
3. The window resets, and you keep going on a fresh one.

Each round burns two 5-hour quotas per tool back-to-back. Run Claude and Codex side by side and one round is four quotas, about half a weekly allowance. Four rounds use up the weekly cap within 48 hours.

## Usage

Set the start and end time, how long it takes you to burn one 5-hour quota, and the weekly quota size (in 5-hour units). The timeline shows:

- **Green dot**: when the scheduled prompt should fire
- **Orange / yellow**: the first and second quota of each round
- **Shaded bands**: sleep (00:00–06:00), lunch (12:00–13:00), dinner (18:00–19:00), which heavy use avoids

Below the timeline:

- **Schedule**: each round's trigger time, local cron expression, both 5-hour windows and their reset times
- **Trigger prompt**: the tiny prompt each cron job sends

**Copy rules for LLM** (top right) copies the rules plus the current schedule as Markdown. Paste it into Claude or Codex and ask it to create the cron jobs.

## Run locally

Open `index.html` in a browser. No build step or dependencies.

## Notes

The ~7.692 ratio is an estimate, and providers may change their limits. Check the usage page in each tool for actual reset times.

## License

MIT
