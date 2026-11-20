# MTC dataset — provenance and verification notes

## Identified source

- **Publisher:** Ministerio de Transportes y Comunicaciones (MTC), Peru.
- **Dataset title:** *Flujo vehicular registrado en las Unidades de Peaje de la Red Vial Nacional 2014–2026 I Trimestre*.
- **Official catalogue:** https://www.datosabiertos.gob.pe/dataset/flujo-vehicular-registrado-en-las-unidades-de-peaje-de-la-red-vial-nacional-2014-%E2%80%93-2026-i
- **Access level shown in catalogue:** Public.
- **Catalogue dates recorded in the working protocol:** released 25 June 2025; last modified 5 June 2026. Recheck these dates when downloading the resource.
- **Licence field shown in catalogue:** “License Not Specified”.

## Items requiring reconciliation

| Item | Values currently documented | Required action |
|---|---|---|
| Record count | Portal preview: 11,532; local research materials: 11,528 rows before cleaning. | Compare the exact downloaded CSV and record its checksum, download date and row count. Explain any difference. |
| Time coverage | Dataset title refers to 2014–2026 first quarter; catalogue description has also been reported as mentioning a 31 March 2025 cutoff. | Inspect resource-level metadata and the actual date column; document the true coverage of the analysed file. |
| Licence | “License Not Specified”. | Do not assume an open licence. Confirm reuse and redistribution conditions with the publisher or applicable authority. |
| Personal identifiers | Documented schema does not list names, national IDs, plates, contacts or individual trajectories. | Inspect the exact raw CSV, including free-text fields, before analysis and before any public release. |

## Safe GitHub handling

- Do not upload the original CSV, data dictionary or metadata files unless their terms permit redistribution.
- A public URL does not itself establish an open licence, consent, or exemption from ethics review.
- Prefer documenting reproducible download instructions, source URL, retrieval date, file hash, schema and cleaning steps.
- If a data file is permitted for redistribution, preserve required attribution and terms.
- Keep any file containing personal, confidential, restricted or unpublished institutional information out of the repository.

These notes record issues identified in the current research protocol. They are not a substitute for checking the live catalogue and the exact resource version used in the analysis.
