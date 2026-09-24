# Day 2 plan: 3.5 hours to a season-ahead projection

Revised 2026-09-24 evening. Priority set by the group: **make forecasting possible.**
Sources: the debrief with Cassidi ([raw](debrief-session-raw.md),
[summary](debrief-session-summary.md)) and our working session
([raw](working-session-raw-09-24-26.md), [summary](working-session-summary-09-24-26.md)).
Starts 9:00 on Sep 25; Cassidi and Jake are both in the room.

## What we're building

A **season-ahead projection**: given next water year's snowpack and melt timing, which
weeks at the Foothills plant are likely to be hard (alkalinity below 60 mg/L, TOC above
4 mg/L), and why.

Why this one:
- Cassidi's biggest pain is that everything is "real-time or historical"; she wants to
  "model these things ahead of time." Nobody forecasts quality at a point today.
- Planners already think in dry, average and wet years. A projection keyed on snowpack
  puts quality next to their quantity plan, which is the gap Scenario 3 names.
- It can be built from data we already have, with no machine learning, and it can
  explain itself.

What it is not: a 12-hour alert. That needs continuous data at the plant intake (see
[QUESTIONS.md](QUESTIONS.md) #7). It goes in the report-out as the next step.

## How the projection works

Three steps, each one visible on the page.

**1. Describe the year** (the input)
- Snow index: basin peak SWE as % of median (4 SNOTEL stations inside the South Platte
  basin: Buckskin Joe, Jackwhacker Gulch, Michigan Creek, Rough And Tumble).
- Peak shift: days the snow peaked before or after the median day.
- Presets from real years: dry like 2026 (index 54%, peak 27 days early, from the
  11-station atlas), wet like 2024, plus manual sliders.
- Later: fill these from live SNOTEL once WY 2027 snow starts on Oct 1.

**2. Find analog years** (the model)
- From WY 2022 to 2026 (the years with plant data), pick the closest by snow index and
  peak shift.
- Shift their weekly quality by the peak-shift difference, so an early-melt year moves
  the runoff weeks earlier.
- The projection is the blend of those analogs, shown as a band from lowest to highest,
  not a single line.

**3. Show the hard weeks** (the output)
- A **hard-weeks calendar**: one row per real water year (2022 to 2026) and one row for
  the projection. Each cell is one week, colored by median alkalinity or TOC. Weeks
  below 60 or above 4 are flagged.
- Next to the projected row: "expect N hard weeks, mostly in May–June; based on WY 2023
  and 2024 shifted 12 days earlier." No hidden math.

**Trust check: backtest.** Project each of 2022 to 2026 from the other four years and
compare with what actually happened, week by week. Show the score next to a naive
baseline (the average of all other years). If the projection doesn't beat the naive
baseline, say so. That result is worth reporting too.

**Stretch: snow to runoff with 40 years of data.** The SNOTEL history goes back to
1980, and DWR flow at the headwater creeks back to about 1985. Fit simple straight
lines for snow index to Apr–Jul runoff volume, and snow peak date to runoff peak date,
and show R². This sharpens step 2's timing shift and gives the quantity team their
view. It needs the DWR history pull, which hit the daily limit tonight, so it can't be
on the critical path.

## Slices, in build order

Each slice can be demoed on its own. The domain rules go in one small module of pure
functions with tests, since these rules are the model:

| Rule | Where it's used |
|---|---|
| Group by water year (Oct 1 to Sep 30), never calendar year | Everything |
| Weekly median of plant samples; weeks with no samples are empty, not zero | Calendar, analogs |
| Hard week: median alkalinity below 60 mg/L, or TOC above 4 mg/L | Calendar, backtest |
| Snow index and peak shift for a water year | Inputs, analogs |
| Closest analogs by snow index and peak shift | Projection |
| Shift a weekly series by N days | Projection |

**1. Hard-weeks calendar (history)** — 9:45–10:30
- Given the Foothills samples, each of WY 2022 to 2026 shows one row of weekly cells, Apr
  to Dec, with hard weeks flagged and a count per row.
- It's the foundation: the projection adds one more row.

**2. Projection row** — 10:30–11:15
- Presets and sliders for snow index and peak shift produce the projected row, its band,
  and the plain-language "why."
- Changing the inputs updates the row immediately.

**3. Backtest score** — 11:15–11:40
- Leave-one-year-out for 2022 to 2026: projected vs actual hard weeks, compared with the
  naive baseline, in a small table.

**4. Stretch, in this order:** snow-to-runoff fits (if the DWR pull works), then the 2023
storm replay (turbidity 185 NTU on May 11–12, 2023; TOC 7.3 mg/L at Foothills on May
19–20), then moving dots on the map.

Put the calendar and projection on the Intake Explorer page so the map and gauge
context stay.

## Schedule

| Time | What | Who |
|---|---|---|
| 9:00–9:15 | Laptops working (personal laptop for the Ford proxy). Everyone reads this page. | All |
| 9:15–9:35 | Questions for Cassidi and Jake ([QUESTIONS.md](QUESTIONS.md)), led by #10 and #11 on the projection. | One person |
| 9:15–9:30 | Kick off the DWR history pull once and save it to the repo, since the API has a daily limit. If it fails, drop the stretch fits. | One person |
| 9:15–9:45 | On the wall: the rules table above, the terms (water year, regime, analog year, hard week, projection, removal requirement), and the three teams (quantity, quality, plant). | Rest |
| 9:45–11:40 | Slices 1 to 3. One person on the rules module and tests, one on the page, one on data and backtest. Merge every 30 minutes. | Split |
| 11:40–12:00 | Show Cassidi or Jake the projection for 5 minutes and fix one thing they say. | All |
| 12:00–12:30 | Rehearse the report-out twice. | All |

## Report-out (3 minutes)

1. **Their words:** "we don't have visualization on this"; quality is "real-time or
   historical"; the 2023 storm that nearly shut the plant.
2. **Demo:** pick "dry like 2026" and "wet like 2024," and watch the hard weeks move.
   Read the "why."
3. **Can you trust it:** the backtest score against the naive baseline, stated plainly.
4. **DDD:** the rules module is the domain model: water year, hard week, regime,
   analog year. Three teams share it and each reads it differently.
5. **Limits and next step:** 5 years of plant data; 2026 source switching; weekly, not
   hourly. Next: live SNOTEL input for WY 2027, and continuous intake data for a 12-hour
   alert.

## Risks

- **Five years of plant data.** Analogs are thin. The backtest makes that visible;
  don't hide it.
- **DWR daily data limit.** Pull once, cache in the repo, and keep the stretch off the
  critical path.
- **2026 source switching.** 2026's quality may partly reflect operations. Label it.
- **Scope.** If slice 1 isn't done by 10:30, drop the stretch entirely.
