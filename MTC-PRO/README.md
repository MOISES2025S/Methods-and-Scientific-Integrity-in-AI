# Reproducible MTC Traffic-Flow Pipeline · Session 5 (UNMSM)

**EN:** One-step-ahead monthly forecasting of `VEH_IMD` per toll station (MTC, Peru's National Road Network). Built so a stranger gets the same number.
**ES:** Pronóstico mensual a un paso de `VEH_IMD` por peaje (MTC, Red Vial Nacional). Hecho para que un extraño obtenga el mismo número.

## Data / Datos
`data/Flujo_vehicular_registrado_en_peajes_2014-2026_I.csv` · MD5 `bb6e20c8830af2511da8746ca42f6aa3` · Source: MTC, Portal Nacional de Datos Abiertos (open data). See `data/DATA_MANIFEST.json`.

## Design / Diseño
- Target: `z_t = log1p(y_t) - log1p(y_t-1)`; forecast `y_t = expm1(log1p(y_t-1) + z_t)` (h = 1 month)
- Split: TRAIN <= 2023 (sin 2020-03..2021-06) · VALID 2024 · TEST 2025 · excluded after test: 2026-01..2026-03
- Data quality: `VEH_IMD` format `miles con espacio '1 234'` (7439 values unreadable without conversion, 0 after); 0 misaligned rows excluded; 838 non-positive values treated as missing; missing months NOT interpolated
- 14 past-only features; variance + |r|>0.95 filter fitted on TRAIN; `SelectKBest` inside the `Pipeline`
- Models: Ridge, RandomForest, HistGradientBoosting vs Naive / Seasonal Naive; model and k chosen on VALID; TEST used once

## How to reproduce / Cómo reproducir
```bash
git clone <this-repo-url> && cd mtc-repro
pip install -r requirements.txt
PYTHONHASHSEED=0 python src/train.py --data "data/Flujo_vehicular_registrado_en_peajes_2014-2026_I.csv" --seed 42
PYTHONHASHSEED=0 python src/run_mlflow.py --data "data/Flujo_vehicular_registrado_en_peajes_2014-2026_I.csv"   # 5 seeds -> results_summary.csv, results_by_model.csv
```

## Test results 2025 · 5 seeds (mean ± SD)
| Model | MAE | MASE | R² within | Skill vs best baseline |
|---|---|---|---|---|
| RandomForest | 173.11 ± 3.07 | 0.4507 ± 0.0012 | 0.6848 ± 0.0213 | +0.3016 |
| HistGB | 173.63 ± 0.00 | 0.4779 ± 0.0000 | 0.7216 ± 0.0000 | +0.2995 |
| Naive (y_t-1) | 247.85 ± 0.00 | 0.6115 ± 0.0000 | 0.2779 ± 0.0000 | +0.0000 |
| Ridge | 250.06 ± 0.00 | 0.6380 ± 0.0000 | 0.3284 ± 0.0000 | -0.0089 |
| SNaive (y_t-12) | 366.22 ± 0.00 | 0.9810 ± 0.0000 | 0.2411 ± 0.0000 | -0.4776 |

Headline metrics: MASE, R² within and skill vs the best baseline. Pooled R² is not reported: it is inflated by between-station variance (saved only as `R2_pooled` in `outputs/`).

## Expected output (seed 42) / Resultado esperado
```json
{
  "modelo_principal": "HistGB",
  "k": "all",
  "test_principal": {
    "MAE": 173.6282,
    "RMSE": 391.2266,
    "MAPE_pct": 5.1569,
    "R2_within": 0.7216,
    "MASE": 0.4779,
    "Skill_vs_SNaive": 0.5259,
    "Skill_vs_mejor_baseline": 0.2995
  },
  "test_Naive": {
    "MAE": 247.8508,
    "RMSE": 630.0859,
    "MAPE_pct": 6.3721,
    "R2_within": 0.2779,
    "MASE": 0.6115,
    "Skill_vs_SNaive": 0.3232,
    "Skill_vs_mejor_baseline": 0.0
  }
}
```

## Environment / Entorno
Python 3.13.15 · packages in `requirements.txt`
