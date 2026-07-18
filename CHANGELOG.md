# Changelog

All notable changes to **Decidedly** are recorded here. The tool is a single
file (`board.html`); each version is a self-contained release of that file.

## v1.0 — 2026-07-18

First public release. A single, self-contained HTML file for running a
discovery session and walking out with the decisions captured — no install, no
server, no dependencies, and no network calls.

### Added
- **Decision chips + custom pick-list** — cycle each row through your own
  vocabulary, with distinct states (e.g. *Agreed* outlined vs *Confirmed*
  filled ✓); the colour drives the row accent and the progress meter.
- **Session-complete state** — when every row is resolved, the meter reads
  "✓ All N resolved" and a calm banner invites you to Export or Copy summary.
- **Spotlight card** — the one decision a session hangs on, framed as options
  with what each *buys* and *costs*.
- **Live sequence diagrams**, **screenshot galleries** (add or paste), **detail
  rows**, **exit criteria**, and a **parking lot** for follow-ups.
- **Edit mode** — rewrite every title, header, option, and step in the browser;
  add or remove rows and sections. No JSON required.
- **Brand colour + logos** for co-branded, client-ready deliverables.
- **Leak check** — keep internal notes off the client screen; the client-facing
  exports run it automatically and block before anything slips out.
- **Exports** — JSON (round-trips back in), Excel (a real `.xlsx`, one sheet per
  section, no library), Save HTML (a frozen shareable snapshot), and Print / PDF.
- **Light / dark** theme (seeds from the OS, remembers your pick), full
  `localStorage` persistence, and a leave-the-page guard.
- **Blank Reset** — clear all text back to placeholders while keeping the
  template scaffold, behind a confirmation.
- **Streamlined toolbar** — exports collapse into an **Export** menu, with
  Import/Reset in an overflow menu (keyboard- and outside-click-dismissable).
- **Neutral, brand-aware header** — the header stays neutral in both themes; your
  picked brand colour drives the accents (meter, chips, tags, wordmark) instead
  of flooding the bar.
- **Accessible & semantic** — `<!doctype html>` + `lang`, real `<h1>`/`<h2>`
  headings, ARIA labels on editable cells, and AA-contrast text throughout.
- **Resilient save** — edits survive even if `localStorage` is full (kept in
  memory, with a badge warning) instead of throwing.
- Permanent **Decidedly** wordmark and author/MIT-license credit in the footer.

MIT-licensed. Created by Ramprasad Bommaganty · https://keepingupwiththecloud.com
