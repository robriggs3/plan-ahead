# Plan ahead.

A single HTML file for personal nomad travel planning. Tracks where you've been, where you are, and where you're going — without sharing your data with anyone.

**[Try it now →](https://robriggs3.github.io/plan-ahead/plan-ahead.html)** · No install. No account. Your data stays in your browser.

## What it is

One page for planning long-term travel: where you are now, where you're going, and what you're considering.

- Itinerary with check-in/check-out dates and gap/overlap detection
- Schengen 90/180 rolling counter
- US days by state (for FEIE / domicile tracking)
- Per-city: neighborhoods, attractions, restaurants, day trips, coworking, friends, accommodations
- Idea inbox for destinations being considered
- Interactive map with 130+ pre-loaded city coordinates
- AI-powered "import from notes" — paste any text, extract destinations
- Auto-snapshots every 10 minutes, last 5 kept
- JSON export/import for backups and cross-device transfer

## What it is not

- A product
- A SaaS app
- A booking tool
- Synced across devices (single browser, single localStorage)

It is a personal planning tool. Built for one specific failure mode: the long-term nomad who needs to track Schengen days, FEIE days, accommodation overlaps, and a dozen potential destinations across an 18-month timeline.

## Install

1. Download `plan-ahead.html`
2. Open it in a browser
3. Bookmark it
4. Edit the HTML directly to change defaults

That's the entire install.

## Philosophy

Inspired by the same single-file, no-server, no-account approach as [Start Here](https://github.com/robriggs3/start-here).

Three principles drove the design:

1. **No backend, ever.** Your travel plans, addresses, friends, and habits don't go to anyone's server. localStorage in your browser, nowhere else.
2. **Honest about what's possible without a server.** No cross-device sync. No live scraping of booking sites. No magical AI without your own API key. The compromises are explicit.
3. **Content elements editable, interface elements not.** Your cities and notes are editable. The "drag to reorder" hint is not. The page should teach itself.

## How it works

Single HTML file. Three layers:

- **HTML structure** — sections and layout
- **CSS** — design tokens at top via custom properties, easy to recolor
- **JavaScript** — state in a single object persisted to localStorage, rendered on every change

External dependencies (all CDN, no installation):

- [Leaflet](https://leafletjs.com/) for the map (via cdnjs)
- [OpenStreetMap](https://www.openstreetmap.org/) tiles
- Built-in geocoding lookup for 130+ common nomad cities; falls back to Nominatim for others
- Optional: Anthropic API for AI-powered note extraction (bring your own key)

## Features

### Day counters
- **Schengen 90/180**: rolling-window math; shows today's count and the peak ahead
- **Per-country**: total nights anywhere
- **Per-US-state**: for domicile evidence and FEIE tracking
- **Total cost**: sums booked accommodations and city estimates

### Itinerary
- Add cities with check-in/check-out dates
- Auto-detects past vs current vs future from today's date
- Past travel collapses into its own drawer but still counts in totals
- Gap detection: warns if you have no accommodation between cities
- Overlap detection: warns if you're paying for two places at once
- Each city expands to show all sub-data

### Map
- Pre-loaded coordinates for common nomad destinations
- Auto-geocodes new cities when name + country match the database
- Manual lat/lng entry + Nominatim lookup for uncommon cities
- Color-coded pins: past, current, future, idea
- Reset view button

### AI helpers (optional, bring your own Anthropic API key)
- Import from notes: paste any text, AI extracts destinations into structured fields
- Assess accommodation: structured prompt against your travel profile
- Works without API key via copy-paste to Claude.ai

### Data safety
- Auto-snapshots every 10 minutes (keeps last 5)
- One-click restore from any snapshot
- JSON export / import / paste
- Reset with double-click confirmation

## Branding and colors

Same [Code Conspirators](https://codeconspirators.com) red as Start Here. Six CSS variables drive everything:

```css
--accent: #c72027;
--accent-hover: #9c181d;
--accent-soft: #f3d1d3;
--bg: #cccccc;
--bg-card: #ffffff;
--text: #242424;
```

## Compatibility

**Tested:** modern Chrome, Safari, Firefox on macOS.

**Known limitation:** mobile drag-and-drop and file pickers are unreliable. Use desktop/laptop for editing, mobile for reading.

**Sandboxed environments** (some iframe contexts): external script blocking can prevent the map from loading. Works correctly on GitHub Pages and as a local file.

## Customizing

Edit `plan-ahead.html` directly. Notable spots:

- `DEFAULT_PROFILE` — the travel profile shown on first load
- `CITY_COORDS` — built-in coordinate lookup table; add cities here for instant geocoding
- `SCHENGEN_COUNTRIES` — adjust if the Schengen Area changes
- Section visibility — delete unused sections in the HTML and their corresponding render functions

## Status

**Early release.** Maintained as time allows. Stable for personal use; not feature-complete by design.

- **Bug reports:** open an issue
- **PRs:** bug fixes welcome
- **Feature requests:** open an issue, expect "no" as a likely answer

## License

MIT.

## Credit

Built by [Rob Riggs](https://robriggs.com) at [Code Conspirators](https://codeconspirators.com).
