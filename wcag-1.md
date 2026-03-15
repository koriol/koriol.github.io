# WCAG 2.1 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Discovery & Automated Audit

### Introduction
Automated tools catch 30-40% of issues (like missing alt text or low contrast) instantly. This provides a "hit list" to clear before moving into the nuanced manual testing. No single tool catches everything. By cross-referencing, I ensure that structure (WAVE) and code-level compliance (Axe) are both addressed.

Before touching a single line of code, I need to establish a quantitative baseline. Lighthouse allows me to measure not just accessibility, but also how accessibility fixes might impact (or improve) SEO and Performance. While Lighthouse scores are high across the board, the goal of a WCAG audit is 100% functional compliance, not just a passing grade. I captured baseline metrics for every page on both mobile and desktop to ensure no regressions occur during the remediation phase.

An effective audit must cover the entire user journey, not just the homepage. By testing all six pages on both Mobile and Desktop, I ensured that accessibility was maintained across different screen sizes and UI components.

| Page | Desktop (A11y) | Mobile (A11y) | Status |
| --- | --- | --- | --- |
| Home | [87](./wcag/nl_index_desktop_lh_score.png) | [91](./wcag/nl_index_mobile_lh_score.png) | ⚠️ Needs Work | Color contrasts; sequential heading elements; main landmark |
| About Us | [97](./wcag/nl_about_desktop_lh_score.png) | [98](./wcag/nl_about_mobile_lh_score.png) | ✅ Pass | Minimal issues; missing main landmark |
| About Founder | [93](./wcag/nl_founder_desktop_lh_score.png) | [96](./wcag/nl_founder_mobile_lh_score.png) | ✅ Pass | Heading sequence; main landmark |
| Affiliations | [97](./wcag/nl_affiliations_desktop_lh_score.png) | [98](./wcag/nl_affiliations_mobile_lh_score.png) | ✅ Pass | Main landmark | 
| Services | [93](./wcag/nl_services_desktop_lh_score.png) | [96](./wcag/nl_services_mobile_lh_score.png) | ✅ Pass | Heading sequence; main landmark |
| Contact | [95](./wcag/nl_contact_desktop_lh_score.png) | [96](./wcag/nl_contact_mobile_lh_score.png) | ✅ Pass | Heading sequence; main landmark |

While conducting the Accessibility audit, I noted the Homepage Performance score was 75. Since Accessibility and Performance often overlap (e.g., properly sized images and clean DOM structures), my remediation plan includes optimizing these elements to boost both scores simultaneously

![](./wcag/accessibility_lh_score_details.png)
> *Initial site-wide baseline: While most pages scored in the 90s, the homepage mobile audit audit revealed specific failures in color contrast, heading sequence and a missing main landmark*

***

### Deep-Dive Accessibility Audit (WAVE & Axe DevTools)
Automated scores (Lighthouse) are a great start, but they don't catch everything. I used WAVE to visualize the document structure and Axe DevTools to inspect the DOM for ARIA and contrast failures that impact screen reader users. Auditing both Desktop and Mobile ensures the responsive design doesn't "break" accessibility (e.g., hidden menus that aren't keyboard-accessible).

I used WAVE to get a visual overlay of the site's structural integrity. Unlike code-only tools, WAVE allows me to see exactly where "Contrast Errors" and "Alerts" appear in the layout, making it easier to identify patterns in the CSS that need global adjustments.

### WAVE Severity Table

| WAVE Category | Portfolio Translation | Severity | Why it matters |
| --- | --- | --- | --- |
| Contrast Errors | WCAG 1.4.3 (Minimum Contrast) | Critical | Prevents users with visual impairments from reading content. |
| Structure | WCAG 1.3.1 (Info & Relationships) | High | Breaks the logical "map" of the site for screen readers. |
| ARIA | WCAG 4.1.2 (Name, Role, Value) | Medium | Can cause "silent failures" where a button is seen but not announced. |
| Alerts | Manual Review Required | TBD | These are "potential" issues that need a human to check. |

I selected WCAG 2.2 Level AA as the audit baseline. This represents the most current international standard and aligns with 2026 legal mandates. While Level AAA is available, it is often impractical for full-site implementation; instead, I will target specific AAA criteria where they provide the most value to the user experience.


#### Audit Evidence Log

| Page | Device | WAVE (Errors / Alerts ) | Axe DevTools Status (Critical / Serious / Moderate) | Key Finding |
| --- | --- | --- | --- | --- |
| Home | [Mobile](./wcag/wave_dex_index_mobile.png) | 0 / 6 | 0 / 7 / 21 | Color contrast ratios, Some page content is not contained by landmarks |
| Home | [Desktop](./wcag/wave_dev_index_desktop.png) | 0 / 6 | 0 / 10 / 21 | Color contrast ratios and redundant links |
| About Us | [Mobile](./wcag/wave_dev_about_mobile.png) | 0 / 1 | 0 / 2 / 10 | Frame names; Ensure that lists are structured correctly |
| About Us | [Desktop](./wcag/wave_dev_about_desktop.png) | 0 / 1 | 0 / 0 / 4 | Heading sequence and main landmark | 
| About Founder | [Mobile](./wcag/wave_dev_founder_mobile.png) | 0 / 3 | 0 / 2 / 19 | Ensure that lists are structured correctly; Sequential heading levels |
| About Founder | [Desktop](./wcag/wave_dev_founder_desktop.png) | 0 / 3 | 0 / 3 / 19 | Ensure that lists are structured correctly; Ensure touch targets have sufficient size and space |
| Affiliations | [Mobile](./wcag/wave_dev_affiliations_mobile.png) | 
| Affiliations | [Desktop](./wcag/wave_dev_affiliations_desktop.png) |
| Services | [Mobile](./wcag/wave_dev_services_mobile.png) |
| Services | [Desktop](./wcag/wave_dev_services_desktop.png) |
| Contact | [Mobile](./wcag/wave_dev_contact_mobile.png) |
| Contact | [Desktop](./wcag/wave_dev_contact_desktop.png) |

While Lighthouse gave the homepage a 87, WAVE revealed 32 specific errors that Lighthouse missed on the homepage. This discovery validated the necessity of a multi-tool audit approach; scores can be deceiving, but the error count doesn't lie

### POUR Alignment

| Pillar | Meaning | Specific Findings |
| --- | --- | --- |
| Perceivable | Can the user see or hear it? | 11 Contrast Errors, Alt Text quality, text resizing. |
| Operable | Can the user navigate and use it? | 14 Structural Errors (if they affect navigation), Keyboard traps, Focus indicators. |
| Understandable | Does it make sense? | Heading sequence (logic), Form labels, error messages. |
| Robust | Does it work with all tech? | 1 ARIA error, clean HTML code, screen reader compatibility. |









