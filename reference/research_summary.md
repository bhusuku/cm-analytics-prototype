# Research Summary — Playable Ads Analytics Market

This file contains key findings from the competitive analysis for reference during prototype development.

## Competitor Landscape

| Solution | Type | Built-in Analytics | AI Recommendations | Custom Events |
|----------|------|-------------------|-------------------|---------------|
| Unity Playworks (Luna Labs) | Creator + Analytics | Yes | No | Yes (256 limit) |
| Sett.ai | AI Analytics | External | Yes | Yes |
| Segwise | AI Tagging | External | Yes | No |
| Playable Factory | Creator + Analytics | Yes | No | Limited |
| Axon (AppLovin) | Ad Network | Partial | Campaign-level | Basic |

## Key Gap in Market

**No platform offers the full closed loop: Create → Analyze → Recommend → Auto-optimize within one product.** This is Code Maestro's opportunity.

## Standard Playable Events (industry standard)
- ad_loaded, ad_ready, first_interaction
- tutorial_start, tutorial_step, tutorial_complete
- game_start, game_win, game_lose
- cta_shown, cta_click, store_redirect

## Key Metrics (3 levels)

### In-Playable
- Engagement Rate (ER), Time to First Interaction, Play Duration
- Completion Rate, Win/Lose Rate, Event Funnel Drop-off
- Heatmap data, CTA Click Rate

### Campaign-Level
- CTR, IPM, CPI, CVR, CPM

### Post-Install
- ROAS, Retention (D1/D7/D30), LTV, In-App Events

## Industry Benchmarks (approximate)
- Playable ads: 319% higher conversion vs video ads
- Average ER for casual games: 65-75%
- Tutorial drop-off benchmark: 5-10%
- Optimal win rate: 55-65% for casual platformers
- Creative fatigue onset: 2-3 weeks
- AppLovin controls 59% of playable traffic

## Technical Architecture (MRAID 3.0)
- Playable = HTML5 app inside WebView
- Communication via MRAID JavaScript bridge
- Events sent via navigator.sendBeacon() or XMLHttpRequest
- Data format: JSON {playable_id, session_id, event_name, properties, timestamp, context}
