# Two-Minute Drill — all your Sleeper lineups in one place

A single-page, phone-first dashboard for every Sleeper league you're in. No backend, no API keys, no login: your phone talks straight to Sleeper's public API and ESPN's public scoreboard. Open it, glance at the top of Alerts, and know in under two minutes whether you're set for the week.

The repo is still named `fantasy-football-dashboard` — only the app's name, icon and colors changed.

## Put it on GitHub Pages (about 3 minutes)

1. Create a new **public** repository on GitHub (any name — `fantasy-football-dashboard` works). Don't add a README or anything else.
2. Upload every file in this folder to the root of the repo (`index.html`, `manifest.webmanifest`, `sw.js`, `icon.svg`, `icon-180.png`, `icon-192.png`, `icon-512.png`). Drag-and-drop on the repo page → **Commit changes**.
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `/ (root)` → Save.**

A minute later the site is live at `https://<your-username>.github.io/<repo-name>/`.

Updating later = replace `index.html` and commit. Pages redeploys automatically.

## Make it feel like an app on your phone

- **iPhone:** open the URL in Safari → Share → **Add to Home Screen**. It gets its own icon and opens full-screen with no browser chrome.
- **Android:** open in Chrome → ⋮ menu → **Add to Home screen** (or "Install app").

## What's inside

| Tab | What it shows |
|---|---|
| **Alerts** | The home screen — opens first, every time. A glance strip up top tells you at once whether anything needs attention or you're all set, then lists anything that needs a decision: starters who are Out / Doubtful / Questionable / IR, starters on bye, empty slots, and cross-league conflicts (a player you start in one league but face in another; a player you face in 2+ leagues). Every alert has a one-tap link that opens that exact league in Sleeper. |
| **Games** | The week's slate grouped by window (Thu night, Sun early / late, SNF, MNF) with primetime badges and network. Each game lists your starters (tagged by league) and the opposing starters you're up against. Live scores and points once games start. |
| **Leagues** | Every lineup on one page: slot, player, opponent, kickoff / live status, injury badge, points. Bench is collapsible. |
| **Players** | Your exposure across leagues: started ×N, benched ×N, facing ×N. Filter by Starting / Facing / Benched. |

Settings (gear icon): change the Sleeper username, show bench by default, hide finished games.

## Why lineup edits aren't in here

Sleeper has no public write API. The app uses private, authenticated calls, and scripting those is against their terms of service and could get your account flagged. The deep links are the honest workaround — one tap lands you on the right roster.

## Data sources

- `api.sleeper.app/v1` — user, leagues, rosters, matchups, players (injury status). Read-only, public, CORS-enabled.
- `site.api.espn.com` scoreboard — kickoff times, live status, network. Falls back to Sleeper's schedule (dates only) if ESPN is unreachable.

The player database (~5 MB) is cached in the browser for 20 minutes; everything else is fetched fresh on load, on the refresh button, and automatically every 90 seconds while a game is live.
