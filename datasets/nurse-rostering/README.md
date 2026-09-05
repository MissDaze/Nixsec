# Nurse Rostering & Acuity-to-Staffing Dataset

## Overview

~24,000 synthetic shift-level roster records across 22 wards on 2 hospital campuses over a 12-month period, linking nurse staffing levels to patient acuity, workload, and adverse event outcomes with realistic understaffing patterns.

## File Manifest

| File | Description | Rows |
|------|-------------|------|
| `nurse_rostering_acuity_staffing_full.csv` | Complete dataset | ~24,090 |
| `nurse_rostering_acuity_staffing_sample.csv` | Stratified free sample (enriched for understaffing/critical) | ~1,000 |
| `data_dictionary.csv` | Column names, types, ranges, and descriptions | 36 |
| `methodology_note.md` | Full generation methodology and born-synthetic confirmation | — |
| `bias_representativeness_statement.md` | Known biases and representativeness limitations | — |
| `summary_statistics.html` | Descriptive statistics with distribution charts | — |
| `known_limitations.md` | Technical and domain-specific limitations | — |
| `README.md` | This file | — |

## Key Features

- **22 wards** across 2 campuses: medical, surgical, critical care, ED, maternity, paediatrics, NICU, mental health, rehabilitation, oncology, palliative care, perioperative
- **5 nursing role categories**: RN, EN, AIN, NUM, CNS with ward-specific skill mix targets
- **NHPPD (Nursing Hours Per Patient Day)**: actual vs. shift-adjusted target with variance tracking
- **Shift-aware adequacy classification**: Night shifts have tighter adequacy margins than AM shifts, reflecting the greater clinical impact of shortfalls at night
- **Understaffing rate**: ~17.5% overall — Night (~24.5%) > PM (~15.1%) > AM (~13.0%); Weekend (~19.9%) > Weekday (~16.6%)
- **Agency and overtime**: modelled as response to staffing shortfalls
- **6 adverse event categories**: patient falls, medication incidents, pressure injuries, rapid response/MET calls, patient complaints, staff injuries — Poisson-distributed with staffing/acuity modulation
- **Workforce context**: vacancy tracking, sick leave callouts, nurse-to-patient ratios

## Key Metrics

| Metric | Value |
|--------|-------|
| Overall understaffing rate | ~17.5% |
| Adequate shifts | ~35.8% |
| Marginal shifts | ~46.8% |
| Critical shifts | ~1.3% |
| Mean actual NHPPD | ~5.2 |
| Mean occupancy | ~86% |

## Terminology

- **NHPPD**: Nursing Hours Per Patient Day — (total staff × shift hours / census) × 3
- **RN**: Registered Nurse
- **EN**: Enrolled Nurse
- **AIN**: Assistant in Nursing
- **NUM**: Nurse Unit Manager
- **CNS**: Clinical Nurse Specialist
- **MET call**: Medical Emergency Team call (rapid response)
- **Acuity band**: Low (<2.5), Moderate (2.5–3.5), High (3.5–4.5), Very High (>4.5)

## Born-Synthetic Confirmation

This dataset is **entirely synthetic**. It was generated programmatically using seeded pseudo-random number generators (seed = 42). No real patient data, hospital records, staffing rosters, or identifiable information was used at any stage. See `methodology_note.md` for full details.

## Licence & Permitted Use

This dataset is licensed for the following purposes only:

- Academic and educational use
- Research and methodology development
- Software testing and demonstration
- AI/ML model training and evaluation
- Dashboard and visualisation prototyping

### Prohibited Use

- **Clinical decision-making**: This data must not be used to set real staffing levels or inform patient care
- **Workforce benchmarking**: This data must not be used to evaluate or compare real hospital staffing
- **Industrial/enterprise agreement use**: This data must not be cited in workforce negotiations or regulatory submissions
- **Redistribution**: Redistribution without attribution is not permitted

## Citation

If you use this dataset in published work, please cite it as:

> Synthetic Nurse Rostering & Acuity-to-Staffing Dataset (2024). Born-synthetic hospital workforce data for research and education. Generated using seeded PRNG methods.

## Contact

For questions about methodology or licensing, contact the dataset author through the marketplace listing.
