# a11y-Bookmarklet-Resize-Text-Measurement

> **Status: work in progress — feedback welcome.**

A bookmarklet that helps auditors test **WCAG Success Criterion 1.4.4 (Resize Text)** by measuring the *actual* rendered size of selected text before and after magnification.
This bookmarklet is correntlyvibe-coded with AI. 

## Purpose

Instead of assuming that "200% zoom" produces 200% larger text, this tool **measures the real result**. It captures the rendered size of the text elements you choose, lets you enlarge the page however you like, and then reports the true magnification in percent.

## How it works

1. **Install** the bookmarklet in your browser (add it as a bookmark).
2. **Open the page** you want to test at 100% font size / 100% zoom.
3. **Run the bookmarklet.** A small box appears in the top-right corner. You can drag it anywhere by its title bar so it doesn't cover the content you're testing.
4. **Set the baseline:** click, one after another, on every text element you want to test — headings, paragraphs, links, buttons, and so on. A hover outline shows which element you're about to select, and each selected element keeps a marker so you can see what you've already picked.
5. When all the texts you want to check are selected, click **"Baseline complete"**.
6. **Enlarge the text** — using browser zoom, browser font-size settings, or any text-resize control the page itself provides.
7. Click **"Update"**.
8. The bookmarklet shows the **current rendered size** of each text and the **calculated magnification in percent**.

You can enlarge further and click "Update" again as often as you like.

## What is measured, and why two factors

The size a user actually sees is produced by two independent things. The tool reports both, then combines them.

### CSS factor

This is the change in the text's own CSS size, read directly from the browser. It already includes everything the stylesheet does — `rem`/`em` scaling, `calc()`, `clamp()`, media queries, and any resize function the site offers. If a media query makes the font *smaller* while you enlarge the page, you'll see it here as a value below the expected amount.

### Zoom factor

Browser zoom does **not** change the CSS size of an element — the browser keeps the same CSS pixels and simply displays them larger. Because of this, measuring the CSS size alone would miss browser zoom entirely. The tool therefore also tracks the browser's zoom level and reports it as a separate factor.

### Effective size

The real, visible magnification is the **CSS factor × zoom factor**. This combined value is what you compare against the 200% requirement.

Reporting the two factors separately also makes it visible *where* the magnification comes from — and, importantly, when a media query is reducing the font size and capping the result below the expected value.


## Notes and limitations

- This tool **supports, but does not replace,** visual inspection of the page at the target magnification.
- Tested in current versions of Firefox and Chromium-based browsers (Chrome / Edge).

## Feedback

This is an early work-in-progress version. Issues, suggestions, and pull requests are very welcome.
