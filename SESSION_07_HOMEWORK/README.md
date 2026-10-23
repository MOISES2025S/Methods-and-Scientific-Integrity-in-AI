# README — Reproducible Documentation

**Research title:** A Reproducible Trustworthy Artificial Intelligence Framework for Traffic-Flow Forecasting Using Open Data from Peru’s National Road Network

## Purpose
This package documents `MTC_Reproducible_Pipeline_v7_ARIMA_SARIMA.ipynb`, which implements a reproducible one-step-ahead monthly forecast of `VEH_IMD` for each toll station on Peru’s National Road Network.

## Data source
Peru’s Ministry of Transport and Communications (MTC), National Open Data Portal: [Vehicle flow recorded at toll stations on the National Road Network, 2014–2026-I](https://www.datosabiertos.gob.pe/dataset/flujo-vehicular-registrado-en-las-unidades-de-peaje-de-la-red-vial-nacional-2014-%E2%80%93-2026-i).

The notebook records MD5 `bb6e20c8830af2511da8746ca42f6aa3` for the file used in the documented run. The local filename depends on the file selected during upload to Colab; the project manifest records the exact filename.

## Main reported results
- Model selected during validation: **HistGradientBoosting (HistGB)**, in 5 out of 5 seeds.
- Test period: 2025.
- MAE: **174.75 ± 0.00**.
- RMSE: **395.71**.
- MAPE: **5.22%**.
- MASE: **0.4844 ± 0.0000**.
- Within-series R²: **0.7199 ± 0.0000**.
- Skill versus the best baseline: **+0.2916 ± 0.0000**.
- Repeatability check with seed 42: two runs produced identical output.

These results are reported by the supplied notebook. The zero standard deviation for HistGB means its outputs were identical across the five seeds under this configuration; it does not imply zero predictive uncertainty.

## Models evaluated
| Category | Model | Brief description |
|---|---|---|
| Regularised regression | **Ridge Regression** (`Ridge`) | Linear model with regularisation. |
| Tree ensemble | **Random Forest Regressor** (`RandomForestRegressor`) | Combines multiple decision trees. |
| Tree boosting | **HistGradientBoosting Regressor** (`HistGradientBoostingRegressor`, `HistGB`) | Trains trees sequentially to correct errors. |
| Statistical model | **ARIMA(1,1,1)** | Non-seasonal statistical benchmark. |
| Seasonal statistical model | **SARIMA(1,1,1)×(1,1,1,12)** | Statistical benchmark with annual seasonality. |
| Baseline | **Naive** | Uses the previous month’s value (`yₜ₋₁`). |
| Seasonal baseline | **Seasonal Naive** (`SNaive`) | Uses the value from 12 months earlier (`yₜ₋₁₂`). |

HistGB was selected during validation for all five reported seeds. Random Forest achieved a slightly lower average MAE in the test comparison, while HistGB achieved the highest within-series R². Therefore, there is no single model that wins across every metric.

## Experimental design
- Target: `VEH_IMD`.
- Forecast horizon: one month ahead.
- Method: time-series forecasting based on log changes. The target is defined as the difference between `log1p` of the current month and `log1p` of the previous month; predictions are transformed back to the original `VEH_IMD` scale.
- Features: 14 features derived from historical data; variance and correlation filters and feature selection are applied within the pipeline.
- TRAIN: through 2023, excluding 2020-03 to 2021-06.
- VALIDATION: 2024.
- TEST: 2025.
- Records after the test period (2026-01 to 2026-03) are not included in the reported evaluation.
- Model and feature-count selection use validation; the test set is reserved for evaluation.
- Five seeds are tracked, and parameters, metrics, and artifacts are logged with MLflow.

## Reported data quality
- 11,528 rows and 22 columns before initial cleaning.
- 82 series in the initial audit; 81 series in the final panel/modeling dataset.
- 37 duplicate series-period records, including 4 with differing values.
- 4 misaligned rows excluded.
- 7,436 `VEH_IMD` values were not parsed correctly due to spaces used as thousands separators; 0 remained after conversion.
- 838 non-positive values were treated as missing.
- Missing months are not interpolated.
- No invalid dates or missing target values were detected before cleaning.

## Reproduction
1. Open the notebook in Google Colab.
2. Run the cells in order.
3. Upload the MTC file used in the experiment.
4. Confirm that its MD5 is `bb6e20c8830af2511da8746ca42f6aa3` to reproduce the documented run exactly.
5. Run the audit, training, repeatability, and MLflow steps.
6. Check `results_summary.csv`, `results_by_model.csv`, the manifest, and outputs for each seed.

## Scope and cautions
MAE is expressed on the scale of `VEH_IMD`; its practical interpretation depends on the exact unit used in the source file. Performance reflects the test period and toll stations included in this dataset. It does not constitute external validation on other road networks or future periods, nor is it a guarantee of operational performance.

## Updated comparative results (TEST, five seeds)
| Model | MAE | MASE | Within-series R² | Skill vs. best baseline |
|---|---:|---:|---:|---:|
| Random Forest | 174.01 ± 3.29 | 0.4548 ± 0.0015 | 0.6823 | +0.2946 |
| HistGradientBoosting | 174.75 ± 0.00 | 0.4844 ± 0.0000 | 0.7199 | +0.2916 |
| SARIMA(1,1,1)×(1,1,1,12) | 244.67 ± 0.00 | 0.6927 ± 0.0000 | 0.5628 | +0.0082 |
| Naive | 246.69 ± 0.00 | 0.6125 ± 0.0000 | 0.2787 | +0.0000 |
| Ridge | 249.99 ± 0.00 | 0.6398 ± 0.0000 | 0.3267 | -0.0134 |
| ARIMA(1,1,1) | 252.00 ± 0.00 | 0.6694 ± 0.0000 | 0.3154 | -0.0215 |
| Seasonal Naive | 363.43 ± 0.00 | 0.9716 ± 0.0000 | 0.2527 | -0.4732 |

HistGB was selected during validation in 5/5 seeds. Random Forest recorded the lowest average MAE, while HistGB recorded the highest within-series R². Selection during validation does not mean that a model is superior across all metrics.
