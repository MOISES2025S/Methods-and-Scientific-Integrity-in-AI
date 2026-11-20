# Session 09 — Research Ethics Protocol

**Researcher:** Moisés Evangelista Gamarra  
**Instructor:** Dr. Loveleen Gaur  
**Institution:** Universidad Nacional Mayor de San Marcos (UNMSM)  
**Course:** Research Methods and Scientific Integrity in AI and Advanced Technologies  
**Version:** Draft v0.1 — 19 November 2026

## Contents

- `RESEARCH_ETHICS_PROTOCOL.md`: readable, version-control-friendly Markdown version of the protocol.
- `RESEARCH_ETHICS_PROTOCOL.docx`: formatted Word companion.
- `DATA_SOURCE_NOTES.md`: provenance, known inconsistencies and checks to complete before final submission.
- `CITATION.cff`: citation metadata for this repository.
- `.gitignore`: excludes local data, credentials, temporary files and model artifacts.

## Research scope

The protocol describes a secondary-data study using monthly vehicle-flow records published by Peru’s Ministry of Transport and Communications (MTC). It does not plan to recruit or interact with human participants. This is a draft for academic review; it is **not** an ethics approval or a determination that review is unnecessary. The competent UNMSM office must determine the appropriate ethics pathway.

## Before pushing to a public GitHub repository

1. Review `DATA_SOURCE_NOTES.md` and reconcile the source-file record count and coverage dates.
2. Inspect the exact CSV for unexpected identifiers or personal information.
3. Confirm the source dataset licence and redistribution conditions. The catalogue currently reports **“License Not Specified”**; do not commit the raw CSV or derived material whose redistribution rights are unclear.
4. Remove local paths, credentials, tokens, private data and unapproved institutional documents.
5. Confirm whether the course platform expects the protocol alone or supporting materials as well.

## Suggested repository title

`SESSION_9_EVANGELISTA_GAMARRA_MOISES`

## Important

Do not add a repository licence (for example, MIT or CC BY) until you have decided what content you own and are authorised to license. A licence for this repository would not override the MTC dataset's terms.
