# Bias & Representativeness Statement — Nurse Rostering & Acuity-to-Staffing Dataset

## Intended Population

This dataset models shift-level nurse rostering and staffing adequacy data for a mid-to-large Australian public hospital system with two campuses. The staffing models, role categories (RN, EN, AIN, NUM, CNS), NHPPD benchmarks, and ward structures reflect Australian acute-care nursing workforce conventions.

## Known Representativeness Limitations

### Geographic and System Bias

- **Australian workforce model**: The nursing role taxonomy (RN, EN, AIN, NUM, CNS) is specific to Australia. Other countries use different role structures (e.g., LPN/LVN in the US, HCA in the UK), scope-of-practice boundaries, and supervisory requirements.
- **NHPPD benchmarking**: NHPPD targets and calculation methods vary internationally. The targets used here (e.g., ICU 10.0, Medical 5.5, Rehabilitation 4.0) are broadly consistent with published Australian benchmarks but would not be directly applicable to health systems with different staffing models.
- **Public hospital focus**: The dataset models a public hospital system. Private hospitals, aged care facilities, community health centres, and primary care settings have materially different staffing patterns, rostering constraints, and workforce composition.

### Staffing Model Simplifications

- **Simplified rostering**: Real nurse rosters are the product of complex enterprise agreements, award conditions, skill requirements, staff preferences, and rostering software optimisation. This dataset generates staffing levels from target ratios with random perturbation rather than from a constraint-satisfaction rostering model.
- **No individual staff modelling**: Staff are counted by category, not individually tracked. There is no concept of individual nurse workload, fatigue accumulation across consecutive shifts, or roster pattern compliance (e.g., maximum consecutive shifts, minimum rest between shifts).
- **Static vacancy rate**: The 4% vacancy rate and 4% sick leave rate are fixed. Real vacancy rates vary by ward, specialty, geography, and labour market conditions. Seasonal illness patterns (e.g., winter sick leave spikes) are not modelled.
- **No graduate nurse programs**: Many Australian hospitals have structured graduate nurse programs that affect ward skill mix seasonally. This is not modelled.

### Acuity Model

- **Ward-level acuity**: Patient acuity is modelled as a ward-level mean with random variation, not derived from individual patient assessments. Real acuity measurement uses standardised tools (e.g., the Nursing Acuity Tool, TrendCare, Allocate) that assess individual patient care requirements.
- **No acuity-based allocation**: Real staffing allocation increasingly uses acuity-based models where staffing is adjusted in response to measured patient care needs. This dataset generates acuity and staffing independently (with correlation, but not a causal feedback mechanism).

### Adverse Events

- **Simplified causation**: Adverse event counts are generated from Poisson distributions modulated by staffing adequacy and acuity. Real adverse events have complex, multifactorial causation involving individual patient factors, environmental conditions, equipment, and system design — not just staffing levels.
- **No event investigation data**: Real adverse event data includes root cause analysis, contributing factors, and outcome severity. This dataset provides counts only.
- **Independence assumption**: Adverse events are generated independently per shift. In reality, an adverse event on one shift can affect subsequent shifts (e.g., a fall leading to increased observation requirements, a complaint leading to changed practices).

## Diversity Considerations

- The dataset does not model nursing workforce demographics (age, gender, ethnicity, country of qualification). These factors influence workforce supply, retention, and are important for workforce planning research.
- Agency and overtime patterns may differ for specific demographic groups or geographic regions — this variation is not captured.

## Recommended Use

This dataset is suitable for developing, testing, and demonstrating nurse staffing analytics, workforce planning tools, dashboards, and educational exercises. It should **not** be used to set real staffing levels, inform enterprise agreement negotiations, benchmark real hospital staffing, or make claims about actual nursing workforce adequacy.
