# Two-League Sleeper Scoreboard

A full-screen fantasy football matchup board that puts two Sleeper leagues side by side, built to be read from across a room. One HTML file, no server, no API keys, no build step.

## What it shows

Per league: your matchup with live scores, every starter with their projection, the NFL game clock for each player, projected final totals, win probability, and a strip of every other matchup in the league. Players currently on the field grow larger and get a teal outline.

Scores refresh every 30 seconds. Starter rows scale automatically to fill the screen height.

## Deploying to GitHub Pages

1. Create a new **public** repository. Pages requires a paid plan for private repos.
2. Upload `index.html` to the root of the default branch.
3. Go to **Settings → Pages**, set Source to **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
4. Wait about a minute. The site appears at `https://<your-username>.github.io/<repo-name>/`.

## Using it

Open the page, enter a Sleeper username, and pick up to two leagues. Selections are stored in the browser and written into the URL, so the address bar can be bookmarked and it will open straight to the board.

That also means configured links are shareable. A URL like:

```
https://<your-username>.github.io/<repo-name>/#u=someone&id=123456789&l=1111111111,2222222222
```

opens directly to that person's two leagues, no setup screen.

If the username lookup fails, the setup screen has a fallback that takes raw league IDs — the long number in a league's web address at `sleeper.com/leagues/<id>/team` — and then lets you pick your team from the league's member list.

### Controls

| Key | Action |
| --- | --- |
| `F` | Fullscreen |
| `R` | Refresh now |
| `+` / `−` | Scale the whole page |

The cursor hides after four seconds of no movement.

## Data sources

- **Sleeper API** (`api.sleeper.app`) — leagues, rosters, matchups, live scoring, and projections. Projections come from an undocumented endpoint and are converted using each league's own `scoring_settings`, so custom formats read correctly. If that endpoint ever changes, projections and win probability disappear and live scoring keeps working.
- **ESPN scoreboard** (`site.api.espn.com`) — NFL game state and clock, used to mark who is currently playing and to weight projected finals by time remaining. Optional; the board works without it.

Each visitor downloads Sleeper's ~5 MB player list once per day and caches it in their browser. Everything else is a few small requests every 30 seconds.

Win probability is estimated locally with a normal approximation over remaining projected output. It will land near Sleeper's number but is not the same calculation.

## Other hosts

Any static host works the same way — Cloudflare Pages, Netlify, Vercel. Netlify Drop accepts the folder dragged onto the page with no repo at all.
