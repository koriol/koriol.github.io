# WCAG 2.1 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Manual Audit Phase: Human-Centric Manual Evaluation

Automated tools are "syntax checkers"—they confirm the presence of code but cannot interpret its meaning. A site can have a 100% Lighthouse score while remaining completely unusable for a blind user or someone navigating via keyboard. This phase is about bridging that gap. The purpose of this evaluation is to simulate the real-world experience of users who rely on assistive technologies (AT) to ensure the site isn't just "compliant on paper," but truly accessible in practice.
* **Verify Logic:** Ensure the Focus Order follows the visual flow, especially where automated tools flagged "Landmark" and "Structural" issues.
* **Test Operability:** Identify any "Keyboard Traps" or "Invisible Focus" states that prevent mouse-less navigation.
* **Audit Meaning:** Manually review Alt Text and Heading Content to ensure they provide a logical road map, rather than just filling a technical requirement.
* **Validate Robustness:** Confirm that interactive components (like the mobile menu) function correctly with screen readers.

#### Skills & Tools
| Tool | Purpose | Skill Honed |
| --- | --- | --- |
| Keyboard-Only Navigation | Navigating the site using only Tab, Shift+Tab, Enter, and Esc. | **Functional Testing:** Identifying blockers for users with motor impairments. |
| VoiceOver / NVDA | Auditing the "Audio UI" to hear how the site is announced. | **AT Proficiency:** Understanding how ARIA roles and landmarks translate to speech. |
| WCAG 2.2 Checklist | Cross-referencing findings against specific success criteria. | **Regulatory Knowledge:** Applying legal standards to UI/UX components. |
| Screen Magnification (200-400%) | Checking for "Reflow" and content overlap at high zoom levels. | **Visual UI** Design: Ensuring layout stability for low-vision users. |

***
### The Bridge to Manual: Accessibility Insights
To ensure a rigorous "Double-Blind" audit, I added Accessibility Insights for Web to the toolset. This tool is unique because it provides a Visual Helper for manual testing—specifically for tracking the keyboard focus path—which allows me to "see" the tab order that a motor-impaired user would experience.











### Keyboard Operability & Focus Path Audit
Given the "Serious" structural alerts in the Axe audit, I suspected the tab order might be illogical. I performed a manual "Tab-through" of all 6 pages to ensure that every interactive element is reachable and that the visual focus indicator is never hidden.

















