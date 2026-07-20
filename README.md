# ISO/IEC 27001:2022 Lead Implementer Portfolio
### Tumaini Capital Ltd — ISMS Implementation Case Study

---

> **Fictional case study.** Tumaini Capital Ltd is a constructed scenario developed to demonstrate ISO/IEC 27001:2022 lead implementer methodology in a realistic Kenyan fintech context. All company details, personnel, incidents, and figures are fabricated for portfolio purposes. No real organisation, individual, or data is represented.

---

## About This Portfolio

This portfolio documents a complete, end-to-end ISO/IEC 27001:2022 ISMS implementation — from business case through internal audit and management review — built around a fictional Kenyan digital lending company. Every artifact was produced using the same methodology, document structure, and reasoning process I would apply on a live client engagement.

The goal is not to demonstrate that I can fill in templates. It is to show the analytical judgment behind the work: why a scope boundary was drawn where it was, why certain policies were not written, which controls needed the most urgent treatment and why, and how an auditor would read the resulting documentation. That reasoning trail is what differentiates a practitioner from someone who has passed an exam.

**Standards and regulatory context:** ISO/IEC 27001:2022, Kenya Data Protection Act 2019, ODPC guidance on personal data processing, Central Bank of Kenya digital lending guidelines, Computer Misuse and Cybercrimes Act 2018.

---

## The Scenario — Tumaini Capital Ltd

**Industry:** Digital lending and microfinance | **Location:** Nairobi (HQ) and Kisumu | **Staff:** 85 | **Active borrowers:** ~120,000

Tumaini Capital is a Nairobi-based digital lender disbursing short-term loans via M-Pesa through a mobile app and USSD channel. The technology stack includes a core lending engine hosted on AWS (eu-west-1), a CRM, integrations with the Safaricom M-Pesa API and two credit reference bureaus, and heavy reliance on Google Workspace and WhatsApp Business for operations. IT support is partly outsourced to an external managed service provider.

**Three pressures drove the decision to pursue ISO/IEC 27001:2022 certification within 12 months:**

1. A regional bank white-label partnership stalled because the bank's procurement team required evidence of a certified ISMS before signing a data-sharing agreement.
2. The ODPC increased enforcement activity under the Data Protection Act 2019 against digital lenders, putting Tumaini's significant KYC and financial data holdings under direct regulatory scrutiny.
3. An internal incident in 2025 where a departing employee's CRM access was not revoked, resulting in the unauthorized export of customer telephone numbers — evidence of a systemic access control failure with no documented response process.

**ISMS lead implementer role:** The Head of Risk & Compliance was formally appointed ISMS Lead. The engagement involved no dedicated security function and required building the entire ISMS from scratch alongside a 12-month certification target.

---

## Portfolio Structure

```
iso27001-isms-implementation-portfolio/
│
├── README.md
│
├── 00-business-case/
│   └── Tumaini_Capital_ISO27001_Business_Case.docx
│
├── 01-context-and-scope/
│   ├── ISMS-DOC-001_Scope_Statement.docx
│   ├── ISMS-DOC-002_Context_4.1_4.2.docx
│   ├── ISMS-DOC-003_Boundary_Worksheet.xlsx
│   ├── ISMS-DOC-004_Scope_Decision_Log.docx
│   └── isms_scope_boundary_diagram.svg
│
├── 02-gap-analysis/
│   └── ISMS-DOC-005_Gap_Analysis.xlsx
│
├── 03-risk-assessment/
│   └── ISMS-DOC-006_Risk_Assessment.xlsx
│
├── 04-risk-treatment-soa/
│   └── ISMS-DOC-007-008_RTP_SoA.xlsx
│
├── 05-policies/
│   ├── ISMS-POL-001_Information_Security_Policy_v1.1.docx
│   ├── ISMS-POL-002_Access_Control_Policy.docx
│   ├── ISMS-POL-003_Incident_Response_Policy.docx
│   ├── ISMS-POL-004_Acceptable_Use_BYOD_Policy.docx
│   └── ISMS-POL-005_Information_Classification_Policy.docx
│
└── 06-audit-and-review/
    ├── ISMS-AUD-001_Internal_Audit_Report.docx
    └── ISMS-MR-001_Management_Review_Minutes.docx
```

---

## Implementation Walkthrough

Each phase below maps to a folder in this repository. The sequence is deliberate — each artifact feeds the next, and that progression is part of what the portfolio is designed to show.

---

### Phase 0 — Business Case

**Artifact:** `Tumaini_Capital_ISO27001_Business_Case.docx`

Before any ISMS work begins, the business case must be put to management. ISO/IEC 27001 Clause 5.1 requires top management to demonstrate genuine commitment, and that commitment is not secured without a clear articulation of why the ISMS is needed in terms management responds to — revenue, regulatory standing, and documented near-misses — rather than security jargon. The business case presented here covers the three certification drivers, financial considerations (KES 1.7M–3.7M indicative range), risks of inaction, and a phased 10–12 month timeline.

**Key design decision:** The business case is intentionally short — one page. A ten-page document does not get read properly. The goal is a signed resource commitment, not a project plan.

---

### Phase 1 — Context and Scope

**Artifacts:** `ISMS-DOC-001` through `ISMS-DOC-004`, `isms_scope_boundary_diagram.svg`

Scope definition (Clause 4.3) is not a technical exercise; it is a risk-appetite and resourcing decision that sits with top management. The implementer's role is to facilitate a structured scoping discussion, surface the trade-offs, and draft the resulting scope statement — not to decide the boundary unilaterally.

The boundary determination workbook (ISMS-DOC-003) separates the three boundary types the standard requires — organizational, physical, and information systems — because each has a different determination process and different audit implications. The scope decision log (ISMS-DOC-004) records every non-obvious boundary call with the options considered, the decision, and the rationale. This is the document that prevents an auditor from questioning why something was excluded.

**Key boundary decisions documented:**

| Boundary Question | Decision | Rationale |
|---|---|---|
| Kisumu office | In scope | Staff access in-scope systems remotely — excluding a location with access to in-scope systems leaves an unmanaged interface |
| HR/Payroll system | Excluded (this cycle) | None of the three certification drivers relate to employee data; adding it adds audit overhead without addressing identified risks |
| BYOD device hardware | Excluded | Tumaini does not own the devices and cannot certify device-level controls; information accessed via BYOD is in scope via policy controls |
| AWS physical infrastructure | Shared responsibility | Physical premises covered by AWS ISO 27001/SOC 2; Tumaini is responsible for the logical layer only |

The context document (ISMS-DOC-002) covers Clauses 4.1 (external/internal issues, using a PESTLE/People-Process-Technology-Governance framework) and 4.2 (interested parties). These are not produced for compliance theatre — they directly drive the risk assessment: the ODPC enforcement risk, the M-Pesa API dependency, the flat organizational structure, and the absence of a dedicated security function all show up here and are traced forward into the risk register.

---

### Phase 2 — Gap Analysis

**Artifact:** `ISMS-DOC-005_Gap_Analysis.xlsx` (7 tabs)

The gap analysis is a systematic comparison of Tumaini Capital's current information security posture against every mandatory clause requirement (Clauses 4–10) and all 93 Annex A controls. It produces the evidence base for the risk assessment and the priority ordering for the risk treatment plan.

**Headline findings:**

| Area | Total | Compliant | Partial | Non-Compliant | N/A |
|---|---|---|---|---|---|
| Mandatory Clauses (4–10) | 26 | 2 | 8 | 16 | 0 |
| Annex A — Organizational (A.5) | 37 | 3 | 12 | 22 | 0 |
| Annex A — People (A.6) | 8 | 1 | 2 | 5 | 0 |
| Annex A — Physical (A.7) | 14 | 3 | 5 | 6 | 0 |
| Annex A — Technological (A.8) | 34 | 4 | 10 | 19 | 1 |
| **Total** | **119** | **13** | **37** | **68** | **1** |

The pattern is consistent with an organization that has been operating on informal technical competence (AWS gives some controls by default; the MSP manages some infrastructure) without any of the governance, policy, or process layer the standard requires. The six key findings on the summary dashboard — no governance structure, no access control process, no incident response procedure, no supplier requirements, no awareness training, and undocumented technical controls — drive every HIGH-priority item in the risk register.

---

### Phase 3 — Risk Assessment

**Artifact:** `ISMS-DOC-006_Risk_Assessment.xlsx` (4 tabs)

The risk assessment follows an asset-based, Likelihood × Impact methodology. 15 information assets were identified and registered; 23 risk scenarios were assessed using a 5×5 risk matrix (score 1–25, mapped to Low / Medium / High / Critical).

**Methodology tab** includes the full 5×5 colour-coded risk matrix with Tumaini-specific impact descriptors across confidentiality, integrity, availability, regulatory, and reputational dimensions.

**Risk register** traces each risk through: asset(s) affected → threat → specific vulnerability with gap analysis reference → likelihood score → impact score → inherent risk score and level → existing controls → treatment option → proposed remediation → Annex A reference → owner → residual risk after treatment.

**Critical risks (score 19–25):**
- `R-001` Unauthorized access to borrower data via CRM (4×5=20) — already happened
- `R-004` ODPC regulatory enforcement for DPA 2019 non-compliance (4×4=16 → assessed as critical given cumulative exposure)
- `R-007` Inadequate incident response worsening a security event (4×4=16)

After treatment controls, the residual risk profile eliminates all Critical risks and reduces the majority of High risks to Medium.

---

### Phase 4 — Risk Treatment Plan and Statement of Applicability

**Artifact:** `ISMS-DOC-007-008_RTP_SoA.xlsx` (4 tabs)

The Risk Treatment Plan (ISMS-DOC-007) maps each risk to specific implementation tasks, phased across the 12-month timeline. Phase 1 (Months 1–2) focuses on the five items that must be in place before a Stage 1 auditor arrives: the IS Policy signed by the CEO, the JML/access control process, the Incident Response Policy, the ISMS Lead formally appointed with authority, and the SoA formally approved.

The Statement of Applicability (ISMS-DOC-008) covers all 93 Annex A controls. 92 are applicable; one is excluded with documented justification:

| Excluded Control | Justification |
|---|---|
| A.8.30 — Outsourced development | All development is conducted in-house by the Engineering team. No outsourced development takes place within the defined ISMS scope. |

Each applicable control carries: reason code (R = risk treatment, L = legal/regulatory, C = contractual, B = best practice), specific justification tied to Tumaini's context, risk register cross-reference, implementation status, and owner.

**Why the SoA matters:** It is the first document a Stage 1 auditor asks for. It must be consistent with the risk assessment (risks drive control selection) and with the risk treatment plan (the SoA records what will be implemented). Any control marked "Implemented" in the SoA must have auditable evidence to support that claim.

---

### Phase 5 — Policies

**Artifacts:** `ISMS-POL-001` through `ISMS-POL-005`

Five policies were developed. The selection was deliberate: these are the documents that address Tumaini Capital's specific risk drivers, not a complete enterprise policy suite applied to an 85-person company with no dedicated security function.

| Document | What it does | Why this one |
|---|---|---|
| ISMS-POL-001 — Information Security Policy | Top-level commitment; signed by CEO | Required by Clause 5.2; authorizes the entire ISMS |
| ISMS-POL-002 — Access Control Policy | JML process; MFA requirements; privileged access; access reviews | Directly closes the 2025 CRM incident gap; the JML section's 24-hour leaver deactivation SLA is non-negotiable |
| ISMS-POL-003 — Incident Response Policy | Full IR lifecycle; ODPC 72-hour notification; evidence preservation | Closes the gap where the CRM incident was handled without a documented process |
| ISMS-POL-004 — Acceptable Use & BYOD Policy | Systems use; WhatsApp Business rules; BYOD device requirements | Addresses the BYOD risk and WhatsApp data transfer gap; combined because they cover the same population |
| ISMS-POL-005 — Information Classification Policy | Four-level scheme (Public/Internal/Confidential/Restricted); handling table | DPA 2019 requires appropriate safeguards proportionate to data sensitivity; KYC documents must be explicitly Restricted |

**Design note:** The Information Security Policy went through a revision (v1.0 → v1.1) after the initial draft named eight specific supporting policies. The risk of naming specific documents is that an auditor treats it as a commitment: if any named document doesn't exist, it's a potential nonconformity. The revised version references the ISMS Document Register (ISMS-REG-001) as the single source of truth instead. That change — and the reasoning behind it — is documented here intentionally, because it demonstrates the kind of practical judgment that distinguishes an implementer from a template-filler.

---

### Phase 6 — Internal Audit and Management Review

**Artifacts:** `ISMS-AUD-001_Internal_Audit_Report.docx`, `ISMS-MR-001_Management_Review_Minutes.docx`

The internal audit (Clause 9.2) was designed as a readiness audit at Month 9 of the 12-month implementation. It audited all Clauses 4–10 and a risk-prioritised sample of Annex A controls using document review, staff interviews, and system walkthroughs.

**Audit findings — realistic, not sanitised:**

| Type | Count | Key findings |
|---|---|---|
| Major Nonconformity | 3 | IS Policy unsigned; SoA unsigned; zero awareness training delivered |
| Minor Nonconformity | 4 | MFA deployment incomplete; backup recovery untested; logging policy missing; no access review conducted since policy approval |
| Observation / OFI | 3 | IR tabletop not scheduled; Kisumu physical assessment not started; IS metrics not being collected |

**Why realistic findings matter for a portfolio:** An internal audit that finds nothing is either a sign of a mature ISMS in its fifth year, or an auditor who wasn't thorough. For a Month 9 first-year implementation, three Major NCs around formal approvals and training are entirely credible — and the corrective actions for them are straightforward. Sanitising the findings would make the portfolio look less, not more, credible.

The management review minutes (ISMS-MR-001) follow Clause 9.3 exactly, covering all mandatory inputs and producing documented management decisions including: closing the IS Policy and SoA MNC findings (CEO signed both two weeks before the review), escalating VLAN segmentation to Phase 2 priority, adding quarterly IS steering meetings, and establishing the Stage 1 audit date.

> **A note on auditor independence — and why this is in the portfolio anyway.**
>
> ISO/IEC 27001:2022 Clause 9.2 requires that internal auditors be selected to ensure objectivity and impartiality. The person who built the ISMS cannot audit their own work — that is a conflict of interest and would itself be a nonconformity. In a live engagement, the audit report would be produced by an independently appointed auditor: a trained staff member from a function entirely separate from the ISMS implementation (Finance or Operations, for example), an external GRC consultant, or a certification body pre-assessment service.
>
> This document is included in the portfolio as a demonstration of internal audit methodology and knowledge of realistic first-year findings — not as a claim that the implementer conducted the audit. The report itself carries a prominent independence disclaimer on page 1, and the Lead Auditor field is left as "To be appointed." Including the document without that transparency would be a credibility problem; including it with the explanation signals something more useful — that the practitioner understands the independence requirement deeply enough to flag it themselves.

---

## Full Document Register

| Document ID | Title | Phase | Format | Standard Reference |
|---|---|---|---|---|
| BIZ-001 | ISO/IEC 27001:2022 Business Case | Business Case | .docx | — |
| ISMS-DOC-001 | ISMS Scope Statement | Context & Scope | .docx | Clause 4.3 |
| ISMS-DOC-002 | ISMS Context Document (Clauses 4.1 & 4.2) | Context & Scope | .docx | Clauses 4.1, 4.2 |
| ISMS-DOC-003 | ISMS Boundary Determination Worksheet | Context & Scope | .xlsx | Clause 4.3 |
| ISMS-DOC-004 | Scope Decision Log | Context & Scope | .docx | Clause 4.3 |
| ISMS-DOC-005 | ISO/IEC 27001:2022 Gap Analysis | Gap Analysis | .xlsx | Clauses 4–10, Annex A |
| ISMS-DOC-006 | Information Security Risk Assessment | Risk Assessment | .xlsx | Clause 6.1.2 |
| ISMS-DOC-007 | Risk Treatment Plan | Risk Treatment | .xlsx | Clause 6.1.3 |
| ISMS-DOC-008 | Statement of Applicability | Risk Treatment | .xlsx | Clause 6.1.3(d) |
| ISMS-POL-001 | Information Security Policy (v1.1) | Policies | .docx | Clause 5.2 |
| ISMS-POL-002 | Access Control Policy | Policies | .docx | A.5.15–5.18, A.8.2–8.5 |
| ISMS-POL-003 | Incident Response Policy | Policies | .docx | A.5.24–5.28 |
| ISMS-POL-004 | Acceptable Use & BYOD Policy | Policies | .docx | A.5.10, A.6.7, A.8.1 |
| ISMS-POL-005 | Information Classification Policy | Policies | .docx | A.5.12, A.5.13 |
| ISMS-AUD-001 | Internal ISMS Audit Report | Audit & Review | .docx | Clause 9.2 |
| ISMS-MR-001 | ISMS Management Review Minutes | Audit & Review | .docx | Clause 9.3 |

---

## Methodology Notes

These are things that are not always obvious from reading the artifacts alone, but reflect the reasoning behind them.

**Why the context comes before the scope, not after.** Many implementers draft a scope statement first and backfill the context to justify it. The standard's logic runs the other way: Clause 4.1 (external/internal issues) and Clause 4.2 (interested party requirements) are the inputs to Clause 4.3 (scope). The context document in this portfolio was built first, and the scope decisions are traceable to specific context findings.

**Why the gap analysis is not the risk assessment.** These are frequently conflated. The gap analysis tells you what controls and processes are missing. The risk assessment tells you which of those gaps represent the most significant risks given the specific threat landscape. The gap analysis came first here, and every HIGH-priority risk in the register traces back to a specific gap analysis finding.

**Why only five policies were written, not eight.** A policy that is written but never read, never attested to, and never enforced is worse than no policy — it creates a false sense of control and audit exposure. For a company of 85 people with no dedicated security function, five substantive policies that will actually be followed are more valuable than a comprehensive suite that creates ongoing maintenance overhead without operational traction.

**Why the IS Policy was revised.** The v1.0 draft named eight specific supporting policies by title. That creates a compliance trap: an auditor who finds one named document missing can raise a nonconformity against the IS Policy itself. The v1.1 revision references the ISMS Document Register as the source of truth instead. This is a small change with meaningful audit implications.

**Why the internal audit found Major Nonconformities.** Because a first-year ISMS does. The Major NCs in this audit are administrative in nature — the policies existed and were substantive; they simply had not been formally signed yet. That is a realistic and correctable finding. An internal audit that concludes "everything is fine" before Stage 1 is a red flag, not a reassurance.

**Why auditor independence is explicitly flagged in both the audit document and this README.** The implementer who builds the ISMS cannot conduct the internal audit of that same ISMS — Clause 9.2 requires objectivity and impartiality, and auditing your own work fails that test directly. This is one of the first things an experienced ISO 27001 practitioner or interviewer would ask when reviewing a portfolio like this. Flagging it proactively — and explaining how it would be handled in a live engagement — demonstrates deeper understanding of the standard than simply having all the documents present.

---

## Regulatory and Standards Context

This portfolio is set in Kenya deliberately. The regulatory environment is specific and consequential:

- **Data Protection Act, 2019 (DPA 2019):** Kenya's primary data protection legislation, administered by the Office of the Data Protection Commissioner (ODPC). Digital lenders handling KYC data are directly in scope for enforcement, including the 72-hour breach notification requirement (Section 43) referenced in the Incident Response Policy.
- **ODPC enforcement:** The ODPC has been increasing its audit and enforcement activity in the fintech sector. This is not background context — it is the second of three certification drivers and appears explicitly in the gap analysis significance ratings and the management review discussion.
- **CBK digital lending guidelines:** The Central Bank of Kenya has issued guidance on digital credit providers. Platform security and customer data protection are areas of explicit regulatory interest.
- **Computer Misuse and Cybercrimes Act, 2018:** Relevant to incident response obligations and evidence preservation requirements referenced in ISMS-POL-003.
- **ISO/IEC 27001:2022:** The 2022 revision introduced four Annex A themes (replacing 14 domains) and updated several controls. This portfolio uses the 2022 version throughout — 93 controls across Organizational, People, Physical, and Technological themes.

---

## Credentials and Context

This portfolio was developed as part of an active pivot from ICT infrastructure and operations into cybersecurity and GRC practice. Supporting credentials and related portfolio work:

- **CGRCE** (Certified GRC Professional) — High Distinction
- **ISO/IEC 27001:2022 Lead Implementer** certified
- **ISO/IEC 42001 Lead Implementer** certified
- **ISC2 CC** — Certified in Cybersecurity
- **CCNA** — Cisco Certified Network Associate
- **MSc Information Security** — GRC focus

**Related portfolio repositories:**
- `aws-portfolio-administrator` — AWS cloud administration labs and governance artifacts
- `windows-server-2022-portfolio` — 21-day Windows Server 2022 lab curriculum

---

*Tumaini Capital Ltd is a fictional company. All scenario details, personnel, incidents, financial figures, and regulatory outcomes described in this portfolio are fabricated for educational and portfolio demonstration purposes only.*
