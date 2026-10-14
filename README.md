# NammaTrip AI

**Your Budget. Your Journey. Your Karnataka.**
ಕನ್ನಡದಲ್ಲಿ ನಿಮ್ಮ ಕರ್ನಾಟಕ ಪ್ರವಾಸದ ಸಂಗಾತಿ

A bilingual (Kannada and English), budget-aware Karnataka trip planner built with plain HTML, CSS and JavaScript.
Made for the **Kannada Digital Innovation Hackathon 2026** (theme: *Code. Create. Celebrate Kannada.*).

> **Prototype note:** The planner uses a transparent **rule-based engine** that runs in your browser.
> It does **not** call any AI service, and it does **not** use live prices, weather, ratings or availability.
> All costs are clearly labelled estimates.

## Problem

Most trip-planning tools are English-first and ignore a simple question: *"Can I afford this, in the days I have?"*
Many Kannada speakers, students and families plan Karnataka trips from scattered posts and videos, with no single plan that respects budget and time.

## Solution

Enter your starting city, days, travellers, budget and interests. NammaTrip AI:

1. scores 13 curated Karnataka destinations against your preferences,
2. chooses stops that fit your days and pace,
3. orders them into a route and builds a day-by-day itinerary,
4. estimates cost at low, mid and high planning rates,
5. **warns you honestly** when the budget is not enough.

Everything works in Kannada or English with one click.

## Features

- Immersive hero with animated Karnataka landscape, floating route pins and a quick-plan card
- Kannada / English toggle covering navigation, forms, errors, results, culture content and destination descriptions
- 13 destinations with bilingual descriptions, attractions, cost ranges, season notes, map links
- Destination carousel (touch scroll, buttons, filters) and a detail panel
- Trip form with validation, live budget slider and live budget split
- Transparent recommendation and cost engine (see below)
- Results dashboard: route map with a **draggable traveller marker** (slider and arrow keys as alternatives), reorderable stops (drag, or up/down buttons), add / remove stops, route optimiser, day-by-day timeline, cost chart, budget vs estimate bars
- Packing checklist and travel tips
- Print-friendly view, download as JSON or text, share (Web Share API with clipboard fallback)
- Culture section: food, dynasties, Kannada phrases, responsible tourism
- Accessible: semantic HTML, skip link, keyboard operation, focus styles, `prefers-reduced-motion`

## Tech stack

HTML5, CSS3 (custom properties, grid, flexbox), vanilla JavaScript (ES6+). No frameworks, no npm, no build step, no API keys.
Fonts (Fraunces, Hanken Grotesk, Noto Sans/Serif Kannada) load from Google Fonts with system fallbacks.

## Run it

1. Put `index.html`, `style.css`, `script.js` in one folder.
2. Open `index.html` in a browser, or use VS Code **Live Server** (right-click `index.html` > *Open with Live Server*).

## Project structure

```
nammatrip-ai/
  index.html   page structure
  style.css    design tokens and components
  script.js    1 data  2 translations  3 engine (no DOM)  4 UI
  README.md
```

## How the engine works

`script.js` section 3 contains pure functions (no DOM), so they can be tested in the browser console with `NammaEngine`:

| Step | Function | What it does |
|------|----------|--------------|
| Validate | `validateTripInputs` | Checks days (1-14), travellers (1-20), budget, date, interests |
| Score | `scoreDestination` | Interests (up to 50), wishes (+25), distance penalty (up to -20), budget fit, family and access adjustments |
| Choose | `selectStops` | Number of stops from days and pace; picks high scorers, rewards nearby stops, discourages repeats |
| Route | `orderByNearest`, `allocateDays` | Nearest-neighbour ordering; days shared by suggested duration |
| Cost | `computeCosts` | Stay + transport + food + activities + 8% contingency at low / mid / high rates |
| Verdict | `buildPlanFromStops` | `comfortable`, `fits`, `tight` or `insufficient` |

Try in the console: `NammaEngine.selfTest()`

### Planning assumptions (all estimates)

- Road distance = straight-line distance x 1.2; average speed 45 km/h
- Transport per person per km: 1.5 / 4 / 7 rupees (low / mid / high); local transport 50 / 150 / 300 rupees per person per day
- Stay is per room (2 people per room); food and activities are per person per day
- Destination cost ranges are team assumptions, not live prices

## Data limitations

- Costs, interest weights and accessibility ratings are editorial estimates by the team
- No live transport schedules, opening hours, ratings or availability
- Official links are limited to the Karnataka Tourism portal and two UNESCO pages. **Verify each link before submission.**
- Kannada text should be reviewed by a native speaker before final submission

## Testing checklist

- [ ] Language toggle changes every visible label, error and result
- [ ] Sample trip works twice (two different samples)
- [ ] Budget slider and number box stay in sync; split updates live
- [ ] Empty days or budget below 2000 shows a clear error
- [ ] Budget of 3000 for 6 days shows "Budget is not enough"
- [ ] Reordering with drag, with up/down buttons, and by keyboard rebuilds the itinerary
- [ ] Marker moves with mouse drag, slider and arrow keys
- [ ] Print preview shows only the plan
- [ ] JSON and text downloads open correctly (Kannada text is readable)
- [ ] No red errors in the browser console

## Deploy on GitHub Pages

1. Create a public repository and upload the four files.
2. Repository **Settings > Pages**, source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
3. Open the public URL after a minute and repeat the testing checklist there.

## Screenshots

Add screenshots here after you test (hero, planner, results, Kannada view).

## Future improvements

- Secure backend that adds a real AI model behind the same plan format (API keys stay on the server)
- Verified data from official sources, with source and date for every figure
- Offline support, more destinations, saved trips
- Review of all Kannada text by community reviewers

## Credits

Built by a BCA student for the hackathon (add your name and college here).
Illustrations are original SVG drawings.
