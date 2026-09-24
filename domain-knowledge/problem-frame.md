# Scenario 3: problem frame

Draft, 2026-09-24. Working notes for our small group at the Explore DDD 2026 Design
Storm. It frames the problem before we pick a build. Every number here is computed
from files in this repo; the readings are provisional (see [Data terms](#data-terms)).

## The ask, in Denver Water's words

From Cassidi Rosenkrance's kickoff ([transcript](denver-water-expert-raw.md)):

> "At Denver Water, we actually have full teams who model this every single day. They
> take historicals and basically predict out next year, 5 years, 10 years, what a wet
> year, a dry year, and an average year might look like. And then begin to make
> predictions on how we might move the water, what sources we might use. Kind of the
> next step in that is how do we pair water quality with that, right? … It kind of
> breaks down that barrier of water quantity versus quality."

And on 2026:

> "Typically we see runoff end of May, early June. We saw peak runoff to our streams in
> the end of March … we actually drained certain reservoirs … We pulled in alternative
> sources where we don't have the best water quality, but we have reliable amounts of
> water to pull from."

## Problem statement

Denver Water already plans water **quantity** by [year type](#year-type) (dry, average,
wet). It has
no matching view of water **quality**. When planners expect a dry year, nobody can
point to what that year will mean for the water arriving at the treatment plants, or
when.

> For a dry, average or wet year, show how the size and timing of the snowpack, and the
> sources Denver Water leans on, turn into TOC and alkalinity at the plants, so the
> quality impact sits beside the quantity plan.

### Why TOC and alkalinity

From Cassidi's primer (`reference/TOC_and_Alkalinity_Summary.pdf`): below **60 mg/L
alkalinity** a plant must remove **35%** of TOC; above it, **25%**. Water that swings
around that line forces plants to change their chemical dosing on the fly, which costs
money and adds regulatory risk.

## Who it is for

| Who | What they need from us |
|---|---|
| Water Quality & Treatment (Cassidi, Jake) | The quality side of dry/average/wet years, in the planners' vocabulary. Primary audience. |
| Supply planners | A quality consequence attached to the scenarios they already build. |
| Plant operators | Which weeks of the year to expect low alkalinity or high TOC. Secondary; Scenario 1 serves them more directly. |

## Questions the model should answer

Ranked by value to Denver Water.

1. **What does a year type do to plant water quality?** For a year with a given snowpack
   size and melt timing, how many days below 60 alkalinity and above 4 TOC should
   Foothills expect, and in which weeks?
2. **How long does the signal take to reach the plant?** From snow peak to runoff to
   a change in water quality at the plant, how many days at each step, and how does
   that shift in an early-melt year like 2026?
3. **Which past years look like this one?** Rank years by snowpack to find analogs, and
   show what the plants received in those years.

## What the data already shows

### Snowpack: 2026 is the extreme

Mean of 11 SNOTEL stations' peak SWE as a percent of each station's median peak
(`water-system-3d/snotel-history.json`):

- WY 2026: **54%** of median, rank **1 of 46** (1981 to 2026, least snow first).
- Peak came on average **27 days earlier** than the median peak day.
- Basin-average SWE peaked **Mar 16, 2026**; the median peak is **Apr 23**.
- Closest analog years by snowpack: 2002 (60%), 1981 (61%), 2012 (66%).

### Quality at Foothills: the dry year looks different

Apr to Aug days at the Foothills plant intake (`data/FoothillsInfluent.csv`):

| WY | Days with alkalinity < 60 | Days with TOC > 4 mg/L |
|---|---|---|
| 2022 | 103 of 153 (67%) | 0 |
| 2023 | 122 of 153 (80%) | 32 |
| 2024 | 98 of 153 (64%) | 39 |
| 2025 | 74 of 153 (48%) | 0 |
| 2026 | 33 of 141 (23%) | 0 |

Monthly means show the same pattern. In 2023 and 2024, TOC rose above 4 mg/L in May
and June during runoff. In 2026, TOC stayed near 2.2 mg/L all season, and alkalinity
stayed near or above 60 without the June dip seen in 2022 and 2025.

## Why the data can't prove the snow → quality link yet

These can mislead us. Say them out loud at the report-out.

1. **Denver Water changed its sources in 2026.** In 2026 Denver Water drained
   reservoirs and pulled from alternative sources. The 2026 quality change could come
   from which sources fed Foothills, not from the snowpack. The repo has no data on
   which sources were used. See [QUESTIONS.md](QUESTIONS.md) #1.
2. **The March 2026 runoff peak is missing from the quality data.** The Foothills file
   has no January to March rows in any year (the river sensor is pulled for winter),
   and the late-March peak falls in that gap.
3. **The river gage we have is below the reservoirs.** DWR PLASPLCO (South Platte at
   South Platte) sits on the mainstem below Antero, Eleven Mile and Cheesman reservoirs,
   so its flow mostly shows how those reservoirs were released. Its 2026 peak was Jul 18 at 620
   cfs, not late March. For natural runoff we need a gage with no reservoir upstream.
4. **Five years of quality data.** Enough to describe a pattern, not to prove a cause
   or make a prediction. We don't need machine learning for this.

## Data inventory

| Data | Covers | Where | Use |
|---|---|---|---|
| SNOTEL SWE, 11 stations | WY 1980 to 2026, daily | `water-system-3d/snotel-history.json` | Snowpack size and timing |
| Reservoir storage: Dillon, Cheesman, Chatfield, Strontia | ~1987 to 2026 (Strontia 2021+), daily | `water-system-3d/storage-history.json` | Quantity context |
| South Platte flow, PLASPLCO | Apr 2022 to Aug 2026, daily | `data/SouthPlatteFlow.csv` | Released flow, not natural runoff |
| USGS water quality above Strontia | 2022 to 2026, daily, with gaps | `data/USGS_South_Platte.csv` | Turbidity, conductance, temperature in the river |
| Foothills influent TOC, alkalinity | Apr to fall each year, Apr 2022 to Aug 2026; no Jan to Mar | `data/FoothillsInfluent.csv` | The outcome we care about |
| Strontia profiling sonde | Apr 7 to Aug 19, 2026 | `data/Strontia 0407_0819.xlsx` | Reservoir depth profiles, drought year only |
| NOAA daily weather | 2022 to 2026 | `data/USC00058022.csv` | Rain, temperature (the March heat) |

To get:

- **Sources feeding Foothills by year**, from Denver Water. Decides confound 1.
- **An unregulated gage** on the South Platte or a tributary, from USGS NWIS or DWR.
  Solves confound 3. Candidate not yet identified.
- **Longer PLASPLCO history**, from the DWR API (`scripts/DWR_gage_grabber.ipynb`).
  Only needed if we keep showing released flow.

## Solution space

Proof of concept of options A to C, quantity only:
[South Platte Water Years](https://claude.ai/artifact/EyoHDXGDRnmyueWTdYam6a) (private).
Each adds a time dimension to the existing 3D map.

| Option | What it is | Answers | Value | Effort | Data gap |
|---|---|---|---|---|---|
| A. Two-year compare | Split map markers, Year A and Year B, day slider | How far apart are a dry year and a wet year on a given date? | Medium | Low | None |
| B. Follow the water | Play a water year; snow melts, river flows, reservoirs fill | When does snow become runoff? | Medium, strong demo | Medium | Needs an unregulated gage |
| C. Year atlas | 46 years ranked by snowpack; analog years | Which past years look like this one? | Medium | Low to medium | None |
| D. Quality overlay | Add Foothills TOC and alkalinity to A or C: days < 60 alkalinity per year, weeks of TOC > 4 | What does this year type mean at the plant? | **High**, the "next step" Cassidi named | Low | Sources (confound 1) |
| E. Year-type card | Pick dry, average or wet; show analog years' snow timing and quality outcome side by side | The planners' question, answered in their words | **High** | Medium | Only 5 years of quality data |

Proof of concept of a quality-against-flow view:
[Foothills Intake Explorer](https://claude.ai/artifact/SKHeCDmnw581Cet88Vd7LL) (private).
TOC or alkalinity against flow, one panel per water year, dots colored by date, with
flow location, lag and a what-if flow slider. Flow for gauges other than PLASPLCO was
pulled from the DWR telemetry API on 2026-09-24.

Tentative direction: **C + D, presented as E.** Find analog years from snowpack, then
show what quality they delivered. Use A or B only if time allows.

## DDD terms

The shared vocabulary for this model: words to use the same way in code, UI and
conversation. Water and statistics terms (SWE, cfs, water year, TOC, baseflow, MAE)
are defined in [`glossary.md`](../glossary.md), which Denver Water has vetted. This
section adds terms the model needs, and says where each one comes from.

Status: **Denver Water** = their word, used as they use it. **Ours** = a term we made
up; provisional until Denver Water confirms or replaces it.

### Year type

**Status:** ours, provisional.

The kind of water year the supply planners plan for. Cassidi described the planners
modeling "a wet year, a dry year, and an average year"; the Scenario 3 slide says
"drought vs wet years." Neither names the concept, and nothing in the materials
defines the categories.

- **Values:** wet, average, dry (from Cassidi's wording). The real set may have more
  categories.
- **Defined by:** unknown. Could be snowpack, streamflow, percent of median, or the
  planners' own models.
- **Open:** [QUESTIONS.md](QUESTIONS.md) #2 asks Denver Water for their term and
  definition. Until they answer, any stand-in we compute is labeled as ours.

Hypothesis for DDD discussion: supply planning (quantity, sources) and water quality
and treatment are separate bounded contexts. Our model sits on the seam between them,
and year type is the concept they could share.

### Other terms

| Term | Status | Meaning here |
|---|---|---|
| Water year (WY) | Denver Water | Oct 1 to Sep 30, named for the year it ends. See glossary. |
| Snowpack, SWE | Denver Water | Water held in snow, in inches. See glossary. |
| Runoff | Denver Water | Snowmelt reaching streams. Not the same as flow at a gage below a reservoir. |
| Source | Denver Water | Where a plant's water came from in a season: a reservoir or river system. |
| Influent | Denver Water | Water arriving at the plant, before treatment. |
| Removal requirement | Denver Water | The required TOC removal, 35% below 60 mg/L alkalinity and 25% above, from Cassidi's primer. |

## Open questions

Tracked with the reason for each and space for answers in
[QUESTIONS.md](QUESTIONS.md).

## Data terms

Denver Water's two notices apply to this document and anything derived from the data.
Full text: [`data/TERMS.md`](../data/TERMS.md). Readings are provisional and subject
to change. Redistribution is restricted.
