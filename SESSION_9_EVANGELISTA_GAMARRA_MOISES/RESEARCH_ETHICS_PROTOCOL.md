# Research Ethics Protocol — Draft v 0.1

**Universidad Nacional Mayor de San Marcos (UNMSM)**  
**Doctoral Program in Deep Technologies**  
**Researcher:** Moisés Evangelista Gamarra  
**Instructor:** Dr. Loveleen Gaur  
**Course:** Research Methods and Scientific Integrity in AI and Advanced Technologies  
**Version date:** 19 November 2026  
**Status:** Academic draft for review — not an ethics approval

> **Research title:** A Reproducible Trustworthy Artificial Intelligence Framework for Traffic-Flow Forecasting Using Open Data from Peru’s National Road Network

| DOCUMENT INFORMATION | DETAILS |
| --- | --- |
| Researcher | Moisés Evangelista Gamarra |
| Course | Research Methods and Scientific Integrity in AI and Advanced Technologies |
| Institution | Universidad Nacional Mayor de San Marcos (UNMSM) |
| Version date | 19 November 2026 |
| Protocol status | Academic draft for review — not an ethics approval |
| Instructor | Dr. Loveleen Gaur |

| PLEASE READ — WHAT THIS DOCUMENT DOES AND DOES NOT DO<br>This protocol describes a study based on secondary vehicle-flow records published by Peru’s Ministry of Transport and Communications (MTC). It is a working academic draft for review. It does not claim that the project is automatically exempt from ethics review; the competent UNMSM office must determine the appropriate pathway. |
| --- |

## Study at a glance

| ELEMENT | CURRENT STUDY DESIGN |
| --- | --- |
| Research material | MTC monthly vehicle-flow records at toll units on the National Road Network. |
| Unit of analysis | Toll-station/month time-series observation — not an individual person. |
| Research activity | Secondary-data analysis and one-month-ahead forecasting of VEH_IMD. |
| Human-participant recruitment | None planned. No interviews, surveys, observation, or intervention. |
| Intended use | Research and exploratory decision support; not autonomous or high-stakes decision-making. |

## Protocol status and scope

This is a draft for academic review (v0.1), not an ethics approval or a determination that review is unnecessary. The study is designed as secondary-data research using the Ministry of Transport and Communications (MTC) open dataset of vehicle flow recorded at toll units on Peru’s National Road Network. The protocol describes the dataset and processing documented in the research materials.

The scope is deliberately limited. Any change to the data source, level of detail, variables, or addition of human-participant data will require the researcher to pause the affected activity, update this protocol, and obtain the institutional ethics determination required by UNMSM before proceeding.

| A NOTE ON THE WORD “PUBLIC”<br>A dataset being publicly accessible does not, by itself, settle questions about licensing, privacy, consent, or ethics review. Those questions are addressed separately below and must be confirmed where indicated. |
| --- |

## 1. Purpose and participants

The purpose of this research is to design and empirically evaluate a reproducible Trustworthy Artificial Intelligence (AI) framework for one-month-ahead forecasting of the monthly vehicle-flow indicator VEH_IMD at toll stations. The study uses secondary records published by the MTC through Peru’s National Open Data Portal.

No drivers, passengers, toll workers, or other individuals will be recruited, contacted, interviewed, observed, or asked to take part. The unit of analysis is a toll-station time series, not a person. The project materials currently describe 11,528 rows and 22 columns before initial cleaning, covering January 2014 to March 2026, with 81 usable toll-station series in the modelling panel after documented quality checks and exclusions. These figures remain subject to the source-file reconciliation described in Section 2.

There is therefore no human-participant recruitment target. If the project later involves people or individual-level records, this description will no longer be sufficient and the protocol must be reassessed.

## 2. Data collection, provenance, and licensing

No primary data will be collected. The study reuses the dataset titled “Flujo vehicular registrado en las Unidades de Peaje de la Red Vial Nacional 2014–2026 I Trimestre”, published by the Ministerio de Transportes y Comunicaciones (MTC) on Peru’s Plataforma Nacional de Datos Abiertos (Portal Nacional de Datos Abiertos).

Official dataset page: <https://www.datosabiertos.gob.pe/dataset/flujo-vehicular-registrado-en-las-unidades-de-peaje-de-la-red-vial-nacional-2014-%E2%80%93-2026-i>

The catalogue identifies the MTC as publisher and the access level as Public. It records a release date of 25 June 2025 and a last modification date of 5 June 2026, and provides a CSV resource, a data dictionary, and a metadata document. The catalogue currently displays “License Not Specified”. For that reason, this protocol does not assume a particular open-data licence or unrestricted permission to redistribute the source file. The researcher will cite the MTC and the portal, preserve the catalogue metadata and access date, and seek clarification from the publisher if reuse or redistribution terms remain unclear.

The portal describes monthly vehicle counts recorded at toll units, including vehicle categories, registration month, and toll-unit identification. Its catalogue preview exposes fields such as ADMINIST, CODIGO_PEAJE, DEPARTAMENTO, NOMBRE_PEAJE, vehicle-category counts, VEH_TOTAL, VEH_IMD, ANIO, MES, and PERIODO.

| PROVENANCE CHECK | WHAT THE CURRENT MATERIALS SAY | ACTION BEFORE FINALISING |
| --- | --- | --- |
| Record count | Portal preview: 11,532 records. Research Datasheet/local analysis: 11,528 rows before cleaning. | Compare the exact downloaded CSV, metadata and data dictionary; record which file was analysed. |
| Coverage dates | Dataset title refers to 2014–2026 I Trimester; catalogue description also mentions a 31 March 2025 cutoff. | Verify the resource-level dates and document the actual coverage of the analysed file. |
| Licence | Catalogue field: “License Not Specified”. | Do not label the data as openly licensed or redistribute it until terms are confirmed. |

The documented analytical schema does not list drivers’ names, national identity numbers, vehicle registration plates, contact details, or individual-level trajectories. The researcher will nevertheless inspect the exact raw file before analysis to check for unexpected identifiers or free-text personal information. If any such fields are found, they will not be used until they have been excluded or appropriately protected and the UNMSM ethics office has been consulted.

## 3. Informed consent strategy

Individual informed consent is not planned because the current design uses secondary vehicle-flow records aggregated by toll station and month, with no direct interaction with people and no intended processing of personal data. The project does not plan to scrape social-media content, private platforms, or identifiable user-generated material.

This is the researcher’s preliminary assessment, not a unilateral exemption. The UNMSM research ethics committee or other authorised institutional office must determine whether the project requires formal review, qualifies for a waiver, or may receive a documented determination that ethics review is not required.

If the committee identifies personal data in the source, or if the project later adds interviews, surveys, individual mobility traces, plate-level records, or other identifiable information, the researcher will not begin that activity until the required approval and consent process are in place. Any consent process will explain the study purpose, data collected, foreseeable risks, voluntary nature of participation, retention, access, withdrawal procedures, and a contact route for questions.

## 4. Risks and potential harms

The current design does not involve recruited participants, and the documented analytical unit is an aggregated toll-station/month record. The main foreseeable risks are therefore indirect rather than participant-facing. Forecast errors, overconfident interpretation, or poorly governed deployment could influence road-operation, maintenance, investment, or resource-allocation discussions. Station-level findings could also be misread as evidence about individual drivers or local communities.

Incomplete records, duplicate station-period observations, unusual periods, and distribution shifts may produce unstable or misleading forecasts. The study will not claim causal effects, treat predictions as ground truth, or imply that performance in the selected test period guarantees performance in other road networks or future periods.

The risk register below identifies the principal risks and the practical steps planned to reduce them.

### Risk and mitigation matrix

| RISK | LIKELIHOOD | SEVERITY | MITIGATION / RESPONSE |
| --- | --- | --- | --- |
| Forecast error is over-trusted in planning | Medium | High | Present forecasts as exploratory decision support; report uncertainty and temporal limits; require human review. |
| Distribution shift or atypical periods distort predictions | High | Medium | Check and report shifts; show performance by period where feasible; treat recalibration as a separate, documented task. |
| Unexpected identifiers or external linkage create re-identification risk | Low, pending raw-file inspection | High | Inspect the source file; exclude identifiers; do not link to vehicle-registration data or reconstruct journeys; consult UNMSM if personal data is found. |
| Data-quality problems or leakage inflate performance | Medium | High | Keep a reproducible audit trail; fit preprocessing on training data only; use validation for selection and reserve the test period for final evaluation. |
| Unauthorised access, loss, or disclosure of working files | Low | Medium | Use access controls, strong authentication, secure transfer and backups; follow the incident-response steps in Section 7. |
| Outputs are repurposed for surveillance or punitive decisions | Low | High | Prohibit individual surveillance and sole reliance on the forecasts for enforcement or safety-critical decisions. |

## 5. Benefits and justification

This study will not provide a direct benefit to individual participants, since no individuals will be recruited or asked to take part in the research. Its value lies instead in the scientific and public-interest contributions it may offer. In particular, the study aims to make the monthly traffic-flow forecasting process easier to audit and reproduce, while providing a clearer account of data quality, uncertainty, and model performance as traffic patterns change over time.

The findings and research materials could also serve as a useful starting point for further studies and for exploratory planning by road agencies. They are not designed to replace professional judgement or to support autonomous decisions, especially where those decisions could have significant consequences. With these limits in place, the study considers the careful analysis of an existing dataset to be justified, provided that the safeguards and limitations described in this protocol are respected throughout the research.

## 6. Confidentiality, privacy, and re-identification

The project will treat the source as public administrative data while still applying data-minimisation and responsible-use principles. The documented fields identify toll stations and monthly periods rather than individual road users. The researcher will not attempt to infer identities, reconstruct individual journeys, link records to vehicle-registration databases, or combine the dataset with external sources for the purpose of identifying people.

Results will be reported at toll-station/month level or at a higher level of aggregation. Before publication, the researcher will review small-cell or unusual-event findings that could create avoidable disclosure or harmful inference.

SHAP values will be described only as model-attribution explanations. They will not be presented as causal effects or as explanations of any individual person’s behaviour. Reports will disclose uncertainty, temporal coverage, known data-quality limitations, and the limits of generalising from the selected test period.

## 7. Data storage, access, retention, and breach response

The original downloaded file will be preserved as a read-only source copy. Working copies, code, metadata, manifests, and model outputs will be stored in access-controlled institutional or researcher-controlled storage protected by strong authentication. Access will be limited to the researcher and authorised doctoral supervisors or reviewers who need the materials for academic oversight.

Data transfers will use secure channels. Public repositories will contain only materials that may lawfully be redistributed under the source terms. Credentials, private tokens, and unrelated personal files will never be committed to a public repository.

The current working retention proposal is five years after the relevant thesis or publication, or longer if required by UNMSM policy, the funder, or applicable law. This period is provisional and must be confirmed with the competent institutional office before final approval. At the end of the approved retention period, non-public working copies will be securely deleted; public records will be handled according to their licence and repository policy.

If unauthorised access, loss, corruption, or disclosure is suspected, the researcher will restrict access, preserve relevant evidence, notify the responsible UNMSM office promptly, assess the scope and potential impact, and follow the institution’s and applicable law’s notification and remediation procedures.

| STORAGE ITEM | PLANNED CONTROL / DETAIL TO CONFIRM |
| --- | --- |
| Original source CSV | Read-only copy; retain source URL, download date, file fingerprint and source metadata. |
| Working data and derived files | Access-controlled storage; identify the actual storage location before final submission. |
| Code, notebooks and model outputs | Version-controlled; exclude credentials and any source material that cannot lawfully be redistributed. |
| Access | Researcher and authorised academic supervisors/reviewers on a need-to-access basis. |
| Retention | Five years proposed; confirm the applicable UNMSM requirement. |
| Incident response | Restrict access, preserve evidence, notify the responsible institutional office, and follow its directions. |

## 8. Conflicts of interest, roles, and research integrity

The researcher will disclose any financial, professional, institutional, or personal interest that could reasonably be perceived to influence data selection, model development, evaluation, interpretation, or publication. No sponsor or third party will be permitted to suppress unfavourable results or alter the analysis without transparent documentation. Any supervisory, employment, or institutional relationship with a potential data provider or intended user of the framework will be disclosed to the doctoral programme and ethics committee where relevant.

The researcher is responsible for the integrity of the analysis, accurate attribution, version control, and transparent reporting of any AI-assisted work. The study will preserve an audit trail of data versions, exclusions, preprocessing, feature construction, random seeds, software versions, model configurations, and evaluation results.

Model selection will use the validation period (2024), while the 2025 test period will remain reserved for final evaluation, as documented in the current research materials. The researcher will report limitations and non-winning results accurately, avoid data leakage, distinguish repeatability from independent reproducibility, and follow the CONCYTEC National Code of Scientific Integrity and UNMSM requirements.

## AI-specific ethical safeguards

| AREA | PRACTICAL COMMITMENT IN THIS STUDY |
| --- | --- |
| Data provenance and licensing | Use the MTC source and document its versions; preserve the official URL, access/download date, file fingerprint, metadata and licence/attribution conditions. Do not redistribute source data unless its terms allow it. |
| Consent and secondary data | Do not treat public availability as blanket consent. No scraping or identifiable online content is planned. Follow the ethics pathway determined by UNMSM. |
| Bias, fairness and distribution shift | Assess performance across toll stations and time periods where sample size permits. Flag missingness, duplicates, atypical periods and shifts. Avoid unsupported comparisons between communities or groups. |
| Transparency and explainability | Document the target, predictors, preprocessing, temporal split, model selection, uncertainty, SHAP limitations, intended use and prohibited use. |
| Human oversight and dual use | Treat forecasts as research outputs and decision support only. Do not use them as the sole basis for safety-critical decisions, enforcement, individual surveillance or automated allocation of public resources. |
| Generative AI and authorship | If generative AI tools assist with editing, coding or analysis, disclose their role as required by course, journal and UNMSM rules. The researcher remains responsible for verification, citations, originality and every scientific claim. |

## Ethical and governance framework

This protocol is guided by the Belmont principles — Respect for Persons, Beneficence, and Justice — and by the Menlo Report’s principles of Respect for Law and Public Interest. For the Peruvian context, the researcher will consider Law No. 29733 on Personal Data Protection and its applicable regulations, Law No. 31814 promoting the use of artificial intelligence, and the CONCYTEC National Code of Scientific Integrity, including the 2024 update cited in the course materials.

The applicability of these instruments to this secondary-data study, and the appropriate UNMSM review route, must be confirmed by the competent institutional office. This draft is not a legal opinion and does not establish an ethics exemption.

## Submission checklist — Session 9

Use this checklist to make the draft ready for academic submission and to identify the points that still need an institutional answer. A checked item means that the researcher has completed or verified it; it does not mean that UNMSM has approved the protocol.

| DONE | CHECK BEFORE SUBMISSION | WHO |
| --- | --- | --- |
| ☐ | Protocol describes the research purpose, dataset, unit of analysis and intended use. | Researcher |
| ☐ | The exact MTC CSV, data dictionary and metadata have been checked against the version used in the analysis. | Researcher |
| ☐ | The 11,532 vs. 11,528 record-count difference and the date-coverage inconsistency have been reconciled or clearly documented. | Researcher |
| ☐ | The licence and permitted reuse/redistribution terms have been checked; “License Not Specified” has not been treated as an open licence. | Researcher / MTC |
| ☐ | The raw file has been inspected for plates, personal identifiers, free text or individual trajectories. | Researcher |
| ☐ | The protocol explains why individual consent is not currently planned and explicitly leaves the ethics determination to UNMSM. | Researcher / UNMSM |
| ☐ | The risk matrix, mitigation measures, privacy safeguards and prohibited uses are included. | Researcher |
| ☐ | The actual storage location, authorised access and retention period have been confirmed against UNMSM requirements. | Researcher / UNMSM |
| ☐ | Any relevant financial, professional or institutional conflicts have been disclosed; if none, this is stated explicitly. | Researcher |
| ☐ | The role of generative AI tools, if used, is disclosed in line with course and institutional rules. | Researcher |
| ☐ | The protocol and supporting Datasheet / Model Card are submitted through the course platform, as requested by the instructor. | Researcher |
| ☐ | Any required ethics review, waiver or formal determination is obtained before activities outside the current secondary-data scope begin. | UNMSM / Researcher |

> **IMPORTANT — ITEMS THAT CANNOT BE SELF-APPROVED**  
> The researcher can verify the source file, improve documentation and submit the protocol. Only the competent UNMSM office can determine the required ethics-review route. The MTC or the applicable data authority must clarify any unresolved source-licensing terms. Do not mark these institutional decisions as complete until written confirmation is available.

## Items to confirm with the ethics committee / institutional office

| QUESTION FOR UNMSM | WHY IT MATTERS / SPACE FOR THE RESPONSE |
| --- | --- |
| Which faculty or institutional ethics committee should receive this protocol? | Confirm the correct submission route, forms and review timeline. |
| Does this secondary-data study require review, expedited review, a waiver, or a formal determination that review is not required? | The researcher must not make this determination independently. |
| What storage, access, retention, incident-reporting and record-keeping rules apply? | Replace the provisional five-year period if institutional policy requires a different period. |
| Are any additional declarations, forms or supporting documents required? | Confirm whether the Datasheet, Model Card, data dictionary or other annexes must accompany the protocol. |

## Researcher’s declaration

| Moisés Evangelista Gamarra | 19 November 2026 |
| --- | --- |

## References

National Commission for the Protection of Human Subjects of Biomedical and Behavioral Research. (1979). The Belmont Report.

U.S. Department of Homeland Security. (2012). The Menlo Report: Ethical Principles Guiding Information and Communication Technology Research.

Tabassi, E. (2023). Artificial Intelligence Risk Management Framework (AI RMF 1.0). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.AI.100-1

High-Level Expert Group on Artificial Intelligence. (2019). Ethics Guidelines for Trustworthy AI. European Commission.

Peru. Law No. 29733, Personal Data Protection Law, and applicable regulations.

Peru. Law No. 31814, Law Promoting the Use of Artificial Intelligence for the Economic and Social Development of the Country (2023).

CONCYTEC. (2024). National Code of Scientific Integrity. Presidential Resolution No. 028-2024-CONCYTEC-P.

Ministry of Transport and Communications (MTC). Vehicle Flow Recorded at Toll Units of the National Road Network (2014–2026, first quarter). Peruvian National Open Data Portal. https://www.datosabiertos.gob.pe/dataset/flujo-vehicular-registrado-en-las-unidades-de-peaje-de-la-red-vial-nacional-2014-%E2%80%93-2026-i

Wilkinson, M. D., et al. (2016). The FAIR Guiding Principles for scientific data management and stewardship. Scientific Data, 3, 160018.

Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. Advances in Neural Information Processing Systems, 30.
