# Annex IV — Documentation Crosswalk

**Research title:** A Reproducible Trustworthy Artificial Intelligence Framework for Traffic-Flow Forecasting Using Open Data from Peru’s National Road Network


> This matrix is a practical traceability guide accompanying the pipeline. It does not claim formal certification or automatic compliance with any specific standard.

| Documentation area | Evidence available in `MTC_Reproducible_Pipeline_v7_ARIMA_SARIMA.ipynb` | Status |
|---|---|---|
| System identification | Notebook name, monthly forecasting task, and main model HistGradientBoosting (HistGB) | Documented |
| Models evaluated | Ridge Regression, Random Forest Regressor, HistGradientBoosting Regressor, ARIMA(1,1,1), SARIMA(1,1,1)×(1,1,1,12), baseline Naive y Seasonal Naive | Documented |
| Data provenance | MTC National Open Data Portal and dataset URL | Documented |
| Data integrity | MD5 `bb6e20c8830af2511da8746ca42f6aa3` en ejecución | Documented |
| Description and quality | 11,528 rows, 22 columns, period 2014-01 to 2026-03, duplicates, conversions, and exclusions | Documented |
| Target and unit of analysis | `VEH_IMD`, monthly series by `CODIGO_PEAJE` | Documented |
| Evaluation design | TRAIN through 2023, excluding the specified COVID period; VALID 2024; TEST 2025 | Documented |
| Method de pronóstico | Time-series forecasting using log changes in the target, 14 historical features, and conversion back to the original scale | Documented |
| Feature selection and prevention of temporal leakage | Filtros de varianza/correlación y selección dentro del pipeline; TRAIN para ajustes, VALIDATION para seleccionar modelo y `k`, TEST reservado para evaluación final | Descrito en notebook |
| Baseline comparison | Naive y Seasonal Naive; comparación con Ridge, RandomForest, HistGB, ARIMA y SARIMA | Documented |
| Métricas | MAE, RMSE, MAPE, MASE, R² within y skill frente a baselines | Documented |
| Reproducibility | Two identical runs with seed 42; five seeds and MLflow logging | Documented |
| Code versioning | Historial Git y commits mostrados en la ejecución | Documented |
| Software environment | `requirements.txt` generado con versiones de paquetes | Documented |
| Limitations | Test de un solo año, sensibilidad de MAPE cerca de cero, duplicados conflictivos y datos faltantes | Documented / requires follow-up |
| External validation | No independent evaluation on another road network or later period is presented | Pending |
| Error analysis by toll station | The notebook genera artefactos por ejecución; la matriz no afirma que exista análisis operativo completo por peaje | Requires artifact review |
| Privacy and personal data | The described fields concern traffic/toll stations; the notebook does not include a formal privacy assessment | Not formally assessed |
| Impact and use governance | Use limitations and human review are recommended; no formal operational impact assessment is provided | Requiere evaluación antes de despliegue |
| Licensing and redistribution | The notebook advierte verificar licencia antes de versionar datos en Git | Review required before redistribution |

## Interpretación
La ejecución respalda la trazabilidad técnica y la evaluación temporal del prototipo. No constituye por sí sola una auditoría independiente, certificación de cumplimiento, validación externa ni autorización para desplegar el sistema en producción.

## Resultados añadidos de ARIMA y SARIMA
En la tabla de prueba de cinco semillas del notebook: ARIMA(1,1,1) obtuvo MAE 252.00 ± 0.00, MASE 0.6694 ± 0.0000 y R² within 0.3154; SARIMA(1,1,1)×(1,1,1,12) obtuvo MAE 244.67 ± 0.00, MASE 0.6927 ± 0.0000 y R² within 0.5628. Estos valores se consignan como resultados de la salida del notebook, no como una evaluación externa.
