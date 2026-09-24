# **Scenario 3 Problem Statement**

- Core question: for a dry, average, or wet year, how does snowpack size and timing translate into TOC and alkalinity at the treatment plant?
- Key insight: TOC and alkalinity are measured by hand from samples, so operators only learn what arrived after it arrived
- Goal: predictability, not surprise, so operators can anticipate high-TOC weeks and plan chemical spend and staffing
- Water quality and quantity must sit side by side in the model
- “Year type” clarified as a domain term for regime: a stretch of time where one mechanism dominates (e.g. snowpack-plus year vs. drought-plus-thunderstorm year)

# **Domain Knowledge Gaps and Key Terms**

- TOC (total organic carbon): dissolved plant and soil matter; more TOC = more treatment work
- Alkalinity: water’s resistance to pH change; high alkalinity = more chemicals needed; low is better for TOC removal
- Snow water equivalent: if snow melted now, how deep a water layer would it make
- Water volume affects quality in two opposite directions:
  - More water dilutes minerals, so alkalinity and conductance fall (good)
  - More water picks up organic matter, so TOC and turbidity rise (bad)
- Group snow data by water year, never calendar year; calendar grouping splits a single snow season across two buckets
- Reservoir blurs incoming water (mixes and settles); models work best with a 2-4 day lag
- 2026 snowpack peaked \~5 weeks early, making it an outlier year
- Foothills plant is the final destination; Marston Plant also exists and may need to be scoped

# **Scenario 3 Features and Visualization**

- Strong core feature: plot TOC or alkalinity against flow, colored by date, one panel per water year
  - Toggle between TOC and alkalinity
  - Filter by year and date range
  - Line chart preferred over scatter; dots are too cluttered
- Spatial map preferred over a simple location dropdown to show quality along the route as water moves
- Projection/extrapolation feature identified as high value
  - Manual flow slider to model hypotheticals beyond historical data
  - Build core graph first, then layer in projections
- Key questions the model should answer:
  - Which weeks of the year should operators expect high TOC?
  - Given this year’s snowpack and melt timing, how many days below a key threshold?
  - How long from snow peak to river peak to plant impact?
  - Which past years resemble 2026?
- Scope boundary: scenario 3 is snowpack-driven; keep storm and runoff events (scenario 2) from leaking in

# **Repo, Tooling, and Next Steps**

- Domain knowledge docs committed to repo root as two markdown files (raw and summary); folder to be renamed domain-knowledge
- Brandon Wesley added to repo; Ford network proxy blocking push from work laptop, will use personal laptop tomorrow
- POC approach agreed for now; if Denver Water wants to carry the code forward, a proper rebuild with DDD would be needed
- UI iteration tip shared: at end of prompt, ask Claude to look at screenshot, find 3 things to improve, repeat 10 times for \~30 quality passes
- Fable agent kicked off to review current UI/UX for clutter and usability
- Projection feature targeted to be ready by tomorrow

# **Next Steps**

- **Create domain-knowledge folder and push docs to repo**
- Rename root markdown files into a dedicated domain-knowledge directory.
- **Build core TOC/alkalinity vs. flow line chart with year/date toggles**
- Get one working graph before adding projection or map layers.
- **Add projection/extrapolation feature to the graph**
- Target completion by 25th September.
- **Replace location dropdown with a spatial map**
- Show TOC/alkalinity readings along the route as water moves toward Foothills.
- **Confirm whether Marston Plant data needs to be included in scope**
- Check the dataset for a second plant entry.

---

Chat with meeting transcript: [https://notes.granola.ai/t/b04e9950-718c-495b-9b05-57d36074979c](https://notes.granola.ai/t/b04e9950-718c-495b-9b05-57d36074979c)