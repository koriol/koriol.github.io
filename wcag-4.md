# WCAG 2.2 AA Accessibility Audit & Remediation: NL Coaching Solutions

## Implementation & Remediation

### Executing the Strategic Roadmap
With the Prioritization Matrix established, I moved into the execution phase, focusing first on the P0 (Critical) structural and perceptual barriers. My goal was to move the site from a "Div-Based" layout to a Semantic Architecture. By refactoring the core HTML5 elements and CSS variables, I addressed over 70% of the audit's total error count in the first development sprint.

***

### The Semantic Refactor (P0: Operable & Robust)

**The Problem:** The site lacked a `<main>` landmark and used generic `<div>` containers for the header and footer. This made the site a "flat land" for screen readers, providing no way for users to skip navigation and jump to the primary content.

**The Fix:** I refactored the global index and sub-pages to wrap content in appropriate HTML5 landmarks.

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


























