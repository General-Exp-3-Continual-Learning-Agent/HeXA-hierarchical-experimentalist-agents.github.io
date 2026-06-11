# Assets to provide

Every item below is currently a labeled placeholder in `index.html`. Drop the file at the
listed path and swap the placeholder `<div>` for an `<img>`/`<video>`. Paths are referenced
exactly as written in the HTML, so matching the filename means zero further edits.

## Figures (export from the paper)

| Path | Paper ref | What it is |
|------|-----------|------------|
| `teaser.png` | Figure 1 | Overview: ReAct vs. HeXA meta-episode vs. cross-level transfer (1600–2000px wide) |
| `loop.png` | Figure 2 / 7 | The actor → evolver → retriever loop (one round) |
| `transfer.png` | Figure 1c | Source banks synthesised into a cross-level bank for catapult |
| `og-card.png` | — | 1200×630 social-share preview card |

## Level gallery — `assets/levels/`

Looping GIF or muted autoplay MP4 of each level being solved (≈4–8s, 480–640px wide).
Static initial-state PNGs (paper Figure 14) also work.

`catapult.gif` · `pass_the_parcel.gif` · `down_to_earth.gif` · `two_body_problem.gif`
· `falling_into_place.gif` · `tipping_point.gif` · `basket_case.gif` · `cliffhanger.gif`

(Optional extras the paper names: `marble_race`, `seesaw`, `the_cradle`, `keyhole`.)

## Episode walkthrough (catapult seed 45)

| Path | Paper ref | What it is |
|------|-----------|------------|
| `trace_react.gif` | Figure 3, top row | ReAct failure: steps 0 → 193, never makes green–blue contact |
| `trace_hexa.gif` | Figure 3, bottom row | HeXA success: lever flings green ball over the blocker into the basket |

## Charts — `assets/charts/`

| Path | Paper ref | What it is |
|------|-----------|------------|
| `catapult_cumulative.png` | Figure 4 | Cumulative success: HeXA / HeXA no-reward / Reflexion |
| `ptp_cumulative.png` | Figure 5 | Pass the Parcel variants vs. ReAct |
| `open_weight.png` | Figure 10 | Open-weight bar charts (DTE, TBP, catapult) |
| `grpo.png` | Figure 11 | GRPO training dynamics vs. HeXA |

## How to swap a placeholder

Find the placeholder div, e.g.:

```html
<div class="level-media" aria-label="catapult animation placeholder">→ assets/levels/catapult.gif</div>
```

Replace with:

```html
<img src="assets/levels/catapult.gif" alt="catapult level being solved" />
<!-- or, for video: -->
<video src="assets/levels/catapult.mp4" autoplay muted loop playsinline></video>
```

## Still TODO (text, not media)

- Real author names / affiliations / links (`<div class="authors">`, `<div class="affiliations">`)
- Paper / arXiv / Code / InterPhyre button URLs (`<div class="links">`)
- Final BibTeX entry
- More skill/mistake entries in the Skill Bank section (copy a `<details class="skill">` block)
