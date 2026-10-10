# Freedom Calculator, brand design version

A duplicate of [freedom-calculator](https://github.com/YogiZoli/freedom-calculator) in the Zoltan Gero "Shine" design system, for a side by side comparison. Same questions, same calculation, same email gate, same webhook payload, same PDF content. Only the visual layer differs.

- Original: https://yogizoli.github.io/freedom-calculator/
- Brand design: https://yogizoli.github.io/freedom-calculator-brand-design/

## Design source

`YogiZoli/design-system`, file `tokens.css` (v3 "Shine", 2026-09-26), inlined verbatim at the top of the `<style>` block in `index.html`. Components read the role tokens only. Fonts: Open Sans and Geist Mono from Google Fonts on the page, Open Sans embedded from `fonts/` in the PDF.

## Stack

- One static file: `index.html` (HTML, CSS, vanilla JavaScript). No build step, no framework, no backend.
- PDF: jsPDF 2.5.1 from cdnjs, generated in the browser.
- Lead capture: optional POST to a webhook (GoHighLevel inbound webhook).
- State: `localStorage` in the visitor's browser.

## Settings

Both are at the top of the last `<script>` block in `index.html`:

- `WEBHOOK_URL`: empty means no POST, the PDF is still delivered.
- `PROGRAM_URL`: the link behind the cohort program CTA (placeholder for now).
