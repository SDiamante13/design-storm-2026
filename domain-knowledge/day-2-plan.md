# Day 2 plan: 3.5 hours to a report-out

Revised 2026-09-24 evening, after the debrief with Cassidi
([raw](debrief-session-raw.md), [summary](debrief-session-summary.md)) and our working
session ([raw](working-session-raw-09-24-26.md),
[summary](working-session-summary-09-24-26.md)). Starts 9:00 on Sep 25; Cassidi and
Jake are both in the room.

## What the debrief changed

| Before the debrief we thought | Cassidi said |
|---|---|
| We had to choose between a seasonal outlook and a 12-hour alert. | Her biggest problem is **no visualization**: "we don't have visualization on this." The goal is a digital twin that tells "the story" of different conditions across the organization, looking ahead, not just at now or the past. |
| One audience: plant operators. | **Three audiences** looking at the same water: the water quantity team (about 50 people: how much, how to move it, water rights), her watershed scientists (quality, regulation, stewardship), and the plants (what's arriving, how to treat it at least cost). |
| We'd have to ask for a real event. | She named one: a **100-year storm in the South Platte in 2023**. They knew it was coming but not its scale. Turbidity nearly shut the plant down; filters went offline for cleaning and the plant slowed the water it could deliver. That was the trigger to "look at ahead of time." |
| The cost of a bad week was unknown. | Treatment chemicals cost "hundreds of millions of dollars." |
| Forecasting might exist somewhere. | Weather and radar feed only the big-picture quantity estimates, "not for looking at a point in a stream." Quality monitoring is real-time or historical only. |

## What the data shows for 2023

Computed from the repo files (provisional readings). We don't know which of these is the
100-year storm. **Ask Cassidi.**

- **May 11–12, 2023:** turbidity above Strontia reached 185 NTU (daily max). TOC at
  Foothills peaked at 7.3 mg/L on May 19–20, about a week later. That's the highest TOC
  in the five years.
- **Aug 1, 2023:** turbidity above Strontia reached 477 NTU, the highest daily max in
  the file.
- Flow at PLASPLCO peaked Jun 17 at 1,090 cfs, which is snowmelt plus releases, not the
  storm.

## Direction

**One view of the water, three lenses, anchored on 2023.** The Intake Explorer already
has the shared skeleton: map, route, water years, flow, and quality at the plant. Day 2
turns it into the story Cassidi asked for:

1. **Replay 2023** (the demo moment). A stacked timeline, one shared date axis, top to
   bottom in flow order: snow at the basin's SNOTEL stations, flow along the route,
   turbidity above Strontia, TOC and alkalinity at Foothills. Mark each peak and the days
   between them. Question it answers: *what did the system show before the plant got
   hit?*
2. **Regime per water year**, now including storms. Label each year by what dominated:
   snowmelt (snowpack size and peak timing) or storm (count of turbidity spikes above a
   threshold we choose). 2023 is both. The glossary's **regime** is the term, and the
   labels stay provisional until the planners give us theirs.
3. **Hard weeks calendar.** One row per water year, one cell per week: weeks with
   alkalinity below 60 mg/L, TOC above 4 mg/L, or a turbidity spike. Answers "which
   weeks should we expect trouble?" for the plant and quality teams.
4. **Three lenses** (stretch). A toggle for quantity, quality or plant that reorders the
   same page for each audience. It's also the DDD story: three bounded contexts sharing
   one model of the water.

Dropped or deferred:
- **Projection:** only 5 years of quality data, so it moves to "next step." If time
  allows, reuse the analog years from the first POC.
- **12-hour alert:** it needs continuous data at the plant intake. Present it as the next
  step after the 2023 replay, which shows how much warning the river sensor gave.
- **Scenario 2 overlap:** the group wanted storms kept out, but Cassidi's own example is
  a storm. Storms stay in only as a regime label and in the 2023 replay; depth profiles
  and in-reservoir modeling stay out.

## Schedule

| Time | What | Who |
|---|---|---|
| 9:00–9:15 | Laptops working (personal laptop for the Ford proxy). Everyone reads this page. | All |
| 9:15–9:35 | Ask Cassidi and Jake the open questions in [QUESTIONS.md](QUESTIONS.md). First: which 2023 date was the storm. | One person |
| 9:15–9:45 | On the wall: the three contexts (quantity, quality, plant), what each needs to see, and the shared terms (water year, regime, gauge, route, sample, removal requirement, lag). | Other two |
| 9:45–11:30 | Build in parallel: (1) 2023 replay, (2) regime labels + hard weeks calendar, (3) data script for the DWR and NLDI pulls, then the lenses toggle if time. Merge every 30 minutes. | Split |
| 11:30–12:00 | Put it together. Screenshot, then "find 3 things to improve" passes. Show Cassidi or Jake for 5 minutes and fix one thing they say. | All |
| 12:00–12:30 | Rehearse the report-out twice. | All |

## Acceptance checks

- **2023 replay:** all tracks share one date axis; no chart has two y-axes. Each peak is
  labeled with its date and value from the files. Missing data shows as a gap, never
  a zero.
- **Regime:** each water year shows snowpack % of median, snow peak shift in days, and
  number of turbidity spike days, with a provisional label.
- **Hard weeks:** weeks with no samples show as empty. The 60 mg/L and 4 mg/L lines
  are named on the page.
- **Everything:** real numbers only, Denver Water's notices kept, "provisional" stated.

## Report-out (3 minutes)

1. **Their words:** "we don't have visualization on this"; three teams looking at the
   same water; the 2023 storm.
2. **Replay 2023:** snow, flow, turbidity, TOC in one view, and how many days of warning
   the river gave before TOC peaked at the plant.
3. **Regimes and hard weeks:** 2023 vs 2026, snowmelt vs storm vs drought.
4. **DDD:** three bounded contexts, one shared model of the water; regime as a domain
   term we learned from the glossary, not invented.
5. **Limits and next step:** 5 years; daily hand samples; 2026 source switching. Next:
   continuous intake data for a 12-hour warning.
