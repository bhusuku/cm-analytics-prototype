# Code Maestro Analytics — Interactive Prototype Specification

## Overview

This is a **demo-only interactive prototype** (single HTML file) that showcases the analytics capabilities planned for Code Maestro. It is NOT a functional application — all data is pre-filled, there are no real calculations or API calls. The purpose is to **validate the concept** with potential clients (e.g., Alexander from Triple Dot Studios) and collect feedback.

## Critical Rules

- **NO real logic or calculations** — all numbers, charts, and data are hardcoded
- **Pre-filled with ONE consistent demo case** throughout all screens
- **Single HTML file** with embedded CSS and JS (no build tools, no frameworks except what's loaded from CDN)
- Use **Chart.js** from CDN for charts
- Must look **production-quality** despite being a prototype — it's the first impression
- Each section must be **independently viewable** via tab navigation
- Language: **English** (for international clients)

---

## Demo Case: "Pixel Quest" by Crystal Games

All pre-filled data tells ONE story:

- **Client**: Crystal Games (fictional game studio)
- **Game**: "Pixel Quest" — a casual platformer (similar to the Mario-style playable visible in Code Maestro screenshots)
- **Playable ad**: Created in Code Maestro, running on AppLovin and Meta
- **Campaign period**: March 1–31, 2026
- **Problem**: High engagement but low conversion to installs — the playable is fun but doesn't drive downloads
- **The analytics reveals**: Users drop off after winning the game (they feel satisfied and don't need to install). Tutorial step 2 is confusing. CTA text "Download Now" underperforms vs "Continue Playing".

This story threads through all three levels:
1. **Dashboard** shows the raw data and the drop-off
2. **AI Insights** identifies the problems and recommends solutions
3. **Hypothesis Lab** proposes auto-generated variant playables to test fixes

---

## Application Layout

### Overall Structure (mirrors Code Maestro app)

```
┌─────────────────────────────────────────────────────────┐
│  [CM Logo]  Code Maestro          [Pixel Quest ▾]  [?]  │  ← Top bar
├──────────┬──────────────────────────────────────────────┤
│          │                                              │
│  Left    │              Main Content Area               │
│  Sidebar │                                              │
│          │                                              │
│ [tabs]   │   (changes based on selected tab)            │
│          │                                              │
│          │                                              │
│          │                                              │
│          │                                              │
│          │                                              │
├──────────┴──────────────────────────────────────────────┤
│  Status bar                                              │
└─────────────────────────────────────────────────────────┘
```

### Left Sidebar (always visible)
- **CM Logo** at top (text "CM" in white, styled)
- **Navigation tabs** (vertical, icon + label):
  - 📊 **Dashboard** — analytics overview (Level 1)
  - 🔬 **Insights** — AI recommendations (Level 2)
  - 🧪 **Hypothesis Lab** — AI experiments (Level 3)
  - ⚙️ **Setup** — event configuration (supplementary)
- **Active tab** highlighted with gold left border (#FCBC16)
- Bottom: "Analytics Beta" badge in violet (#6848D1)

### Top Bar
- CM logo + "Code Maestro" text (left)
- Project selector dropdown: "Pixel Quest — Crystal Games" (center)
- Period selector: "Mar 1–31, 2026" (right)
- Help icon (right)

---

## Tab 1: Dashboard (Level 1 — Analytics)

This is the core analytics view. Shows pre-filled metrics and visualizations.

### Layout
```
┌─────────────────────────────────────────────────┐
│  KPI Cards Row (4 cards)                         │
├─────────────────────┬───────────────────────────┤
│  Engagement Funnel  │  Performance Over Time     │
│  (vertical funnel)  │  (line chart)              │
├─────────────────────┼───────────────────────────┤
│  Drop-off Analysis  │  Network Comparison        │
│  (bar chart)        │  (table)                   │
├─────────────────────┴───────────────────────────┤
│  Event Timeline (horizontal flow)                │
└─────────────────────────────────────────────────┘
```

### KPI Cards (top row, 4 cards)
Each card: dark panel (#20222B), with metric name, big number, delta vs previous period.

| Metric | Value | Delta | Color |
|--------|-------|-------|-------|
| Engagement Rate | 73.2% | +5.1% ↑ | Green |
| Completion Rate | 41.8% | -2.3% ↓ | Red |
| CTA Click Rate | 18.4% | +1.2% ↑ | Green |
| IPM (Installs/Mille) | 12.6 | -3.8 ↓ | Red |

### Engagement Funnel
Vertical funnel visualization showing user flow:
```
Ad Loaded:        100%  ████████████████████  (52,400 sessions)
First Interaction: 73%  ██████████████████    (38,252)
Tutorial Start:    68%  █████████████████     (35,632)
Tutorial Complete: 49%  ████████████          (25,676)  ← notable drop
Game Start:        47%  ███████████           (24,628)
Game Win:          38%  █████████             (19,912)
CTA Shown:         36%  ████████              (18,864)
CTA Click:         18%  ████                  ( 9,432)
Store Redirect:    16%  ███                   ( 8,384)
```

Key visual: **RED highlight on Tutorial Start → Tutorial Complete** drop (68% → 49% = -19pp) and **Game Win → CTA Click** drop (38% → 18% = -20pp).

### Performance Over Time (Line Chart)
X-axis: Mar 1–31, daily
Y-axis: dual axis — ER% (left), IPM (right)
Two lines:
- Gold line: Engagement Rate (hovers around 70–75%)
- Violet line: IPM (starts at 16, gradually drops to 9 by end of month — creative fatigue)

### Drop-off Analysis (Horizontal Bar Chart)
Shows the % drop at each funnel step:
- Ad Loaded → First Interaction: -27%
- First Interaction → Tutorial Start: -5%
- Tutorial Start → Tutorial Complete: **-19%** (RED, highlighted)
- Tutorial Complete → Game Start: -2%
- Game Start → Game Win: -9%
- Game Win → CTA Shown: -2%
- CTA Shown → CTA Click: **-18%** (RED, highlighted)
- CTA Click → Store Redirect: -2%

### Network Comparison Table
| Metric | AppLovin | Meta | Google |
|--------|----------|------|--------|
| Impressions | 34,200 | 12,800 | 5,400 |
| ER | 76.1% | 68.3% | 71.0% |
| IPM | 14.2 | 9.8 | 11.1 |
| CPI | $1.82 | $2.41 | $2.15 |
| CTA Click Rate | 19.8% | 15.2% | 17.6% |

### Event Timeline (bottom)
Horizontal timeline showing average user journey:
`[Load 0s] → [First Touch 1.2s] → [Tutorial 2.8s] → [Game 8.4s] → [Win 14.1s] → [CTA 15.3s] → [Click 17.8s]`
With average duration between each step shown.

---

## Tab 2: Insights (Level 2 — AI Recommendations)

This tab combines a summary view with AI-generated insights. Think Google Analytics Intelligence panel.

### Layout
```
┌──────────────────────────────────────────┬──────────────┐
│  Summary Cards (3)                       │  AI Insights │
├──────────────────────────────────────────┤  Panel       │
│  Detailed Insight Cards                  │  (scrollable │
│  (expandable, scrollable)                │   chat-like) │
│                                          │              │
│  [Insight 1: Tutorial Drop-off]          │  "Ask AI"    │
│  [Insight 2: Win Rate Problem]           │  input at    │
│  [Insight 3: CTA Optimization]           │  bottom      │
│  [Insight 4: Creative Fatigue]           │              │
│  [Insight 5: Geo Variation]              │              │
└──────────────────────────────────────────┴──────────────┘
```

### Summary Cards (top, 3 cards)
| Card | Icon | Title | Description |
|------|------|-------|-------------|
| 🔴 Critical | ⚠️ | 2 Critical Issues | Tutorial drop-off and CTA underperformance need immediate attention |
| 🟡 Opportunities | 💡 | 3 Opportunities | Difficulty tuning, geo-targeting, CTA A/B testing |
| 🟢 Strengths | ✓ | 4 Strengths | Strong engagement hook, good AppLovin performance, visual appeal |

### Detailed Insight Cards (main area, left)

Each card has: severity badge (Critical/Warning/Info), title, analysis text, chart/data snippet, recommended action, "Apply Fix" button (gold).

**Insight 1 — Critical: Tutorial Drop-off (19% loss)**
```
Analysis: 19% of users drop off between Tutorial Start and Tutorial Complete.
The current tutorial has 3 steps with text instructions. Playables with 1-step
visual tutorials in the same genre show 8% average drop-off.

Data:
- Current: 3 steps, text-based → 19% drop
- Benchmark (casual platformers): 1 step, visual → 8% drop
- Estimated impact: +5,800 users reaching game start per month

Recommendation: Reduce tutorial to 1 visual step showing tap-to-jump gesture.
[Apply to Playable →]
```

**Insight 2 — Critical: "Satisfaction Trap" after Win (20% loss)**
```
Analysis: 38% of users win the game, but only 18% click CTA. Users who WIN
feel satisfied and don't need to install. This is the "Satisfaction Trap" —
the playable is too complete an experience.

Data:
- Win → CTA Click: only 47% conversion
- Lose → CTA Click: 72% conversion (users who lose WANT to continue)
- Optimal win rate for casual platformers: 55-65%

Recommendation: Increase difficulty so win rate drops to ~60%.
Add "Level 2 awaits!" teaser after win to create curiosity gap.
[Apply to Playable →]
```

**Insight 3 — Warning: CTA Text Underperformance**
```
Analysis: "Download Now" CTA performs 23% below industry benchmark for casual games.
Action-oriented CTAs ("Continue Playing", "Play Full Game") consistently outperform
download-focused CTAs in playable ads.

Recommendation: Change CTA to "Continue Your Adventure →"
[Apply to Playable →]
```

**Insight 4 — Warning: Creative Fatigue Detected**
```
Analysis: IPM has declined 44% over 30 days (16.0 → 8.9). This matches typical
creative fatigue patterns. Refresh cycle needed every 2-3 weeks for this genre.

Recommendation: Generate 3 visual variants with different themes/backgrounds.
[Generate Variants →]
```

**Insight 5 — Info: Geo Performance Variation**
```
Analysis: US performs 2.1x better than LATAM on IPM but costs 3.4x more per install.
LATAM has untapped potential with localized CTA text.

Recommendation: Create Spanish-language CTA variant for LATAM markets.
[Create Localized Variant →]
```

### AI Insights Panel (right sidebar, chat-like)

A scrollable chat-style panel with pre-filled AI messages:

```
🤖 Code Maestro AI
━━━━━━━━━━━━━━━━━━
I've analyzed 52,400 sessions for "Pixel Quest"
playable ad. Here's what I found:

📊 Your playable has STRONG engagement (73% ER)
but WEAK conversion (12.6 IPM). The gap is caused
by two critical issues:

1. Tutorial friction — losing 19% of users
2. Satisfaction trap — winners don't convert

Together, fixing these could increase IPM by
an estimated 40-60%.

━━━━━━━━━━━━━━━━━━
💡 Quick wins available:
• Simplify tutorial (est. +5,800 users/mo)
• Adjust difficulty (est. +3,200 installs/mo)
• Update CTA text (est. +12% CTR)

Want me to generate optimized variants?
━━━━━━━━━━━━━━━━━━
```

At the bottom: input field "Ask about your analytics..." (disabled in prototype, with placeholder text)

---

## Tab 3: Hypothesis Lab (Level 3 — AI Self-Learning)

This is the most forward-looking feature. The AI doesn't just analyze — it proposes experiments, generates playable variants, and learns from results.

### Layout
```
┌─────────────────────────────────────────────────────────┐
│  Active Experiments Status Bar (horizontal)              │
├────────────────────────────┬────────────────────────────┤
│  Experiment Cards          │  Learning Feed             │
│  (main area)               │  (right panel)             │
│                            │                            │
│  [Exp 1: Tutorial Fix]     │  "What AI learned"         │
│  [Exp 2: Difficulty Tune]  │  timeline of validated     │
│  [Exp 3: CTA Variants]     │  insights                  │
│                            │                            │
├────────────────────────────┤                            │
│  Generated Variants        │                            │
│  Preview                   │                            │
└────────────────────────────┴────────────────────────────┘
```

### Active Experiments Status Bar
Horizontal bar showing:
- 🟢 Running: 2 experiments
- ✅ Completed: 1 experiment
- 📋 Queued: 3 experiments
- 🧠 Insights validated: 7 total

### Experiment Cards

**Experiment 1 — COMPLETED ✅**
```
Hypothesis: Reducing tutorial from 3 steps to 1 visual step will
decrease tutorial drop-off from 19% to <10%.

Status: COMPLETED — Hypothesis CONFIRMED ✓

Results:
┌──────────────┬──────────┬──────────┐
│              │ Original │ Variant  │
├──────────────┼──────────┼──────────┤
│ Tutorial drop│  19.0%   │   7.2%   │  ← 62% improvement
│ Completion   │  41.8%   │  53.1%   │
│ IPM          │  12.6    │  16.8    │  ← +33% 🎉
│ Sessions     │  26,200  │  26,200  │
└──────────────┴──────────┴──────────┘

AI Learning: "Single-step visual tutorials outperform multi-step text
tutorials for casual platformers. Applied to knowledge base."

[View Variant] [Apply as Default →]
```

**Experiment 2 — RUNNING 🟢 (Day 5 of 7)**
```
Hypothesis: Increasing difficulty to achieve ~60% win rate (from current 82%)
will increase CTA clicks by 25%+.

Status: RUNNING — Early results promising

Progress: ████████████░░░░  Day 5/7, 18,400 sessions collected

Preliminary Results:
┌──────────────┬──────────┬──────────┐
│              │ Original │ Variant  │
├──────────────┼──────────┼──────────┤
│ Win Rate     │  82.0%   │  61.3%   │  ← on target
│ CTA Click    │  18.4%   │  26.1%   │  ← +42% so far
│ IPM          │  12.6    │  17.2    │  ← +37% 🔥
│ Confidence   │   —      │  94.2%   │
└──────────────┴──────────┴──────────┘

[Pause Experiment] [View Live Data]
```

**Experiment 3 — RUNNING 🟢 (Day 2 of 7)**
```
Hypothesis: "Continue Your Adventure →" CTA will outperform "Download Now"
by 15%+ on CTA click rate.

Status: RUNNING — Collecting data

Progress: ████░░░░░░░░░░░░  Day 2/7, 8,100 sessions

[View Details]
```

### Generated Variants Preview (bottom)
Shows 3 thumbnail previews of AI-generated playable variants:
1. "Tutorial-Optimized" — 1-step visual tutorial (green "Applied" badge)
2. "Difficulty-Tuned" — harder gameplay, 60% target win rate (yellow "Testing" badge)
3. "CTA-Optimized" — new CTA text + larger button (yellow "Testing" badge)

Each thumbnail is a dark card with a small preview image area (placeholder) and metadata.

### Learning Feed (right panel)
Scrollable timeline of validated AI learnings:

```
🧠 Knowledge Base — 7 validated insights

[Mar 28] ✅ CONFIRMED
"1-step visual tutorials reduce drop-off by 62%
vs 3-step text tutorials for casual platformers"
Confidence: 99.1% | Based on: 52,400 sessions

[Mar 25] ✅ CONFIRMED
"Countdown timers increase engagement +18% in
casual genres but hurt mid-core (-8%)"
Confidence: 97.3% | Based on: 34,100 sessions

[Mar 22] ❌ REJECTED
"Adding score multiplier increases play duration"
Result: No significant effect (p=0.43)

[Mar 18] ✅ CONFIRMED
"Portrait orientation outperforms landscape by 12%
on Meta, but landscape wins on AppLovin by 8%"
Confidence: 96.8% | Based on: 41,200 sessions

[Mar 15] ✅ CONFIRMED
"Gold CTA buttons outperform green by 9% on
dark backgrounds"
Confidence: 95.1% | Based on: 28,400 sessions

... (more entries)
```

---

## Tab 4: Setup (Supplementary — Event Configuration)

Shows how events are configured in the playable. This tab is informational, showing the connection between the playable editor and analytics.

### Layout
Simple list view showing configured events:

```
Event Configuration — Pixel Quest Playable
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Standard Events (auto-tracked) ✓
  ☑ ad_loaded
  ☑ ad_ready
  ☑ first_interaction
  ☑ cta_shown
  ☑ cta_click
  ☑ store_redirect

Custom Events (configured)
  ☑ tutorial_start        — Trigger: Tutorial overlay appears
  ☑ tutorial_step          — Trigger: Each step completion {step: 1|2|3}
  ☑ tutorial_complete     — Trigger: Tutorial dismissed
  ☑ game_start            — Trigger: First gameplay input
  ☑ enemy_defeated        — Trigger: Koopa/Goomba collision {enemy_type}
  ☑ coin_collected        — Trigger: Coin pickup {count}
  ☑ game_win              — Trigger: Level flag reached
  ☑ game_lose             — Trigger: Lives = 0

Code snippet (read-only):
  CodeMaestro.track("tutorial_step", { step: 2, duration_ms: 1200 });

Integration Status:
  ✅ AppLovin — Connected, receiving events
  ✅ Meta — Connected, receiving events
  ⏳ Google — Pending setup
```

---

## Design Tokens

### Colors (from Code Maestro brand)
```css
--bg-primary: #05070F;       /* Main background */
--bg-secondary: #080B15;     /* Alternate dark bg */
--bg-card: #20222B;          /* Cards, panels */
--bg-surface: #161823;       /* Surface layer */
--border: #36383E;           /* Borders, dividers */
--text-primary: #FAFAFA;     /* Primary text */
--text-secondary: #EEEEEE;   /* Secondary text */
--text-muted: #737373;       /* Muted text */
--accent-gold: #FCBC16;      /* Primary accent */
--accent-gold-light: #FCC344; /* Gold hover */
--accent-orange: #F57A3F;    /* Warm accent */
--accent-violet: #6848D1;    /* Secondary accent */
--accent-violet-light: #6969DD; /* Violet hover */
--accent-magenta: #B0308C;   /* Special accent */
--accent-blue: #206BCE;      /* Info elements */
--accent-red: #E72D53;       /* Errors, critical */
--success: #22C55E;          /* Positive metrics */
--warning: #F59E0B;          /* Warning states */
```

### Typography
```css
/* Headings */
font-family: 'Inter', Arial, sans-serif;
font-weight: 700;

/* Body text */
font-family: 'Montserrat', Arial, sans-serif;
font-weight: 400;
```

### UI Patterns
- Border radius: 8px for cards, 6px for buttons, 12px for modals
- Card shadow: 0 2px 8px rgba(0,0,0,0.3)
- Active tab: left border 3px solid #FCBC16
- Hover state: background lightens to #2A2C35
- Scrollbar: thin, #36383E track, #6848D1 thumb
- Charts: gold (#FCBC16) primary line, violet (#6848D1) secondary line, red (#E72D53) for issues

### Component Patterns (matching Code Maestro UI)
- **Left sidebar**: 240px wide, bg #080B15, items have icon + label
- **Top bar**: 56px height, bg #0A0D17, border-bottom #36383E
- **Cards**: bg #20222B, border 1px solid #36383E, padding 20px
- **Tables**: header bg #161823, alternating rows #20222B / #1A1C26
- **Buttons primary**: bg gradient #6848D1 → #6969DD, text white
- **Buttons accent**: bg #FCBC16, text #05070F (dark)
- **Badge critical**: bg #E72D53 with 20% opacity, text #E72D53
- **Badge warning**: bg #F59E0B with 20% opacity, text #F59E0B
- **Badge success**: bg #22C55E with 20% opacity, text #22C55E
- **Badge info**: bg #6848D1 with 20% opacity, text #6969DD

---

## Responsive Behavior

Prototype is designed for **desktop demo only** (1440px+ width). No mobile responsiveness needed. If window is too narrow, show a "Best viewed at 1440px+ width" notice.

---

## Libraries (CDN)

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Montserrat:wght@400;500;600&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
```

No other external dependencies. Pure HTML + CSS + vanilla JS.

---

## File Output

Single file: `index.html` — contains all HTML, CSS, and JavaScript inline. Open directly in browser.
