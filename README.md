# Goodland Bruins 13U Gold — Analytics Dashboard

Private analytics dashboard for the Goodland Bruins 13U Gold travel baseball program. Static HTML site hosted on GitHub Pages. Password protected.

**Live site:** [alissa-bruins.github.io/bruins](https://alissa-bruins.github.io/bruins)  
**Season:** October 2025 – March 2026  
**Record:** 24–7 · +92 run differential · 3 championships

---

## Access

PIN protected. Enter **1327** on any page to unlock.  
Cache reset: append `?reset=1` to any URL.

---

## Site Structure

All data is embedded directly in each HTML file — no backend, no API, no build step. Upload any file to the repo and it is live immediately.

| File | Page | Description |
|------|------|-------------|
| `index.html` | Team | Season record, tournament log, run differential chart, performance by class |
| `batting.html` | Batting | OPS rankings, player cards, season totals |
| `pitching.html` | Pitching | Staff summary, pitcher selector, ERA trend chart, pitch count chart, game log |
| `fielding.html` | Fielding | Position depth grid, FPCT table, innings charts, player fielding breakdown |
| `defense.html` | Defense | 3-scenario defensive lineups — Swartz / Demmin / Lopes pitching |
| `trends.html` | Trends | Hot/cold tracker, AVG & OBP trend charts by tournament |
| `lineups.html` | Lineups | Batting order by opponent class, pool play vs bracket rotation |
| `scouting.html` | Games | 34 game cards with box score modal, filterable by tournament |
| `players.html` | Players | Full player profiles — season stats, per-tournament breakdown, pitching, fielding |
| `flags.html` | Flags | Active health flags, development gaps |

---

## Roster

| # | Name | B/T | Grad | Primary Position |
|---|------|-----|------|-----------------|
| 2 | James Short | R/R | 2031 | C / 3B |
| 3 | Walker Torres | R/R | 2032 | 2B / SS / P / OF |
| 5 | Aiden Herrera | R/R | 2031 | C / SS |
| 9 | Will Oswald | R/R | 2031 | SS / C / 2B / 3B |
| 13 | Rio Lopes | L/L | 2031 | CF / P |
| 15 | Calvin Firestone | R/R | 2032 | SS / 1B / 3B / P |
| 17 | Joseph Demmin | L/L | 2031 | 1B / P |
| 22 | Eli Swartz | L/L | 2031 | P / LF / RF |
| 24 | Jackson Murdock | L/R | 2031 | 2B / C |
| 27 | Brennan Zant | R/R | 2031 | LF / CF / RF / P |
| 50 | Robert Denny | R/R | 2031 | LF / CF / RF / P |

**Three LHP starters:** Lopes (#13), Demmin (#17), Swartz (#22)  
**Class of 2032 playing up:** Torres, Firestone

---

## Data Sources

| Data | Source | Status |
|------|--------|--------|
| Season batting totals | GameChanger CSV export | ✅ Authoritative |
| Season pitching totals | GameChanger CSV export | ✅ Authoritative |
| Fielding innings by position | GameChanger Innings Played screenshot | ✅ Authoritative |
| Per-tournament batting | Extracted from 32 box score PDFs | ✅ Validated against CSV (all 11 players within ±10 AB) |
| Per-game pitching logs | Extracted from 32 box score PDFs | ✅ Lopes/Zant exact match |
| Box scores | 32 game PDFs embedded as JS | ✅ All 34 games |

### PDF Extraction Notes

GameChanger box scores use a two-column layout with both teams on the same line. Extraction uses:
- **Jersey number** as primary player identifier (handles truncated names like `J Murdo…`)
- **PDF filename** to determine column order — `GoodlandBruins_vs_X` = Goodland is left column, `X_vs_GoodlandBruins` = Goodland is right column
- **Opponent name** always read from filename, never from PDF text (score digits bleed into team names in the raw text)

---

## Pitching Rotation

| Situation | Starter | Notes |
|-----------|---------|-------|
| Pool play G1 | Lopes | Best K/9 (16.4), best K/BB (2.29) |
| Pool play G2 | Demmin | Best ERA (2.53), 0.47 ERA last 4 outings |
| Bracket / elimination | Swartz | Healthy ERA 1.03 — save for when it matters |

**Swartz return protocol (active):** 60P max · No game-2 same day · 5-day rest minimum · RF/LF field only

---

## Updating the Site

After each tournament:

1. Export a new cumulative CSV from GameChanger
2. Update `shared_data_v4.js` with new season totals
3. Add new PDF box scores to the project folder
4. Re-run PDF extraction scripts to update `tournament_stats.json` and `pitching_logs.json`
5. Rebuild affected HTML pages
6. Upload to repo — changes are live immediately

**Validation step:** After any extraction, compare box score AB totals to CSV season totals. All 11 players should be within ±10 AB.

---

## Technical Notes

- **No build step** — pure HTML, CSS, vanilla JS
- **Chart.js** loaded via cdnjs CDN in `<head>` of each page
- **Auth** — PIN stored in `localStorage` under key `bruins_ok`
- **All data embedded** — each page is fully self-contained
- **Script order matters** — shared data → tour/pitching data → auth → global functions → `onUnlock()`
- **Global scope required** — all interactive functions must be defined before `onUnlock()`, never inside it

---

## Head Coach

Jesse Landeros  
Goodland Bruins Baseball — Goleta / Santa Barbara, CA  
Independent nonprofit travel baseball. Separate from GVSLL.
