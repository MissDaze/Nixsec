# Methodology Note — Nurse Rostering & Acuity-to-Staffing Dataset

## Born-Synthetic Confirmation

This dataset is **entirely synthetic**. Every row was generated programmatically using seeded pseudo-random number generators (NumPy PRNG, seed = 42). No real patient records, hospital data, staffing rosters, or identifiable information was used at any stage of production. The dataset cannot be reverse-engineered to identify any real individual, facility, or staffing arrangement.

## Generation Approach

### Architecture

The generator produces approximately 24,000 shift-level roster records across a simulated 12-month period (July 2023 – June 2024) for a fictional two-campus Australian public hospital system. Each row represents one ward's staffing situation during one shift (AM, PM, or NIGHT) on one date.

### Ward Structure

22 wards across 2 campuses are modelled, spanning:

- Medical wards (acute, aged care, respiratory, cardiology)
- Surgical wards (general, orthopaedic, neurosurgical)
- Critical care (ICU, CCU, HDU)
- Emergency departments
- Maternity, paediatrics, neonatal (NICU/SCN)
- Mental health (acute, sub-acute)
- Rehabilitation, oncology, palliative care, perioperative

Each ward has defined: bed capacity, target NHPPD (Nursing Hours Per Patient Day), target nurse-to-patient ratio, target RN percentage in skill mix, and base acuity level.

### Staffing Model

#### Staff Categories

Five nursing staff categories are modelled:

- **RN** (Registered Nurse): Core clinical staff, highest proportion
- **EN** (Enrolled Nurse): Work under RN supervision
- **AIN** (Assistant in Nursing): Support workers
- **NUM** (Nurse Unit Manager): Ward management, typically 1 per shift (AM/PM)
- **CNS** (Clinical Nurse Specialist): Specialty expertise, typically 0–1 per shift

#### Staffing Level Generation

For each shift, base staffing is calculated from the ward's target nurse-to-patient ratio and current patient census:

1. **Patient census**: Generated around the ward's bed capacity with random occupancy variation (70–105% for most wards, higher for ED/ICU)
2. **Base staff requirement**: Census divided by target nurse-to-patient ratio
3. **Shift adjustment**: PM shifts staff at ~80% of AM levels; Night shifts at ~55%
4. **Random perturbation**: ±15% variation to simulate real rostering variability
5. **Vacancy and sick leave**: Each shift has independent probabilities of vacant shifts (4%) and sick leave callouts (4%), which reduce available staff

#### Skill Mix

The RN/EN/AIN split is determined by ward-specific target RN percentages (e.g., ICU targets 95% RN, Rehabilitation targets 55% RN) with random variation. NUM and CNS positions are overlaid based on shift type and ward acuity.

### NHPPD Calculation

Nursing Hours Per Patient Day (NHPPD) is calculated for each shift as:

```
actual_nhppd = (total_nursing_staff × shift_hours) / patient_census × 3
```

The `× 3` factor extrapolates a single 8-hour shift to the daily rate (3 shifts per day). Target NHPPD is adjusted by shift type to reflect intentional staffing variation:

- **AM shift**: Full target NHPPD applies
- **PM shift**: Target × 0.85 (planned lower staffing)
- **NIGHT shift**: Target × 0.65 (planned minimum staffing)

This shift-adjustment prevents PM and Night shifts from being automatically classified as understaffed simply because they have fewer staff by design.

### Staffing Adequacy Classification

The NHPPD variance (actual minus shift-adjusted target) determines staffing adequacy:

| Category | Criteria |
|----------|----------|
| **Adequate** | NHPPD variance ≥ threshold AND RN% ≥ 85% of target |
| **Marginal** | NHPPD variance ≥ marginal threshold AND RN% ≥ 70% of target |
| **Understaffed** | NHPPD variance ≥ critical threshold |
| **Critical** | NHPPD variance below critical threshold |

Thresholds are shift-aware, with Night shifts having tighter margins (a small NHPPD shortfall at night, when there are already fewer staff, has greater clinical impact than the same shortfall during the day):

| Shift | Adequate threshold | Marginal threshold | Critical threshold |
|-------|-------------------|-------------------|-------------------|
| AM | −0.5 | −1.4 | −3.5 |
| PM | −0.5 | −1.5 | −3.0 |
| NIGHT | −0.25 | −1.1 | −2.2 |

This produces an overall understaffing rate of approximately 17.5%, with Night shifts (~24.5%) more frequently understaffed than PM (~15.1%) or AM (~13.0%), and weekends (~19.9%) more frequently understaffed than weekdays (~16.6%).

### Agency Staff and Overtime

When planned staffing falls short:

1. **Agency staff**: Deployed with probability proportional to the shortfall magnitude, capped at 3 per shift
2. **Overtime hours**: If shortfall remains after agency deployment, remaining gaps generate 2–4 overtime hours per unfilled position

### Adverse Events

Six categories of adverse events are modelled using Poisson distributions with lambda values modulated by staffing adequacy and patient acuity:

- **Patient falls**: λ base = 0.15, increased by understaffing and high acuity
- **Medication incidents**: λ base = 0.10, increased by understaffing
- **Pressure injuries (new)**: λ base = 0.05, increased by high census
- **Rapid response / MET calls**: λ base = 0.08, increased by acuity
- **Patient complaints**: λ base = 0.12, increased by understaffing
- **Staff injuries**: λ base = 0.03, increased by understaffing

### Sample Generation

The 1,000-row sample uses stratified sampling to ensure representation of:

- All staffing adequacy categories (including rare "Critical" shifts)
- Both campuses
- All shift types and days of week
- Shifts with adverse events

### Reproducibility

The entire generation process uses `numpy.random.seed(42)`, making the dataset fully reproducible.
