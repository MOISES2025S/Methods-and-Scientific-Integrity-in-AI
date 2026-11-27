# Bias Audit Report: Regional Fairness of a Toll-Traffic Forecasting Model

> MTC toll-station traffic (`VEH_IMD`) · regression audit with Microsoft Fairlearn · sensitive attribute: natural macro-region

**Session 12 Workshop** | Research Methods and Scientific Integrity in AI | Doctoral Program in Deep Technologies, UNMSM  

**Professor:** Dr. Loveleen Gaur | **Student:** Moisés Evangelista Gamarra (Student Code: 26207275) | **Date:** November 2026  

**Toolkits:** Fairlearn 0.15.0, scikit-learn 1.6.1  

**Notebook:** [Session12_MTC_Bias_Audit_EVANGELISTA_GAMARRA_MOISES.ipynb](Session12_MTC_Bias_Audit_EVANGELISTA_GAMARRA_MOISES.ipynb)

MTC toll-station traffic (VEH_IMD) · regression audit with Microsoft Fairlearn · sensitive attribute: natural macro-region

Session 12 Workshop | Research Methods and Scientific Integrity in AI | Doctoral Program in Deep Technologies, UNMSM

Professor: Dr. Loveleen Gaur | Student: Moisés Evangelista Gamarra (Student Code: 26207275) | November 2026

Toolkits: Fairlearn 0.15.0, scikit-learn 1.6.1 | Notebook: Session12_MTC_Bias_Audit_EVANGELISTA_GAMARRA_MOISES.ipynb

Summary. I audited a one-month-ahead traffic forecasting model (Ridge regression on log VEH_IMD) trained on 82 toll stations of Peru's National Road Network for unequal forecast quality between natural regions. Sierra received the least accurate forecasts (MAPE 10.89% against 7.99% on the coast), but its median error is only +0.96 pp above the coast's, so much of the gap comes from a few stations with structural breaks. Fairlearn's ExponentiatedGradient with a BoundedGroupLoss constraint moved the worst-region MAPE from 10.89% to 10.88% and overall MAPE by +0.22 pp. No change survived the 10 rolling origins. The audit points to data, not to the model, as the lever for regional fairness: a region's error is set by its volatility and by station-level breaks, which a constraint on the loss function cannot remove.

# 1. Dataset, task and audit groups

| Item | Value |
| --- | --- |
| Dataset | MTC, "Flujo Vehicular Registrado en las Unidades de Peaje de la Red Vial Nacional" (Peru National Open Data Portal): 11,532 rows, 82 toll stations, 2014-01 to 2026-03 |
| Data provenance | data/Flujo_vehicular_registrado_en_peajes_2014-2026_I.csv (uploaded and versioned with Git), MD5 bb6e20c8830af2511da8746ca42f6aa3; source URL in data/DATA_MANIFEST.json |
| Cleaning | 37 duplicate station-months (administration changes) summed; 805 station-months with VEH_IMD = 0 (no operation) removed |
| Prediction task | Regression: VEH_IMD (average daily vehicles) of each toll station, one month ahead |
| Toolkit | Microsoft Fairlearn (MetricFrame, ExponentiatedGradient, BoundedGroupLoss), because the target is continuous; AIF360 is reserved for binary targets |
| Sensitive attribute | Natural macro-region of the road each toll serves: Costa, Sierra, Selva. Longitudinal routes by axis (PE-1 Costa, PE-3 Sierra, PE-5 Selva, read from CODIGO_PEAJE); transversal routes by department; Matarani Concesión -> Costa, Corcona-Concesión -> Sierra by documented override |
| Reference group | Costa |
| Comparison group | Interior = Sierra + Selva |
| Split | Train until 2024-03 (COVID window removed); validation 2024-04 to 2025-03; test 2025-04 to 2026-03 (858 station-months) |
| Baseline model | Ridge regression (alpha 1.0) on log1p(VEH_IMD) with calendar lags 1, 2, 3, 12, rolling mean, last change and month of year |

## Statement of direction

A regression model has no favorable label, but it has a harmful direction of error. I define the signed error as (forecast - actual) / actual, so a negative value is an under-forecast. Under-forecasting a region's traffic is the harmful direction: maintenance budgets, capacity and toll-lane staffing sized on that forecast would under-serve the region's road users. The notebook asserts this sign convention in code. Read backwards, a region that is systematically under-estimated would appear to be favoured by the model.

Toll stations are not people. The audit treats region as the sensitive attribute because investment decisions informed by these forecasts reach the people who live in each region, and road investment in Peru has historically concentrated on the coast.

# 2. Bias present before any model exists

| Region | Stations | Station-months | Share of rows (%) | Median VEH_IMD | Median monthly volatility (%) |
| --- | --- | --- | --- | --- | --- |
| Costa | 46 | 6019 | 56.30 | 2,012 | 15.27 |
| Sierra | 28 | 3512 | 32.85 | 1,292 | 15.99 |
| Selva | 8 | 1159 | 10.84 | 832 | 12.83 |

![Figure](assets/figure_1.png)

Figure 1. Representation and forecastability by region, computed before any model was trained.

The data are unbalanced before any model exists. Costa contributes the most stations and Selva the fewest (8). The most volatile region is Sierra (median monthly volatility 15.99%) and the least volatile is Selva (12.83%). A single model fitted to all stations learns mostly from the regions that dominate the rows, and volatile series are harder to forecast for any model. Both properties set a floor on the regional error that no mitigation can remove.

# 3. Before metrics: the unmitigated baseline

A regression has no favorable label, so disparate impact and the parity differences cannot be computed directly. The audit uses their regression counterparts on forecast error, shown in the second column.

| Metric | Workshop counterpart | Value | Target | Reading |
| --- | --- | --- | --- | --- |
| MAPE overall (%) | Accuracy | 8.54 | lower | Average relative error of the forecasts |
| Error-parity ratio, MAPE(Costa)/MAPE(Interior) | Disparate impact (ratio) | 0.850 | 1.0 (0.8 screen) | PASS (>= 0.8) |
| MAPE difference, Interior - Costa (pp) | Statistical parity difference | +1.40 | 0 | Positive = Interior forecasts less accurate |
| Bias difference, MPE Interior - MPE Costa (pp) | Equal opportunity difference (error direction) | +0.78 | 0 | Negative = Interior under-forecast more |
| Worst-region MAPE (%) | - | 10.89 | lower | Worst region: Sierra |

| Region | n (test) | MAPE (%) | Median APE (%) | Signed bias MPE (%) | MAE (vehicles/day) |
| --- | --- | --- | --- | --- | --- |
| Costa | 520 | 7.99 | 5.18 | +0.13 | 378 |
| Sierra | 242 | 10.89 | 6.13 | +1.90 | 206 |
| Selva | 96 | 5.62 | 4.77 | -1.57 | 60 |

Before mitigation the worst-served region was Sierra, with a MAPE of 10.89% (against Costa 7.99%, Selva 5.62%). Pooled as the Interior, Sierra and Selva had a MAPE +1.40 pp above the coast and an error-parity ratio of 0.850, above the 0.8 screening value; pooling hides the difference, because the two interior regions sit on opposite sides of the coast. In the harmful direction, Selva (signed bias -1.57%) is under-forecast on average; the other regions are over-forecast.

The mean hides a concentration. In the worst region (Sierra) the mean APE is 10.89% but the median is 6.13%, against 5.18% on the coast (median gap +0.96 pp). The largest single error belongs to Uchumayo-Concesión (Sierra, MAPE 57.10% over 12 months), so part of the regional gap is carried by a few stations with structural breaks rather than by every station of the region.

The 0.8 value is borrowed from the four-fifths rule only as a screening heuristic; it has no legal meaning for forecast errors.

# 4. Mitigation applied, and why

| Design choice | Justification |
| --- | --- |
| Method | Fairlearn ExponentiatedGradient with a BoundedGroupLoss constraint (Agarwal, Dudík & Wu, 2019), wrapping the same Ridge model |
| Family | In-processing: the constraint enters the training objective |
| Fairness criterion it targets | Bounded group loss: the mean absolute log error of every region must stay below a bound, while the average error is minimized |
| Bound selection | Candidates [1.0, 0.9, 0.8, 0.7] x the baseline training loss; chosen on validation only (smallest worst-region MAPE with overall MAPE at most 5% above the baseline). Selected factor: 1.0 |
| Deterministic predictions | The randomized mixture is replaced by the weighted average of its Ridge models. Absolute loss is convex, so by Jensen's inequality each region's loss cannot exceed the mixture's expected loss; every station receives one forecast |
| Alternatives considered | Group-balanced sample weights (pre-processing, my first draft): no target metric. Region-specific bias correction (post-processing): equalizes bias but not accuracy |

## Why this method fits this harm

The harm is allocative and regional: if one region's traffic is forecast poorly, decisions built on the forecast serve that region worse. A criterion that bounds the error of the worst-served region addresses that harm directly. Equalizing errors by making the best-served region worse would satisfy a parity metric without helping anyone, so I chose a minimax-style bound rather than strict parity of errors.

## What I gave up by choosing it

Bounded group loss does not require equal errors or equal signed bias across regions, so a gap can remain after mitigation. It may also trade some average accuracy for the worst region. Because the regions differ in volatility (Section 2), exact parity of forecast errors is neither achievable nor desirable: it would mean degrading the more predictable coastal series.

# 5. After metrics, and the trade-off

| Metric | Before | After | Change |
| --- | --- | --- | --- |
| MAPE overall (%) | 8.538 | 8.758 | +0.219 |
| Error-parity ratio (Costa/Interior) | 0.850 | 0.890 | +0.040 |
| MAPE difference (Interior-Costa, pp) | 1.404 | 1.031 | -0.373 |
| Bias difference (Interior-Costa, pp) | 0.782 | 0.856 | +0.074 |
| Worst-region MAPE (%) | 10.886 | 10.876 | -0.010 |

![Figure](assets/figure_2.png)

Figure 2. MAPE and signed bias by region on the test year, before and after the BoundedGroupLoss mitigation.

| Region | MAPE before | MAPE after | MPE before | MPE after |
| --- | --- | --- | --- | --- |
| Costa | 7.99 | 8.35 | +0.13 | -0.22 |
| Sierra | 10.89 | 10.88 | +1.90 | +1.59 |
| Selva | 5.62 | 5.62 | -1.57 | -1.78 |

The mitigation moved the worst-region MAPE from 10.89% to 10.88% and the error-parity ratio from 0.850 to 0.890, while overall MAPE changed by +0.22 pp.

## Feasibility of the bound and reducibility of the gap

Only 1 of the 4 candidate bounds was feasible for a single shared Ridge model. Tighter bounds could not bind: the worst region's training loss stayed at 0.1023 log units, above bounds of 0.0881 or less, so the selected model is almost the baseline. The reducibility check shows that a model fitted to the worst validation region alone (Sierra) changes its validation MAPE by +5.4%, so most of the gap is irreducible for this model class: it reflects the region's volatility, not a pooled model.

| Region | Validation MAPE, pooled | Validation MAPE, region-specific | Relative change (%) |
| --- | --- | --- | --- |
| Costa | 8.46 | 8.12 | -4.1 |
| Selva | 6.78 | 7.24 | +6.8 |
| Sierra | 9.65 | 10.18 | +5.4 |

No gap crossed zero: the mitigation did not reverse the direction of any regional disparity.

Cross-check: Fairlearn's MetricFrame and an independent pandas group-by give identical regional MAPE values. The scale trap is real in these data: ranked by MAE in vehicles the worst region is Costa, ranked by MAPE it is Sierra. An audit based on absolute errors would have named the wrong region.

# 6. Uncertainty: which changes survive resampling?

Random splits would leak future months into training, so the time-series equivalent of the workshop's 10 splits was used: the whole pipeline (split, baseline, bound selection on validation and mitigation) was re-run at 10 forecast origins spaced 3 months apart, with 12-month test windows from 2023-01 to 2026-03. Consecutive windows share 9 months, as random splits share rows; this overlap shrinks the spread, so the 2-sd rule is lenient and a change that fails it is clearly noise.

| Metric | Before mean | Before sd | After mean | After sd | Mean change | Verdict |
| --- | --- | --- | --- | --- | --- | --- |
| MAPE overall (%) | 10.047 | 2.666 | 10.102 | 2.620 | +0.055 | not distinguishable from noise |
| Error-parity ratio (Costa/Interior) | 0.745 | 0.210 | 0.756 | 0.231 | +0.011 | not distinguishable from noise |
| MAPE difference (Interior-Costa, pp) | 3.935 | 3.627 | 3.911 | 3.868 | -0.024 | not distinguishable from noise |
| Bias difference (Interior-Costa, pp) | 3.280 | 3.538 | 3.433 | 3.633 | +0.152 | not distinguishable from noise |
| Worst-region MAPE (%) | 14.868 | 6.109 | 14.907 | 6.163 | +0.039 | not distinguishable from noise |

![Figure](assets/figure_3.png)

Figure 3. Error-parity ratio before and after mitigation at each of the 10 rolling origins (1.0 = parity; dashed line = 0.8 screen).

| Metric (main test year) | Before [95% CI] | After [95% CI] | Change 95% CI |
| --- | --- | --- | --- |
| Error-parity ratio (Costa/Interior) | 0.850 [0.565, 1.292] | 0.890 [0.592, 1.350] | [+0.022, +0.069] |
| MAPE difference (Interior-Costa, pp) | 1.404 [-2.098, 5.731] | 1.031 [-2.482, 5.413] | [-0.509, -0.237] |
| Bias difference (Interior-Costa, pp) | 0.782 [-2.392, 5.204] | 0.856 [-2.294, 5.310] | [-0.021, +0.162] |

None of the five changes exceeds twice its spread across the 10 rolling origins, so none is a finding. The gap itself moves between origins: the baseline error-parity ratio ranged from 0.490 (2023-04..2024-03) to 0.968 (2024-10..2025-09), a larger swing than any mitigation effect. The baseline fails the 0.8 screen at 5 of the 10 origins (test windows 2023-01 to 2024-12), where Interior forecasts carry roughly twice the coast's relative error; after mitigation 5 of 10 still fail, so the constraint does not remove the flag where it matters. On the main test year the station bootstrap places the baseline error-parity ratio in [0.565, 1.292], an interval that includes 1.0, so the regional gap of that year is not statistically clear on its own; the paired change after mitigation, [+0.022, +0.069], is consistent within that year but small next to the variation between origins.

# 7. Recommendation

- Do not replace the baseline on fairness grounds alone: the regional gains are not robust across the rolling origins. Keep the baseline, publish its regional error table, and treat the bounded-group-loss model as an experiment.

- Address the gap upstream rather than in the loss function: because region-specific models do not lower the worst region's error, the remedy is better data (more stations and covariates that explain volatility, such as road closures, landslides and strikes) and wider prediction intervals for that region, not a fairness constraint.

- Before any planning use, report MAPE and signed bias per region with intervals, and increase coverage of the least represented region (Selva, 8 stations), whose estimates carry the widest uncertainty.

# 8. Honest limitations of this audit

- Region is read from the national route for longitudinal roads, but transversal tolls take their department's predominant region (two documented overrides), and transversal roads climb from coast to highlands, so a few tolls remain approximate.

- Error disparity between regions is not evidence of discrimination against people; it is a risk of unequal service when forecasts drive investment, and the causal link to allocation decisions was not tested.

- Only one model family (Ridge on log traffic, one-month horizon) was audited; the gradient-boosting models and longer horizons of my ITFF pipeline may behave differently.

- Intersectional and finer cells (region x vehicle class, region x station size) were not examined, and stations with fewer than 12 test months weigh less in the regional averages.

Closing statement of the trade-off. I chose bounded group loss because the harm I want to prevent is a region whose traffic is forecast worse than the rest, and the protection it needs is a ceiling on its error, not a lower accuracy for the coast. In this run the worst-region MAPE moved from 10.89% to 10.88% and overall MAPE by +0.22 pp. I gave up exact parity of errors and of signed bias, and this report states which differences survived resampling and which did not.

# References

Agarwal, A., Beygelzimer, A., Dudík, M., Langford, J., & Wallach, H. (2018). A reductions approach to fair classification. ICML.

Agarwal, A., Dudík, M., & Wu, Z. S. (2019). Fair regression: Quantitative definitions and reduction-based algorithms. ICML.

Bellamy, R. K. E., et al. (2019). AI Fairness 360: An extensible toolkit for detecting and mitigating algorithmic bias. IBM Journal of Research and Development, 63(4/5).

Hyndman, R. J., & Athanasopoulos, G. (2021). Forecasting: Principles and practice (3rd ed.). OTexts.

Suresh, H., & Guttag, J. (2021). A framework for understanding sources of harm throughout the machine learning life cycle. EAAMO.

Weerts, H., Dudík, M., Edgar, R., Jalali, A., Lutz, R., & Madaio, M. (2023). Fairlearn: Assessing and improving fairness of AI systems. Journal of Machine Learning Research, 24(257).

Ministerio de Transportes y Comunicaciones (MTC). Flujo vehicular registrado en las unidades de peaje de la Red Vial Nacional. Plataforma Nacional de Datos Abiertos del Perú.
