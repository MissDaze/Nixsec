# Nurse Rostering & Acuity-to-Staffing — Dataset README

## Overview

32,850 synthetic shift-level roster records across 8 fictional hospital facilities and 10
ward/unit types, spanning 2025-01-01 to 2025-12-31. Each row links patient census and acuity
to actual vs. recommended staffing, sick leave, agency use, and overtime for one ward on one
shift. 100% synthetic — see the disclaimer below.

- **Rows:** 32,850 (full) / 700 (sample preview)
- **Columns:** 19
- **Grain:** one row per ward per shift

## Schema summary

Facility/ward, shift date/type, patient census, average acuity score, recommended vs. actual
RN/EN counts, agency staff used, sick leave count, overtime hours, actual vs. recommended
nurse:patient ratio, understaffed flag, and skill-mix percentage. Full column list and types:
see `data_dictionary.md`.

## Main modelled relationships (illustrative simulation rules, not real-world evidence)

- Recommended nurse:patient ratios vary by ward type (e.g. ICU modelled far more intensively
  than a rehabilitation ward).
- Actual staffing is derived from rostered staffing minus a modelled sick-leave effect (higher
  on nights/weekends), partially backfilled by agency staff and overtime.
- `understaffed_flag` is fully derived from actual vs. recommended ratio — auditable from the
  other columns, not independently randomised.
- These are modelling choices made to produce a usable, directionally-realistic synthetic
  dataset — not measurements of any real health service's rostering data.

## Included assets

`data_dictionary.md`, `methodology_bias_limitations.md`, `summary_statistics.md`,
`business_questions.md`, `sql_practice_queries.sql`,
`notebooks/03_nurse_rostering_acuity_analysis.ipynb`, `charts/`, and a ready-to-open
interactive dashboard in `dashboard/` (see `dashboard/nurse_rostering_dashboard_user_guide.md`).

## Quick-start snippets

**Interactive dashboard (no code required):** open `dashboard/nurse_rostering_dashboard.html`
directly in any browser — it works fully offline.

**Python:**
```python
import pandas as pd
df = pd.read_csv("nurse_rostering_acuity_full.csv")
df.groupby('shift_type')['understaffed_flag'].apply(lambda s: (s == 'Yes').mean())
```

**SQL (after loading — see sql_practice_queries.sql):**
```sql
SELECT ward_unit, AVG(actual_nurse_patient_ratio) AS avg_ratio
FROM nurse_rostering_acuity
GROUP BY ward_unit
ORDER BY avg_ratio;
```

**Power BI / Tableau:** Get Data → Text/CSV → select `nurse_rostering_acuity_full.csv`.

## Limitations

No persistent/named synthetic staff across shifts; only a generic "sick leave" count (no
leave-type breakdown); acuity is a single simplified numeric score, not a specific acuity
instrument; not reviewed or validated by any health service or regulator. Full detail:
`methodology_bias_limitations.md`.

## ⚠️ Synthetic data disclaimer

100% synthetic. No real patients, staff, or facilities. Not clinically validated. For
research, education, software testing, and AI/ML training/evaluation only — see
`LICENSE_AND_ACCEPTABLE_USE.md`.

Business questions: `business_questions.md`. Notebook: `notebooks/03_nurse_rostering_acuity_analysis.ipynb`.

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
