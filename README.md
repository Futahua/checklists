# Long horizon

**If you are an EXECUTOR picking this up — Claude, Codex, or Hermes — the previous EXECUTOR
session ran out of usage mid-task. This repository is how you continue without it.**

This repository documents a fixed workflow: ChatGPT in the attached browser is the AUTHOR.
The EXECUTOR is whichever supported disk/tool-side agent is active: Claude, Codex, or
Hermes. The creator is outside the active loop, reviews later, and alone gives final product
acceptance. The AUTHOR may judge whether the EXECUTOR's reported evidence satisfies its
stated technical acceptance conditions, but it never claims to have run those commands
itself. The EXECUTOR applies and executes; it does not redesign or decide final product
acceptance.

Nothing here assumes the previous session can be asked. Every checklist carries a **Status**
block at the top saying where the work stopped, what is committed, what is not, and the exact
next operation. Read that block first. It is the handoff.

## The one rule

**Replace the Status block in place. Never append to it.**

A running progress log grows without bound, and every EXECUTOR session that opens the file
pays for the whole history whether it needs it or not. Status is current state only. History
lives in git, where it costs nothing to ignore.

The checkboxes work the other way round: **a ticked box names the commit that closed it**,
and one line saying what that commit critically changed. That is what makes the work
reversible without reading the log — but it is a line, not a diary.

## Before touching anything

- [AGENTS.md](AGENTS.md) — the loop and the handful of things that go wrong. One page.
- [BROWSER.md](BROWSER.md) — the AUTHOR's brief. At the start of a session, hand the browser
  model a raw URL pinned to the exact intended SHA:
  `https://raw.githubusercontent.com/Futahua/long-horizon/<sha>/BROWSER.md`. Never use a
  moving branch URL for an AUTHOR packet.
- `reference/` — how the rules were worked out, and the failures behind each. Read for
  reasoning; never as instructions.

## What a checklist is

Stages, checkboxes, technical acceptance criteria, the evidence that closes each item, and
hard gates saying what must not start before something else finishes.

A ticked box means the AUTHOR judged the EXECUTOR's reported evidence sufficient for that
item's stated technical acceptance criteria and the commit that closed it is named on the
box. It does not mean the creator has given final product acceptance.

- **Hard gates** state what breaks if the order is violated, so skipping one is a decision
  rather than an oversight.
- **Open questions stay open**, written as questions, with where the answer belongs once it
  exists. Never resolved by assertion to make a document look complete.
- **No technical verification step may require the creator to click something and report
  back.** If a stage cannot be evidenced programmatically it is not technically closed —
  find the programmatic route, or record a missing capability. The creator's later final
  product acceptance is separate from technical verification.
