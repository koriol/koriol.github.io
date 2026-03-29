# WCAG 2.1 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Introduction
The goal of this project was to conduct a comprehensive accessibility audit and remediation for NL Coaching Solutions to ensure the platform is inclusive for all users, including those with visual, motor, auditory, or cognitive impairments.

* **Inclusivity:** Every potential client deserves equal access to professional coaching services, regardless of ability.
* **Legal Compliance:** Adhering to WCAG 2.1 AA standards mitigates legal risks under the ADA (Americans with Disabilities Act).
* **SEO & UX:** Accessible websites typically have cleaner code, better SEO rankings, and a more intuitive user experience for everyone. 

## Tools & Skills
* **Tools:** Axe DevTools, WAVE (Web Accessibility Evaluation Tool), NVDA or VoiceOver (Screen Readers), Colour Contrast Analyser (CCA).
* **Skills:** Semantic HTML5, WAI-ARIA implementation, Keyboard focus management, Accessibility auditing, Technical reporting. 

## Roadmap
1. [Discovery & Automated Audit](./wcag-1.md) – Baseline scan of all top-level pages.
2. [Manual Testing](./wcag-2.md) – Keyboard navigation, screen reader flow, and zoom testing.
3. [Remediation Plan](./wcag-3.md) – Prioritizing "blocker" issues and estimating fix times.
4. Implementation – Executing code changes.
5. Final Validation – Verifying fixes and issuing a conformance statement.

***

## Audit Readiness
1. Start with the purpose and clarify goals: to make the pages more accessible and welcoming for all users.
2. Scope: define which pages to focus on, mainly of the high-impact and traffic pages. Is there any specific content to exclude or focus on?
3. What technical environments will be used? (Automated or manual and why)
4. Who will be involved?
5. Prepare Resources: templates, checklists, reports, etc.

## Follow POUR
* **Percievable:** List issues such as missing alt text, absent captions and insufficient color contrast.
* **Operable:** Keyboard navigation gaps, invisible focus indicators and timing constraints.
* **Understandable:** Collect ambiguous linked text, unclear form error messages and inconsistent navigation labels.
* **Robust:** Incorrect area roles, non-semantic HTML structure and JavaScript-driven content that screen readers misinterpret.

## Steps for auditing
Categorize each concerned accessibility violation according to the four WCAG principles: perceivable, operable, understandable, and robust, to create ​a coherent remediation framework. ​Under perceivable, list issues such as missing alt text, absent captions, and insufficient ​color contrast. ​Operable covers keyboard navigation gaps, invisible focus indicators, and timing constraints. 

## Tools
| Feature | Axe DevTools (by Deque) | WAVE (by WebAIM) | Lighthouse |
| --- | --- | --- | --- |
| Best For | Developers fixing code | Visual learners and designers | - |
| Interface | Integrated into the Browser Console | Visual icons overlaying the website | - |
| Accuracy | Extremely high (zero false-positives) | High, but can be visually cluttered | - |
| Unique Power | Explains exactly which line of code failed | Highlights page structure and ARIA icons | - |
| Portfolio Value | Use of developer tools | Provides great ""Before/After"" visual screenshots. | - |

## WAVE AIM Score
The WAVE Accessibility IMpact (AIM) score provides a measure of impact of page accessibility issues on users with disabilities. The WAVE tools reports an Automated AIM based upon:

1. Number of detectable errors
2. Error density (number of detectable errors by page elements)
3. Number of WAVE alerts (possible or likely accessibility issues)

These factors are all aligned with the results from the annual WebAIM Million analysis of 1,000,000 home pages
to provide a comparative score from 1 to 10. A score of 5 indicates that the page's score is roughly average compared to web pages generally.

> *A high AIM Score does not necessarily indicate that the page is highly accessible or compliant with accessibility guidelines. Manual testing is always necessary to determine accessibility and compliance.*
















