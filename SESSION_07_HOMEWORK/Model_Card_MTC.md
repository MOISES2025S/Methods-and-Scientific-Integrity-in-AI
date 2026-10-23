# Model Card

**Research title:** A Reproducible Trustworthy Artificial Intelligence Framework for Traffic-Flow Forecasting Using Open Data from Peru’s National Road Network


## 1. Identification
- **Nombre del sistema:** Pipeline reproducible de pronóstico de flujo vehicular MTC.
- **Artifact version:** `MTC_Reproducible_Pipeline_v7_ARIMA_SARIMA.ipynb`.
- **Dominio:** movilidad y transporte por carretera.
- **Tarea:** pronóstico mensual a un paso del indicador `VEH_IMD` for each toll station.
- **Main reported model:** HistGradientBoosting (`HistGB`).
- **Data source:** MTC, Portal Nacional de Datos Abiertos, flujo vehicular registrado en unidades de peaje de la Red Vial Nacional (2014–2026-I).

## 2. Intended use
Support temporal-pattern analysis and planning based on estimated monthly vehicle flow at each toll station. It can serve as an analytical prototype for exploring trends, comparing methods, and assessing the usefulness of short-term forecasts.

## 3. Out-of-scope uses
- Do not use predictions as the sole basis for critical road-safety, budget-allocation, or public-policy decisions.
- Do not assume performance will generalise to unevaluated toll stations, regions, or periods.
- Do not present the model as causal: it predicts observed patterns and does not estimate causal effects.
- Do not treat the reported metrics as external validation.

## 4. Data and target
- **Target:** `VEH_IMD`.
- **Granularidad:** monthly series by peaje.
- **Periodo observado en la auditoría:** enero de 2014 a marzo de 2026.
- **Series identifier:** `CODIGO_PEAJE`.
- **Features temporales:** `PERIODO` (YYYYMM), o `ANIO` + `MES`, o `FECHA`, según el formato de origen.
- **MD5 fingerprint of the file used in the run:** `bb6e20c8830af2511da8746ca42f6aa3`.

## 5. Models used
The notebook compares tres modelos de aprendizaje automático, dos modelos estadísticos de series temporales y dos métodos de referencia (baselines):

| Tipo | Modelo | Función en el experimento |
|---|---|---|
| Modelo de regresión lineal regularizada | **Ridge Regression** (`Ridge`) | Modelo de referencia de aprendizaje automático; regulariza los coeficientes para controlar su magnitud. |
| Tree ensemble | **Random Forest Regressor** (`RandomForestRegressor`) | Combina predicciones de múltiples árboles de decisión. |
| Tree boosting | **HistGradientBoosting Regressor** (`HistGradientBoostingRegressor`, `HistGB`) | Construye árboles secuenciales para reducir el error; fue seleccionado como modelo principal por validación en las cinco semillas reportadas. |
| Statistical model | **ARIMA(1,1,1)** | Modelo autorregresivo integrado de media móvil, sin componente estacional explícito. |
| Seasonal statistical model | **SARIMA(1,1,1)×(1,1,1,12)** | Modelo ARIMA con estacionalidad anual para datos mensuales. |
| Baseline ingenuo | **Naive** | Pronostica el valor del mes anterior (`yₜ₋₁`). |
| Baseline estacional | **Seasonal Naive** (`SNaive`) | Pronostica el valor del mismo mes del año anterior (`yₜ₋₁₂`). |

La selección del modelo y de `k` (número de variables seleccionadas) se realiza con VALIDATION. ARIMA y SARIMA amplían la comparación con métodos estadísticos clásicos; los baselines permiten medir mejoras frente a reglas sencillas.

## 6. Method
Se utiliza un **método de pronóstico de series temporales basado en variaciones logarítmicas**. El objetivo se expresa como el cambio entre el logaritmo del flujo vehicular del mes actual y el del mes anterior; después, las predicciones se convierten nuevamente a la escala original de `VEH_IMD`. El cuaderno construye 14 variables a partir de datos históricos y aplica filtros de varianza y correlación, además de selección de variables dentro del pipeline. La selección del modelo y del número de variables (`k`) se realiza con VALIDATION; TEST se reserva para la evaluación final. HistGradientBoosting (HistGB) fue seleccionado en validación en 5/5 semillas. ARIMA y SARIMA se incorporan como comparadores estadísticos.

## 7. Partición temporal
- **TRAIN:** hasta 2023, excluyendo marzo de 2020 a junio de 2021.
- **VALIDATION:** 2024.
- **TEST:** 2025.
- **Fuera del test:** enero–marzo de 2026.

Para la ejecución con semilla 42, el cuaderno informa 6,067 filas de entrenamiento, 704 de validación y 763 de test, distribuidas en 81 series modelables.

## 8. Rendimiento reportado
### HistGB, prueba 2025 (5 semillas)
| Métrica | Resultado |
|---|---:|
| MAE | 174.75 ± 0.00 |
| RMSE | 395.71 |
| MAPE | 5.22 % |
| MASE | 0.4844 ± 0.0000 |
| R² within | 0.7199 ± 0.0000 |
| Skill vs. Seasonal Naive | +0.5192 |
| Skill vs. mejor baseline | +0.2916 ± 0.0000 |

HistGB fue seleccionado en validación en 5/5 semillas. La comparación por modelo reporta:
- Random Forest: MAE 174.01 ± 3.29; MASE 0.4548 ± 0.0015; R² within 0.6823; skill versus the best baseline +0.2946.
- HistGB: MAE 174.75 ± 0.00; MASE 0.4844 ± 0.0000; R² within 0.7199; skill +0.2916.
- SARIMA(1,1,1)×(1,1,1,12): MAE 244.67 ± 0.00; MASE 0.6927 ± 0.0000; R² within 0.5628; skill +0.0082.
- Naive: MAE 246.69 ± 0.00; MASE 0.6125 ± 0.0000; R² within 0.2787.
- Ridge: MAE 249.99 ± 0.00; MASE 0.6398 ± 0.0000; R² within 0.3267; skill -0.0134.
- ARIMA(1,1,1): MAE 252.00 ± 0.00; MASE 0.6694 ± 0.0000; R² within 0.3154; skill -0.0215.
- Seasonal Naive: MAE 363.43 ± 0.00; MASE 0.9716 ± 0.0000; R² within 0.2527; skill -0.4732.

Random Forest presenta el MAE promedio más bajo de la tabla, mientras HistGB registra el mayor R² within. Por ello, no debe afirmarse que HistGB gana todas las métricas. El valor de MAE del baseline Naive fue 246.69; el de Seasonal Naive, 363.43. RandomForest obtuvo MAE medio 174.01 ± 3.29, MASE 0.4548 ± 0.0015 y skill versus the best baseline +0.2946. Por tanto, RandomForest muestra un MAE promedio ligeramente menor, aunque el procedimiento del cuaderno seleccionó HistGB como modelo principal en todas las semillas según validación.

### Validación 2024, semilla 42
MAE 236.75; RMSE 575.63; MAPE 8.36 %; R² within 0.5595; MASE 0.5408.

## 9. Reproducibility
- La ejecución con semilla 42 se repitió dos veces y generó salida idéntica.
- Se registraron cinco semillas: 0, 1, 2, 3 y 42.
- MLflow guarda parámetros, commit de Git, MD5, métricas y artefactos.
- El cuaderno fija versiones de `numpy`, `pandas`, `scikit-learn`, `openpyxl` y `mlflow` en `requirements.txt`.
- La reproducibilidad exacta depende de utilizar el mismo archivo de datos y entorno compatible.

## 10. Limitations y riesgos
- Los duplicados serie-periodo deben tratarse con cuidado: la auditoría identificó 37 casos, incluidos 4 con valores distintos.
- Los valores no positivos de `VEH_IMD` se tratan como faltantes para el modelado.
- Los meses faltantes no se interpolan; esto reduce el número de observaciones utilizables.
- La evaluación reportada cubre el año 2025; los datos de 2026 no forman parte del test.
- El MAPE puede ser sensible a valores cercanos a cero; conviene interpretarlo junto con MAE, RMSE y MASE.
- La ausencia de variación de algunas métricas entre semillas refleja resultados idénticos en esta configuración, no incertidumbre nula del fenómeno.
- Se requiere validación posterior en nuevos periodos y análisis por peaje antes de cualquier uso operativo.

## 11. Mantenimiento
Ante una actualización de los datos, registrar nombre de archivo, fecha de descarga, licencia, MD5, periodo cubierto, cambios de esquema y nuevas métricas temporales. No actualizar el modelo sin volver a ejecutar la auditoría y conservar el test temporal fuera del proceso de selección.
