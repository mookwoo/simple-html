PR title
feat: add scroll offset for in-page anchors (CSS + JS)

Summary
- Improve in-page navigation UX by adding a top scroll offset so target sections are not flush with the top of the viewport.
- This combines a CSS solution for native anchor jumps and a small JS fallback to ensure consistent smooth scrolling across browsers.

What changed
- styles.css
  - Added `scroll-padding-top: 90px;` to `html` so native anchor navigation respects a top breathing room.
- index.html
  - Added offset-aware smooth-scroll JavaScript:
    - Intercepts `a[href^="#"]` clicks and performs `window.scrollTo({ top: ..., behavior: 'smooth' })` with a 90px offset.
    - Updates the URL hash without causing a jump (uses history.pushState).
    - Applies a small correction on initial page load when a hash is present.

Motivation
- When navigating to sections via anchors, content was appearing flush against the top of the viewport. A small top offset (90px by default) improves readability and visual comfort, especially on pages with prominent headings or fixed headers.

Testing
1. Open the site and click the "Get Started" button (→ `#features`).
2. Click the "View Examples" button (→ `#code-examples`).
3. Both navigations should smoothly scroll to their targets and leave ~90px of space between the top of the viewport and the section top.
4. Open the page with a hash in the URL (e.g., `index.html#code-examples`) — the page should adjust after load to include the offset.

Notes & options
- The offset value is set to 90px. To change it:
  - Update `scroll-padding-top` in `styles.css`.
  - Update `SCROLL_OFFSET` in `index.html`.
- If you plan to add a fixed header later, we can make the offset dynamic by reading the header’s computed height instead of hard-coding the value.

Files changed
- `styles.css` — add `scroll-padding-top: 90px;` on `html`
- `index.html` — add offset-aware smooth-scroll JS and initial-hash adjustment

Changelog entry (optional)
- feat: add top offset for anchor navigation to improve UX

Suggested reviewers / labels
- Reviewers: frontend / UX
- Labels: enhancement, ux

---
Use this file to copy/paste into the PR body if you prefer editing the PR manually.
