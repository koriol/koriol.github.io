# WCAG 2.2 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Implementation & Remediation

### Executing the Strategic Roadmap
To ensure high-quality code and zero regressions, I followed a four-stage lifecycle for every identified barrier:
* **Identify & Triage:** Map the finding to a WCAG Success Criterion and assign a Severity Heatmap color.
* **Engineer:** Refactor the HTML/CSS/JS in a local environment.
* **Verify:** Perform a dual-test (Automated via Axe + Manual via Windows Narrator).
* **Sign-Off:** Update the Risk Matrix to "Resolved" and log the new Lighthouse score.

With the Prioritization Matrix established, I moved into the execution phase, focusing first on the P0 (Critical) structural and perceptual barriers. My goal was to move the site from a "Div-Based" layout to a Semantic Architecture. By refactoring the core HTML5 elements and CSS variables, I addressed over 70% of the audit's total error count in the first development sprint.

***

### The Semantic Refactor (P0: Operable & Robust)

**The Problem:** The site lacked a `<main>` landmark and used generic `<div>` containers for the header and footer. This made the site a "flat land" for screen readers, providing no way for users to skip navigation and jump to the primary content.

**The Fix:** I refactored the global index and sub-pages to wrap content in appropriate HTML5 landmarks.

Before with Div Soup:
```
<header>
        <div class="container">
            <div id="branding">
                <div class="logo">
                    <a href="index.html">
                        <img src="Images/nclsLogo.png" alt="NLCS Logo - Dr. Juan T. Vives Jr. - Executive Coach in North White Plains, NY" style="width: 80px; height: 80px; margin-right: 10px" loading="lazy">
                    </a>
                </div>
                <div class="logo-text-main">
                    <div class="text-2xl font-bold">NLCS</div>
                    <span class="logo-text-sub">Next Level Consulting Solutions</span>
                </div>
            </div>
            <button class="menu-toggle" aria-label="Open navigation menu">&#9776;</button>
            <nav>
                <ul>
                    <li class="current"><a href="index.html">Home</a></li>
                    <li><a href="about.html">About Us</a></li>
                    <li><a href="about-dr-vives.html">About Founder</a></li>
                    <li><a href="affiliations.html">Affiliations</a></li>
                    <li><a href="services.html">Services</a></li>
                    <li><a href="contact.html">Contact Us</a></li>
                </ul>
            </nav>
        </div>
    </header>
```



After with Semantic Architecture:
```
<header role="banner">
        <div class="container">
            <div id="branding">
                <div class="logo">
                    <a href="index.html" aria-label="NLCS Home">
                        <img src="Images/nclsLogo.png" alt="NLCS Logo - Dr. Juan T. Vives Jr. - Executive Coach in North White Plains, NY" style="width: 80px; height: 80px; margin-right: 10px" loading="lazy">
                    </a>
                </div>
                <div class="logo-text-main" aria-hidden="true">
                    <div class="text-2xl font-bold">NLCS</div>
                    <span class="logo-text-sub">Next Level Consulting Solutions</span>
                </div>
            </div>

            <button class="menu-toggle" aria-label="Open navigation menu" aria-expanded="false" aria-controls="main-nav">&#9776;</button>
            <nav id="main-nav" aria-label="Primary Navigation">
                <ul>
                    <li class="current"><a href="index.html" aria-current="page">Home</a></li>
                    <li><a href="about.html">About Us</a></li>
                    <li><a href="about-dr-vives.html">About Founder</a></li>
                    <li><a href="affiliations.html">Affiliations</a></li>
                    <li><a href="services.html">Services</a></li>
                    <li><a href="contact.html">Contact Us</a></li>
                </ul>
            </nav>
        </div>
    </header>
```

### Contrast Remediation
During the perceptual audit, a discrepancy was identified between automated scanning tools (WAVE) and manual pixel-sampling tools (TPGi CCA). WAVE flagged the hero text as a "Contrast Failure" because it could not programmatically detect the CSS pseudo-element overlay. I resolved this by implementing "Solid Fallback" colors, ensuring that even if CSS assets fail to load, the text remains legible against a dark background.

The Challenge: "Phantom" Contrast Failures
Automated auditing via WAVE identified a critical contrast failure (1.09:1) in the Hero and Background sections. However, manual sampling via TPGi Colour Contrast Analyser confirmed a compliant ratio of 9.6:1.

The Technical Discovery:
The discrepancy was caused by the automated tool’s inability to calculate the opacity of the CSS ::before pseudo-element used for the dark overlay. The scanner was comparing white text against the default white background of the container, ignoring the "tinted glass" layer I had engineered for visual depth.

Technical Implementation (Code Comparison)
Before (Non-Compliant for Scanners):

```
/* The container had no fallback color, causing a "White-on-White" false positive */
.hero-section {
    background-image: url('hero.jpg');
    color: #fff;
    position: relative;
}
.hero-section::before {
    content: '';
    background-color: rgba(0, 0, 0, 0.7); /* Dark overlay visible to humans, invisible to tools */
}
```

After (Robust & Compliant):
```
/* Added a solid fallback color to provide a "safety net" for the accessibility tree */
.hero-section {
    background-color: #0d0d0d; /* Solid fallback satisfying WCAG 4.5:1 ratio */
    background-image: url('hero.jpg');
    color: #fff;
    position: relative;
}
```

Refining the Brand Colors (Actual Visual Fix)
I also identified a real contrast barrier in the header sub-text where the brand’s secondary gray (#ccc) failed Level AA standards.
| Element | Original Color | Remedied Color | Contrast Ratio | Result |
| --- | --- | --- | --- | --- |
| Logo Sub-text | #ccc | #E0E0E0 | 4.8:1 | PASS (AA) |

Balancing Brand Identity and WCAG AA Compliance
The Problem: A secondary action link color (#F0AD4E) failed the WCAG AA contrast threshold when placed on light backgrounds (#f9f9f9), yielding a 1.8:1 ratio.

![Color contrast fail ratio](./wcag/ccfail.png)
> *Color contrast dropper showing color ratio 1.8:1 on original branding color*

The Solution: I performed a "Color Deepening" remediation. By shifting the hue to a darker mustard-gold (#9E6600), I maintained the brand's visual identity while achieving a 4.62:1 ratio, surpassing the legal requirement of 4.5:1.

Why I didn't use a border: While a border provides a visual boundary, it does not solve the core issue of text legibility. Deepening the ink color ensures that users with low vision or color-blindness can read the characters themselves, not just see the outline of a box.

UI Pattern Pivot & Creative Problem Solving.

Why: Sometimes the "math" of two colors simply won't work for accessibility. A professional knows when to stop fighting the colors and instead change the design structure to ensure compliance without losing the brand's soul.

Minimalist Accessible Design and Interactive State Management.

Why: This approach prioritizes Readability (P1). By moving away from decorative colors for primary navigation/links, we ensure the user's focus remains on the content while maintaining a sophisticated "Executive" aesthetic.

Visual Hierarchy & Decorative Compliance.

Why: This proves the difference between meaningful content (which must be accessible) and decorative flair (which can be as "brand-heavy" as preferred). It shows we can satisfy a creative director and a compliance auditor at the same time.












