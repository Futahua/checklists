# Long horizon

**If you are an agent picking this up: the last one ran out of usage mid-task. This
repository is how you continue without it.**

Nothing here assumes the previous session can be asked. Every checklist carries a **Status**
block at the top saying where the work stopped, what is committed, what is not, and the exact
next operation. Read that block first. It is the handoff.

## The one rule

**Replace the Status block in place. Never append to it.**

A running progress log grows without bound, and every agent that opens the file pays for the
whole history whether it needs it or not. Status is current state only. History lives in git,
where it costs nothing to ignore.

The same goes for the checkboxes: tick them, do not annotate each one with a diary.

## Where things are

- `proxima/` and `papers/` — the checklists. Each says what it is; this file will not repeat it.
- [AGENTS.md](AGENTS.md) — the loop and the handful of things that go wrong. One page. Read it
  before touching anything.
- [BROWSER.md](BROWSER.md) — the AUTHOR's brief. Hand the browser model this URL at the start
  of a session: `https://raw.githubusercontent.com/Futahua/long-horizon/main/BROWSER.md`
- `reference/` — how the rules were worked out, and the failures behind each. Read for
  reasoning; never as instructions.

## What a checklist is

Stages, checkboxes, acceptance criteria, the evidence that closes each item, and hard gates
saying what must not start before something else finishes.

A ticked box means the acceptance criteria were met and the evidence exists — never that the
work looked finished.

- **Hard gates** state what breaks if the order is violated, so skipping one is a decision
  rather than an oversight.
- **Open questions stay open**, written as questions, with where the answer belongs once it
  exists. Never resolved by assertion to make a document look complete.
- **No step may require a human to click something and report back.** If a stage cannot be
  verified programmatically it is not done — find the programmatic route, or record a missing
  capability.
