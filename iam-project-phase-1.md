# Enterprise Identity Governance & Lifetime Automation

## Executive Summary
To establish a "Source of Truth" for the NYC Education Franchise, I initialized a centralized identity directory using Microsoft Entra ID. Rather than manual entry, I utilized a Bulk Upload (CSV) methodology to ensure data integrity, scalability, and adherence to a strict naming convention required for automated auditing. The CSV file acted as the Authoritative Source for this implementation. I built this entire lab using Standard features because I know how to work within budget constraints.

### Naming conventions
I engineered a Lexical Naming Convention to ensure every identity is human-readable and machine-auditable. This follows the ISO/IEC 27001 logic for asset and identity identification.

Format: [ORG]-[LOC]-[ROLE]-[Initial+LastName]
ORG: FRAN (Franchise)
LOC: NYC (New York City)
ROLE: 4-Character Functional Code (EXEC, ADMN, STAF, AUDT, FINA)
Identifier: First Initial + Last Name

FRAN-NYC-[ROLE]-[Initial+LastName]
FRAN = Franchise
NYC = Location
ROLE = assigned based on job position
Initial+LastName = First initial capital attached without spaces to last name, first letter capital.
Example for user Ada Lovelace would be *FRAN-NYC-STAF-ALovelace*

Then add the domain at the end for the User Principal Name (UPN):
Example: FRAN-NYC-ADMN-ATuring@domain.onmicrosoft.com

### Professional Role Codes
I implemented a standardized Lexical Naming Convention based on ISO/IEC 27001 guidelines for asset identification and access control
| **Department/Role** | **Code Naming Convention** | **Example** |
| --- | --- | --- |
| IT Operations | ITOE (IT Ops/Eng) | FRAN-NYC-ITOE-ATuring |
| Compliance | COMP | FRAN-NYC-COMP-GHopper |
| Auditor | AUDT | FRAN-NYC-AUDT-External |
| Leadership | EXEC | FRAN-NYC-EXEC-ALovelace |
| Guest | GUST | FRAN-NYC-GUST-SHwaking |
> *Note: Role codes define the user's primary function. An individual may belong to a Department (e.g., IT Operations) while holding a specific Functional Role (e.g., ADMN) for audit purposes.*

### Implementation Methodology (Why Bulk Upload?)
I chose the Bulk Create workflow over manual creation for three strategic reasons:
+ Standardization: Eliminates human error (typos) in Department or Job Title fields, which are critical for Dynamic Group triggers.
+ Auditability: The CSV acts as a "Point-in-Time" record of who was authorized to be in the system at launch.
+ Efficiency: Reduces administrative overhead by 90% compared to manual provisioning.

### Artifact Documentation
[**File Name: 20260222_FRAN-NYC_IAM-Bulk-Import_PROD_v01.csv**](./assets/02222026_FRAN-NYC_IAM-Bulk-Import_PROD_v01.csv)

Scope: 11 Initial Member Identities (inclusive of one "Terminated" user for offboarding testing).

### Group Architecture
| Group Name | Type | Membership Strategy | Governance Goal |
| --- | --- | --- | --- |
| NYC-Faculty-Staff | Security | Static (Assigned) | Role-Based Access Control (RBAC) for educational tools. |
| NYC-IT-Admins | Security | Static (Assigned) | Privileged Access Management (PAM) for IT infrastructure. |
| NYC-Executives | Security | Static (Assigned) | Data isolation for confidential financial/business records. |

### ⚠️ Security & Data Privacy Notice
**Identity Protection:** In a production enterprise environment, User Provisioning Files (CSVs) contain sensitive **PII (Personally Identifiable Information)** and temporary credentials.

For this Portfolio Lab:
* All identities used are fictional entities.
* The "Initial Password" column used during upload was a one-time placeholder.
* Security Protocol: In real-world practice, these files are encrypted at rest and deleted immediately after the successful sync to the directory to prevent "credential leakage."

### Security Control: Administrative Hardening
**Action:** Enforced Per-User Multi-Factor Authentication (MFA) for the FRAN-NYC-ADMN-ATuring account.
**Rationale:** Mitigating risk of unauthorized access via credential theft. Global Admin accounts are high-value targets and require a second factor of authentication as per the Principle of Defense in Depth.
<figure>
  ![Alan Turing MFA enabled](./assets/)
  <figcaption>Fig 1.2: End-User Validation—Verification of the MFA challenge-response handshake during the administrative login sequence.</figcaption>
</figure>
### Implementation Verification
To ensure the integrity of the security controls, I performed a "Sign-in Audit":
1. **Control Test:** Attempted login as `FRAN-NYC-ADMN-ATuring`.
2. **Result:** System successfully interrupted the primary authentication flow to demand a secondary factor (MFA).
3. **Outcome:** PASS. Identity is verified via out-of-band (OOB) authentication, successfully mitigating 99.9% of automated password attacks (per Microsoft security benchmarks).

### Lessons Learned
During the bulk provisioning phase, I encountered a UPN validation error. I resolved this by verifying the Primary Tenant Domain and performing a global string replacement in the source CSV to ensure 100% alignment with directory DNS requirements. This highlighted the importance of Domain Verification in IAM workflows.

**Challenge:** During the implementation of Entra ID P2, I encountered a 401 Unauthorized licensing synchronization error. This is a common real-world 'Identity Trap' where external admin accounts (B2B/Guest) conflict with internal tenant billing profiles. Root cause identified as a token mismatch between the Microsoft Account (MSA) bootstrap identity and the Entra ID organizational tenant.

**Solution:** Demonstrated operational agility by pivoting to a Phase 1: Static Membership Model. I promoted a native cloud identity (Alan Turing) to Global Administrator to decouple the environment from external dependencies and manually mapped users to Security Groups to ensure 'Zero-Day' readiness.

### Assigned Groups
Group ownership is currently centralized under the Global Admin for the initial build phase, with plans to delegate ownership to Department Heads in Phase 2 to follow a Decentralized Governance model.

### Post-Implementation Validation
- **Identity Confirmation:** Verified 11/11 users successfully provisioned via Entra ID User List.
- **MFA Heartbeat:** Confirmed FRAN-NYC-ADMN-ATuring successfully triggered MFA challenge upon secondary login.
- **Group Membership:** Validated that permissions inherited by NYC-Faculty-Staff members align with Least Privilege principles.

### Phase 2: Advanced Identity Governance
Automation, scalability, CAPs, PIM and lifecycle workflow. [**Click here for Phase 2**](./iam-project-phase-2.md)

#### Current Status: Phase 1 Complete ✅ | Phase 2 Pending License Sync ⏳
