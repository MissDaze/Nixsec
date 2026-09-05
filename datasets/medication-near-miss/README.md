# Medication Administration & Near-Miss Safety Dataset

## Overview

30,000 synthetic medication administration events across 10 hospital wards over a 12-month period, with realistic near-miss and error patterns modulated by shift, time-of-day, staffing, medication risk class, and staff experience.

## File Manifest

| File | Description | Rows |
|------|-------------|------|
| `medication_administration_near_miss_full.csv` | Complete dataset | 30,000 |
| `medication_administration_near_miss_sample.csv` | Stratified free sample (enriched for incidents) | ~850 |
| `data_dictionary.csv` | Column names, types, ranges, and descriptions | 25 |
| `methodology_note.md` | Full generation methodology and born-synthetic confirmation | — |
| `bias_representativeness_statement.md` | Known biases and representativeness limitations | — |
| `summary_statistics.html` | Descriptive statistics with distribution charts | — |
| `known_limitations.md` | Technical and domain-specific limitations | — |
| `README.md` | This file | — |

## Key Features

- **82 medications** across 14 therapeutic classes with APINCHS high-risk flagging
- **Multiplicative error modelling**: near-miss/error probability varies by night shift (×1.40), handover windows (×1.50), low experience (×1.60), weekend (×1.15), and administration density
- **NCC MERP severity grading**: Categories A (near miss) through G (permanent harm) with realistic severity pyramid
- **Error types**: wrong dose, wrong time, omission, wrong route, wrong patient, wrong medication, documentation error, deteriorated medication
- **Staffing context**: nurse-to-patient ratios, staff experience bands, double-check compliance rates
- **Overall near-miss/error rate**: ~3.7%

## Terminology

- **APINCHS**: Australian high-risk medication classification (Anti-infectives, Potassium, Insulin, Narcotics, Chemotherapy, Heparin, Sedatives)
- **NCC MERP**: National Coordinating Council for Medication Error Reporting and Prevention severity index
- **AIN**: Assistant in Nursing
- **EN**: Enrolled Nurse
- **RN**: Registered Nurse

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

- **Clinical decision-making**: This data must not be used to inform real patient care decisions
- **Facility benchmarking**: This data must not be used to evaluate or compare real hospitals
- **Regulatory submission**: This data must not be presented as evidence in any regulatory or accreditation context
- **Redistribution**: Redistribution without attribution is not permitted

## Citation

If you use this dataset in published work, please cite it as:

> Synthetic Medication Administration & Near-Miss Safety Dataset (2024). Born-synthetic hospital operations data for research and education. Generated using seeded PRNG methods.

## Contact

For questions about methodology or licensing, contact the dataset author through the marketplace listing.
