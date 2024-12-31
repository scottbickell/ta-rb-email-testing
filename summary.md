# Dark mode & dynamic logo support

**DYNAMIC LOGO?** We have two logo images. One is for light mode (red icon, black text), the other is for dark mode (all white)

**GOAL**

The goal is to show the correct logo depending on the user's preference

I worked through several iterations to address dark mode logo display issues in email across major clients, including Gmail (Android and iOS), Outlook on Windows, and Apple Mail on macOS and iOS. These issues stemmed from the lack of consistent support for dark mode styles in email clients, compounded by the absence of universal email standards, unlike modern web development.

<br>

## Necessary context
**EMAIL DEVELOPMENT CHALLENGES:**  

Unlike web pages, email development faces significant hurdles due to outdated rendering engines, lack of standards, and proprietary client-specific behaviors. Dark mode exacerbates these challenges by introducing automatic transformations that developers cannot fully control.

Overall Progress: I iterated through solutions to target Gmail, Outlook, and Apple Mail specifically. While some progress was made, the inconsistencies highlight the need for simplifying the approach.

**RECOMMENDATION:** 

Adopt a light mode-only strategy for now to ensure brand consistency and minimize complexity. Explore universal design approaches to streamline future development.

<br>

## Key Issues Encountered

**Gmail (Android/iOS Dark Mode):**

- Issue: Gmail displayed the light mode logo in dark mode despite targeted CSS.

*Attempted fixes:*  

- Used u + body targeting to apply Gmail-specific styles.
- Added inline display styles `(style="display:none")` with `!important` for stronger specificity.
- Experimented with explicit media query types (`all` and `screen`) to align with Gmail’s developer documentation.

**Outlook (Windows dark mode):**

- Issue: Both the light mode logo and dark mode logo were displayed simultaneously.

*Attempted fixes:*  

- Used conditional comments `(<!--[if mso]>)` to isolate logo display for Outlook-specific rendering engines.
- Applied `[data-ogsc]` and `[data-ogsb-mode="dark"]` targeting for Outlook dark mode.

**Apple Mail (macOS dark mode):**
- Issue: Apple Mail displayed the wrong logo in dark mode.

*Attempted fixes:*  

- Focused on `@media (prefers-color-scheme: dark)` for dark mode targeting.
- Ensured background and text colors were explicitly declared to avoid unwanted transformations.

**General Testing Gaps:**
- Different email clients override styles unpredictably, often ignoring `@media` queries or inline styles.

<br>

## Why email development is so problematic

**Lack of Standardization:**
- Unlike web development, email clients lack consistent support for modern standards (CSS3, media queries).
- Each client interprets styles differently, leading to unpredictable behavior.

**dark mode Complexity:**
- dark mode transforms background and text colors automatically in some clients, overriding developer styles.
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
**1. Short-Term Solution:**
- Force light mode for all clients to simplify development and align with Transamerica's current branding [whose websites **do not explicitly support dark mode** (nor does Aegon's)].

**2. Long-Term Strategy:**
- Collaborate with design and branding teams to consider a universal logo design that works on both light and dark backgrounds (transparent background with a white or black outline).
- Advocate for email-friendly dark mode design practices across your organization.

**3. Ongoing Improvements:**
- Leverage tools like Litmus or Email on Acid for consistent testing.
- Stay updated on client-specific dark mode rendering rules (Gmail’s developer updates).

<br>
<br>
<br>
<br>
<br>

# Dark mode support and the role of `<meta name="supported-color-schemes">`
<br>

**Explicit** dark mode support with `<meta name="supported-color-schemes">`

This meta tag is a way to explicitly signal to email clients that your email is designed to support both *light* **and** *dark* modes.

For example:

```html
<meta name="supported-color-schemes" content="light dark">
```

- When both *light* and *dark* are specified, it tells clients that the email is optimized for color scheme changes and includes appropriate styling for both.

<br>

**No Meta Tag or Only light Specified:**

- If the meta tag is omitted or only light is specified:

```html
<meta name="supported-color-schemes" content="light">
```


- This signals to clients that dark mode is not explicitly supported, and the email should render as if it’s in light mode, even when viewed in a dark mode environment.
- Clients that rely on this meta tag (e.g., Apple Mail, some WebKit-based clients) will not attempt to apply dark mode transformations.

	3.	Behavior Without the Meta Tag:
- When the tag is omitted entirely, some email clients may guess whether the email supports dark mode and apply transformations inconsistently. This can lead to unpredictable behavior, such as:
- Background colors being inverted.
- Text colors being automatically lightened.
- Images like logos becoming difficult to see due to mismatched contrast.

Implications
- Including <meta name="supported-color-schemes" content="light dark"> explicitly signals to email clients that your email is designed to handle dark mode gracefully.
- Omitting the meta tag or limiting it to light ensures the email appears in light mode, but it also means the email client might override your design in unexpected ways (e.g., Gmail’s auto-dark mode).

Recommendation

For consistency, we recommend:
- Include the meta tag: Use <meta name="supported-color-schemes" content="light"> if you want to force light mode only.
- If you want full dark mode support, pair <meta name="supported-color-schemes" content="light dark"> with careful testing to ensure compatibility across clients.