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

<details>
<summary>📸 Click to view Baseline Audit Screenshots (12 total)</summary>
* [Homepage mobile scores](./wcag/nl_index_mobile_lh_score.png)
* [Homepage desktop scores](./)


















