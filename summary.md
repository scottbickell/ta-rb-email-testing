# Dark mode status report

I worked through several iterations to address dark mode logo display issues in email across major clients, including Gmail (Android and iOS), Outlook on Windows, and Apple Mail on macOS and iOS. These issues stemmed from the lack of consistent support for dark mode styles in email clients, compounded by the absence of universal email standards, unlike modern web development.

## Necessary context
**Email Development Challenges:**  

Unlike web pages, email development faces significant hurdles due to outdated rendering engines, lack of standards, and proprietary client-specific behaviors. Dark mode exacerbates these challenges by introducing automatic transformations that developers cannot fully control.

Overall Progress: I iterated through solutions to target Gmail, Outlook, and Apple Mail specifically. While some progress was made, the inconsistencies highlight the need for simplifying the approach.

**Recommendation:** 

Adopt a light mode-only strategy for now to ensure brand consistency and minimize complexity. Explore universal design approaches to streamline future development.

## Key Issues Encountered

**Gmail (Android/iOS Dark Mode):**

- Issue: Gmail displayed the light mode logo in dark mode despite targeted CSS.

*Attempts:*  

- Used u + body targeting to apply Gmail-specific styles.
- Added inline display styles `(style="display:none")` with `!important` for stronger specificity.
- Experimented with explicit media query types (`all` and `screen`) to align with Gmail’s developer documentation.

**Outlook (Windows Dark Mode):**

- Issue: Both the light mode logo and dark mode logo were displayed simultaneously.

*- Attempts:*  

- Used conditional comments `(<!--[if mso]>)` to isolate logo display for Outlook-specific rendering engines.
- Applied `[data-ogsc]` and `[data-ogsb-mode="dark"]` targeting for Outlook dark mode.

**Apple Mail (macOS Dark Mode):**
- Issue: Apple Mail displayed the wrong logo in dark mode.

*- Attempts:*  

- Focused on `@media (prefers-color-scheme: dark)` for dark mode targeting.
- Ensured background and text colors were explicitly declared to avoid unwanted transformations.

**General Testing Gaps:**
- Different email clients override styles unpredictably, often ignoring `@media` queries or inline styles.

## Why Email Development Is So Problematic

**Lack of Standardization:**
- Unlike web development, email clients lack consistent support for modern standards (CSS3, media queries).
- Each client interprets styles differently, leading to unpredictable behavior.

**Dark Mode Complexity:**
- Dark mode transforms background and text colors automatically in some clients, overriding developer styles.
- Some clients (Gmail) handle dark mode via proprietary rules that are poorly documented or inconsistently implemented.

**Legacy Constraints:**
- Email clients are constrained by older rendering engines (**Word-based rendering in Outlook**), which do not support modern web techniques.

**Testing Limitations:**
- Testing across all major email clients is time-consuming and requires tools Litmus. 
- Careful notes are necessary to keep track on iterations as different fixes are appied.
- Even with thorough testing, edge cases can emerge due to updates or quirks in specific clients.

**Summary of Findings**
1.Gmail dark mode is highly inconsistent and often ignores even aggressive styling techniques.
2. Outlook dark mode requires strict separation of light and dark mode styles using conditional comments and proprietary selectors.
3. Apple Mail and other clients with robust dark mode support (`@media (prefers-color-scheme: dark)`) are easier to target but may still present issues if other clients override rules.

## Recommended Next Steps
**1.Short-Term Solution:**
- Force light mode for all clients to simplify development and align with your company’s current branding (which does not support dark mode).

**2. Long-Term Strategy:**
- Collaborate with design and branding teams to consider a universal logo design that works on both light and dark backgrounds (transparent background with a white or black outline).
- Advocate for email-friendly dark mode design practices across your organization.

**3. Ongoing Improvements:**
- Leverage tools like Litmus or Email on Acid for consistent testing.
- Stay updated on client-specific dark mode rendering rules (Gmail’s developer updates).
