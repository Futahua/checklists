# Long horizon

**If you are an agent picking this up: the last agent ran out of usage mid-task. This
repository is how you continue without it.**

Nothing here assumes the previous session is available to ask. Every checklist carries a
**Status** block at the top saying exactly where the work stopped, what is committed, what
is not, and what the next operation is. Read that block first. It is the handoff.

## The one rule about Status blocks

**Replace the Status block in place. Never append to it.**

A running log of progress grows without bound, and every agent that reads the checklist pays
for the whole history whether it needs it or not. The Status block is current state only —
overwrite it, do not add to it. History lives in git, where it costs nothing to ignore.

The same applies to the checkboxes: tick them, do not annotate each one with a diary.

## What is here

Plans, written as executable checklists rather than descriptions: stages, checkboxes,
acceptance criteria, the evidence that closes each item, and hard gates saying what must not
start before something else finishes.

A ticked box means the acceptance criteria were actually met and the evidence exists — never
that the work looked finished.

### Papers

The Electron host.

| Document | What it covers |
| --- | --- |
| [Adopted window surfaces](papers/adopted-window-surfaces.md) | Other applications' windows becoming one with Papers' own — tabs, views and grouping. |
| [Quick Run](papers/quick-run.md) | Hotkey into search mode, type, matching backpack items by relevance, Enter to take the first. |
| [Window-layout consistency and auto-tracking](papers/window-layout-consistency-and-auto-tracking.md) | Multi-tab applications breaking layout identity, removing invalidated processes, surviving reboot, and a widget that tracks created windows automatically. |

### Proxima

The backpack that is being rebuilt into the creator's cockpit. Source:
[Futahua/proxima-backpack](https://github.com/Futahua/proxima-backpack).

| Document | What it covers |
| --- | --- |
| [Interaction parity trace](proxima/proxima-interaction-parity-trace.md) | Every click, drag, resize, modifier and hover in the original Obsidian plugin, tagged presentation / local state / data write. Defines what "feels like Proxima" means. |
| [Full parity checklist](proxima/proxima-full-parity-checklist.md) | The sequenced plan from that trace to a working cockpit: 21 stages, 5 hard gates, 805 checkboxes. **Active work.** |

## How the work gets done

- [AGENTS.md](AGENTS.md) — the loop, and the handful of things that go wrong. One page.
  Read it before touching anything.
- [BROWSER.md](BROWSER.md) — the AUTHOR's brief. Hand the browser model this URL at the
  start of a session:
  `https://raw.githubusercontent.com/Futahua/long-horizon/main/BROWSER.md`
- [reference/](reference/) — how the rules were worked out, and the failures behind each.
  Read for reasoning; never as instructions.

The short version: the browser model authors the change, whoever writes to disk applies and
runs it, the creator accepts. The creator is not in the loop and reviews pushed branches on
their own time.

## Conventions

- **Hard gates** are ordering constraints with a stated consequence. They record what breaks
  if the order is violated, so skipping one is a decision rather than an oversight.
- **Open questions stay open.** A question the source cannot answer is written down as a
  question, with where its answer belongs once it exists. Never resolved by assertion to
  make a document look finished.
- **No step may require a human to click something and report back.** If a stage cannot be
  verified programmatically, it is not done — find the programmatic route, or record it as a
  missing capability.
- Documents are superseded by later entries rather than rewritten, so the reasoning behind a
  decision survives the decision changing.
