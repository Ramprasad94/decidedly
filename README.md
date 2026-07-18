# Decidedly

> **The meeting is the write-up.**

[![Use it now in your browser](https://img.shields.io/badge/Use%20it%20now-in%20your%20browser-2f6f4f?style=for-the-badge)](https://www.ramprasadbommaganty.com/decidedly/board.html)
&nbsp;
[![Download board.html](https://img.shields.io/badge/Download-board.html-24292f?style=for-the-badge&logo=html5&logoColor=white)](https://github.com/Ramprasad94/decidedly/releases/latest/download/board.html)

A single HTML file you open in a browser to run a discovery session and capture the decisions as they land. Put it on the screen, work the room, click as things get agreed. Export the result as JSON, Excel, a frozen HTML snapshot, or PDF.

I built it because facilitating a requirements call while also typing into a spreadsheet makes you the bottleneck. This keeps the write-up in the meeting itself: every row is a question with a proposed answer, and you accept, amend, or park it live.

<!-- Add a screenshot of your own board here once you've customised it:
     ![The board mid-session](docs/screenshot.png) -->

## Get it

It's one self-contained file, `board.html` (~86 KB). The model, CSS, and JavaScript are all inlined; there's no build step, no dependencies, and no network calls in it, so nothing leaves your machine after it loads. That's the point: it runs on a locked-down client laptop with no admin rights.

- **In your browser:** [www.ramprasadbommaganty.com/decidedly/board.html](https://www.ramprasadbommaganty.com/decidedly/board.html)
- **Offline:** download `board.html` from the [latest release](https://github.com/Ramprasad94/decidedly/releases/latest) and double-click it.

You only ever need `board.html`. Clone the repo only if you want to fork the source:

```
git clone https://github.com/Ramprasad94/decidedly.git
```

## Use it in five minutes

1. **Open `board.html` in a browser.** You'll see a sample board for a fictional retail returns project ("OmniCart"). Click around — cycle a decision chip, park a row, expand a detail, open the **Export** menu.
2. **Make it yours.** Hit **Edit** in the toolbar to rewrite titles, headers, options, and steps in place and add or remove rows and sections. Or edit the `MODEL` JSON block near the top of the file in a text editor — everything on screen renders from that one object.
3. **Run your session.** Decisions colour the rows; the meter (top-right) tracks how many are resolved.
4. **Export before you close the tab.** The "● unexported changes" badge is your reminder. JSON to keep working on it later; Excel, Save HTML, or PDF to hand to the team.

## What's on the board

| Feature | What it does |
|---|---|
| **Decision chips** | Click to cycle a row through your pick-list (blank → Needs definition → Agreed → Confirmed). Each state reads distinctly, so the room sees at a glance what's settled. |
| **Custom pick-list** | In Edit mode, rename, recolour, reorder, add, or delete the decision values. Renames cascade to every row already holding the old value. |
| **Spotlight card** | The one decision the session hangs on, framed as options with what each buys and costs. Click to pick. |
| **Park button** | Send anything you can't close to the Parking lot with one click. |
| **Filter** | Cycle the view between All / Unresolved / Parked to focus wrap-up. View-only; every export uses the full board. |
| **Progress meter** | Fraction of rows resolved, live in the header. When everything's resolved, a banner confirms the session's captured. |
| **Sequence diagram** | A `sequence` section draws a live lane diagram from a table of steps and redraws as you edit them. Exports to Excel as a From / To / Message sheet. |
| **Screens** | A `screens` section is a captioned screenshot gallery. Add an image or paste one (Ctrl / ⌘ + V); it inlines into the file. |
| **Detail rows** | Long reasoning tucks behind a "▸ detail" toggle instead of bloating the cell. Still exported. |
| **Exit criteria** | Each section carries its "Leaving with" chips — the conditions for calling that topic done. |
| **Branding** | A brand-colour swatch drives the accents; two logo slots (your firm, the client) inline into the file for a co-branded deliverable. |
| **Light / dark toggle** | Seeds from your OS, then remembers your pick. Save HTML freezes the current theme into the snapshot. |
| **Session metadata** | Optional date / facilitator / present-count under the title. Shows in every export. |
| **Leak check** | Put your internal words and phrases in the model's `leaks` list; the button scans every cell and shows what it found. Client-facing exports (Excel, HTML, PDF, Copy summary) run the same scan and block on a match. Save HTML strips the `leaks` list itself from the snapshot. See [The leak check](#the-leak-check). |
| **Exports** | JSON (re-imports here), Excel (real `.xlsx`, hand-assembled, one sheet per section), Save HTML (frozen snapshot), PDF, and Copy summary (decisions as markdown, ready to paste). |
| **State** | Persists to `localStorage`, with a leave-the-page warning so you don't lose a session. If storage fills, edits stay in memory and the badge warns you. |
| **Accessible** | Real `<h1>`/`<h2>` headings, `lang` set, ARIA labels on editable cells, AA-contrast text. |

## Customising the model

Open `board.html` and find the `<script type="application/json" id="model">` block:

```json
{
  "meta": { "title": "...", "subtitle": "..." },
  "vocab": {
    "decision": ["", "Needs definition", "Agreed", "Confirmed"],
    "tone": { "Confirmed": "done", "Agreed": "ok", "Needs definition": "warn" }
  },
  "sections": [
    {
      "id": "current", "title": "How returns work today", "tag": "current state",
      "fill": "decision",
      "cols": [
        { "f": "topic", "h": "Topic" },
        { "f": "heard", "h": "What we heard", "edit": true },
        { "f": "decision", "h": "Decision", "pick": "decision" },
        { "f": "detail", "h": "Detail", "edit": true, "detail": true }
      ],
      "rows": [
        { "topic": "Return window", "heard": "30 days...", "decision": "Confirmed" }
      ],
      "close": ["Exchange-vs-refund decision made"]
    }
  ]
}
```

- **`cols`** defines a section's grid. `"edit": true` makes a cell inline-editable; `"pick": "decision"` turns it into a click-to-cycle chip driven by `vocab.decision`; `"detail": true` moves the column behind the expand toggle.
- **`fill`** names the column that drives a row's colour and counts toward the meter — usually the decision column.
- **`vocab.tone`** maps each pick-list value to `done` (filled green ✓), `ok` (green outline), `warn` (amber), or nothing (open). Change the palette via the `--accent` / `--warn` CSS variables near the top of the `<style>` block.

### Sequence sections

A section with `"kind": "sequence"` renders a lane diagram that redraws whenever you edit its steps:

```json
{
  "id": "flow", "title": "The returns flow", "tag": "sequence", "kind": "sequence",
  "actors": ["Customer", "Returns portal", "Warehouse"],
  "steps": [
    { "from": 0, "to": 1, "msg": "Start a return" },
    { "from": 1, "to": 2, "msg": "Print label" },
    { "from": 2, "to": 1, "msg": "Item received", "dashed": true }
  ]
}
```

`from` and `to` are positions in `actors`, starting at 0. Set `"dashed": true` for a return/async arrow. In the running board you get a From/To dropdown and a "+ step" button; rename or add actors in Edit mode.

### The leak check

Discovery boards go on a shared screen, so your internal prep notes must not ride along. Put the words and phrases you consider internal into the `leaks` array:

```json
"leaks": ["internal", "don't reopen", "confidential", "our estimate", "TODO", "/\\bAB\\d+\\b/"]
```

Each entry is a case-insensitive substring; wrap it in `/ … /` for a regex (the last example catches ticket IDs like `AB12`). The **Leak check** button scans every cell and lists what it found. Client-facing exports run the same scan and block the first time they hit a match. (Export JSON doesn't gate — that's your working copy.) The sample ships with one deliberate internal note so you can watch the check catch it.

That's the whole API. If you break the JSON, the board tells you when it loads.

## A note on where this came from

I build these for a living — I'm a Salesforce architect and tech lead, and discovery is where projects are won or lost. This template is the client-free version of the boards I generate as part of a larger pipeline that turns a session transcript into downstream delivery artifacts (Q&A trackers, decision logs, backlog, readouts). I built and refined it with [Claude Code](https://claude.com/claude-code). The board is the part I could share without any client data attached — so here it is.

If you use it, I'd genuinely like to hear how it went. Find me at [keepingupwiththecloud.com](https://keepingupwiththecloud.com/).

## License

MIT — free to use, fork, and modify. One thing to keep: the **Decidedly** name and the author credit in the page footer. MIT already asks that the attribution notice travels with copies, so leave that footer line in place; everything else is yours.

Created by Ramprasad Bommaganty — [keepingupwiththecloud.com](https://keepingupwiththecloud.com/).
