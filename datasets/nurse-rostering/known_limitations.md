# Known Limitations — Nurse Rostering & Acuity-to-Staffing Dataset

## Technical Limitations

1. **Fixed seed, single realisation**: The dataset uses a single PRNG seed (42). Different seeds produce datasets with the same statistical properties but different individual rows.

2. **Shift-level granularity only**: Each row represents one ward during one 8-hour shift. Intra-shift dynamics (meal break staffing dips, mid-shift admissions/discharges changing census, staff redeployment between wards) are not captured.

3. **Static ward parameters**: Ward characteristics (bed capacity, target NHPPD, acuity baseline) are fixed for the entire 12-month period. Real wards undergo reconfiguration, bed closures, and service changes.

4. **Independence between wards**: Each ward's staffing is generated independently. In reality, wards share a common nursing pool, and understaffing in one ward may lead to staff redeployment from another — creating correlated staffing patterns across wards.

5. **Three-shift model**: The dataset uses a fixed AM/PM/NIGHT 8-hour shift structure. Many Australian hospitals use 8-, 10-, and 12-hour shift combinations, with overlap periods that improve handover safety. The dataset does not model shift length variation or overlap.

## Clinical / Domain Limitations

6. **No individual patient modelling**: Patient acuity is a ward-level aggregate, not built from individual patient assessments. Real staffing adequacy depends on the distribution of patient acuity within a ward (e.g., one very high-acuity patient may require 1:1 care), not just the mean.

7. **No feedback loop**: Staffing levels do not respond to acuity in real time. In practice, charge nurses and bed managers adjust staffing throughout a shift based on changing patient needs. This reactive staffing mechanism is not modelled.

8. **Simplified adverse event model**: Adverse events are generated from Poisson distributions with staffing/acuity modifiers. Real adverse events arise from complex interactions of patient, provider, system, and environmental factors. The staffing-adverse event relationship in this dataset should not be interpreted as causal.

9. **No workforce planning variables**: The dataset does not include variables for staff satisfaction, intention to leave, overtime fatigue, education levels, or years of experience — all of which are important for workforce planning research.

10. **No enterprise agreement modelling**: Australian nursing workforce is governed by enterprise agreements that specify minimum staffing ratios, maximum consecutive shifts, minimum rest periods, and penalty rates. These constraints shape real roster construction but are not modelled here.

11. **Two-campus simplification**: While the dataset models two campuses, there is no cross-campus staff sharing, float pool, or centralised bed management — all of which are common in multi-campus health services.

## Data Quality Notes

12. **No missing data**: Every field is populated. Real rostering data contains gaps due to system errors, incomplete shift reports, and retrospective corrections.

13. **Clean adverse event counts**: Adverse event counts are integer values with no ambiguity. Real adverse event data involves classification disputes, delayed reporting, and varying definitions across facilities.

14. **Deterministic staffing adequacy**: The adequacy classification is applied at generation time using fixed thresholds. Real adequacy assessment is more nuanced, incorporating qualitative factors (ward layout, patient complexity, equipment availability) alongside quantitative measures.

15. **No temporal autocorrelation**: Consecutive shifts on the same ward are generated independently. In reality, staffing patterns show strong autocorrelation (the same roster structure repeats weekly, and understaffing tends to persist until intervention).
