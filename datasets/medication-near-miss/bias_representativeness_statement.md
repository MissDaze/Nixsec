# Bias & Representativeness Statement — Medication Administration & Near-Miss Safety Dataset

## Intended Population

This dataset models medication administration events in a mid-to-large Australian public hospital system. The ward structures, medication formulary, terminology (APINCHS high-risk classification, NCC MERP severity index), and staffing patterns reflect Australian acute-care hospital operations.

## Known Representativeness Limitations

### Geographic and System Bias

- The dataset reflects Australian public hospital conventions. Private hospitals, primary care, aged care facilities, and non-Australian health systems may have materially different medication administration patterns, staffing models, and error profiles.
- The APINCHS high-risk medication classification is an Australian standard. Other jurisdictions use different high-risk frameworks (e.g., ISMP in the US), which would produce different high-risk flagging patterns.

### Temporal Simplifications

- The 12-month window does not model seasonal variation in admission volumes (e.g., winter respiratory surges, summer trauma peaks) that would affect medication administration density.
- Public holiday effects are not modelled separately from weekends.
- The dataset does not capture long-term trends such as gradual formulary changes, introduction of electronic medication management systems, or evolving staffing models.

### Clinical Simplifications

- Patient acuity is modelled at the ward level (mean acuity per ward), not at the individual patient level. Real medication error risk varies with individual patient complexity, polypharmacy, and comorbidities.
- The medication pool of 82 drugs is representative but not exhaustive. Actual hospital formularies contain hundreds of items.
- Drug interactions and contraindications are not modelled. In reality, many near-miss events involve drug-drug or drug-allergy interactions.

### Error Rate Assumptions

- The 2.8% base error rate and multiplicative risk modifiers are drawn from published literature but represent a single plausible configuration. Real error rates vary substantially between facilities (1–12% in published studies) depending on technology adoption (e.g., barcode scanning, smart pumps), culture, and reporting practices.
- Under-reporting is a well-documented issue in medication incident data. This dataset models a "perfect reporting" scenario where all incidents are captured, which overstates the completeness of real-world incident databases.

### Staffing Model

- Nurse-to-patient ratios are modelled as ward-level parameters with random perturbation rather than being derived from actual rostering constraints (leave, vacancies, skill mix requirements).
- The experience distribution is static across the 12-month period. Real workforces experience turnover, new graduate intakes, and seasonal staffing fluctuations.

## Diversity Considerations

- Patient demographics (age, sex) are generated with plausible distributions but are not calibrated to any specific population. They should not be used to draw conclusions about demographic-specific medication safety.
- The dataset does not include variables for patient ethnicity, language, disability, or socioeconomic status, all of which can influence medication safety in real settings.

## Recommended Use

This dataset is suitable for developing, testing, and demonstrating analytical methods, machine learning pipelines, dashboards, and educational exercises. It should **not** be used as a basis for clinical decision-making, policy setting, benchmarking real facilities, or making claims about actual medication safety rates.
