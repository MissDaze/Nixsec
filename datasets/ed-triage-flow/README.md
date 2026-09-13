# ED Triage & Patient Flow — Dataset README

## Overview

45,000 synthetic emergency department presentations across 6 fictional hospital facilities,
spanning 2025-01-01 to 2025-12-30. Uses the Australasian Triage Scale (ATS 1–5) and models
department crowding effects on time-to-clinician and length of stay. 100% synthetic — see the
disclaimer below.

- **Rows:** 45,000 (full) / 700 (sample preview)
- **Columns:** 16
- **Grain:** one row per ED presentation

## Schema summary

Presentation date/hour/day-of-week, arrival mode, presenting complaint, age band, sex, ATS
triage category, department occupancy at arrival, time-to-triage, time-to-clinician, length of
stay, disposition, and bed-block flag. Full column list and types: see `data_dictionary.md`.

## Main modelled relationships (illustrative simulation rules, not real-world evidence)

- Presenting complaint influences the ATS category distribution (e.g. chest pain and major
  trauma skew toward more urgent categories).
- Department occupancy is modelled with hour-of-day and weekend effects.
- Time-to-clinician and length of stay scale with modelled crowding and ATS category targets.
- Mental health presentations are modelled with longer length of stay.
- These are modelling choices made to produce a usable, directionally-realistic synthetic
  dataset — not measurements of any real emergency department.

## Included assets

`data_dictionary.md`, `methodology_bias_limitations.md`, `summary_statistics.md`,
`business_questions.md`, `sql_practice_queries.sql`,
`notebooks/02_ed_triage_patient_flow_analysis.ipynb`, `charts/`, and a ready-to-open interactive
dashboard in `dashboard/` (see `dashboard/ed_triage_dashboard_user_guide.md`).

## Quick-start snippets

**Interactive dashboard (no code required):** open `dashboard/ed_triage_dashboard.html`
directly in any browser — it works fully offline.

**Python:**
```python
import pandas as pd
df = pd.read_csv("ed_triage_patient_flow_full.csv")
df.groupby('ats_triage_category')['length_of_stay_minutes'].mean()
```

**SQL (after loading — see sql_practice_queries.sql):**
```sql
SELECT ats_triage_category, AVG(time_to_clinician_minutes) AS avg_time_to_clinician
FROM ed_triage_patient_flow
GROUP BY ats_triage_category
ORDER BY ats_triage_category;
```

**Power BI / Tableau:** Get Data → Text/CSV → select `ed_triage_patient_flow_full.csv`.

## Limitations

No linked multi-facility transfer records; no free-text notes or vital signs; comorbidity
beyond presenting complaint/age not modelled; does not capture known real-world seasonal
effects beyond generic hour/weekend patterns. Full detail: `methodology_bias_limitations.md`.

## ⚠️ Synthetic data disclaimer

100% synthetic. No real patients, staff, or facilities. Not clinically validated. For
research, education, software testing, and AI/ML training/evaluation only — see
`LICENSE_AND_ACCEPTABLE_USE.md`.

Business questions: `business_questions.md`. Notebook: `notebooks/02_ed_triage_patient_flow_analysis.ipynb`.

## Bonus content included in this package

Beyond this dataset's own materials above, this package also includes:
- **`dashboard/`** — the interactive dashboard .html files for all three datasets in the
  wider bundle (medication safety, ED patient flow, nurse rostering), not just this one. Every
  .html file is fully self-contained and opens directly in a browser, no matter which package
  it came in.
- **`case_studies/`** — a short PDF case study for all three datasets, showing a sample
  analysis and key findings for each.

This gives you a preview of the full "Synthetic Australian Hospital Operations Dataset
Bundle" even when purchasing this single dataset.

**Note on regenerating the bonus dashboards:** the .py script for *this* dataset's own
dashboard works from inside this package (its CSV is included). The .py scripts for the other
two datasets' dashboards need their own CSV, which isn't included in this single-dataset
package — running them here will tell you so clearly rather than failing silently. Their
pre-built .html files still work perfectly; only regenerating them from scratch needs the full
bundle or that dataset's own standalone package.
