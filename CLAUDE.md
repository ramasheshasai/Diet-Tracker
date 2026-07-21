# Diet Tracker — Project Rules

## What this project is
A vanilla JS PWA (zero frameworks, zero build tools). Everything lives in `index.html`.
`manifest.json` and `sw.js` handle PWA install + offline caching.

## Stack & constraints
- **No frameworks** — plain HTML/CSS/JS only. No React, Vue, Tailwind, etc.
- **No build step** — the file is served directly with `python3 -m http.server 8080`
- **Single file** — all code stays in `index.html` (styles, markup, scripts together)
- **Storage** — `localStorage` only. No backend, no database, no API calls
- **Charts** — Chart.js 4.x loaded from CDN (already in the file)

## User profile
- 21 yo male, 47 kg, goal: **weight gain + muscle**
- Diet: vegetarian + 1 egg/day
- Daily targets: ~2700 kcal, 110g protein, 350g carbs, 75g fat, 30g fiber
- Activity: lightly active

## Design system
- **Theme**: dark by default (`--bg: #111827`), light mode toggle available
- **Accent color**: `#22c55e` (green) — use for progress, positive values, CTAs
- **Danger color**: `#ef4444` (red) — use for over-target, delete actions only
- **Max width**: 430px centered — mobile-first, phone screen layout
- **Font**: system font stack (`-apple-system, BlinkMacSystemFont, "Segoe UI"`)
- Always use CSS variables (`--bg`, `--surface`, `--accent`, etc.) — never hardcode hex colors in new CSS
- Border radius: cards = 16px, buttons = 12px, chips = 99px
- Spacing unit: multiples of 4px

## Code rules
- No comments explaining WHAT code does — only WHY if non-obvious
- No TypeScript, no JSDoc, no type annotations
- No `console.log` left in final code
- Validate user input only at entry points (input fields) — trust internal functions
- Use `localStorage` keys prefixed with `dt_` (e.g. `dt_log_`, `dt_profile`, `dt_weights`)
- Nutritional values are always **per 100g** in the food database
- Always call `refreshDashboard()` after any change that affects today's totals or targets

## Key functions to know
- `refreshDashboard()` — re-renders the home view (ring, bars, water)
- `applyTargets(profile)` — recalculates and sets TARGETS from profile
- `loadTodayLog()` / `saveTodayLog(log)` — read/write today's meal data
- `loadProfile()` / `saveProfile(p)` — read/write user profile
- `computeTotals(log)` — aggregates all meal entries into nutrient totals
- `showToast(msg)` — shows the green toast notification

## What NOT to do
- Don't split into multiple files — keep everything in `index.html`
- Don't add npm, package.json, or any dependencies beyond what's already there
- Don't add features outside the current task scope
- Don't use `alert()` or `confirm()` — use the existing toast or in-UI feedback
- Don't hardcode today's date — always use `todayKey()` or `new Date()`
