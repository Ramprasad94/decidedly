# Decidedly

> **The meeting is the write-up.**

A single HTML file you open in a browser to **run a discovery session and walk out with the decisions captured** — nothing installed, nothing to host, no data leaving the room.

It's the artifact I reach for when I'm facilitating a requirements or discovery call and I don't want to be the bottleneck typing into a spreadsheet while ten people wait. You put the board on the screen, work the room, and click as decisions land. When you're done, you export what the room actually decided as JSON, Excel, or a frozen HTML snapshot.

<!-- Add a screenshot of your own board here once you've customised it:
     ![The board mid-session](docs/screenshot.png) -->

## Get it

**It's one self-contained file — `board.html` (~82 KB). No install, no dependencies, no other files to download.** The JSON model, the CSS, and all the JavaScript are inlined into that single file; there isn't a single network call in it.

- **Use it now, in your browser:** **[ramprasad94.github.io/decidedly/board.html](https://ramprasad94.github.io/decidedly/board.html)**. It runs instantly, and because nothing in the file phones home, nothing leaves your machine after it loads. *(Live once Pages is enabled: Settings → Pages → Deploy from branch → `main` / root.)*
- **Or download and run offline:** grab `board.html` from the [latest release](https://github.com/Ramprasad94/decidedly/releases/latest) — or **Code → Download ZIP**, or open the file and right-click *Raw* → *Save As* — then **double-click it**. It works with no internet at all, which is the point: it runs on a locked-down client laptop with no admin rights.

You only ever need `board.html`. Everything else here is documentation. Clone the repo only if you want to fork and modify the source:

```
git clone https://github.com/Ramprasad94/decidedly.git
```

## Why it exists

Most discovery sessions end one of two ways: a wall of raw notes nobody reads again, or a "we'll write it up later" that quietly never happens. This board makes the write-up *the session itself*. Every row is a question with a proposed answer; you and the room accept, amend, or park it live. The decision is captured the moment it's made, not reconstructed from memory three days later.

Three things make it worth carrying into a real client meeting:

- **It's one file.** No server, no build step, no CDN, no fonts pulled from the internet. Double-click, it opens. That matters when you're on a locked-down client laptop or a conference-room screen with no admin rights.
- **Nothing leaves the room.** State lives in the browser's `localStorage`. There's no network call anywhere in the file — you can verify that yourself, it's all right there in the source.
- **The exports are real.** Export Excel writes an actual `.xlsx` (hand-assembled, no library), so the workbook opens in Excel or Sheets like any other. Export JSON round-trips straight back into the board — it's your source of truth. Save HTML freezes the whole filled-in board as a shareable snapshot.

## Use it in five minutes

1. **Download `board.html`.** That's the whole thing.
2. **Open it in a browser.** You'll see a sample board for a fictional retail returns project ("OmniCart"). Click around — cycle a decision chip, park a row, expand a detail, hit Export Excel — to see how it behaves.
3. **Make it yours, two ways:** hit **Edit** in the toolbar to rewrite titles, headers, options and steps in place and add/remove rows and sections — then Export JSON to save it. Or, if you'd rather, open `board.html` in a text editor and edit the `MODEL` block near the top (plain JSON, clearly marked). Everything on screen is rendered from that one object; you never touch the code underneath either way.
4. **Run your session.** Put it on the screen and work the room. Decisions colour the rows; the meter (top-right) tracks how many are resolved.
5. **Export before you close the tab.** The "● unexported changes" badge is your reminder. Export JSON if you want to keep working on it later; Export Excel or Save HTML to hand something to the team.

## What's on the board

| Feature | What it does |
|---|---|
| **Decision chips** | Click to move a row through your pick-list (blank → Needs definition → Agreed → Confirmed). The chip colour flows to the whole row, so the room can see at a glance what's settled and what's still open. |
| **Custom pick-list** | In **Edit** mode, a small editor lets you rename, recolour (green / amber / neutral), reorder, add or delete the decision values. Renaming cascades everywhere — the tone map and every row already holding that value follow, so the meter stays honest. |
| **Light / dark toggle** | A **☀ / ☾** button in the toolbar. It seeds from your OS the first time, then remembers your pick. **Save HTML** freezes whatever theme is on screen into the snapshot, so a client sees exactly what you saw regardless of their machine. |
| **Brand colour** | The swatch in the toolbar recolours the whole board to a client's or your firm's colour. The soft tint and the text-on-colour are derived automatically, so any hue stays readable in both light and dark. Stored in the model — it exports and re-imports. |
| **Logos** | Two slots in **Edit** mode — your firm on the left, the client on the right — for a co-branded deliverable. Images are inlined (downscaled on a canvas, no upload anywhere), so they ride along in Save HTML and the JSON. |
| **Screens** | A `kind:"screens"` section is a captioned screenshot gallery. Add an image with the button or just paste one (Ctrl / ⌘ + V). Images inline into the file; captions export to Excel. |
| **Edit mode** | Hit **Edit** in the toolbar and the whole board becomes editable — section titles, column headers, the spotlight text, actors, all of it — with dashed buttons to add or remove rows, sections, options and steps. Customise the board in the browser, no JSON required. Export JSON to keep your version. |
| **Session metadata** | Optional date / facilitator / present-count under the title (editable in Edit mode). Provenance that makes an exported board read as a deliverable, not a scratchpad — it shows in every export. |
| **Print / PDF** | Ctrl+P gives a clean, branded PDF: the toolbar drops away, every section and detail expands, logos and brand colour stay, and the palette forces to light (whatever theme you're viewing) so it prints well. |
| **Copy summary** | One click copies the decisions and parked items as markdown, ready to paste into an email or Teams the moment the session ends. It runs the leak check first — it's client-facing. |
| **Filter** | Cycle the view between All / Unresolved / Parked to focus the room during wrap-up. View-only: every export still uses the full board. |
| **Leak check** | Keep internal notes off the client screen. Put your own internal words/phrases in the model's `leaks` list; the **Leak check** button scans every cell and shows what it found and where. The client-facing exports (Excel, HTML, Copy summary) run the same scan automatically and stop you the first time they hit something. Save HTML also **strips the `leaks` list itself** from the snapshot, so your denylist never ships to the client. And because leak check reads text, not pixels, any embedded logos or screenshots prompt a separate "check these images" confirmation before a client export. It flags — *you* decide what's confidential. |
| **Sequence diagram** | A `sequence` section draws a live lane diagram from a table of steps. Add or change a step (or an actor) and the picture above redraws. The steps export to Excel as a From / To / Message sheet. |
| **Progress meter** | Fraction of rows resolved, live in the header. A simple "are we done yet." |
| **Spotlight card** | The one decision the session hangs on, framed as options with what each *buys* and *costs*. Click to pick. |
| **Park button** | Anything you can't close goes to the Parking lot with one click — an owned follow-up, not a lost thread. |
| **Detail rows** | Long reasoning tucks behind a "▸ detail" toggle instead of bloating the cell. Still exported — the workbook keeps the *why*. |
| **Exit criteria** | Each section carries its "Leaving with" chips — the conditions for calling that topic done. On the board, not in someone's head. |
| **State + guard** | Everything persists to `localStorage`; a badge and a leave-the-page warning keep you from losing a session's work. |
| **Three exports** | JSON (re-imports here), Excel (real `.xlsx`, one sheet per section), HTML (a frozen snapshot of the current state). |

## Customising the model

Open `board.html` and find the `<script type="application/json" id="model">` block. It looks like this:

```json
{
  "meta": { "title": "...", "subtitle": "..." },
  "vocab": {
    "decision": ["", "Needs definition", "Agreed", "Confirmed"],
    "tone": { "Confirmed": "ok", "Agreed": "ok", "Needs definition": "warn" }
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

A few conventions worth knowing:

- **`cols`** defines a section's grid. `"edit": true` makes a cell inline-editable; `"pick": "decision"` turns it into a click-to-cycle chip driven by `vocab.decision`; `"detail": true` moves the column behind the expand toggle.
- **`fill`** names the column that drives a row's colour and counts toward the meter. Usually the decision column.
- **`vocab.tone`** maps each pick-list value to `ok` (green), `warn` (amber), or nothing (open). Change the palette by editing the `--accent` / `--warn` CSS variables near the top of the `<style>` block.

### Sequence sections (the live diagram)

A section with `"kind": "sequence"` renders a lane diagram that redraws whenever you edit its steps — no drawing tools, no image files. Add or change a step in the table and the picture above updates on the spot.

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

`from` and `to` are **positions in `actors`**, starting at 0. Set `"dashed": true` for a return/async arrow. In the running board you get a From/To dropdown and a "+ step" button for every step; rename or add actors in **Edit mode**. Steps export to Excel as their own From / To / Message sheet.

### The leak check

Discovery boards go on a shared screen, so your internal prep notes must not ride along. Put the words and phrases *you* consider internal into the `leaks` array:

```json
"leaks": ["internal", "don't reopen", "confidential", "our estimate", "TODO", "/\\bAB\\d+\\b/"]
```

Each entry is a case-insensitive substring; wrap it in `/ … /` to use a regex (the last example catches ticket IDs like `AB12`). The **Leak check** toolbar button scans every cell and lists what it found and where. **Export Excel** and **Save HTML** — the two things you hand to a client — run the same scan and block the first time they find a match, so nothing slips out by accident. (Export JSON doesn't gate: that's your own working copy.) The tool only flags; you decide what counts as a leak by what you put in the list. The sample ships with one deliberate internal note in a detail cell so you can watch the check catch it.

That's the whole API. Add sections, add rows, rename the pick-list to your own vocabulary — or just hit **Edit** and do it all in the browser. If you break the JSON, the board will tell you when it loads.

## A note on where this came from

I build these for a living — I'm a Salesforce architect and tech lead, and discovery is where projects are won or lost. This template is the distilled, client-free version of the boards I generate as part of a larger pipeline that turns a session transcript into the downstream delivery artifacts (Q&A trackers, decision logs, backlog, readouts). I built and refined the whole thing with [Claude Code](https://claude.com/claude-code). The board is the part I could share without any client data attached — so here it is.

If you use it, I'd genuinely like to hear how it went. Find me at [keepingupwiththecloud.com](https://keepingupwiththecloud.com/).

## License

MIT — free to use, fork, and modify. One thing to keep: the **Decidedly** name and the author credit in the page footer. MIT already asks that the attribution notice travels with copies, so leave that footer line in place; everything else is yours to change.

Created by Ramprasad Bommaganty — [keepingupwiththecloud.com](https://keepingupwiththecloud.com/).
