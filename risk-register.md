# Risk Register
## Introduction
This portfolio entry demonstrates a comprehensive Risk Assessment of a Mathnasium Learning Center using the NIST Risk Management Framework (RMF). By categorizing the system under FIPS 199, I identified 31 specific risks across physical and digital domains and developed a prioritized remediation roadmap.

### Quick View
Total Risks Identified: 31 | Critical/High Risks: 8 | Top Information Type: Student PII (Moderate)

### Top Three Immediate Actions
1. MFA Implementation (IA family)
2. Network Segmentation (SC family)
3. Physical MDF Lock (PE family)

## I. Security Categorization Summary (FIPS 199):
The security categorization of the Mathnasium Center information system is determined by the potential impact on the organization, its assets, and individuals should a loss of confidentiality, integrity, or availability occur. Following the NIST Risk Management Framework (RMF), this assessment utilizes the FIPS PUB 199 standard to establish a security baseline.

In accordance with NIST SP 800-60 Vol. II, specific information types were selected as 'In-Scope' for the Mathnasium New York system. These include Student Records (D.15.1), Personnel Administration (C.3.3.1), and Information Infrastructure Management (C.3.1.2). Information types irrelevant to the local learning center mission, such as Higher Education (D.15.2) and Federal Research, were formally excluded. The resulting categorization follows the 'High Water Mark' principle to ensure that security controls are commensurate with the risk to student PII and organizational integrity.

The following table identifies the specific information types processed by the Mathnasium New York system. Each type has been mapped to the impact levels defined in NIST SP 800-60 Vol. II to determine the appropriate security baseline.

| Information Type | NIST Code | Confidentiality | Integrity | Availability | Professional Justification |
| --- | --- | --- | --- | --- | --- |
| Primary & Secondary Education | **D.15.1** | Moderate | Moderate | Low | Includes student progress reports and learning plans. Loss of C or I would cause serious adverse effects on parental trust and mission success.|
|Personnel Administration | **C.3.3.1** | Moderate | Low | Low | Covers tutor background checks and PII. C is Moderate due to sensitive vetting data required for staff working with minors (NIST PS-03).|
| Payroll & Expense Management | **C.3.5.1** | Moderate | Moderate | Low | Covers franchise fees and staff compensation. I is Moderate to ensure financial records are not modified by unauthorized users.|
| Public Affairs | **C.2.1.1** | Low | Low | Low | Marketing materials and Guest Wi-Fi portal info. Impact of a breach is limited as this info is intended for public consumption.|
| Information Infrastructure | **C.3.1.2** | Moderate | Moderate | Moderate | **Critical Row**: Covers network configs and admin passwords. Compromise here results in the compromise of all other data types.|

System Security Category ($SC$): Based on the information types processed, the High Water Mark for the system is established as **MODERATE**. This baseline dictates the selection of NIST 800-53 security controls.

*SC*<sub>Mathnasium NY<sub> = {({Confidentiality, Moderate}), ({Integrity, Moderate}), ({Availability, Moderate})}

## II. Risk Heatmap Analysis:

## III. Risk Distribution & Controls:
This shows how we are defending the center.
| Function | Count | Purpose |
| --- | --- | --- |
| <span style="color:blue">Preventive</span> | 18 | Stopping unauthorized access before it happens. |
| <span style="color:gold">Detective</span> | 7 | Identifying gaps and monitoring current activity. |
| <span style="color:purple">Corrective</span> | 6 | Ensuring data can be recovered after an event. |

## IV. Detailed Findings & Mitigation Plan:

### Methodology & Compliance
Framework: NIST 800-53 Rev 5
Categorization: FIPS 199 (Moderate Baseline)
Data Taxonomy: NIST SP 800-60 Vol. II
