# Veezy.ai

AI-graded NBA lines, picks and edges for today's slate: one static `index.html`, no build step.

Veezy.ai is a rebuild of the earlier **Courtside Skeptic v3.5** page, which is still in git history.

## How the original worked

Courtside Skeptic was one HTML file with inline CSS and JS:

1. **Data source:** no odds API. On load it sent one `POST https://api.anthropic.com/v1/messages` with the `web_search` server tool and a prompt asking Claude to find today's NBA games and return a JSON array (`away_team`, `home_team`, `time_et`, `away_ml`, `home_ml`, `spread`, `total`, `pick`, `pick_reason`, `grade`).
2. **Parsing:** it joined the `text` blocks, stripped Markdown code fences, regex-matched the first `[...]`, then ran `JSON.parse`.
3. **Caching:** it kept the result in `localStorage` for 20 minutes (`cs_games_v2` / `cs_ts_v2`). "Force refresh" skipped the cache.
4. **Rendering:** one card per game showing moneylines, spread, total, a grade badge (A+ / A / B / C / PASS) and the AI pick with a reason.

Problems found:

- **No auth:** the request sent no API key and no browser-access header, so it only worked inside a sandbox that adds them (such as a Claude artifact). Opened as a normal web page, it always failed.
- **XSS:** AI output (team names, pick reasons) went straight into `innerHTML`.
- **Truncation:** `max_tokens: 1000` is too small once web search runs, so the JSON got cut off.
- **Paused searches:** it didn't handle `pause_turn` (a long web search pausing) or `refusal`.
- **Stale cache:** the cache wasn't tied to the date, so yesterday's slate could show after midnight.
- **Outdated model and tool:** it used an old model and an old web search tool version.

## What Veezy.ai changes

- **New look:** the Veezy.ai brand, and the layout works on phones.
- **Your own API key:** you enter an Anthropic key in ⚙ Settings. It is stored only in your browser. Calls go through the official `@anthropic-ai/sdk`, loaded as an ES module from jsDelivr.
- **Current model:** `claude-opus-5-5` with adaptive thinking, an adjustable effort level, `web_search_20260209`, streaming, and resume on `pause_turn`.
- **Refusal fallback:** if the main model declines, another model runs the request automatically (server-side `fallbacks: "default"`).
- **Safe output:** everything is HTML-escaped. Source links must be `http(s)`.
- **Odds math:** moneylines are converted to no-vig win probabilities, and the book's hold is shown.
- **New fields:** a confidence score (0–100) and source links for each pick.
- **Filters:** grade filters (A-tier, B+, hide PASS), with games sorted by grade and then confidence.
- **Date-aware cache:** the cache is tied to the local date and kept for 20 minutes.

## Running

Open `index.html` in a browser, or serve the folder with any static host (for example `python3 -m http.server`). Click **⚙ Settings**, paste your Anthropic API key, then press **Refresh slate**.

> The key sits in browser storage and is sent directly to Anthropic. Only use this on a device you trust. For a public deployment, move the API call behind your own backend.

For entertainment and research only. Bet responsibly.
