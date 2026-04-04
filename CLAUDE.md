# Code Maestro Analytics Prototype — Project Instructions

## What This Project Is

You are building an **interactive demo prototype** for Code Maestro's planned analytics feature. Code Maestro is an AI Copilot for game creation that helps users build playable ads. This prototype demonstrates how in-app analytics would work.

**THIS IS A DEMO, NOT A REAL APP.** All data is hardcoded. No real calculations, no APIs, no backend. Just a beautiful, interactive HTML page with pre-filled data that tells a compelling story.

## Your Task

Create a single `index.html` file following the specification in `PROTOTYPE_SPEC.md`. Read that file carefully — it contains exact layouts, data values, colors, typography, and component specifications.

## Critical Requirements

1. **Single HTML file** — all CSS and JS inline, no build tools
2. **Pre-filled data only** — every number, chart, and text is hardcoded per the spec
3. **Code Maestro dark design** — matches the existing app's look and feel (dark backgrounds, gold/violet accents)
4. **Tab navigation** — 4 tabs in left sidebar: Dashboard, Insights, Hypothesis Lab, Setup
5. **Chart.js for charts** — load from CDN, dark theme
6. **Google Fonts** — Inter (headings) + Montserrat (body)
7. **Desktop only** — optimized for 1440px+ screens
8. **Production quality visuals** — this will be shown to investors and enterprise leads

## Design System (from Code Maestro brand)

### Colors
- Background: `#05070F` (main), `#080B15` (sidebar), `#20222B` (cards)
- Text: `#FAFAFA` (primary), `#EEEEEE` (secondary), `#737373` (muted)
- Gold accent: `#FCBC16` (primary highlight, CTAs)
- Violet accent: `#6848D1` (buttons, badges)
- Red: `#E72D53` (critical issues)
- Green: `#22C55E` (positive metrics)
- Borders: `#36383E`

### Typography
- Headings: Inter Bold 700
- Body: Montserrat Regular 400
- Monospace for code: system monospace

### Component Patterns
- Cards: `#20222B` bg, `#36383E` border, 8px radius
- Active sidebar tab: 3px left border `#FCBC16`
- Tables: `#161823` header, alternating `#20222B` / `#1A1C26` rows
- Primary buttons: violet gradient
- Accent buttons: gold `#FCBC16` with dark text

## What NOT To Do

- Don't add real analytics logic or event tracking
- Don't use React, Vue, or any framework — vanilla JS only
- Don't create multiple files — everything in one index.html
- Don't make it responsive for mobile — desktop demo only
- Don't add working "Ask AI" input — it's a placeholder
- Don't use localStorage or sessionStorage

## How To Build

1. First read `PROTOTYPE_SPEC.md` completely
2. Start with the shell: overall layout, sidebar, top bar
3. Build Tab 1 (Dashboard) with all charts and data
4. Build Tab 2 (Insights) with insight cards and AI panel
5. Build Tab 3 (Hypothesis Lab) with experiment cards and learning feed
6. Build Tab 4 (Setup) with event configuration
7. Add tab switching logic
8. Polish: transitions, hover states, scrollbars, typography
9. Test in browser at 1440px width

## Demo Case Context

All data is about a fictional game studio "Crystal Games" and their "Pixel Quest" casual platformer playable ad. The analytics tells a story: high engagement but low conversion due to tutorial friction and the "satisfaction trap" (users who win don't install). See PROTOTYPE_SPEC.md for exact values.
