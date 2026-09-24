# Questions for Denver Water

For Cassidi Rosenkrance (decides how the plants respond) and Jake Slawson (knows the
data). Ask on the morning of Sep 25, before we build.

**Status after the Sep 24 debrief:** #1 answered, #3 and #4 partly answered. Start
tomorrow with #0, then #2.

Our first set asked about data details: which gauge, which plant, what the terms mean.
Those make us accurate, but they don't tell us what would be **valuable**. These
questions find the decision Denver Water makes, when they make it, and what a better
signal would change.

How to ask:
- Ask about the last real time something happened, not "would you use…". People say
  yes to hypotheticals.
- Don't pitch before question 5. Show the POC only at "show and react."
- Record answers with who said them. Write down numbers and words exactly: hours,
  dollars, names of actions.

Context: [problem-frame.md](problem-frame.md), [day-2-plan.md](day-2-plan.md).

## For Cassidi: the decision

### 0. Which dates was the 2023 South Platte storm?

The files show two candidates: turbidity above Strontia hit 185 NTU on May 11–12, 2023
(Foothills TOC peaked at 7.3 mg/L a week later, May 19–20), and 477 NTU on Aug 1, 2023.

**What it tells us:** which event to replay in the demo.

**Answer:** _open_

### 1. Tell us about the last time runoff or a storm caught a plant off guard.

What happened, when did the plant find out, what did they change, and what did it
cost?

**What it tells us:** a real event gives us the lead time they had, the action they
took, and the cost of being late. That's the baseline our tool has to beat.

**Answer (Cassidi, Sep 24 debrief):** a 100-year storm in the South Platte watershed
in 2023. "We knew it was coming, but we didn't know what scale it was." Turbidity was
too much for the filters; the plant almost had to shut down. They treated it with
chemicals, but filters went offline for major cleaning, which slowed how much water
they could put into the system. It became the trigger to "look at ahead of time."
Still open: how many hours of warning they had, and when the plant found out.

### 2. When a plant knows a change is coming, what can it actually do, and how much notice does each action need?

Prompt if needed: adjust coagulant or acid dose, change the intake depth at Strontia,
blend or switch sources, pull more from Marston, add staff.

**What it tells us:** each action has its own lead time. Hours suggests an event alert
(her 12-hour comment). Weeks suggests a seasonal outlook (Scenario 3). This one answer
picks our build.

**Answer:** _open_

### 3. What does a bad week cost?

Extra chemical, missing the 35% TOC removal, disinfection-byproduct risk, overtime,
something else? Which of these does she get asked about most?

**What it tells us:** the measure of value for the report-out, for example "days near
the 60 mg/L line" versus "dollars of coagulant." It also tells us which parameter to
lead with, TOC or alkalinity.

**Partial answer (Cassidi, Sep 24 debrief):** treatment chemicals are "hundreds of
millions of dollars expensive." Still open: which cost of a bad week hurts most.

### 4. What do you look at today to see it coming, and who looks?

Which screens, reports, spreadsheets or phone calls? How often? What's the most
annoying part?

**What it tells us:** our real competitor. If an analyst builds a report by hand
(the group suspected this), our tool replaces that report and should look like its
answer.

**Partial answer (Cassidi, Sep 24 debrief):** "we don't have visualization on this."
Monitoring is real-time or historical: "we look at it from the treatment plant
perspective of what's happening right now." Weather and radar feed only big-picture
quantity estimates, "not for looking at a point in a stream." Three audiences: the
quantity team (about 50 people), her watershed scientists, and the plants. Still open:
who looks at what, and how often.

### 5. Before runoff season, does anyone plan for water quality the way planners plan for quantity?

If yes, what's in that plan? If no, why not?

**What it tells us:** whether a seasonal quality outlook fills an empty seat or
competes with something that already exists. We haven't said what we're building yet,
so this answer won't be shaped by our pitch.

**Answer:** _open_

## Show and react (bring the Intake Explorer)

### 6. If you had seen this replay before the 2023 storm, what, if anything, would you have done differently?

Show the 2023 replay and WY 2023 next to WY 2026. Then ask: what's wrong or missing on this screen?

**What it tells us:** whether the view leads to an action. "Nothing" is useful too:
it means we're showing interesting data, not a decision.

**Answer:** _open_

## For Jake: can we build it

### 7. What is measured continuously at or near the plant intake, and can we get it?

For example turbidity, conductance, pH, or an online organics sensor such as UV254.
(UV254 as a stand-in for TOC is general water-treatment knowledge, not from these
materials.)

**What it tells us:** whether an hours-ahead warning is possible for anything the
plant cares about. Our TOC and alkalinity data are daily hand samples, too coarse for
a 12-hour warning.

**Answer:** _open_

### 8. Is it recorded which sources fed Foothills each day, and could we use it?

**What it tells us:** 2026 looks different (alkalinity below 60 on 23% of Apr to Aug
days vs 64% in 2024), but Denver Water also switched sources that year. Without the
source record we can't tell snowpack effects from operating choices.

**Answer:** _open_

### 9. Do the planners already label years dry, average or wet? By what rule?

**What it tells us:** we use their labels instead of our own. The glossary term
**regime** covers the physics; the planners' label is what they'll recognize.

**Answer:** _open_

## Only if there's time

- Which SNOTEL station does the model use now? In the debrief Jake said they switched
  from Michigan Creek to "I think Buckskin Joe"; the repo's materials say Hoosier Pass
  (`data/HoosierPass.csv`).

- Which gauge best shows natural runoff? Jake's gauge (PLASPLCO) sits above the North
  Fork confluence, so it misses Dillon water from the Roberts Tunnel. Did he try the
  North Fork?
- Does Marston tell a different story from Foothills?
