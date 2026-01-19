# Agent Skills: Frontend Mastery

This file contains specialized logic blocks and technical capabilities available to the UI/UX Agent.

## Skill 1: Design System Tokenization
**Trigger:** "Extract tokens", "Create variables", "Standardize colors"
**Capability:**
Analyze a block of raw CSS or a mock-up description and convert magic numbers/hex codes into a systematic CSS Variable list.
* **Action:** Group colors into `brand`, `neutral`, `status`.
* **Action:** Group spacing into a `t-shirt` size scale (`--spacing-xs` to `--spacing-xl`).
* **Output Pattern:**
    ```css
    :root {
      /* Palette */
      --color-surface: #ffffff;
      --color-text-main: #2d3436;
      /* Typography */
      --font-scale-base: 1rem;
    }
    ```

## Skill 2: SVG Optimization & Inline Handling
**Trigger:** "Clean SVG", "Add icon", "Optimize vector"
**Capability:**
Take raw SVG code (often messy from design tools like Figma) and sanitize it for HTML embedding.
* **Routine:**
    1.  Remove `width` and `height` attributes (control via CSS).
    2.  Remove `fill` attributes (replace with `fill="currentColor"` for CSS coloring).
    3.  Strip unnecessary metadata (e.g., `xml:space`, `generator`).
    4.  Ensure `viewBox` is preserved.

## Skill 3: Critical Rendering Path (CRP) Audit
**Trigger:** "Make it faster", "Fix CLS", "Optimize loading"
**Capability:**
Identify CSS/JS that blocks the initial paint of the website.
* **Checklist:**
    * Are font files preloaded?
    * Is "Above the Fold" CSS inlined?
    * Are images explicit with `width`/`height` to prevent Layout Shifts (CLS)?
* **Resolution:** Suggest specific `<link rel="preload">` tags and `font-display: swap` properties.

## Skill 4: WCAG 2.1 Accessibility Patcher
**Trigger:** "Fix a11y", "Make accessible", "Screen reader check"
**Capability:**
Systematically scan the code for common WCAG violations and provide code-fix patches.
* **Logic:**
    * *If* `<a>` has no text -> Suggest `aria-label`.
    * *If* `<button>` is just a `div` -> Rewrite as `<button>` or add `role="button"` + `tabindex="0"` + JS Keydown listeners.
    * *If* Color contrast is low -> calculate nearest accessible hex color.

## Skill 5: Responsive Layout Debugger
**Trigger:** "Fix mobile view", "Overflow issue", "Responsive check"
**Capability:**
Diagnose layout breakage without seeing the screen by checking CSS logic.
* **Heuristics:**
    * Detect fixed widths (`width: 900px`) -> Suggest `max-width: 100%`.
    * Detect missing `flex-wrap` on containers with dynamic children.
    * Detect extensive use of absolute positioning which removes elements from the document flow.
