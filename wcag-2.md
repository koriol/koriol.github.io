# WCAG 2.1 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Manual Audit Phase: Human-Centric Manual Evaluation

Automated tools are "syntax checkers"—they confirm the presence of code but cannot interpret its meaning. A site can have a 100% Lighthouse score while remaining completely unusable for a blind user or someone navigating via keyboard. This phase is about bridging that gap. The purpose of this evaluation is to simulate the real-world experience of users who rely on assistive technologies (AT) to ensure the site isn't just "compliant on paper," but truly accessible in practice.
* **Verify Logic:** Ensure the Focus Order follows the visual flow, especially where automated tools flagged "Landmark" and "Structural" issues.
* **Test Operability:** Identify any "Keyboard Traps" or "Invisible Focus" states that prevent mouse-less navigation.
* **Audit Meaning:** Manually review Alt Text and Heading Content to ensure they provide a logical road map, rather than just filling a technical requirement.
* **Validate Robustness:** Confirm that interactive components (like the mobile menu) function correctly with screen readers.

While automated tools like Axe and WAVE provided a technical hit-list, they are incapable of evaluating user intent and navigational logic. This phase focuses on a human-centric evaluation using the Accessibility Insights for Web framework. By shifting from code-scanning to active interaction, I can identify barriers that only emerge when a user attempts to navigate the site using assistive technology.

#### The Purpose of This Phase
The primary goal is to validate the "Four Pillars" (POUR) through a series of structured manual tests. I am specifically looking for:
* Operability: Can a keyboard-only user access every part of the site?
* Understandability: Does the reading order make sense when heard via a screen reader?
* Perceptibility: Does the site remain usable at high zoom levels (Reflow)?

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

One of the most common manual failures is an illogical "Tab Order." A user should move through the page in a predictable, linear fashion. I used the Tab Stops feature in Accessibility Insights to create a visual "map" of the site's interactive path. This allows me to see if the focus jumps around randomly or gets stuck in invisible elements—issues that a standard automated scan would likely mark as a "Pass."

![Homepage with the Tab Stops numbered circles and lines showing the path](./wcag/tab_stops_index.png)
> *Visualizing Navigation Logic: The Tab Stops tool confirms a linear and predictable navigation path, ensuring users don't get 'lost' in the page structure.*

***

### Reflow, Zoom, and Visual Stability
Low-vision users often zoom their browsers to 400% to read content. If your site isn't built with a "Responsive" mindset, elements will start to overlap, text will get cut off, or—worst of all—a horizontal scrollbar will appear. Horizontal scrolling is a massive accessibility failure because it forces the user to scroll left and right for every single line of text.

<u>The Purpose:</u>
To ensure that at 400% zoom, the site "reflows" into a single column (much like a mobile view) without losing any functionality or information.

While a site might look great on a standard mobile device, WCAG 1.4.10 (Reflow) requires that content remains functional at a 320px width equivalent (400% zoom on a 1280px screen). I chose the Homepage as the primary test case because it contains the most complex UI components—hero sections, overlapping text, and various grid layouts—making it the most likely candidate for "Reflow" failures.

![At 400% zoom, desktop menu has transformed into a mobile "Hamburger" menu.](./wcag/index_zoom.png)
> *Responsive Reflow (400% Zoom): The navigation successfully collapses into a mobile-friendly menu, ensuring no functionality is lost for high-magnification users.*

While the site successfully reflows into a single-column layout, I identified a horizontal overflow issue (the 'white bar' on the right). This indicates an element is not using relative units (like %), forcing a horizontal scrollbar. This violates WCAG 1.4.10 because it requires the user to scroll in two dimensions to perceive the content.

| Tool | Purpose | Skill Honed |
| --- | --- | --- |
| Browser Zoom (400%) | Simulating high-magnification needs. | Responsive Debugging: Ensuring layout integrity at extreme breakpoints. |
| Viewport Testing | Checking for horizontal scrollbars. | Reflow Optimization: Mastering the 320px CSS pixel standard. |

### Keyboard Operability & Focus Path Audit
Given the "Serious" structural alerts in the Axe audit, I suspected the tab order might be illogical. I performed a manual "Tab-through" of all 6 pages to ensure that every interactive element is reachable and that the visual focus indicator is never hidden.


### The Testimonial Carousel Conflict
While automated tools like Axe and WAVE flagged "Moderate" errors for this section, they could not detect the dynamic interaction failure occurring in real-time. During my manual screen reader audit, I identified that the auto-playing testimonial slider creates a "Focus Conflict." As the slides rotate, the Screen Reader loses its place, reading fragmented text or jumping to the next section before the user can finish the current testimonial.

![](./wcag/screenreader_testimonial.png)
> *Dynamic Content Failure: The Screen Reader history confirms a 'Focus Conflict' where the auto-playing testimonial slider interrupts the audio UI, preventing the user from reading the feedback.*

### Interactive Content & Pronunciation Audit
While automated tools check if a link exists, they don't check if it sounds right. During the manual walkthrough with Windows Narrator, I identified several "Audio UX" friction points, ranging from confusing link text to a broken testimonial slider that the client has since decided to phase out in favor of a user-controlled interface.

#### Manual Audit Summary Table
| Page | Keyboard Flow | 400% Reflow | Screen Reader (Audio) | Manual Status |
| --- | --- | --- | --- | --- |
| Home | ✅ Pass | ⚠️ Overlap | ⚠️ Missing | Detailed in Audit |
| About Us | ✅ Pass | ✅ Pass | ✅ Pass | Verified |
| About Founder | ✅ Pass | ✅ Pass | ⚠️ Alt Text | Verified |
| Affiliations | ✅ Pass | ✅ Pass | ✅ Pass | Verified |
| Services | ✅ Pass | ✅ Pass | ⚠️ Lists | Verified |
| Contact | ✅ Pass | ✅ Pass | ⚠️ Labels | Verified |

### Audit Conclusion: The Roadmap to 100%
The automated and manual audits revealed a site that is visually professional but structurally "noisy" for assistive technology.
* **Primary Barriers:** Lack of a main landmark, redundant link text, and an inaccessible auto-playing carousel.
* **Secondary Barriers:** Color contrast failures and non-sequential heading levels.
Next Step: I will now move into the Remediation Phase, where I will refactor the HTML5 structure and CSS variables to meet the WCAG 2.2 AA standard.












