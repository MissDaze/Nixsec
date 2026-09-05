# Bias & Representativeness Statement — ED Triage & Patient Flow Dataset

## Intended Population

This dataset models emergency department presentations in a mid-to-large Australian public hospital. The triage system (Australasian Triage Scale), performance benchmarks (NEAT 4-hour target), and clinical terminology reflect Australian emergency medicine practice.

## Known Representativeness Limitations

### Geographic and System Bias

- The Australasian Triage Scale (ATS) is used in Australia, New Zealand, and some Southeast Asian countries. Other jurisdictions use different triage systems (e.g., ESI in the US, CTAS in Canada, MTS in the UK) with different category structures and time targets.
- The NEAT 4-hour target is an Australian policy benchmark. UK, Canadian, and other EDs operate under different time-based targets, and US EDs generally do not have a national time target.
- The complaint mix and admission rates reflect a metropolitan Australian ED. Rural, regional, remote, and paediatric-only EDs have materially different casemix profiles.

### Temporal Simplifications

- Seasonal variation is not explicitly modelled. Real Australian EDs see winter surges (influenza, respiratory illness) and summer trauma peaks (drowning, heat-related illness) that significantly affect volume, acuity, and flow.
- The sinusoidal arrival pattern captures the broad shape of daily variation but does not model event-driven surges (mass casualty incidents, infectious disease outbreaks, major sporting events).
- Public holiday effects are not separated from weekend effects.

### Clinical Simplifications

- The 62 presenting complaints are representative but not exhaustive. Real ED information systems use hundreds of presenting complaint codes.
- Triage category assignment is probabilistic per complaint. In reality, triage is a complex clinical judgment incorporating vital signs, pain scores, mechanism of injury, and patient history — none of which are modelled at the individual level.
- The dataset does not model re-presentations (patients who return to the ED within 48 hours), which represent an important quality indicator.

### Flow Model

- ED occupancy is modelled as a smooth function of arrival density. Real occupancy is more volatile, affected by bed block (admitted patients waiting for inpatient beds), ambulance ramping, staffing levels, and departmental configuration.
- The relationship between occupancy and wait times is modelled as a deterministic modifier. In reality, this relationship is mediated by staffing, patient acuity mix, and senior clinician availability.
- Access block (admitted patients boarding in the ED) is not explicitly modelled as a separate phenomenon, though its effects are partially captured in the occupancy-driven LOS inflation.

### Disposition

- Disposition probabilities are static. In reality, admission rates vary with bed availability, time of day (after-hours admissions are more conservative), and individual clinician practice patterns.
- The Did Not Wait (DNW) rate is modelled as occupancy-dependent but does not account for individual patient factors (wait tolerance, perceived severity, access to alternative care).

## Diversity Considerations

- Patient demographics (age, sex) are generated with complaint-appropriate distributions but are not calibrated to any specific population census.
- The dataset does not include variables for patient ethnicity, Indigenous status, language spoken, disability, or socioeconomic indicators, all of which influence ED presentation patterns, triage outcomes, and disposition in real settings.
- Interpreter use, which affects ED throughput and care quality, is not modelled.

## Recommended Use

This dataset is suitable for developing, testing, and demonstrating ED analytics methods, patient flow simulations, dashboard prototypes, and educational exercises. It should **not** be used to benchmark real ED performance, inform triage policy, or make claims about actual emergency department operations.
