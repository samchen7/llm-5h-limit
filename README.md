# llm-5h-limit

A single-page timeline calculator for squeezing the most out of $20 Claude and ChatGPT (Codex) plans during a 48-hour hackathon.

**Live:** https://samchen7.github.io/llm-5h-limit/

## Idea

Both plans use a rolling 5-hour usage window, and the weekly cap is roughly 7.7 of those windows. A window opens with your first message and resets 5 hours later, so the plan follows your day:

1. **Before you wake up** (and before the hackathon starts), a cron job sends a tiny prompt. The window it opens resets shortly after you start working, so you burn that quota in one burst and get a fresh window right away.
2. **During the day**, the first message after each reset opens the next window. Windows run back to back, and each quota is spread over its window, so the work per hour stays light.
3. **At bedtime**, whatever window is open has to be used up before you sleep.

## Usage

Set the start and end time on the page. **Settings** (top right) holds the rest: how long it takes you to burn one 5-hour quota, the weekly quota size (in 5-hour units), and your sleep, breakfast, lunch and dinner times (a length of 0 turns one off). Work never overlaps those off-hours.

The hour grid has one cell per hour (a row per day on desktop, a column per day on phones):

- **Green**: quota being spent. Dark cells are the burst right after waking (the cron window); lighter cells are daytime windows, whose quota is spread over five hours.
- **Light green ring**: a cron trigger fires in that hour.
- **Grey**: sleep and meals.
- **White**: free.

Below the grid:

- **Schedule**: every window, whether a cron job or your first message opens it, when you work in it, the load per hour and when it resets
- **Trigger prompt**: the tiny prompt each cron job sends

**Copy rules for LLM** (top right) copies the rules plus the current schedule as Markdown. Paste it into Claude or Codex and ask it to create the cron jobs.

## Run locally

Open `index.html` in a browser. No build step or dependencies.

## Notes

The ~7.692 ratio is an estimate, and providers may change their limits. Check the usage page in each tool for actual reset times.

## License

MIT
