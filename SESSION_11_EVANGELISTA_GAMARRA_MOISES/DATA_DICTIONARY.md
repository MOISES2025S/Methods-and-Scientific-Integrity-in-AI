# DATA DICTIONARY AND SOURCE-PROVENANCE RECORD
## MTC traffic-flow dataset – initial file inspection

## 1. Catalogue provenance

| Element | Value |
|---|---|
| Dataset | Flujo vehicular registrado en las unidades de peaje de la Red Vial Nacional 2014–2026 I |
| Publisher | Ministerio de Transportes y Comunicaciones (MTC), Peru |
| Catalogue identifier | `2281b672-9fcf-412f-aab3-5fd72ea700f4` |
| Dataset cut-off date | 2026-03-31 |
| Metadata creation / last update | 2026-05-31 / 2026-05-31 |
| Public Access Level | Public |
| Update frequency | Quarterly |
| Dataset version | 1.0 |
| Format / language | XLSX / Spanish |
| Coverage | Peru, 2026 |
| Contact | estadistica@mtc.gob.pe |
| Licence in supplied metadata document | **Open Data Commons Attribution License** |
| Earlier catalogue snapshot | **License Not Specified** (release 2025-06-25; modified 2026-06-05) |
| Tags | Transporte; Peajes |
| Metadata description | Catalogue fields compatible with DCAT |
| Landing page | https://www.datosabiertos.gob.pe/dataset/flujo-vehicular-registrado-en-las-unidades-de-peaje-de-la-red-vial-nacional-2014-%E2%80%93-2026-i |

**Rights interpretation:** The supplied MTC metadata document reports an Open Data Commons Attribution License. An earlier catalogue snapshot used in the first DMP draft displayed “License Not Specified”. The project records this discrepancy and will verify the exact licence version, official URL, attribution wording, and whether the licence applies to the relevant XLSX/CSV resource before redistribution. Public access alone is not a substitute for checking licence terms. Until verification is documented, do not publish the original source data.

## 1.1 National Open Data Platform – institutional context

The platform-level contact, policy, governance, and Pacific Alliance portal references supplied for Session 11 are documented in the Data Management Plan and `NATIONAL_OPEN_DATA_PLATFORM_CONTEXT.md`. They are not dataset-level metadata and do not change the MTC dataset's licence status.

## 2. File inspected

- **File:** `Flujo vehicular registrado en peajes_2014-2026_I (1).csv`
- **Delimiter:** semicolon (`;`)
- **Encoding:** Latin-1
- **Rows:** 11,532
- **Columns:** 25 (22 named fields and 3 unnamed trailing fields)
- **Observed period:** 201401–202603
- **Toll-station codes:** 82
- **Departments:** 20
- **Monthly periods:** 147

These are observations from the supplied CSV, not all necessarily catalogue-level metadata. Re-run validation if a new source-file version is downloaded.


## 2.1 Official portal data dictionary supplied

The portal-supplied Excel dictionary is the publisher's field-description reference. It is kept distinct from the earlier CSV structural inspection because the two schemas are not identical. Do not assume that field lists or column counts from different resource versions are interchangeable.

| Variable | Description | Data type | Size | Related source | Additional information |
|---|---|---|---:|---|---|
| ID_FLUJO | Identificador correlativo | Numérico | 10 |  |  |
| ADMINIST | Tipo de administración de la unidad de peaje | Texto | 30 | Fuente: MTC | Valores=[Concesionado,No Concesionado] |
| DEPARTAMENTO | Departamento donde se localiza la unidad de peaje | Texto | 70 |  |  |
| NOMBRE_PEAJE | Denominación de la unidad de peaje | Texto | 70 |  |  |
| VEH_LIGEROS_TAR_DIF | Número de vehículos ligeros con tarifa diferenciada | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_LIGEROS_AUTOMOVILES | Número de vehículos ligeros automóviles | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_PESADOS_TAR_DIF | Número de vehículos pesados con tarifa diferenciada | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_PESADOS_2E | Número de vehículos pesados de 2 ejes | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_PESADOS_3E | Número de vehículos pesados de 3 ejes | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_PESADOS_4E | Número de vehículos pesados de 4 ejes | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_PESADOS_5E | Número de vehículos pesados de 5 ejes | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_PESADOS_6E | Número de vehículos pesados de 6 ejes | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_PESADOS_7E | Número de vehículos pesados de 7 a más ejes | Numérico | 10 | Fuente: PVN/OSITRAN |  |
| VEH_LIGEROS_TOTAL | Total de vehículos ligeros | Numérico | 10 |  |  |
| VEH_LIGEROS_IMD | Índice medio diario de vehículos ligeros | Numérico | 10 |  | El IMD es el cociente obtenido al dividir el total de vehículos registrados entre los días considerados para el registro. |
| VEH_PESADOS_TOTAL | Total de vehículos pesados | Numérico | 10 |  |  |
| VEH_PESADOS_IMD | Índice medio diario de vehículos pesados | Numérico | 10 |  | El IMD es el cociente obtenido al dividir el total de vehículos registrados entre los días considerados para el registro. |
| VEH_TOTAL | Total de vehículos ligeros y pesados | Numérico | 10 |  |  |
| VEH_IMD | Índice medio diario de vehículos ligeros y pesados | Numérico | 10 |  | El IMD es el cociente obtenido al dividir el total de vehículos registrados entre los días considerados para el registro. |
| FECHA_CORTE | Mes en el que se generó el dataset | Numérico | 8 |  | Formato: aaaamm |

## 3. Field groups

| Field | Description based on field name / observed structure | Data handling |
|---|---|---|
| `ADMINIST` | Administration category (`Concesionado`, `No concesionado`) | Categorical text |
| `CODIGO_PEAJE` | Toll-station code | Station identifier; not an individual identifier |
| `DEPARTAMENTO` | Department | Categorical text |
| `NOMBRE_PEAJE` | Toll-station name | Text |
| `VEH_LIGEROS_TAR_DIF` | Light-vehicle category with differentiated tariff | Numeric count; source stored as text |
| `VEH_LIGEROS_AUTOMOVILES` | Light-vehicle automobiles | Numeric count; source stored as text |
| `VEH_PESADOS_TAR_DIF` | Heavy-vehicle category with differentiated tariff | Numeric count; source stored as text |
| `VEH_PESADOS_2E`–`VEH_PESADOS_7E` | Heavy vehicles by axle category | Numeric counts; source stored as text |
| `VEH_LIGEROS_TOTAL` | Total light vehicles | Numeric count; source stored as text |
| `VEH_LIGEROS_IMD` | Average daily traffic indicator for light vehicles | Numeric indicator; confirm official definition |
| `VEH_PESADOS_TOTAL` | Total heavy vehicles | Numeric count; source stored as text |
| `VEH_PESADOS_IMD` | Average daily traffic indicator for heavy vehicles | Numeric indicator; confirm official definition |
| `VEH_TOTAL` | Total vehicles | Numeric count; source stored as text |
| `VEH_IMD` | Overall average daily traffic indicator | Candidate main research indicator; confirm official definition, unit, and calculation |
| `ANIO` | Year | Integer |
| `MES` | Month number | Integer |
| `PERIODO` | Year-month key, observed as YYYYMM | Integer or ISO year-month string |

The exact official definitions, units, formulas, and collection methodology must be taken from MTC documentation. Do not infer them solely from column names.

## 4. Initial quality observations

- No missing values were observed in the first 22 named columns in the supplied file.
- `Unnamed: 22` and `Unnamed: 23` are entirely empty.
- `Unnamed: 24` has four non-empty values (0, 60, 363, 184). Their meaning is not established; investigate before excluding this field from a derivative.
- There are no exact duplicate rows.
- There are 37 repeated combinations of `CODIGO_PEAJE` and `PERIODO`; these correspond to different `ADMINIST` categories. The triple `CODIGO_PEAJE` + `PERIODO` + `ADMINIST` is unique.
- Numeric traffic values are stored as text with spaces as thousands separators. Convert carefully and validate totals after parsing.
- Preserve the source CSV unchanged. Perform cleaning in a separate script and derivative file.

## 5. Data handling and publication rules

1. Preserve the original source file as a read-only reference, subject to applicable terms and institutional retention requirements.
2. Record the retrieval date and calculate a cryptographic checksum for each downloaded version.
3. Never silently delete or reinterpret the four non-empty values in `Unnamed: 24`.
4. Document parsing, cleaning, transformations, exclusions, and validation in code.
5. Publish code and documentation, not the original CSV, until the ODC Attribution licence version, official URL, attribution terms, and resource scope have been verified.
6. The supplied metadata document reports an **Open Data Commons Attribution License**; an earlier catalogue snapshot showed **License Not Specified**. Verify the exact licence version, URL, attribution terms, and resource scope before redistribution.
7. Seek MTC clarification before redistribution of the source or a derivative that may reproduce protected content.
