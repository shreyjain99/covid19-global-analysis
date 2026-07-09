# Week 1 Notes — COVID-19 Global Data Analysis

**Repo:** https://github.com/shreyjain99/covid19-global-analysis

## What was set up

- **Environment:** Python with pandas, plotly, statsmodels, and Jupyter (see
  `requirements.txt`). Reproducible via `pip install -r requirements.txt`.
- **Data:** OWID COVID-19 dataset pulled from the official GitHub repo into
  `data/raw/` via `scripts/download_data.py`.
- **Project scaffold:** `data/`, `docs/`, `notebooks/`, `scripts/`, `outputs/`
  with a README and .gitignore (the 98 MB CSV is git-ignored and re-downloadable).

## Understanding the dataset (60+ columns)

- **Shape:** ~429,000 rows × **67 columns**, daily, **2020-01-01 → 2024-08-14**,
  ~230 countries plus continent and income-group aggregates.
- Columns group into families: identifiers/time, confirmed cases, deaths,
  hospital & ICU, testing, vaccinations, policy (stringency), demographic/context
  variables (static per country), and excess mortality. Full reference in
  `docs/data_dictionary.md`.
- **Coverage is uneven.** Case and death series are ~95% populated. The sparsest
  fields are excess mortality and weekly ICU admissions (~3%), and ICU/hospital
  occupancy (~9%) — only some countries reported them.
- **Two modelling gotchas noted:** (1) `location` mixes countries with aggregates
  (filter on `continent.notna()` for country-level work); (2) use smoothed,
  per-capita series for cross-country comparison.

## First insights (starter charts)

1. **Case trends** — plotting `new_cases_smoothed_per_million` shows the successive
   waves clearly, with the large early-2022 Omicron spike standing out across most
   focus countries.
2. **Vaccination rollout** — `people_fully_vaccinated_per_hundred` traces the classic
   S-curve through 2021; final coverage in the focus set ranged from ~35% (South
   Africa) to ~83% (Japan).
3. **Mortality** — cumulative deaths per million rises with median age. A simple
   (illustrative, uncontrolled) OLS gives ~+107 deaths/million per additional year of
   median age (R² ≈ 0.47). Highest per-capita mortality among larger countries: Peru,
   Bulgaria, Hungary.
4. **World totals (latest):** ~776M cumulative cases, ~7.06M deaths, naive CFR ≈ 0.91%.

## Blockers

- None. PNG export via Plotly/kaleido needs a local Chrome install; interactive HTML
  export and matplotlib previews both work without it, so this isn't blocking.

