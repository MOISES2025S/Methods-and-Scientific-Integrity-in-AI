# DATA MANAGEMENT PLAN (DMP)
## Responsible Data Management: FAIR Principles & Privacy

**Researcher:** Moisés Evangelista Gamarra  
**Programme:** Doctoral Program in Deep Technologies – Universidad Nacional Mayor de San Marcos (UNMSM)  
**Course:** Research Methods & Scientific Integrity in AI – Session 11  
**Instructor:** Dr. Loveleen Gaur  
**Versión:** 0.1  
**Date:** 19 November 2026  

**Research title:** *A Reproducible Trustworthy Artificial Intelligence Framework for Traffic-Flow Forecasting Using Open Data from Peru’s National Road Network.*

---

## Dataset identification and catalogue metadata

| Metadata element | Catalogue value |
|---|---|
| Dataset title | Flujo vehicular registrado en las unidades de peaje de la Red Vial Nacional 2014–2026 I |
| Publisher | Ministerio de Transportes y Comunicaciones (MTC), Peru |
| Catalogue identifier | `2281b672-9fcf-412f-aab3-5fd72ea700f4` |
| Dataset landing page | https://www.datosabiertos.gob.pe/dataset/flujo-vehicular-registrado-en-las-unidades-de-peaje-de-la-red-vial-nacional-2014-%E2%80%93-2026-i |
| Dataset cut-off date | 31 March 2026 |
| Metadata creation date | 31 May 2026 |
| Metadata last update | 31 May 2026 |
| Update frequency | Quarterly |
| Dataset version | 1.0 |
| Public access level | Public |
| Licence stated in supplied metadata document | **Open Data Commons Attribution License** |
| Language / format | Spanish / XLSX |
| Coverage | Peru, 2026 |
| Source institutions | MTC; data sources identified as PVN / OSITRAN |
| Contact | estadistica@mtc.gob.pe |
| Tags | Transporte; red vial; peaje; flujo vehicular; tráfico vehicular |
| Earlier catalogue snapshot | Release date 25 June 2025; modified date 5 June 2026; licence shown as “License Not Specified” |

**Critical rights statement.** The supplied MTC dataset metadata document reports an Open Data Commons Attribution License. An earlier catalogue snapshot used in the first DMP draft displayed “License Not Specified”. These source records therefore contain a licence-metadata discrepancy. The DMP records the licence stated in the supplied metadata document, but before redistributing the source XLSX/CSV or adapted data, the researcher must verify the exact licence version, official licence URL, attribution wording, and that the licence applies to the relevant resource and all underlying data. Until this verification is documented, do not upload the original source data to GitHub or Zenodo. Public access alone is not a substitute for checking the licence terms.

## National Open Data Platform – institutional information

The following institutional information was transcribed from the National Open Data Platform information supplied for this revision. It describes the platform's administration and support channels; it is not dataset-level metadata and does not establish the MTC dataset's licence or reuse conditions.

### Secretariat of Digital Government and Digital Transformation
**Presidency of the Council of Ministers (PCM)**

- **Address:** Calle Schell 310, Miraflores 15074, Lima, Peru.
- **Telephone switchboard:** +51 1 219 7000, extensions 5111.
- **Support email:** mesadeayuda@gobiernodigital.gob.pe.
- **Email subject:** Data.
- **Public data requests and suggestions:** [Share your opinion on which public or private data should be published on the National Open Data Platform](https://facilita.gob.pe/t/1024).

### Institutional documentation

- [Emergency Decree establishing the National Digital Transformation System (Decreto de Urgencia No. 006-2020)](https://www.gob.pe/institucion/pcm/normas-legales/395320-006-2020).
- [Emergency Decree approving the Digital Trust Framework (Decreto de Urgencia No. 007-2020)](https://www.gob.pe/institucion/pcm/normas-legales/395322-007-2020).
- [Digital Government Law (Ley de Gobierno Digital)](https://www.datosabiertos.gob.pe/sites/default/files/leydigital.pdf).
- [Data Governance – National Open Data Platform](https://www.datosabiertos.gob.pe/%C2%BFqu%C3%A9-es-gobernanza-de-datos).

### Pacific Alliance – national open-data portals

- [Colombia – Datos Abiertos](https://www.datos.gov.co/).
- [Mexico – datos.gob.mx](https://datos.gob.mx/).
- [Chile – Datos.gob.cl](https://datos.gob.cl/).

**Use in this research.** These links provide institutional, policy, governance, support, and regional open-data context. They are not evidence that the MTC traffic-flow dataset is licensed for redistribution. Dataset-specific rights remain subject to the separate MTC metadata records and licence verification described above.

## 1. Data description

The research uses secondary traffic-flow records published in the MTC open-data catalogue, concerning vehicles recorded at toll stations on Peru’s National Road Network. The inspected CSV contains **11,532 records and 25 columns**, covering **January 2014 to March 2026**, with **82 toll-station codes**, **20 departments**, and **147 monthly periods**. The visible fields describe administration category, toll-station code and name, department, light- and heavy-vehicle categories and totals, average daily traffic indicators, year, month, and reporting period. `VEH_IMD` is the candidate principal traffic-flow indicator; its official definition, unit, and calculation must be confirmed from MTC documentation before final modelling and publication.

The portal also provides a separate Excel data dictionary. It defines fields including `ID_FLUJO`, `ADMINIST`, `DEPARTAMENTO`, `NOMBRE_PEAJE`, vehicle-category counts and totals, `VEH_LIGEROS_IMD`, `VEH_PESADOS_IMD`, `VEH_TOTAL`, `VEH_IMD`, and `FECHA_CORTE`. This official dictionary must be treated as the publisher's field-description reference. Its schema is not identical to the earlier CSV inspection described below; the researcher will map the two versions explicitly rather than assuming that similarly named fields or column counts are interchangeable.

The supplied file is semicolon-delimited and encoded in Latin-1. Numeric traffic fields are represented as text with spaces used as thousands separators. The CSV has 22 named fields and three unnamed trailing columns: two are empty, while the last contains four values (0, 60, 363, and 184). The meaning of those four values is not established by the visible schema. They must be investigated against the publisher’s source documentation; they must not be silently discarded or interpreted. The untouched source file will be retained as a read-only reference, and any cleaning will occur in a separately documented derivative.

The initial structural inspection found no direct personal identifiers (such as names, identity numbers, registration plates, telephone numbers, or individual travel trajectories) in the visible columns. This is a limited schema-based observation, not a guarantee that all possible linkage, inference, confidentiality, or legal risks are absent. The assessment will be revisited if additional datasets, fine-grained records, or external sources are joined.

> ## ## 2. FAIR compliance

**Findable.** We will keep the dataset title, MTC as the publisher, the catalogue identifier, the official landing-page link, the release and modified dates, the catalogue tags, the date we accessed the data, the file name and, where available, its checksum. The README and data dictionary will explain where the data came from and how we prepared it. We may publish the research code and documentation on GitHub and archive them in Zenodo. We will only include a DOI once the deposit has actually been completed.

**Accessible.** The dataset can be found in the MTC catalogue, where its access level is listed as Public. However, the metadata document supplied for this assignment reports an Open Data Commons Attribution License, while an earlier catalogue snapshot shows “License Not Specified”. We will keep this difference on record and check the exact licence version, official link, attribution requirements and the resources it covers before sharing the original XLSX/CSV files or adapted data. Until that check is complete, we will not upload the source data to GitHub, Zenodo or any other public repository. The repository can still include our code, documentation, metadata and research outputs that are cleared for publication, along with a link to the official source. In short, public access lets people find the dataset; it does not automatically give permission to redistribute it.

**Interoperable.** Our scripts will explain how we read the semicolon-separated file, handled its Latin-1 encoding, converted numeric values written as text with spaces, standardised dates and periods, assigned data types and checked the results. The analytical files will use UTF-8 and clearly documented variable names. We will keep the original field names in the provenance notes and describe every change. We will also retain DCAT-compatible catalogue metadata. This helps different catalogues exchange information; it does not define the dataset’s licence.

**Reusable.** We will make the research workflow easier to follow by sharing the code, documentation, data dictionary, source history, software and dependency versions, and clear instructions to reproduce the analysis. We will not apply a new licence to the original MTC data. Before redistributing it, we must confirm the exact version and scope of the licence reported in the supplied metadata, as well as the required attribution. We will assign a separate licence to our own code only after checking authorship, institutional ownership, third-party dependencies and licence compatibility. Any derived tables or outputs will be shared only after checking that publication is allowed and that they do not disclose restricted information.

## 6. Sharing plan

The public GitHub repository will include the code developed for this research, the README, data dictionary, source information, configuration examples without passwords or other secrets, instructions to reproduce the work, and research outputs that have been cleared for publication. It will not include the original MTC CSV, credentials, private Google Drive links, access tokens or any data for which redistribution rights have not yet been confirmed.

To make the source easy to identify, the repository will show its official title, MTC as the publisher, catalogue identifier, relevant dates, public access status, licence information and official landing-page link. It will clearly state: “Catalogue licence: License Not Specified; source CSV not redistributed.” Our code will have its own licence only after we have checked ownership and dependencies. We may also archive a version of the code and documentation in Zenodo, but we will not claim a DOI until the deposit is complete. If the MTC later provides a clear licence or written permission, we will review and update this sharing plan before redistributing any source data.

## 3. Anonymization strategy and privacy risk

The inspected file appears to contain aggregate counts by toll station and month rather than person-level records. Its visible schema does not include direct personal identifiers. Person-level k-anonymity, l-diversity, t-closeness, or differential privacy will not be applied automatically: these techniques address particular disclosure risks and should be selected only where a suitable threat model and data structure justify them. Applying noise to aggregate traffic counts without a defensible need could distort the measurements used for forecasting.

The project will apply data minimization and a linkage-risk review. The researcher will check whether added datasets, metadata, or external sources could make a record attributable to an identifiable person or reveal sensitive information. Public outputs will focus on model methods, evaluation, and appropriately aggregated results. If personal or sensitive data are introduced, processing will pause until a revised privacy assessment, lawful basis, safeguards, and any required ethics/legal review are completed.

## 4. Storage and backup

The primary working location will be Google Drive, preferably an institutionally managed Google Workspace account where available. The researcher will verify the account type, provider terms, actual storage region (if disclosed), administrative controls, and applicable institutional policies; no specific data-residency location is assumed. The original CSV will be kept in a restricted, read-only `raw/` folder. Cleaned derivatives, scripts, documentation, and outputs will be separated. Access will be limited to authorized collaborators, multi-factor authentication will be enabled, and public link sharing will be disabled unless specifically required and approved.

The project will implement a 3-2-1 backup approach: three copies, on at least two different storage types, with one copy stored separately/off-site. Google Drive synchronization alone does not constitute three independent backups. A proposed arrangement is the controlled Drive working copy, an encrypted external-drive backup, and a second independently managed backup. Backup frequency, integrity checks, restoration tests, and access permissions will be recorded. Encryption and recovery settings will be checked for each storage medium.

## 5. Legal and ethical compliance

The catalogue metadata supplied for this DMP identifies the publisher as the MTC, access level as Public, and licence as **License Not Specified**. The project will not infer a copyright waiver, open licence, or permission to redistribute from the Public access field. Before reproducing the source CSV, publishing substantial extracts, or distributing adapted data, the researcher will seek clarification of applicable MTC terms and record the response. Until then, the original CSV will not be included in public repositories. The catalogue’s public availability and the project’s research use are documented separately from the legal permission to redistribute.

The project will assess Peru’s **Law No. 29733, Personal Data Protection Law**, and its Regulation approved by **Supreme Decree No. 016-2024-JUS**, to the extent that personal-data processing is involved. The current CSV schema review does not identify direct personal-data fields, but this does not replace institutional or legal review. GDPR applicability will be considered only if the project’s data subjects, processing activities, or territorial circumstances create a relevant EU connection; it is not assumed to apply merely because a cloud service is used. Cross-border transfer safeguards will be assessed if personal data are later transferred to or accessed from another country.

The current study does not recruit human participants or collect interviews, surveys, health data, biometric data, or Indigenous-community data. Participant consent and CARE-based Indigenous data governance are therefore not currently applicable to the described source. These conclusions must be revisited if the project scope or sources change. The researcher will request a formal determination from the UNMSM ethics/research office if institutional rules require it. This DMP is an academic planning document, not a legal opinion or institutional approval.

> ## 6. Sharing plan
>
> The public GitHub repository will contain researcher-authored code, README files, a data dictionary, source-provenance metadata, configuration examples without secrets, reproducibility instructions, and research outputs whose publication has been assessed as permissible. It will **not** contain the original MTC CSV, credentials, private Drive links, access tokens, or data whose redistribution rights have not been verified.
>
> The repository will identify the source by its official title, MTC publisher, catalogue identifier, dates, access-level metadata, licence status, and landing-page URL. It will explicitly state **“Catalogue licence: License Not Specified; source CSV not redistributed.”** The code will have a separate licence only after ownership and dependency checks. A versioned archive of the code and documentation may be deposited in Zenodo. No DOI will be claimed before the deposit is completed. If the MTC later provides a licence or written permission, the project will update the rights assessment and sharing plan before any redistribution.

## 7. Retention period and secure deletion

The selected retention period for project working data and research records is **five years after the doctoral thesis defence**, subject to any longer period required by UNMSM, a funder, publisher, or applicable law. The researcher will record the actual defence date and calculate the corresponding review/deletion date. The source CSV will be retained only as permitted by applicable terms and institutional requirements; this DMP does not create a right to retain or redistribute it.

At the end of the applicable retention period, local working copies and backups will be securely deleted using procedures appropriate to the storage medium, and cloud copies will be removed from the relevant Drive locations and trash in accordance with provider procedures. Bibliographic references, publication records, code, and non-confidential documentation may be retained where lawful and useful for reproducibility. Deletion actions will be logged.

---

## Project decisions and outstanding actions

| Item | Decision / status |
|---|---|
| Primary storage | Google Drive; verify institutional account, settings, region information, and terms |
| Public repository | Code and documentation; no original MTC CSV |
| Source licence | **Not specified in catalogue; no redistribution assumed** |
| Dataset identifier | `2281b672-9fcf-412f-aab3-5fd72ea700f4` |
| Retention | Five years after doctoral defence |
| Unnamed trailing field | Investigate four non-empty values before excluding from analytical derivative |
| `VEH_IMD` definition | Confirm official definition, units, and calculation with MTC |
| MTC reuse conditions | Obtain clarification before distributing source or adapted data |
| Ethics/legal status | Confirm institutional requirements; this draft is not a legal determination |

**Status:** Versión: 0.1. No MTC reuse permission, legal clearance, ethics approval, or Zenodo DOI is claimed.
