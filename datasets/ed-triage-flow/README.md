# ED Triage & Patient Flow Dataset

## Overview

40,000 synthetic emergency department presentations over a 12-month period, with Australasian Triage Scale categories, realistic arrival patterns, occupancy-driven wait time degradation, and disposition outcomes including 4-hour NEAT target compliance.

## File Manifest

| File | Description | Rows |
|------|-------------|------|
| `ed_triage_patient_flow_full.csv` | Complete dataset | 40,000 |
| `ed_triage_patient_flow_sample.csv` | Stratified free sample (enriched for high-acuity) | ~1,000 |
| `data_dictionary.csv` | Column names, types, ranges, and descriptions | 30 |
| `methodology_note.md` | Full generation methodology and born-synthetic confirmation | — |
| `bias_representativeness_statement.md` | Known biases and representativeness limitations | — |
| `summary_statistics.html` | Descriptive statistics with distribution charts | — |
| `known_limitations.md` | Technical and domain-specific limitations | — |
| `README.md` | This file | — |

## Key Features

- **Australasian Triage Scale (ATS)**: 5-category triage with realistic distributions (ATS 1 ~0.4%, ATS 2 ~12%, ATS 3 ~35%, ATS 4 ~37%, ATS 5 ~16%)
- **62 presenting complaints** across 20 clinical categories with complaint-specific triage weights, ambulance rates, and admission probabilities
- **Occupancy-driven flow degradation**: time-to-clinician inflates non-linearly when ED occupancy exceeds 90%, with steep escalation above 110%
- **NEAT compliance**: ~69% of presentations meet the 4-hour target, consistent with published Australian ED benchmarks
- **Arrival mode modelling**: ambulance, private vehicle, walk-in, police/correctional, helicopter — proportions driven by complaint acuity
- **Temporal realism**: sinusoidal arrival patterns with morning/evening peaks, day-of-week effects, and realistic shift-based variation
- **Disposition outcomes**: admitted, discharged, transferred, did not wait (DNW), deceased — with ATS- and complaint-driven probabilities

## Terminology

- **ATS**: Australasian Triage Scale (1 = immediately life-threatening, 5 = less urgent)
- **NEAT**: National Emergency Access Target (4-hour benchmark for ED throughput)
- **DNW**: Did Not Wait — patient left before being seen or completing treatment
- **LOS**: Length of Stay in the emergency department
- **TTC**: Time to Clinician — minutes from triage to first clinician assessment

## Born-Synthetic Confirmation

This dataset is **entirely synthetic**. It was generated programmatically using seeded pseudo-random number generators (seed = 42). No real patient data, hospital records, or identifiable information was used at any stage. See `methodology_note.md` for full details.

## Licence & Permitted Use

This dataset is licensed for the following purposes only:

- Academic and educational use
- Research and methodology development
- Software testing and demonstration
- AI/ML model training and evaluation
- Dashboard and visualisation prototyping

### Prohibited Use

- **Clinical decision-making**: This data must not be used to inform real patient care or triage decisions
- **Facility benchmarking**: This data must not be used to evaluate or compare real emergency departments
- **Regulatory submission**: This data must not be presented as evidence in any regulatory or accreditation context
- **Redistribution**: Redistribution without attribution is not permitted

## Citation

If you use this dataset in published work, please cite it as:

> Synthetic ED Triage & Patient Flow Dataset (2024). Born-synthetic emergency department operations data for research and education. Generated using seeded PRNG methods.

## Contact

For questions about methodology or licensing, contact the dataset author through the marketplace listing.
