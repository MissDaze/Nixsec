# Methodology Note — Medication Administration & Near-Miss Safety Dataset

## Born-Synthetic Confirmation

This dataset is **entirely synthetic**. Every row was generated programmatically using seeded pseudo-random number generators (NumPy PRNG, seed = 42). No real patient records, hospital data, or identifiable information was used at any stage of production. The dataset cannot be reverse-engineered to identify any real individual, facility, or clinical event.

## Generation Approach

### Architecture

The generator produces 30,000 medication administration events across a simulated 12-month period (July 2023 – June 2024) for a fictional multi-campus Australian hospital system ("Metro General Hospital").

### Ward Structure

Ten hospital wards are modelled, each with defined bed capacity, volume weighting (how many administrations each ward contributes relative to its size), mean acuity, and shift-specific staffing ratios:

- Emergency Department (ED-01): 30 beds, highest volume weight
- Intensive Care Unit (ICU-01): 16 beds, highest acuity
- Medical wards (MED-01, MED-02): 32 beds each
- Surgical wards (SURG-01, SURG-02): 28–30 beds
- Paediatrics (PAED-01): 20 beds
- Mental Health (MH-01): 24 beds
- Maternity (MAT-01): 22 beds
- Rehabilitation (REHAB-01): 26 beds

### Medication Pool

82 medications spanning 14 therapeutic classes are modelled. Each medication carries attributes for: therapeutic class, high-risk flag (based on the APINCHS classification used in Australian hospitals), permitted routes, dose range, unit, and frequency weight (how commonly it is administered relative to others).

High-risk medication classes include: Anti-infectives (selected), Potassium and electrolytes, Insulin, Narcotics/opioids, Chemotherapy agents, Heparin/anticoagulants, and Sedatives.

### Temporal Distribution

- **Date selection**: Uniform random across the 12-month window, generating realistic day-of-week distributions
- **Shift assignment**: Three 8-hour shifts (AM 07:00–15:00, PM 15:00–23:00, NIGHT 23:00–07:00) with ward-specific volume ratios (e.g., ICU has more even distribution; Rehab is heavily AM-weighted)
- **Administration time**: Drawn from within the assigned shift window with a bias toward common medication rounds (08:00, 12:00, 18:00, 22:00)

### Near-Miss and Error Modelling

The overall base error/near-miss probability is 2.8%, modulated multiplicatively by the following risk factors:

| Factor | Condition | Multiplier |
|--------|-----------|------------|
| Shift | Night shift | ×1.40 |
| Shift | PM shift | ×1.15 |
| Handover | Hours 07, 15, 23 | ×1.50 |
| Risk interval | ≥7 administrations in window | ×1.50 |
| Risk interval | ≥6 administrations in window | ×1.30 |
| Staff experience | <1 year | ×1.60 |
| Day of week | Weekend | ×1.15 |
| High-risk medication | APINCHS class | ×0.90 (protective — extra checks) |

This produces an overall near-miss/error rate of approximately 3.7%, consistent with published literature ranges of 2–8% for medication administration incidents in hospital settings.

### Error Severity Classification

Error severity follows an adapted NCC MERP (National Coordinating Council for Medication Error Reporting and Prevention) index:

- **Category A** (Near miss – caught before reaching patient): ~45% of incidents
- **Category B** (Reached patient, no harm): ~25%
- **Category C** (Reached patient, monitoring needed): ~15%
- **Category D** (Reached patient, intervention needed): ~8%
- **Category E** (Temporary harm): ~4%
- **Category F** (Prolonged hospitalisation): ~2%
- **Category G** (Permanent harm): ~1%

### Error Type Distribution

When an error occurs, the error type is drawn from a weighted distribution: wrong dose (30%), wrong time (25%), omission (20%), wrong route (8%), wrong patient (5%), wrong medication (5%), documentation error (5%), deteriorated medication (2%).

### Staffing and Experience

- **Nurse-to-patient ratio**: Ward-specific with shift adjustment and random perturbation (±15%)
- **Staff experience levels**: Drawn from a weighted distribution (<1 yr: 12%, 1–3 yr: 22%, 3–5 yr: 20%, 5–10 yr: 25%, 10+ yr: 21%)
- **Double-check compliance**: 95% for high-risk medications (slightly lower on night shift), 40% for standard medications

### Reproducibility

The entire generation process uses `numpy.random.seed(42)`, making the dataset fully reproducible. Running the same script with the same seed produces identical output.
