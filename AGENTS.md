# The loop

**AUTHOR** — the browser. Writes the change. No hands, cannot run anything.
**EXECUTOR** — whoever writes to disk. Applies it and runs it. Does not redesign.
**The creator** — reviews afterwards, on their own time. Not in the loop.

```
AUTHOR writes → EXECUTOR applies and runs → it worked?
                                             yes → AUTHOR checks the evidence,
                                                   EXECUTOR commits and pushes
                                             no  → back to AUTHOR
```

**Run for hours. Do not wait for the creator.** When a slice closes, start the next one.
Push so they can review when they choose; never block on them being there.

That is the workflow. The rest of this page is the handful of things that go wrong.

## Five rules

1. **The EXECUTOR never accepts its own work.** The AUTHOR judges the evidence against
   the acceptance conditions it set. That separation is what survives the creator being
   away — it is not a formality to skip when nobody is watching.
2. The AUTHOR decides what the code means. The EXECUTOR never does.
3. The EXECUTOR may fix *how* something was delivered — a mangled patch, a short SHA, a
   wrong path — when it can show the result is identical. Never *what* it does.
4. Say every fix you made. Working is not a reason to leave it out.
5. The AUTHOR never says something passed. It cannot run anything.

## What the AUTHOR sends

Repo, the SHA it read, and the files it read. Then, per change: the path, the **exact
existing text**, and the **exact replacement**. Full contents only for a new file. Then the
commands to run, and what counts as passing.

Guarded replacements, not diffs — hunk metadata does not survive the browser.

## What comes back

Baseline SHA, whether it applied, the commands **exactly as authored** with their exit
codes, changed files, and the first real failure — not the cascade. Full logs stay on disk.

Any fix the executor made, and whether it can *prove* the result was identical or only
believes it. Both are allowed; pretending is not.

## Attaching to the reviewer tab

Claim the exact tab, then drive it by role — never by screen coordinates, never by taking
over the mouse.

1. Ask the connector for browser instances and open tabs.
2. Tell the Chrome instances apart by browser ID or profile name.
3. Find the reviewer by its exact title and URL.
4. Claim that tab by the returned tab ID.
5. Drive it through the accessibility tree.

```js
const state = await cua.getState();
const reviewerTab = await cua.getTab("returned-tab-id", { browser: "returned-browser-id" });
const snapshot = await reviewerTab.getAXState();

reviewerTab.playwright.getByRole("textbox", { name: "Chat with ChatGPT" });
reviewerTab.playwright.getByRole("button", { name: "Send prompt" });
```

Once the reviewer tab is selected, touch nothing else — not the other Chrome instance, not
other tabs. Role locators also avoid a real hazard of synthetic coordinate clicks: they can
fire page handlers you did not intend, including a copy handler that overwrites the
creator's clipboard.

## Watching the reviewer tab

One bounded watcher against the same attached tab. Not screenshots, not refreshes, not
mouse control, not batches of sleeps.

```js
let sawGenerating = false;

while (Date.now() - startedAt < timeoutMs) {
  const generating =
    (await tab.playwright
      .getByRole("button", { name: "Stop answering" })
      .count()) > 0;

  sawGenerating ||= generating;

  if (sawGenerating && !generating) {
    return "finished";
  }

  await wait(1000);
}
```

**Both edges are required.** Seeing the button gone proves nothing on its own — it is also
what the page looks like before generation starts. Latch that it appeared, then wait for it
to go. Checking only for absence is how a half-written answer, or no answer at all, gets
read as finished.

Then read the completed response **once**, apply it, run the tests, and send the next
evidence update.

If a watcher is interrupted or times out, reclaim the tab and check. Never assume it
finished while you were away.

## Pushing

Push at accepted slice boundaries so there is something reviewable. That is allowed and
expected; abusing it is not. Not per edit, not a stream of one-line commits, not work that
does not pass its own acceptance conditions.

Feature branches only. **These still wait for the creator, however long that takes:**
merging to main, force-push, rewriting history, deleting branches, anything touching their
vault or real data, and anything else that cannot be undone by checking out the previous
commit.

Keep big files out of context — read the part you need.

## Keeping the checklist handoff-able

This repository exists because sessions run out of usage mid-task. Whoever picks the work up
next has only what is written down.

Every checklist carries a **Status** block at the top: accepted branch and SHA, unaccepted
work and where it is parked, current suite totals, what is done, what is in flight, and the
exact next operation. Update it whenever any of those change.

**Replace that block in place. Never append to it.** A running progress log grows without
bound and costs every future agent the whole history whether or not it needs it. Status is
current state only; history lives in git, where it costs nothing to ignore.

## Ticking a box

**Every ticked box names the commit that closed it.** One line, appended to the box:

```
- [x] Unknown action type returns a typed refusal. — `4554fea` the guard now refuses a
      result whose category contradicts the registry, so an unregistered type cannot be
      answered as if it had been handled.
```

The SHA is what makes the work reversible. Without it, undoing one decision means reading
the whole log to find out which commit made it; with it, `git show` and `git revert` are one
command away, and a later agent can tell what a box actually bought.

Write the **critical** change — what a reverting agent needs to know, and anything that
would surprise them. Not how you got there, not what you tried first. A box that closed
alongside its sub-items is annotated on the parent only; annotating every child is the diary
this rule is not.

If two commits closed one box, name both. If a commit is later reverted, untick its boxes
and say so in Status — a tick whose commit is gone is worse than no tick.

Never leave work uncommitted at the end of a run. If a slice is not accepted yet, park it on
a clearly named side branch with a message saying what fails and why, and keep the accepted
branch clean. Losing an hour of applied work to an exhausted session is avoidable.

## What ends the run

**A turn ends when you stop making tool calls and speak.** Nothing external restarts you.
The creator's next message is the only thing that begins another turn.

So the loop is not something you set up — it is something you simply do not stop. Chain
tool calls: watch, apply, verify, watch again. The in-page watcher keeps you alive only for
the duration of one tool call; what keeps you working is issuing the next one. Hours of work
fit inside a single turn.

**Reporting is what kills the run.** A status update hands the turn back and everything
stops until the creator returns, which may be many hours. So report at real milestones — a
slice accepted and pushed, a decision only they can make, a blocker with no route around it
— and not at every step. If you find yourself writing a progress summary, ask whether the
next tool call would serve them better.

Work that must survive *across* turns needs a scheduled wakeup, not a browser script. Say so
plainly rather than promising an autonomy the setup does not have.

## Pace

Both agents have finite capacity — Claude's five-hour window, Codex's own limits — and
running out mid-project is the failure that matters, not the cost. Watch your own burn; the
creator should never have to.

```bash
python "D:/Letters/MatTroiSeConMoc/Tools/claude-usage.py" --brief
```

Then measure it against the work remaining, not against the clock. A checklist with
hundreds of boxes and a rate of two or three per session will not finish, and the answer is
**bigger slices, not more hours**. If the pace does not reach the end, the slice size is
wrong.

So bias aggressive. Take the largest slice that still ends somewhere judgeable. Bundle
independent changes into one packet. Ask the AUTHOR for more per exchange, not less. Round
trips are the expensive thing — a slice that takes an hour to author and applies cleanly
beats six that each cost an exchange.

Slow down only where a mistake is expensive: anything irreversible, anything touching real
data, anything where being wrong is discovered late. Everywhere else, speed is the safer
choice, because the loop's failure mode is running out of capacity with the checklist
barely touched.

## When something blocks

Do not stop and wait. Try the other way round: reclaim the tab, restart the browser
session, re-read the file, re-ask the AUTHOR with the failure attached. Work the problem
with whatever the browser allows.

Stop only for a decision that is genuinely the creator's — an irreversible action, a
conflict between two things they asked for, or a question the source cannot answer. Leave
it stated plainly and move to work that is not blocked by it.

## Elsewhere

[BROWSER.md](BROWSER.md) is the AUTHOR's brief; hand it that URL at session start.
[reference/](reference/) is how all this was worked out, including every failure behind a
rule. Read it if you want the reasoning. It is not law.

A script gets written only after the same failure has cost a round trip twice. So far:
none, correctly.
