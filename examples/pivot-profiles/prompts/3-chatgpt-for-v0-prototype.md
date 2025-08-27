You are a Design+Frontend agent. Build a **single HTML file** (inline CSS + JS) that renders a consultant profile from a provided **YAML** blob. No build step. Use only CDN scripts if needed.

## Inputs
- I will provide `consultant-profile.yaml` (YAML with name, role, summary, skills[], industries[], employment[], education[], projects[] etc.). Parse it client-side.
- Assume the YAML structure is stable for this PoC.

## Goals
1) **Brand look**: Match SixPivot’s public website aesthetic—clean, minimal, professional black/white with a cool gray accent.  
   Provide CSS design tokens in a `:root` block:

   ```css
   :root {
     --sp-ink: #111827;       /* darkest charcoal for headings & text */
     --sp-muted: #475569;     /* medium gray for body copy */
     --sp-bg:  #f5f7fb;       /* soft off-white page background */
     --sp-card: #ffffff;      /* card / panel white */
     --sp-border: #e5e7eb;    /* subtle border */
     --sp-accent: #0ea5e9;    /* bright blue accent (links, buttons) */
     --sp-badge-bg: #e0f2fe;  /* light blue badge background */
   }
````

Include a **dark theme** via `[data-theme="dark"]` override:

```css
[data-theme="dark"] {
  --sp-ink: #f3f4f6;     /* near white text */
  --sp-muted: #94a3b8;   /* lighter gray for copy */
  --sp-bg:  #1e293b;     /* dark navy background */
  --sp-card: #293145;    /* card background */
  --sp-border: #475569;  /* darker border */
  --sp-accent: #38bdf8;  /* lighter blue accent for contrast */
  --sp-badge-bg: #075985;/* dark accent for badges */
}
```

2. **Profile rendering**: From the YAML, render sections:

   * Header: name, role/title, industries (badges)
   * Summary (paragraph)
   * Skills (compact badges)
   * Education & Employment (chronological lists)
   * Projects (cards with year, client, blurb)
   * Placeholder for attachments

3. **Scoped view controls**: Sidebar with toggles for each section (Summary, Skills, Projects, Employment, Education). Toggling hides/shows the respective section.

4. **Customer viewer preview**: Main pane shows the scoped profile with:

   * “Expires in X days” banner (simulate as 14 days)
   * Download buttons: PDF & DOCX (for this PoC, these trigger `alert("Download PDF")`)

5. **Analytics demo**: Use `IntersectionObserver` to track when each visible section is in view ≥60% for ≥2s. Show a live **Activity** panel with:

   * “Views” (page loads)
   * “Section Reads” (counts per section ID)
   * “Downloads” (count of button clicks)

6. **Local‐dev friendly**: Entirely functional offline, no external calls beyond optional CDNs. All logic in the single HTML file.

7. **Accessibility & print**:

   * Use appropriate ARIA roles, focus style.
   * Include `@media print { ... }` rules to layout profile for clean A4 PDF printing, using the Light theme.

## Constraints

* One static HTML file. Inline all CSS + JS.
* Allowed CDNs: **js-yaml**, optionally **marked** if handling narrative markdown.
* No frameworks—just vanilla JS.
* System fonts only, no external fonts.

## Layout & Design guidance

* Two-column layout at ≥1024px: Left 25% controls & activity, Right 75% profile preview.
* Card UI with 1px border (`--sp-border`), 16px border-radius, 12px padding.
* Typography scale: 32px (h1), 24px (h2), 18px (body), 14px (small).
* Badges: rounded pills with background `--sp-badge-bg`, text `--sp-ink`, padding 4px 8px, font-size 14px.

## Deliverable

A single HTML file with:

* A `<style>` block containing the design tokens and responsive rules.
* A `<script>` block for:

  * YAML parsing (via `js-yaml` CDN)
  * Section toggles
  * IntersectionObserver analytics
  * Theme toggle
  * Download button handlers
* A `<script id="yaml">…</script>` with a realistic sample YAML (commented in), so the file runs as-is.
* A small footer: “Confidential viewer; usage is logged.”

---

**Expected outcome**:
When opened, the page allows you to toggle dark/light, show/hide sections, scroll the profile, see counts increment in the Activity panel, and click Download (alerts). All styled with SixPivot brand tokens.
