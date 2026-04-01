# Design System Document: The Architect’s Portfolio

## 1. Overview & Creative North Star: "The Digital Curator"
The Creative North Star for this design system is **"The Digital Curator."** In a world of cluttered, template-driven tech portfolios, this system stands apart through editorial restraint, authoritative scale, and physical depth. It is designed for a senior expert who doesn’t just write code, but orchestrates complex systems.

To break the "generic template" look, we move away from rigid, centered grids. Instead, we utilize **intentional asymmetry**—large display typography offset against dense informational clusters. The layout should feel like a high-end technical journal: breathing room on one side, and high-density data visualization on the other. We emphasize "Information Density with Grace," ensuring that live demos and technical specs feel premium, not overwhelming.

---

## 2. Colors: Tonal Depth & Accents
The palette is rooted in a "Deep Space" navy (`#0c1324`), utilizing an Emerald Primary (`#4edea3`) and Lavender-Indigo Tertiary (`#c0c1ff`) to create a high-contrast, professional tech aesthetic.

### The "No-Line" Rule
**Standard 1px borders are strictly prohibited for sectioning.** Boundaries must be defined solely through background color shifts. To separate the Hero from the "Work" section, transition from `surface` to `surface-container-low`. The eye should perceive the change in depth, not a line on the screen.

### Surface Hierarchy & Nesting
Treat the UI as a series of physical layers. Use the hierarchy below to "nest" importance:
- **Base Level:** `surface` (#0c1324) – The infinite canvas.
- **Section Level:** `surface-container-low` (#151b2d) – Large content blocks.
- **Component Level:** `surface-container` (#191f31) – Cards or interactive zones.
- **Elevated Level:** `surface-container-high` (#23293c) – Floating states or active modals.

### The "Glass & Gradient" Rule
To achieve "Premium Tech" polish:
- **Glassmorphism:** Navigation bars and floating action panels must use a semi-transparent `surface-container-highest` with a `24px` backdrop blur.
- **Signature Textures:** Main CTAs should not be flat. Use a subtle linear gradient from `primary` (#4edea3) to `primary-container` (#004e34) at a 135-degree angle to provide a "metallic" emerald sheen.

---

## 3. Typography: The Editorial Voice
We use a pairing of **Manrope** (Display/Headlines) for its modern, geometric authority and **Inter** (Body/Labels) for its unparalleled legibility in technical contexts.

*   **Display (Manrope):** Use `display-lg` (3.5rem) for hero statements. Tighten letter-spacing by `-0.04em` to create a "locked-in" professional look.
*   **Headlines (Manrope):** `headline-md` (1.75rem) should be used for section titles, often placed asymmetrically (e.g., top-left of a wide container).
*   **Body (Inter):** `body-lg` (1rem) is the workhorse. Maintain a line-height of `1.6` to ensure that even dense technical explanations remain readable during live demos.
*   **Labels (Inter):** `label-md` (0.75rem) in `on-surface-variant` is used for metadata, timestamps, and "Automation Logs." Use All-Caps with `0.1em` letter spacing for an "instrument cluster" feel.

---

## 4. Elevation & Depth: Tonal Layering
Traditional drop shadows are too "software-default." We use light and tone to imply height.

*   **The Layering Principle:** Place a `surface-container-lowest` (#070d1f) card on a `surface-container-low` (#151b2d) section. This creates a "recessed" look, perfect for code snippets or data feeds.
*   **Ambient Shadows:** For floating elements (like a "Live Demo" pop-out), use a shadow: `0px 20px 40px rgba(7, 13, 31, 0.4)`. The shadow color is a darker tint of the background, making it feel like a natural occlusion of light.
*   **The "Ghost Border" Fallback:** If accessibility requires a border, use the `outline-variant` (#3f4945) at **15% opacity**. It should be a whisper, not a statement.
*   **Glassmorphism Depth:** When using glass, apply a 1px inner-glow (top and left edges) using `primary` at 10% opacity to simulate light hitting the edge of a glass pane.

---

## 5. Components: Precision Primitives

### Buttons
*   **Primary:** Gradient (`primary` to `primary-container`), `md` roundedness (0.375rem). No border. Label in `on-primary` (#003824).
*   **Secondary:** Ghost style. No background. `Ghost Border` (outline-variant at 20%). On-hover: background becomes `surface-container-highest`.
*   **Tertiary:** `label-md` typography with a `primary` underline that expands on hover.

### Cards & Lists
*   **The Divider Ban:** Never use a horizontal line to separate list items. Use a `2.5` (0.5rem) spacing gap and a subtle background shift on hover to `surface-container-low`.
*   **Technical Cards:** Use `surface-container` with a `xl` (0.75rem) corner radius. Use `spacing-5` (1.1rem) for internal padding to maintain a "dense but breathable" feel.

### Automation "Pulse" (Custom Component)
*   For a senior automation specialist, include a **Status Pulse**. A small circular dot using `primary` (#4edea3) with a CSS scale animation to show "System Live." Combine with `body-sm` monospace text for "Live Metrics."

### Input Fields
*   **Text Inputs:** Use `surface-container-lowest` as the fill. The label should be `label-sm` floating above the field in `secondary`. No bottom border; use a full-perimeter `Ghost Border`.

---

## 6. Do’s and Don’ts

### Do:
*   **Do** use asymmetrical margins. If the left margin is `spacing-20`, try a right margin of `spacing-10` for a modern, editorial feel.
*   **Do** use "Monospace" (Inter with `font-feature-settings: "tnum"`) for any numerical data or automation logs to emphasize technical precision.
*   **Do** embrace "Active White Space." Large gaps between disparate sections make the content that *is* there feel more important.

### Don't:
*   **Don't** use pure black (#000000). Always use `surface` (#0c1324) to maintain the "Deep Space" sophisticated tone.
*   **Don't** use standard "Material" shadows. They are too heavy and muddy the "Premium Tech" aesthetic. 
*   **Don't** center-align long blocks of text. Keep technical copy left-aligned for an authoritative, "documentation" feel.
*   **Don't** use 100% opaque borders. They create "visual noise" that fights with the high-quality typography.