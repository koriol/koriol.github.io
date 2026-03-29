# WCAG 2.1 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Remediation Phase: The Strategy

### Introduction: Prioritizing Impact
With a total of 32 automated errors and several manual "blockers" identified, the remediation phase must be handled systematically. My goal is to move from Global Fixes (high-impact structural changes) to Granular Fixes (page-specific text and link adjustments). This ensures that the most critical barriers—such as the missing main landmark and the auto-playing carousel—are resolved first.

#### The "Top 5" Priority Roadmap
To achieve WCAG 2.2 AA compliance efficiently, I have prioritized the following technical tasks:
* **Semantic Refactor (Structural):** Implementing HTML5 <main>, <header>, and <footer> tags to provide a navigational "map" for screen readers.
* **Global CSS Variable Update (Perceptual):** Adjusting the primary and muted text color variables to meet the 4.5:1 contrast ratio across all 12 audited views.
* **Heading Hierarchy Repair (Understandable):** Re-sequencing <h1> through <h3> tags to ensure a logical "Table of Contents" on every page.
* **Carousel Reconstruction (Operable):** Disabling the auto-scroll feature and implementing manual navigation buttons to give users control over moving content.
* **Audio UI Cleanup (Robustness):** Fixing the "About U S" pronunciation and removing redundant "Services" list announcements using aria-label or cleaner HTML text.

### Skills & Tools
| Tool | Purpose | Skill Honed |
| --- | --- | --- |
| VS Code / CSS Variables | Implementing site-wide color changes. | **Scalable Styling:** Using variables for efficient, global accessibility fixes. |
| Semantic HTML5 | Replacing <div> containers with landmarks. | **Information Architecture:** Building code that conveys meaning, not just layout. |
| ARIA Attributes | Fine-tuning how Screen Readers "speak" the content. | **Technical Communication:** Overriding default browser behavior for a better Audio UI. |

***

### Planning the "Global Contrast" Fix
Instead of fixing 11 individual contrast errors, I will target the root cause: the CSS theme. By identifying the hex codes that failed the audit (e.g., #A1A1A1) and replacing them with WCAG-compliant alternatives (e.g., #767676), I can resolve nearly 30% of the audit's errors in a single code push.

![A snippet of your CSS code showing the "Old" color commented out and the "New" compliant color active.](./wcag/)
> *Global Style Remediation: Updating CSS variables to ensure every page meets the WCAG 2.2 AA contrast standard simultaneously.*
























