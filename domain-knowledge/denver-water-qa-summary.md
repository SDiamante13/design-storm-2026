# Q&A with Denver Water, Sep 24

Answers from Cassidi Rosenkrance (she refers to "Jake and I"). Raw transcript:
[denver-water-qa-raw.md](denver-water-qa-raw.md). The transcription garbles names:
"Strongfield Springs" means Strontia Springs.

## What matters for us

- **Their #1 problem is visualization.** Her ideal is a **digital twin**: one visual
  tool that models constituents, compares against historical years, and pulls in
  scattered datasets, cleaned up. That is Scenario 3.
- **The goal is to tell the story** of current conditions to people across the
  organization, not just to model.
- **Today everything is real time.** They look at the past or at what's happening
  now. Seeing ahead is the gap.

## Who the visualization is for

| Group | Focus |
|---|---|
| Water quantity team (~50 people) | How much water, how to move it, demand, water rights |
| Water quality + watershed scientists (Cassidi's team) | Quality, effects of moving water, regulation, environmental stewardship |
| Treatment plants | What's coming in right now, and how to treat it efficiently at the least cost. Chemicals cost "hundreds of millions" |

## Answers by topic

**Sensors**
- They're at some sites, not everywhere. Each one has a lat/long, so you can place it on
  the map relative to Strontia Springs and Foothills and "see the progression of water."

**Filling gaps in data (interpolation)**
- This is an open question for them too. The data is snapshots in time, and they ask
  "what are we missing in that story?"

**Pressure / radar in their models**
- Only in **water quantity** forecasting: historical data, real-time streamflow,
  snowpack, and SWE estimates, used to size storms.
- It's for the big picture ("what might we see this year?"), **not for acute events**
  or a single point on a stream.

**Non-technical problems**
- **Water rights** are legal and political. They must leave enough water for others
  downstream, and still serve their own customers.
- **Drought optics:** customers can water only 2 days a week, while crews flush hydrants
  to protect water quality. The public sees this as a double standard.
- **Parks and partners** may follow different rules because of separate agreements and
  MOUs.
- **Shared users:** rafting (a terrible year) and fisheries, which want certain flows
  and temperatures. Denver Water moves water to meet demand, not to suit the fish.

**Filtration and pathogen risk**
- Yes. The risk factor is calculated at the start of treatment, and it sets the
  required filter time and disinfectant residual.

**SNOTEL stations**
- There are no official groups. Pick stations by location.
- The model started on Michigan Creek, then switched to **Buckskin Joe** because of
  data anomalies.

**An event that caught them off guard**
- ~2023, a "100-year storm" in the South Platte watershed. They knew it was coming, but
  not how big it would be.
- Turbidity almost forced Foothills to shut down. Chemicals handled it, but filters went
  offline for heavy cleaning, which cut how much water they could send out.
- This is the event that pushed them toward looking ahead.

## Checked against the repo (our check, not theirs)

- **Storm year:** the highest daily max turbidity in `USGS_South_Platte.csv` is **477
  FNU on 2023-08-01**, the top value in the record. That's likely the storm, but not
  confirmed.
- **Buckskin Joe vs Hoosier Pass:** the notebooks name Buckskin Joe (938), but the
  shipped `HoosierPass.csv` matches Hoosier Pass (531). This is already noted in
  `guide.md`. Ask which one is right.

## To ask tomorrow (9:00, Cassidi and Jake there)

- What's the "random red line" across the map?
- Was the 2023 storm on Aug 1, 2023?
- Buckskin Joe or Hoosier Pass: which snow station should we use?
- Where should we focus for the big picture?
