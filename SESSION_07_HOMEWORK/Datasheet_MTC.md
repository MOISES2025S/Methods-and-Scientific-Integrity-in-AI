# Datasheet

**Research title:** A Reproducible Trustworthy Artificial Intelligence Framework for Traffic-Flow Forecasting Using Open Data from Peru’s National Road Network


## 1. Identification and provenance
- **Dataset:** flujo vehicular registrado en las unidades de peaje de la Red Vial Nacional.
- **Entidad fuente:** Ministerio de Transportes y Comunicaciones (MTC), Perú.
- **Portal:** Portal Nacional de Datos Abiertos del Perú.
- **URL:** https://www.datosabiertos.gob.pe/dataset/flujo-vehicular-registrado-en-las-unidades-de-peaje-de-la-red-vial-nacional-2014-%E2%80%93-2026-i
- **Huella del archivo usado en el notebook:** MD5 `bb6e20c8830af2511da8746ca42f6aa3`.
- **Archivo:** el notebook conserva el nombre exacto en `data/DATA_MANIFEST.json`; it is selected during upload to Colab.

## 2. Contents
The notebook audits a file with 11,528 filas y 22 columnas antes de la depuración inicial. The audit covers enero de 2014 a marzo de 2026. The toll-station identifier is `CODIGO_PEAJE`, the target is `VEH_IMD` and the dataset includes administration and location fields, light- and heavy-vehicle counts, totals, and period information.

## 3. Unit of observation
Each row represents a vehicle-flow record associated with a toll station and a time period. The pipeline converts the data into monthly time series by `CODIGO_PEAJE`.

## 4. Relevant fields
- `CODIGO_PEAJE`: identificador de la serie por peaje.
- `NOMBRE_PEAJE`: nombre del peaje.
- `DEPARTAMENTO`: ubicación administrativa.
- `ADMINIST`: tipo de administración reportado.
- `PERIODO`, `ANIO`, `MES`, `FECHA`: campos para reconstruir el tiempo, según disponibilidad.
- `VEH_IMD`: variable objetivo del pronóstico.
- Features `VEH_LIGEROS_*` y `VEH_PESADOS_*`: conteos o indicadores de clases de vehículos presentes en el archivo.

## 5. Identified data quality
- Original rows: 11,528.
- Columnas originales: 22.
- Series identificadas inicialmente: 82.
- Periodo mínimo y máximo: 2014-01-01 a 2026-03-01.
- Duplicados exactos: 0.
- Duplicados por serie-periodo: 37.
- De los duplicados serie-periodo, 4 presentan valores distintos.
- Fechas inválidas: 0.
- Filas desalineadas excluidas: 4.
- `VEH_IMD` nulo en la auditoría inicial: 0.
- Valores de `VEH_IMD` que no se interpretan sin conversión: 7,436, por el formato de miles con espacio, por ejemplo `1 234`.
- Valores no numéricos después de la conversión: 0.
- Valores de `VEH_IMD` menores o iguales a cero: 838, tratados como faltantes.
- Columnas vacías eliminadas: `UNNAMED: 22` y `UNNAMED: 23`.
- Filas modelables después de la construcción de rezagos: el reporte de semilla 42 contiene 6,067 de entrenamiento, 704 de validación y 763 de prueba; se modelan 81 series.

## 6. Procesamiento
1. Carga del archivo CSV/XLSX.
2. Identificación de la columna temporal y del identificador de serie.
3. Conversión del objetivo `VEH_IMD` a formato numérico.
4. Auditoría de duplicados, fechas, valores no positivos y registros desalineados.
5. Exclusión de filas desalineadas y tratamiento de valores no positivos como faltantes.
6. Construcción de 14 variables históricas a partir del pasado, sin usar información futura.
7. Transformación del objetivo mediante variaciones logarítmicas entre meses consecutivos y retorno de las predicciones a la escala original.
8. Aplicación de filtros de varianza y correlación y selección de variables dentro del pipeline; los ajustes se realizan con TRAIN.
9. Missing months are not interpolated.
10. División cronológica TRAIN/VALID/TEST; la selección del modelo y de `k` se realiza con VALIDATION y TEST se reserva para la evaluación final.

## 7. Modelos de pronóstico comparados
El pipeline no utiliza un único algoritmo sin comparación. Evalúa los siguientes métodos:

- **Ridge Regression (`Ridge`):** regresión lineal regularizada.
- **Random Forest Regressor (`RandomForestRegressor`):** ensamble de árboles de decisión.
- **HistGradientBoosting Regressor (`HistGradientBoostingRegressor` o `HistGB`):** método de boosting basado en árboles.
- **Naive:** baseline que utiliza el último valor observado, `yₜ₋₁`.
- **Seasonal Naive (`SNaive`):** baseline que utiliza el valor de hace 12 meses, `yₜ₋₁₂`.

El modelo y el número de variables `k` se seleccionan usando el año de validación 2024; el conjunto de prueba 2025 se reserva para la evaluación final. En los resultados documentados, HistGB fue seleccionado en las cinco semillas. Random Forest también se compara y presenta un MAE promedio ligeramente menor en la tabla de resultados por modelo; por ello, la selección de HistGB como modelo principal debe interpretarse como resultado del criterio de selección configurado en validación, no como superioridad en todas las métricas.

## 8. Usos previstos y limitaciones
El dataset se utiliza para investigación y desarrollo de pronósticos de flujo vehicular mensual. Los resultados dependen de la cobertura, calidad y consistencia de los registros de los peajes incluidos. Antes de compartir el conjunto, debe revisarse la licencia y las condiciones de redistribución del portal de datos abiertos, como advierte el notebook.

## 9. Recomendaciones de gobernanza
Mantener el manifiesto con nombre de archivo, URL, fecha de obtención, huella, periodo cubierto y versión. Documentar cualquier cambio en nombres de columnas, unidades, cobertura de peajes o reglas de consolidación de duplicados. Conservar un registro de exclusiones y evitar modificar datos originales sin dejar trazabilidad.

## 8. Modelos comparados en la versión actualizada
The notebook actualizado incluye Naive, Seasonal Naive, Ridge Regression, Random Forest Regressor, HistGradientBoosting Regressor, ARIMA(1,1,1) y SARIMA(1,1,1)×(1,1,1,12). Las métricas comparativas se documentan en la Model Card y README. ARIMA y SARIMA son comparadores estadísticos, no se describen como ganadores del experimento.
