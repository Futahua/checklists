# Checklists

Planned work, tracked remotely. One document per feature, each written as an executable
checklist rather than a description: stages, checkboxes, acceptance criteria, the
evidence that closes each item, and hard gates saying what must not start before
something else finishes.

These are plans, not records of work done. A ticked box means the acceptance criteria
were actually met and the evidence exists — never that the work looked finished.

The repository is public on purpose. The review workflow fetches these documents over
`raw.githubusercontent.com`, which does not work against a private repository.

## Papers

The Electron host.

| Document | What it covers |
| --- | --- |
| [Adopted window surfaces](papers/adopted-window-surfaces.md) | Other applications' windows becoming one with Papers' own — tabs, views and grouping. |
| [Quick Run](papers/quick-run.md) | Hotkey into search mode, type, matching backpack items by relevance, Enter to take the first. |
| [Window-layout consistency and auto-tracking](papers/window-layout-consistency-and-auto-tracking.md) | Multi-tab applications breaking layout identity, removing invalidated processes, surviving reboot, and a widget that tracks created windows automatically. |

## Proxima

The "As you Go" sibling backpack — an Elastic board, calendar and projects over the
creator's own files. Source: [Futahua/proxima-backpack](https://github.com/Futahua/proxima-backpack).

| Document | What it covers |
| --- | --- |
| [Interaction parity trace](proxima/proxima-interaction-parity-trace.md) | Every click, drag, resize, modifier and hover in the original Obsidian plugin, tagged presentation / local state / data write. Defines what "feels like Proxima" means. |
| [Full parity checklist](proxima/proxima-full-parity-checklist.md) | The sequenced plan from that trace to a working cockpit: 21 stages, 5 hard gates, 805 checkboxes. |

## The loop

- [AGENTS.md](AGENTS.md) — the constitution. Eight rules, the gate states, and what is
  machinery rather than memory. This is the whole of the mandatory brief.
- [BROWSER.md](BROWSER.md) — the AUTHOR's brief, handed to the browser at session start.
- [SCHEMAS.md](SCHEMAS.md) — required fields for every artifact in the loop.
- [reference/](reference/) — how the rules were arrived at, and the failures that produced
  each one. Read for reasoning; never as instructions.

## Conventions

- **Hard gates** are ordering constraints with a stated consequence. They record what
  breaks if the order is violated, so skipping one is a decision rather than an oversight.
- **Open questions stay open.** A question the source cannot answer is written down as a
  question, with where its answer belongs once it exists. It is never resolved by
  assertion to make a document look finished.
- **No step may require a human to click something and report back.** If a stage cannot
  be verified programmatically, it is not done — find the programmatic route or record
  it as a missing capability.
- Documents are superseded by later entries rather than rewritten, so the reasoning
  behind a decision survives the decision changing.
