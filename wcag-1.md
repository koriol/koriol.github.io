# WCAG 2.1 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Discovery & Automated Audit

### Introduction
Automated tools catch 30-40% of issues (like missing alt text or low contrast) instantly. This provides a "hit list" to clear before moving into the nuanced manual testing. No single tool catches everything. By cross-referencing, I ensure that structure (WAVE) and code-level compliance (Axe) are both addressed.

Before touching a single line of code, I need to establish a quantitative baseline. Lighthouse allows me to measure not just accessibility, but also how accessibility fixes might impact (or improve) SEO and Performance. While Lighthouse scores are high across the board, the goal of a WCAG audit is 100% functional compliance, not just a passing grade. I captured baseline metrics for every page on both mobile and desktop to ensure no regressions occur during the remediation phase.

An effective audit must cover the entire user journey, not just the homepage. By testing all six pages on both Mobile and Desktop, I ensured that accessibility was maintained across different screen sizes and UI components.

| Page | Desktop (A11y) | Mobile (A11y) | Status |
| --- | --- | --- | --- |
| Home | 87 | 91 | ⚠️ Needs Work | Color contrasts; sequential heading elements; main landmark |
| About Us | 97 | 98 | ✅ Pass | Minimal issues; missing main landmark |
| About Founder | 93 | 96 | ✅ Pass | Heading sequence; main landmark |
| Affiliations | 97 | 98 | ✅ Pass | Main landmark | 
| Services | 93 | 96 | ✅ Pass | Heading sequence; main landmark |
| Contact | 95 | 96 | ✅ Pass | Heading sequence; main landmark |

* [Homepage mobile scores](./wcag/nl_index_mobile_lh_score.png)
* [Homepage desktop scores](./wcag/nl_index_desktop_lh_score.png)
* [About Us mobile scores](./wcag/nl_about_mobile_lh_score.png)
* [About Us desktop scores](./wcag/nl_about_desktop_lh_score.png)
* [About Founder mobile scores](./wcag/nl_founder_mobile_lh_score.png)
* [About Founder desktop score](./wcag/nl_founder_desktop_lh_score.png)
* [Affiliations mobile score](./wcag/nl_affiliations_mobile_lh_score.png)
* [Affiliations desktop score](./wcag/nl_affiliations_desktop_lh_score.png)
* [Services mobile score](./wcag/nl_services_mobile_lh_score.png)
* [Services desktop score](./wcag/nl_services_desktop_lh_score.png)
* [Contact Us mobile score](./wcag/nl_contact_mobile_lh_score.png)
* [Contact Us desktop score](./wcag/nl_contact_desktop_lh_score.png)

While conducting the Accessibility audit, I noted the Homepage Performance score was 75. Since Accessibility and Performance often overlap (e.g., properly sized images and clean DOM structures), my remediation plan includes optimizing these elements to boost both scores simultaneously

![](./wcag/accessibility_lh_score_details.png)
> *Initial site-wide baseline: While most pages scored in the 90s, the homepage mobile audit audit revealed specific failures in color contrast, heading sequence and a missing main landmark*

***

### Deep-Dive Accessibility Audit (WAVE & Axe DevTools)
Automated scores (Lighthouse) are a great start, but they don't catch everything. I used WAVE to visualize the document structure and Axe DevTools to inspect the DOM for ARIA and contrast failures that impact screen reader users. Auditing both Desktop and Mobile ensures the responsive design doesn't "break" accessibility (e.g., hidden menus that aren't keyboard-accessible).

Audit Evidence Log
| Page | Device | WAVE Status | Axe DevTools Status | Key Finding |
| --- | --- | --- | --- | --- |
| Home | Mobile |
| Home | Desktop |
| About Us | Mobile |
| About Us | Desktop |
| About Founder | Mobile |
| About Founder | Desktop |
| Affiliations | Mobile |
| Affiliations | Desktop |
| Services | Mobile |
| Services | Desktop |
| Contact | Mobile |
| Contact | Desktop |














