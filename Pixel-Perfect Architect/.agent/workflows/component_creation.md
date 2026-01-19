# Workflow: Create New UI Component

**Trigger:** When the user asks to "create", "build", or "design" a new UI element (e.g., Modal, Navbar, Card).

## Step 1: Requirements Gathering
* Ask for the component's purpose.
* Determine necessary states: Default, Hover, Active, Disabled, Loading, Error.

## Step 2: Architecture Setup
1.  **HTML Structure:** Draft the semantic HTML skeleton.
2.  **CSS Tokens:** Identify which CSS variables are needed (colors, spacing).
3.  **Accessibility Check:** Determine required ARIA roles (e.g., `role="dialog"` for modals).

## Step 3: Implementation
* Generate the HTML.
* Generate the CSS (Mobile First).
* Generate the JS (if interaction is needed).

## Step 4: Verification (Self-Correction)
* *Check:* Is the contrast ratio > 4.5:1?
* *Check:* Does it work without a mouse (Keyboard Navigation)?
* *Check:* Is it responsive down to 320px width?

## Output Format
Provide the code in three distinct blocks (HTML, CSS, JS) followed by a "Usage Example."
