# ShiftNote LP02 — Design QA

Date: 2026-10-29 (Asia/Tokyo)

final result: passed

## Reference and implementation

- Visual truth: `redesign/stitch-desktop.png`, original Stitch screen `projects/4690497384793290053/screens/f2d2ef34cfaa4c23adde0aef46d6cdab`.
- Same-viewport reference capture: `design/qa/reference-desktop.png` (1280 × 4802).
- Implemented Japanese page: `design/qa/desktop-ja.png` (1280 × 4810).
- Viewport: 1280 × 900 CSS pixels, light theme, top of page, FAQ and menu closed, demonstration figures. Both comparison captures are 1 image pixel per CSS pixel. Original Stitch export is 2560 × 9604; the fresh browser reference is used to avoid density mismatch.
- Full-view combined evidence: `design/qa/final-full.jpg`.
- Hero comparison: `design/qa/final-hero.jpg`.
- Focused dashboard comparison: `design/qa/final-detail.jpg` (same 572 × 662 CSS-pixel region in each capture).
- Mobile evidence: `design/qa/mobile-ja-320.png`, `design/qa/mobile-ja-390.png`, `design/qa/mobile-en.png`.
- English desktop evidence: `design/qa/desktop-en.png`.
- Browser: Codex in-app browser. Screenshots were captured from the rendered pages, not generated from source HTML.

## Findings and comparison history

1. First browser check found cached LP01 CSS after replacing the stylesheet. Fixed with an explicit LP02 stylesheet version in both HTML pages; the next capture confirmed the compiled palette and layout.
2. Initial desktop comparisons (`comparison-full.jpg`, `comparison-hero.jpg`, `comparison-detail.jpg` in `design/qa/`) showed the Google icon incorrectly turning white on the citron final CTA. Restricted the white icon treatment to the dark hero button and kept the final CTA mark dark. Final comparison confirms the intended contrast and icon size.
3. The 320px mobile check found a single-character wrap in the dashboard header. Reduced that metadata label and its marker at mobile widths. Rechecked at 320px; the date/title is now a single line, with the demo label on its own row.
4. Final full-page, hero, and dashboard comparisons show no remaining actionable P0/P1/P2 differences. The 8px document-height difference is attributable to the functional language switch and copy corrections.

## Required fidelity surfaces

- **Fonts and typography:** Noto Sans JP for Japanese/body copy and Manrope for financial figures; reference headline size, weight, line-height and two-line Japanese wrapping retained. English uses Manrope for the hero and adapts wrapping. Narrow metadata and long English labels remain readable.
- **Spacing and layout:** Same desktop split hero, 1280px container, 48px side padding, dashboard proportions, asymmetric feature panels, step sequence, pricing band, FAQ and final CTA. Mobile uses stacked sections and a working menu; calendar samples become readable stacked entries. No horizontal document overflow at 320, 390, 768 or 1280px in either language.
- **Colors and tokens:** Stitch forest, ivory, sage and citron tokens are kept in `tailwind.config.cjs`. Local CSS replaces the runtime Tailwind CDN. The final CTA mark has the correct dark treatment on citron.
- **Image quality and asset fidelity:** No stock images or invented illustrations added. The supplied Stitch dashboard/chart markup and Material Symbols are retained. The Google mark is a supplied local asset from the existing frontend; no raster stretching or broken images found.
- **Copy and content:** Japanese visual hierarchy retained; English translated to match. Demonstration figures are explicitly labeled. Fixed October 2026 weekdays and changed the unsupported “42 confirmed hours” text to “sample”. Calendar setup copy reflects connecting from the app after account creation. Legal destinations were absent in both the original LP and proposal; labels are noninteractive and marked as coming soon instead of pointing at nonexistent anchors.

## Interaction and validation

- Japanese/English navigation works in both directions.
- Mobile menu opens, closes after a section link, and closes with Escape while returning focus to its summary.
- Mobile menu FAQ link scrolls to `#faq`; native FAQ details expand/collapse and reveal the matching answer.
- Registration, sign-in and demo links target the existing frontend routes on `app.shift-note.jp`. No login forms were submitted and no accounts were created.
- Local asset existence, unique IDs, anchor targets, one h1/main landmark per locale, and absence of runtime Tailwind scripts checked.
- Skip link, visible keyboard focus, icon hiding, chart description and reduced-motion CSS included.
- Browser console errors/warnings checked: none on the implemented pages.
- `npm ci`, `npm run build`, `node --check assets/site.js`, and `git diff --check` passed. CSS build printed only the upstream Browserslist data-age advisory.

## Implementation checklist

- [x] Preserve LP01 on local `archive/lp01` and tag `lp01`.
- [x] Implement the selected Stitch design in both existing locale routes.
- [x] Compile shared CSS and wire the core links.
- [x] Verify responsive layouts and primary interactions.
- [x] Compare the final rendered page against the selected visual truth.

## Follow-up polish / limits

- Existing sharing-card images and favicon are retained; a separately designed LP02 sharing card could be added later.
- Google Fonts remain an external dependency. No backend/authentication changes, deployment, Cloudflare configuration changes or successful remote writes are part of this task.
- No separate mobile visual target was supplied; the mobile layout is a responsive interpretation of the approved desktop design.
