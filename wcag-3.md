# WCAG 2.1 AA Accessibility Audit & Remediation: NL Coaching Solutions

## The Remediation Planning Phase: Strategic Prioritization

### The Risk & Impact Matrix
| Finding | Frequency | User Impact | POUR Pillar | Priority | Rationale |
| --- | --- | --- | --- | --- | --- |
| Missing main Landmark | 100% (Global) | Critical | P0 | Prevents "Skip to Content." Without this, the site fails basic navigation standards. |
| Color Contrast (Low) | 100% (Global) | Critical | P0 | Legibility barrier. Most common reason for accessibility lawsuits. |
| Skipped Heading Levels | High | Serious | P1 | Breaks the document outline. Confuses non-visual users. |
| Unlabeled Mobile Menu | Home/Global | Serious | P1 | A button that says nothing is a "dead end" for blind users. |
| Auto-Play Carousel | Home | Serious | P1 | "Focus Trap" that interrupts reading. |
| Pronunciation (About Us) | Low | Friction | P2 | Minor UX annoyance ("U S"). |

Based on this matrix, I have selected the P0 and P1 issues for immediate remediation. This strategy targets "Global High-Impact" items first—fixing these will technically resolve over 70% of the audit's total error count with minimal lines of code changed.


#### The Priority Roadmap
To achieve WCAG 2.2 AA compliance efficiently, I have prioritized the following technical tasks:
| Task | Remediation Method | Est. Time | Portfolio Value |
| --- | --- | --- | --- |
| Semantic HTML Refactor | Replace div with <main>, <header>, <footer>. | 30 mins | Shows "Structural Integrity" skills. |
| CSS Theme Update | Update :root variables for text/background contrast. | 15 mins | Shows "Scalable Styling" efficiency. |
| Carousel Logic Fix | Disable JS auto-play; add aria-live and buttons. | 1 hour | Shows "JavaScript/ARIA" proficiency. |
| Heading Alignment | Audit H1-H6 tags for sequential logic. | 45 mins | Shows "Attention to Detail." |
| Link Text Cleanup | Remove "click here"" and fix ""About U S"" labels.",30 mins,"Shows ""Audio UI (A11y)"" expertise."|

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
























