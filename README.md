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

The checkboxes work the other way round: **a ticked box names the commit that closed it**,
and one line saying what that commit critically changed. That is what makes the work
reversible without reading the log — but it is a line, not a diary.

## Standing completion mandate

When the creator instructs the agent to finish LongHorizon, that instruction covers every
document in this repository titled **Complete Implementation Checklist**, including the
Proxima checklist and all checklists under `papers/`. Finish the active checklist in its
required dependency order, then immediately inventory and continue the next unfinished
checklist. Do not mistake supporting traces or reference documents for checklists, and do
not overlook a checklist merely because its filename does not contain `checklist`.

The creator's standing instruction to continue is authorization for ordinary reversible
implementation work throughout those checklists. An AUTHOR packet may bound a slice and
enforce hard-gate sequencing, but wording such as “not authorized” or “await explicit
authorization” does not create a new user-permission checkpoint when the creator has already
directed the run to complete everything. Stop only for a genuinely unresolved creator-owned
product decision, an irreversible/destructive operation, conflicting creator instructions,
or an external blocker with no safe in-scope route around it. If one path is blocked, continue
any other dependency-safe checklist work instead of ending the run.

## Before touching anything

- [AGENTS.md](AGENTS.md) — the loop and the handful of things that go wrong. One page.
- [BROWSER.md](BROWSER.md) — the AUTHOR's brief. Hand the browser model this URL at the start
  of a session: `https://raw.githubusercontent.com/Futahua/long-horizon/main/BROWSER.md`
- `reference/` — how the rules were worked out, and the failures behind each. Read for
  reasoning; never as instructions.

## What a checklist is

Stages, checkboxes, acceptance criteria, the evidence that closes each item, and hard gates
saying what must not start before something else finishes.

A ticked box means the acceptance criteria were met, the evidence exists, and the commit
that closed it is named on the box — never that the work looked finished.

- **Hard gates** state what breaks if the order is violated, so skipping one is a decision
  rather than an oversight.
- **Open questions stay open**, written as questions, with where the answer belongs once it
  exists. Never resolved by assertion to make a document look complete.
- **No step may require a human to click something and report back.** If a stage cannot be
  verified programmatically it is not done — find the programmatic route, or record a missing
  capability.
