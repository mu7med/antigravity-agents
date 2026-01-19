# Global Workflow: UI/UX Audit & Refactor

**Trigger:** When the user requests a "review," "audit," or "modernization" of a page or site.

## Phase 1: Visual Regression Analysis
1.  Analyze the CSS file size and specificity graph.
2.  Identify "Dead CSS" (selectors that no longer match HTML).
3.  Flag inconsistent UI tokens (e.g., using 5 different shades of gray that look almost identical).

## Phase 2: UX Heuristic Evaluation
Evaluate the interface against Nielsen’s 10 Usability Heuristics:
* **Visibility of system status:** Does the user know what's happening?
* **Error prevention:** Are form inputs validated before submission?
* **Aesthetic and minimalist design:** Is there too much noise?

## Phase 3: Refactoring Plan
1.  **Consolidate:** Merge duplicate styles into utility classes.
2.  **Modernize:** Replace `float` layouts with Grid/Flexbox. Replace `var` with `let/const`.
3.  **Optimize:** Implement lazy loading for images (`loading="lazy"`).

## Deliverable
Return a markdown table summarizing issues found, categorized by "Critical", "Moderate", and "Minor", followed by the refactored code blocks.
