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

## Reliability and troubleshooting

- The PDF tool loads from `vendor/` first, then from two CDNs. If none loads, the visitor sees what to do and a Try again button.
- A lead is posted as JSON, then as a form post if the browser blocks that. If both fail it is kept in the visitor's browser (up to 5 leads, 7 days) and sent again on the next visit or when the connection returns. Every lead carries a `submissionId`, so a duplicate can be spotted.
- The thank-you screen always says whether the visitor still has to wait or can close the page, and offers an "Open the PDF in a new tab" link in case the download did not start.
- "Something not working? Show details" at the bottom of the page opens the report. Ask the visitor to press Copy report and send it.

## Logging

Every line has the time, the milliseconds since the page opened, a session id, a running number and a level (INFO, WARN, ERROR). The last 500 lines are kept in the visitor's browser across visits and are also printed to the browser console with the `[freedom-calculator]` prefix.

What is logged: the environment when the page opens (version, browser, viewport, connection, frame, referrer), every button press and changed field, every result shown, each step of loading the PDF tool and fonts with timings, each step of building and handing over the PDF, each lead attempt with HTTP status and timing, retries of waiting leads, script errors with a stack, files that fail to load, blocked requests, lost connection, and the page being hidden or closed while work is running. Name and email are never written in full.

Each lead sent to the webhook also carries a `client` field with the version, session id, browser, and the last five warnings or errors of that visit.

## Palette

The page uses exactly this palette and nothing else (see the `:root` block at the top of `index.html`): text `#0F172A`, muted text `#475569`, page `#F5F7FA`, card `#FFFFFF`, borders `#E2E8F0`; accents Teal `#0E7490` on `#E6F4F7`, Navy `#1E3A8A` on `#E8EDFB`, Emerald `#047857` on `#E7F6F0`; attention Amber `#B45309` on `#FEF3E2` with `#92400E` text for warnings and errors. Blocks rotate teal, navy, emerald. The state before the colour change is tagged `before-color-fix`.
