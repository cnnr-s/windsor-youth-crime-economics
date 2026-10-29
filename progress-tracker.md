# Windsor-Essex Youth Crime Economics - Progress Tracker

## Project summary
- **Goal:** Is police-reported youth (12–17) involvement in violent, property and drug offences correlated with local economic conditions (unemployment and low-income rates) across Windsor-Essex municipalities, 2001–2021?
- **Context:** Fresh start with a clear question. Previous data and notebooks discarded. Amherstburg's own police data ends 2018 (Windsor Police took over in 2019).
- **Scope:** In: 8 municipalities × 5 census years (2001, 2006, 2011, 2016, 2021); Amherstburg 2021 estimated by ratio imputation. Out (for now): annual Windsor CMA time-series; causal claims.
- **Tools:** Python, pandas, Jupyter, statsmodels, StatCan tables + census profiles, Power BI, GitHub, Obsidian
- **Skill level:** pandas - beginner-intermediate; stats - some; StatCan tables - comfortable; Power BI - new
- **Method:** Build a municipality × census-year panel (~40 rows), compute youth rates per 1,000, then correlations, scatterplots and a simple regression. Pipeline: raw → clean → analysis, one notebook per step, commit after each chapter.
- **Rules:** Never edit files in `data/raw/`. Relative paths from line one. Log every download in `notes/data-sources.md`.
- **Time:** 1–3 hrs/week; subsections ~30–60 min

## 1. Reset and organize
- [x] 1.1. Write the research question and method at the top of `README.md`
- [x] 1.2. Create `data/raw/`, `data/clean/`, `notebooks/`, `notes/`
- [x] 1.3. Add `.ipynb_checkpoints/` to `.gitignore`
- [ ] 1.4. Delete or archive the old `jupyter notebooks/` folder; commit the empty structure

## 2. Collect raw data
- [ ] 2.1. Create `notes/data-sources.md` (table name, ID, link, download date for each file)
- [ ] 2.2. Download StatCan police-reported crime by detailed violation (police services in Ontario) for all 8 municipalities, 2001–2021 → `data/raw/crime/`
- [ ] 2.3. Download youth 12–17 and total population per municipality from the 2001, 2006, 2011, 2016, 2021 censuses → `data/raw/population/`
- [ ] 2.4. Download unemployment and low-income rates per municipality, same 5 census years → `data/raw/economics/`
- [ ] 2.5. Log every file in `data-sources.md` and commit

## 3. Clean the crime data (`01_clean_crime.ipynb`)
- [ ] 3.1. Load the raw crime file(s) with a `clean()` function using relative paths
- [ ] 3.2. Standardize location names (lowercase, match population and economics files)
- [ ] 3.3. Build a dict mapping every offence → violent / property / drug / other
- [ ] 3.4. Apply the mapping; keep youth charged + youth not charged
- [ ] 3.5. Aggregate youth involvement by location × year × offence group
- [ ] 3.6. Save `data/clean/crime_youth.csv` and sanity-check with a line plot

## 4. Estimate Amherstburg after 2018
- [ ] 4.1. Calculate Amherstburg ÷ Windsor youth ratio by year and offence group, 2001–2018
- [ ] 4.2. Plot the ratios and choose an averaging window (e.g. 2014–2018)
- [ ] 4.3. Estimate Amherstburg 2021, subtract from Windsor 2021, add an `imputed` flag
- [ ] 4.4. Save the updated `crime_youth.csv`

## 5. Clean the population data (`02_clean_population.ipynb`)
- [ ] 5.1. Load the 5 census population files
- [ ] 5.2. Tidy into `location`, `year`, `total_pop`, `youth_12_17`
- [ ] 5.3. Sanity-check: municipal youth totals vs county youth totals
- [ ] 5.4. Save `data/clean/youth_pop.csv`

## 6. Clean the economic data (`03_clean_economics.ipynb`)
- [ ] 6.1. Check definitions match across years (2011 voluntary long form; low-income measure changes)
- [ ] 6.2. Tidy into `location`, `year`, `unemployment_rate`, `low_income_rate`
- [ ] 6.3. Save `data/clean/economics.csv`; write caveats in `notes/caveats.md`

## 7. Merge and analyze (`04_analysis.ipynb`)
- [ ] 7.1. Merge the three clean files on location + year
- [ ] 7.2. Calculate the rate per 1,000 youth for each offence group
- [ ] 7.3. Scatterplots: each offence group rate vs unemployment, and vs low income
- [ ] 7.4. Pearson and Spearman correlations with p-values; interpret them
- [ ] 7.5. Simple regression with `statsmodels`; interpret it and list limitations
- [ ] 7.6. Write 5–7 bullet-point findings in `notes/findings.md`

## 8. Share it
- [ ] 8.1. Export the analysis tables for Power BI
- [ ] 8.2. Power BI: load the data and set up the data model
- [ ] 8.3. Power BI: 3 visuals (trend line, scatter, municipality bar chart) + filters
- [ ] 8.4. Write a 2–4 page report
- [ ] 8.5. GitHub README: findings, charts, how to run it
- [ ] 8.6. Draft the LinkedIn post
