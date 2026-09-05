# Known Limitations — ED Triage & Patient Flow Dataset

## Technical Limitations

1. **Fixed seed, single realisation**: The dataset uses a single PRNG seed (42). Different seeds would produce datasets with the same statistical properties but different individual rows. Ensemble analyses should generate multiple realisations.

2. **Simplified occupancy model**: ED occupancy is derived from a smooth function of arrival density rather than from a discrete-event simulation of patient flow. This means occupancy does not respond dynamically to individual patient arrivals and departures, and cannot capture the feedback loop where high occupancy causes longer LOS, which further increases occupancy.

3. **No queuing dynamics**: Patients do not explicitly queue for beds, clinicians, or diagnostics. Wait times are generated from parameterised distributions rather than arising from resource contention. This limits the dataset's utility for operations research applications that require true queuing behaviour.

4. **Static parameters**: All generation parameters are fixed for the 12-month period. Real EDs experience parameter changes due to staffing fluctuations, departmental redesigns, and external shocks (e.g., pandemic surges).

## Clinical / Domain Limitations

5. **No diagnostic pathway modelling**: The dataset does not model the sequence of investigations (blood tests, imaging, specialist consultation) that drive real ED length of stay. LOS is generated from aggregate distributions rather than built up from component activities.

6. **No re-presentation tracking**: Patients who return to the ED within 48–72 hours (a key quality metric) are not linked. Each row is an independent event with no patient longitudinal identifier.

7. **Simplified triage**: Triage category assignment is probabilistic per complaint category. Real triage involves vital signs, pain assessment, mechanism of injury, comorbidities, and clinical judgment. The dataset cannot be used to build or validate triage prediction models.

8. **No access block modelling**: Access block (admitted patients boarding in the ED while waiting for an inpatient bed) is a major driver of ED crowding in Australian hospitals. This dataset captures its aggregate effect on LOS and occupancy but does not model it as a distinct phenomenon with its own metrics.

9. **No staffing interaction**: ED staffing levels, medical officer availability, and nurse-to-patient ratios are not modelled. In reality, these are primary determinants of time-to-clinician and flow performance.

10. **No ambulance ramping**: Ambulance offload delays (ramping) are not modelled. In high-occupancy periods, real EDs may have ambulances queued outside, which affects both system-level metrics and individual patient outcomes.

## Data Quality Notes

11. **No missing data**: Every field is populated. Real ED datasets contain missing values due to incomplete triage documentation, system downtime, and patients who leave before registration is complete.

12. **No free-text fields**: Real ED data includes triage nurse notes, clinician assessments, and discharge summaries. This dataset uses categorical fields only.

13. **Deterministic disposition**: Disposition is assigned at generation time, not as an outcome of modelled clinical assessment. There is no mechanism for disposition to change during the ED stay (e.g., a patient initially planned for discharge who deteriorates and requires admission).

14. **Single ED**: Data represents one fictional ED. Multi-site network analyses would require generating additional datasets with different parameter configurations.
