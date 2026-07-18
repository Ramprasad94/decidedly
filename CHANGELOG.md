# Changelog

All notable changes to **Decidedly** are recorded here. The tool is a single
file (`board.html`); each version is a self-contained release of that file.

## v1.0 — 2026-07-18

First public release. A single, self-contained HTML file for running a
discovery session and walking out with the decisions captured — no install, no
server, no dependencies, and no network calls.

### Added
- **Decision chips + custom pick-list** — cycle each row through your own
  vocabulary; the colour flows to the whole row and the progress meter.
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
- Permanent **Decidedly** wordmark and author/MIT-license credit in the footer.

MIT-licensed. Created by Ramprasad Bommaganty · https://keepingupwiththecloud.com
