# Changelog

All notable changes to **Decidedly** are recorded here. The tool is a single
file (`board.html`); each version is a self-contained release of that file.

## v1.2.2 — 2026-07-19

### Added
- **A first-run welcome bar.** The board opens full of the OmniCart sample, and
  "Reset board" hides in the ⋯ overflow menu — so a first-time opener had no
  obvious way to clear it and start their own session. On the very first open, a
  slim, dismissible bar now names the sample content and offers a one-click
  **Start a blank board**. It retires for good once dismissed, on your first
  edit, or when you enter Edit mode, and never appears on an exported snapshot a
  client opens.

## v1.2.1 — 2026-07-18

### Changed
- **The header shows one brand at a time.** Decidedly by default; the moment you
  add a company logo it steps aside and your logo(s) take the identity slot, so
  the tool's mark and a client's mark never sit side by side as if they were
  partners. Decidedly's attribution moves to the footer, which now reads
  **"Made with Decidedly."**

### Fixed
- **Adding a logo no longer breaks the toolbar.** A right-side logo used to float
  into the middle of the header, and any logo could push the overflow (⋯) menu
  onto a second row where its dropdown opened off-screen. The controls now stay
  in one right-aligned cluster and logos live in a dedicated slot.
- **The leak / image-export banner scrolls into view** when a client export is
  blocked, so you can see why it stopped instead of nothing appearing to happen.

## v1.2 — 2026-07-18

### Added
- **A proper identity.** A "Decidedly" logo — a folded write-up sheet with a
  decision check, on an amber tile, paired with a serif wordmark. It appears as
  the favicon (inlined, no network call), in the header, and in the footer.

### Changed
- **Brand colour is now amber** (`#a15d0e`) instead of the old green, matching
  the logo. AA contrast verified for every accent pairing.
- **Clearer status colours.** With amber as the brand, the palette now reads as
  three distinct signals: amber = agreed / confirmed, **blue** = needs
  definition, **red** = destructive actions and the leak stop-signal. (Blue and
  red both used to be amber.)

### Fixed
- The decision-tone editor no longer mislabels its options with a fixed colour
  name ("green ✓") — the labels now describe the treatment, so they stay honest
  when you change the brand colour.

## v1.1 — 2026-07-18

### Added
- **Download a sequence diagram as PNG** — a ⬇ PNG button under each live
  diagram rasterises it at 2× in the current theme. It's client-facing, so it
  runs the same leak check as the other exports before saving.

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
