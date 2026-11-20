# LEGAL COMPLIANCE CHECKLIST
## Session 11 – Responsible Data Management

**Researcher:** Moisés Evangelista Gamarra  
**Research:** *A Reproducible Trustworthy Artificial Intelligence Framework for Traffic-Flow Forecasting Using Open Data from Peru’s National Road Network*  
**Source:** Ministerio de Transportes y Comunicaciones (MTC), Datos Abiertos del Perú  
**Versión:** 0.1  
**Date:** 19 November 2026

## Dataset catalogue facts relevant to compliance

| Field | Catalogue value |
|---|---|
| Publisher | Ministerio de Transportes y Comunicaciones – MTC |
| Catalogue identifier | `2281b672-9fcf-412f-aab3-5fd72ea700f4` |
| Release date | 2025-06-25 |
| Modified date | 2026-06-05 |
| Public Access Level | Public |
| Licence in supplied metadata document | **Open Data Commons Attribution License** |
| Earlier catalogue snapshot | **License Not Specified** |
| Tags | Transporte; Peajes |

**Key distinction:** Public access is not the same as an open licence or permission to redistribute. Since the catalogue states “License Not Specified”, this project does not assume permission to republish the original CSV or adapted copies. The source file is excluded from the planned GitHub/Zenodo public release unless MTC terms or written authorization establish otherwise.

## 12-point checklist

| # | Control from Session 11 | Preliminary status | Evidence / action required |
|---:|---|---|---|
| 1 | Lawful basis recorded (consent / legitimate interest) | N/A – provisional | The inspected source appears to contain aggregate station-period counts and no direct personal identifiers. Record the basis for concluding that personal-data processing is not currently identified; reassess if sources are joined or personal data appear. |
| 2 | Consent is specific, informed and documented | N/A – current scope | No human participants, survey, or interview are planned. Obtain an institutional ethics determination if required. |
| 3 | Sensitive data identified (health, biometric, ethnicity) | Yes – initial schema review | No sensitive personal-data fields are apparent in the inspected CSV. Recheck all future sources and derived datasets. |
| 4 | Data minimization – only what the study needs | Action required | Inspect the three unnamed trailing columns. Two are empty; the last has four values (0, 60, 363, 184). Establish their meaning before excluding them from an analytical derivative; preserve the original file unchanged. |
| 5 | Ley 29733 obligations mapped to this project | Action required | Document the personal-data applicability assessment and verify applicable obligations with current official guidance/institutional counsel. Do not treat the schema review as a legal determination. |
| 6 | GDPR checked – any EU data subjects? | N/A – current scope, conditional | No EU data subjects are currently identified. Reassess if data subjects, processing operations, or territorial circumstances change. |
| 7 | Cross-border transfer mechanism in place if needed | Conditional – verify | No personal data are currently apparent. Verify Google Drive account terms and storage-region information; assess transfer requirements if personal data are later processed across borders. |
| 8 | Storage location, encryption and access controls set | Action required | Configure and document Google Drive access restrictions, MFA, encryption/security settings, backup copies, and restoration tests. Do not assume settings are already active. |
| 9 | Breach-response plan (ANPD notification as described in lecture) | Action required | Prepare an incident escalation plan and verify current legal notification duties and deadlines against official rules. Do not rely solely on the lecture’s stated deadline without legal verification. |
| 10 | Retention period and secure-deletion date defined | Planned – date pending | Retain project working data and records for five years after thesis defence, subject to longer institutional/legal requirements. Insert actual defence date and calculate review/deletion date. |
| 11 | Data Protection Officer consulted if required | Conditional / N/A provisional | No personal or sensitive personal-data processing is currently apparent. Confirm whether UNMSM, MTC, or another responsible institution requires consultation. |
| 12 | CARE principles applied for Indigenous-community data | N/A – current scope | The described source concerns toll-station traffic counts, not data collected from Indigenous communities. Reassess if community-derived data are introduced. |

## Additional rights and licensing control (essential for this dataset)

| Control | Status | Required action |
|---|---|---|
| Catalogue licence identified | Confirmed metadata | Supplied metadata document reports Open Data Commons Attribution License; earlier catalogue snapshot showed License Not Specified. Verify version, URL, attribution and scope. |
| Public access distinguished from reuse permission | Required control | Do not rely on Public access alone; verify the ODC Attribution licence version, URL, attribution requirements and scope. |
| Source CSV redistribution | Not authorized by this DMP | Do not upload the original XLSX/CSV until the reported ODC Attribution licence has been verified for the resource. |
| Adapted/derived dataset publication | Review required | Assess whether planned outputs reproduce substantial source content or are subject to source restrictions; seek MTC clarification where uncertain. |
| Code licence | Pending | Select a separate licence for researcher-authored code only after ownership, institutional policy, and dependency compatibility checks. |
| Source attribution | Planned | Include dataset title, MTC publisher, catalogue ID, release/modified dates, access level, licence status, and source URL. |

## Evidence to retain

- Snapshot or PDF of the MTC catalogue metadata showing the identifier, dates, Public access level, and “Open Data Commons Attribution License” in the supplied metadata document, alongside the earlier catalogue snapshot.
- Any written clarification or authorization received from MTC concerning reuse, adaptation, and redistribution.
- Data dictionary, source checksum, and preprocessing log.
- Google Drive security/access configuration and backup/restore evidence.
- Ethics-office determination, if required.
- Retention schedule with the actual thesis defence date and deletion/review date.

**Important:** This is a preliminary project checklist based on the supplied dataset metadata, inspected CSV structure, and Session 11 teaching material. It is not legal advice, a formal legal determination, or institutional approval. Verify current legal obligations and MTC reuse conditions before final dissemination.


## National Open Data Platform – institutional context

The platform information supplied for this revision identifies the Secretariat of Digital Government and Digital Transformation, Presidency of the Council of Ministers (PCM), as the institutional contact point. Support details: Calle Schell 310, Miraflores 15074, Lima, Peru; telephone +51 1 219 7000, extension 5111; mesadeayuda@gobiernodigital.gob.pe (email subject: Data). The platform also provides a public suggestion form for proposing data publication: https://facilita.gob.pe/t/1024.

The supplied institutional documentation links cover Emergency Decrees No. 006-2020 and No. 007-2020, the Digital Government Law, and the platform's Data Governance page. Regional reference portals are listed for Colombia, Mexico, and Chile. These are contextual references only. They do not establish permission to reuse or redistribute the MTC traffic-flow dataset.

**Dataset-specific control remains unchanged:** the earlier catalogue snapshot states “License Not Specified”, while the separately supplied MTC metadata document states “Open Data Commons Attribution License”. Confirm the applicable licence, version, URL, attribution requirements, and resource scope before redistributing source files or derivatives.
