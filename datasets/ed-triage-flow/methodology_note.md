# Methodology Note — ED Triage & Patient Flow Dataset

## Born-Synthetic Confirmation

This dataset is **entirely synthetic**. Every row was generated programmatically using seeded pseudo-random number generators (NumPy PRNG, seed = 42). No real patient records, hospital data, or identifiable information was used at any stage of production. The dataset cannot be reverse-engineered to identify any real individual, facility, or clinical event.

## Generation Approach

### Architecture

The generator produces 40,000 emergency department presentations across a simulated 12-month period (July 2023 – June 2024) for a fictional Australian public hospital ED.

### Presenting Complaints

62 presenting complaints are modelled, grouped into clinical categories: Cardiac, Respiratory, Neurological, Gastrointestinal, Trauma, Mental Health, Paediatric, Obstetric/Gynaecological, Infectious, Renal/Urological, and General/Other. Each complaint carries:

- **ATS weights**: A 5-element probability vector defining the likelihood of being triaged to each Australasian Triage Scale category (1–5)
- **Frequency weight**: How commonly this complaint presents relative to others
- **Ambulance rate**: Proportion arriving by ambulance (e.g., 90% for cardiac arrest, 10% for sore throat)
- **Admission rate**: Base probability of hospital admission

### Australasian Triage Scale (ATS)

Patients are triaged on the 5-category ATS scale:

| Category | Description | Target time | Distribution |
|----------|-------------|-------------|--------------|
| ATS 1 | Immediately life-threatening | Immediate | ~0.4% |
| ATS 2 | Imminently life-threatening | ≤10 min | ~12.3% |
| ATS 3 | Potentially life-threatening | ≤30 min | ~34.5% |
| ATS 4 | Potentially serious | ≤60 min | ~37.0% |
| ATS 5 | Less urgent | ≤120 min | ~15.8% |

### Arrival Patterns

- **Temporal distribution**: Arrival times follow a sinusoidal pattern with peak hours 10:00–14:00 and 18:00–22:00, and a trough 02:00–06:00. This is modelled using rejection sampling from a time-of-day density function.
- **Day-of-week effects**: Monday presentations are ~10% higher than average; weekends show a different complaint mix (more trauma, fewer GP-redirected visits).
- **Arrival mode**: Ambulance, private vehicle, walk-in, police/correctional, and helicopter, with proportions driven by the presenting complaint's ambulance rate.

### ED Occupancy and Flow

- **Occupancy**: Calculated as a rolling function of arrival density with a base of 75%, peaking above 110% during surge periods. Occupancy directly modulates wait times and length of stay.
- **Time to clinician**: Base time drawn from a lognormal distribution anchored to ATS category targets (ATS 1: 0 min, ATS 2: 8 min, ATS 3: 25 min, ATS 4: 55 min, ATS 5: 90 min). When occupancy exceeds 90%, an occupancy modifier inflates wait times progressively. At >110% occupancy, the modifier escalates non-linearly.
- **Length of stay (LOS)**: Generated from lognormal distributions conditioned on ATS category and disposition. Admitted patients have longer LOS (mean ~5–8 hours) than discharged patients (mean ~2.5–4 hours). ATS 1–2 patients have longer LOS due to resuscitation and stabilisation time.

### Disposition

Patient disposition is determined probabilistically based on ATS category and presenting complaint:

- **Admitted**: Higher probability for ATS 1–2 and complaints with high base admission rates
- **Discharged**: Most common for ATS 4–5
- **Transferred**: Small probability (~1–3%) for specialty or higher-acuity patients
- **Did not wait (DNW)**: Modelled at ~3–5% with higher rates for ATS 4–5 during high-occupancy periods
- **Deceased in ED**: Rare (~0.1%), concentrated in ATS 1

### 4-Hour Rule (NEAT Target)

The dataset allows analysis against the Australian National Emergency Access Target (NEAT), which sets a 4-hour (240-minute) benchmark for ED length of stay. The generated data produces approximately 69% 4-hour compliance, consistent with published Australian ED performance figures.

### Triage Compliance

For each ATS category, a binary flag indicates whether the patient was seen within the ATS-recommended time window. Compliance rates are highest for ATS 1 (~98%) and degrade for lower-acuity categories, particularly during high-occupancy periods.

### Reproducibility

The entire generation process uses `numpy.random.seed(42)`, making the dataset fully reproducible. Running the same script with the same seed produces identical output.
