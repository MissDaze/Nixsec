# Known Limitations — Medication Administration & Near-Miss Safety Dataset

## Technical Limitations

1. **Fixed seed, single realisation**: The dataset uses a single PRNG seed (42). While this ensures reproducibility, it means the dataset represents one specific realisation of the underlying probabilistic model. Different seeds would produce datasets with the same statistical properties but different individual rows.

2. **Independence assumption**: Medication administration events are generated independently. In reality, errors can cluster (e.g., a fatigued nurse making multiple errors in a shift, or a system failure affecting an entire ward). The dataset does not model cascading or correlated error chains.

3. **Static parameters**: All generation parameters (base error rates, shift multipliers, ward characteristics) are fixed for the entire 12-month period. Real hospitals experience parameter drift due to staffing changes, quality improvement interventions, technology adoption, and seasonal effects.

4. **Discrete time modelling**: Administration times are generated within shift windows with medication-round biases. Real administration timing follows more complex patterns driven by individual patient schedules, procedure timing, and clinical workflows.

## Clinical / Domain Limitations

5. **Simplified patient model**: Patients are not individually modelled. There is no concept of patient journey, length of stay, polypharmacy, or cumulative risk. Each administration event is effectively independent of the patient's other events.

6. **No drug interaction modelling**: The dataset does not account for drug-drug interactions, drug-allergy checks, or contraindications. A significant proportion of real near-miss events involve these interaction-based catches.

7. **Perfect reporting assumption**: Every near-miss and error in the dataset is "reported." Real incident reporting systems capture only a fraction of actual events (estimated 10–50% in published literature). Analyses treating this data as representative of reported-only data should adjust for this.

8. **Uniform ward behaviour**: All wards of the same type behave identically in terms of their error-generation parameters. Real wards develop distinct safety cultures, workaround practices, and reporting norms.

9. **No intervention modelling**: The dataset does not model the effect of safety interventions (barcode medication administration, smart infusion pumps, pharmacist-led reconciliation). Users building predictive models should be aware that intervention variables are absent.

10. **Single facility**: Data represents one fictional hospital system. Multi-site studies would require generating additional datasets with different parameter configurations to simulate inter-facility variation.

## Data Quality Notes

11. **No missing data**: Every field is populated for every row. Real clinical datasets invariably contain missing values due to documentation omissions, system errors, and workflow interruptions. Users testing imputation methods should introduce missingness artificially.

12. **No free-text fields**: Clinical incident reports typically contain rich narrative text. This dataset uses categorical error types and severity codes only. Natural language processing applications would need a different data source.

13. **Rounded values**: Dose values, ratios, and timestamps are rounded to clinically plausible precision. This may slightly affect distributional analyses at the tails.
