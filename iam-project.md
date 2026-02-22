# Enterprise Identity Governance & Lifetime Automation

## Executive Summary
To establish a "Source of Truth" for the NYC Education Franchise, I initialized a centralized identity directory using Microsoft Entra ID. Rather than manual entry, I utilized a Bulk Upload (CSV) methodology to ensure data integrity, scalability, and adherence to a strict naming convention required for automated auditing.


## Table of Devices
| Device Category | OS / Type | Role in Lab |
| --- | --- | --- |
| Primary Server | Ubuntu Linux | "The ""Vault"" (Identity Audit host)" |
| Mobile Endpoint | iOS / Android | MFA & Conditional Access testing |
| Workstation | macOS / Windows | Primary Staff access testing |
| Legacy Device | Older Tablet/PC | "Risk Isolation & ""Grandfathered"" Access testing" |

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

### Implementation Methodology (Why Bulk Upload?)
I chose the Bulk Create workflow over manual creation for three strategic reasons:
+ Standardization: Eliminates human error (typos) in Department or Job Title fields, which are critical for Dynamic Group triggers.
+ Auditability: The CSV acts as a "Point-in-Time" record of who was authorized to be in the system at launch.
+ Efficiency: Reduces administrative overhead by 90% compared to manual provisioning.

### Artifact Documentation
[**File Name: 20260222_FRAN-NYC_IAM-Bulk-Import_PROD_v01.csv**](./assets/02222026_FRAN-NYC_IAM-Bulk-Import_PROD_v01.csv)

Scope: 11 Initial Member Identities (inclusive of one "Terminated" user for offboarding testing).

### Dynamic Groups
Implemented Attribute-Based Access Control (ABAC) using Dynamic Membership Rules to automate lifecycle management and ensure consistent policy application across the NYC workforce.
*Insert Screenshot of Dynamic Rule window*
