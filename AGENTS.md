# How these documents get made

This repository holds plans, not code. Every document here was produced by the same
workflow, and this file exists so that workflow can be repeated without rediscovering
its failure modes.

Read this before adding or updating a checklist.

---

## Why there is a second reviewer at all

The creator's compute is limited and long-horizon planning burns it fast. So the deep
reading — a whole unfamiliar repository, a plugin's entire interaction surface, a
decade of gate history — is delegated to a browser-driven reviewer in an inline ChatGPT
session, and the agent driving the terminal spends its own tokens on verification,
judgement and writing files.

The division that works:

- **The reviewer reads.** Whole repositories, long histories, exhaustive traces.
- **The driving agent verifies.** Every load-bearing claim gets checked against the
  local tree before it is written down or acted on.
- **The driving agent decides.** Reviewer rankings are input, not a ballot handed to
  the creator. Do not relay a menu of options; pick, say why, and proceed.

The reviewer is audit-only. It never touches the working tree.

---

## Feeding the reviewer

**Give it pushed SHAs and public URLs. Never paste code.**

Pasting source into the chat wastes the exact budget the reviewer exists to protect,
and it silently drifts from what is actually committed. Push first, then hand over the
SHA.

**Its sandbox has no git network.** `git clone` and `git ls-remote` fail on DNS
resolution and it will stall trying. Give it the raw-file pattern explicitly:

```
https://raw.githubusercontent.com/<owner>/<repo>/<sha>/<path>
```

**This is why this repository is public.** A private repository cannot be read that
way, and the workflow stops working. Nothing secret goes in here.

**Pin a SHA, not a branch.** A branch moves under the reviewer mid-read and its line
references stop matching. When the tree moves during a conversation, tell it the new
SHA and what changed in one paragraph.

**Give it a reading order.** An unfamiliar repository with 250 files will otherwise be
explored at random. Name the ten or fifteen files that carry the architecture, and say
which directories are noise — one repository here carried a hundred one-off `patch-*.js`
scripts that were development detritus, and saying so up front saved a great deal of
wasted reading.

**Tell it what not to do.** "Orientation only, no design." "Trace only, no checklist."
"Checklist only, no implementation." Without that it will helpfully skip ahead, and the
work will be built on an understanding nobody has checked yet.

---

## Verifying what comes back

**The reviewer is often right and sometimes confidently wrong. Check before acting.**

Two examples from this repository's own history, both cheap to check and both material:

- It reported a widget was unguarded. It wasn't — the guard sat one line past where the
  reading stopped. Verified locally, correction accepted, no code changed on a false
  premise.
- It said `AGENTS.md` in another repository was stale about `VaultWriter`. It was, and
  a single `sed -n` confirmed it before the file was rewritten.

The rule: any claim that changes code, ordering, or a decision gets verified against
the local tree first. Quote the file and line when reporting back, so the next reader
can check the check.

**Corrections from the creator override the reviewer.** When the reviewer proposed a
saved-versus-session layout split, the creator's "layouts aren't even named" retired
the entire proposal — and the reviewer, once told, verified the point in code itself.
Pass creator corrections through verbatim and early.

---

## Document conventions

Every checklist here follows these. They are not stylistic.

**Hard gates state their consequence.** A gate is an ordering constraint plus what
breaks if it is violated. "Do A before B" is a preference; "do A before B because B
silently deletes Chrome windows from layouts otherwise" is a gate. Write the second.

**Open questions stay open.** A question the source cannot answer is recorded as a
question, with the exact wording of what must be decided and which document the answer
belongs in once it exists. It is never resolved by assertion to make a document look
finished. Each checklist here ends with a list of these.

**No step may require a human to click something and report back.** If a stage cannot
be verified programmatically, it is not done — find the programmatic route, or record
it as a missing capability with the trigger that would justify building it. This
applies to the acceptance criteria inside the documents and to the workflow that
produces them.

**Supersede, do not rewrite.** A ledger records what was decided when. When a later
gate overtakes an earlier row, add a superseding pointer beneath it; do not edit the
history or flip its boxes. Present-tense orientation documents — READMEs, agent guides
— are the opposite: those should simply be correct.

**Tag interactions by what they cost.** Where a document describes UI, every
interaction is tagged presentation / local state / data write. That tagging is what
makes a plan sequenceable: the presentation half usually ships long before the storage
question is settled.

---

## Driving the browser reviewer

This is the part that was got wrong first and corrected, so it is written out in full.

### The rule that matters

**Absence of a running indicator is never evidence of completion.**

Completion needs positive terminal evidence. A missing stop button is a UI affordance
changing, not a generation finishing. Never write:

```js
const done = !stopButton && lastAssistantLength > 100;   // wrong, both halves
```

Classify each turn into an explicit state instead: `RUNNING`, `DONE`, `CLIENT_STALE`,
`ERROR_RETRYABLE`, `BLOCKED_EXPERIMENT`, `QUIET_UNKNOWN`, `HARD_STALL`.

### Signal priority

1. **Generation transport.** The terminal event on the streaming response is the real
   completion signal. Read network traffic rather than re-executing JavaScript in the
   page on a timer.
2. **Server conversation state.** When the client goes stale but the server keeps
   generating, the stored conversation is the recovery authority.
3. **DOM.** Blocker and error detection, and last-resort extraction. Not the source of
   truth.

Everything under `/backend-api/` is private web-client machinery, not a supported API,
and it has already changed during 2026. Discover what the loaded client is actually
using; do not hard-code a URL. When discovery stops matching, fail loudly with a
"transport changed" error rather than quietly falling back to the stop button.

### Cadence

Do not sleep in fixed blocks and probe between them. Install a page-resident
`MutationObserver` once, writing a heartbeat to a `window` object, and wait on it:

```js
window.__monitor = { rev: 0, lastMutationAt: performance.now(), assistantCount: 0,
                     lastAssistantChars: 0, bodyTail: '' };
const update = () => {
  const a = [...document.querySelectorAll('[data-message-author-role="assistant"]')];
  Object.assign(window.__monitor, {
    rev: window.__monitor.rev + 1,
    lastMutationAt: performance.now(),
    assistantCount: a.length,
    lastAssistantChars: a.at(-1)?.innerText.length ?? 0,
    bodyTail: document.body.innerText.slice(-500),
  });
};
new MutationObserver(update).observe(document.body,
  { subtree: true, childList: true, characterData: true, attributes: true });
update();
```

Then one long wait with a watchdog: at 90–120 seconds of no network and no DOM
mutation, make a single server-state probe. Server advanced → `CLIENT_STALE`. Server
terminal → `DONE`. Server unchanged → keep waiting, because a reasoning model is
legitimately silent for minutes. A three-second answer and a seven-minute answer then
cost the same one wait.

Do not stop a generation merely because output has been quiet.

### Extraction

**Prefer the raw text over reconstructed markdown.** A DOM→markdown walker runs after
markdown has been parsed into HTML: fence choice, list indentation, whitespace and
literal punctuation are already gone. Every document in this repository needed manual
repair of code fences and nested lists because of this. Take the assistant text from
the transport stream or the stored conversation message; keep the walker as fallback.

**The conversation is a tree, not a list.** Never take `assistantMessages.at(-1)`.
Walk from the user message that was actually submitted to its selected descendant on
the active branch. With A/B experiments and message versions live, an abandoned
candidate branch can otherwise become "the answer".

**Classify errors before accepting content.** A delivery-timeout turn renders as a
short assistant message with a Retry control; a minimum-length check accepts it as a
real answer. Explicit error banner or error-associated Retry control means never
answer content, regardless of length.

### Observed failure modes

All of these happened while producing the documents in this repository. Selectors and
strings are what was observed, not stable product contracts.

| Symptom | What was actually happening | Handling |
| --- | --- | --- |
| Stop button gone, zero assistant turns, length 0 | Still generating; only the thinking-trace text at the end of `document.body` was changing | Never treat as done; watch trailing body text |
| Minutes of silence on "Searching …", no stop button | Client stream stale, server generating normally the whole time | Server-state probe; reload is recovery, not discovery |
| Two candidate answers, ~800 chars each, both stop permanently | A/B experiment: "You're giving feedback on a new version of ChatGPT" | First-class `BLOCKED_EXPERIMENT`; clicking "I prefer this response" resumes generation |
| 52-character assistant turn | "Message delivery timed out. Please try again." with Retry | `ERROR_RETRYABLE`; click Retry |
| Long answer stops mid-flow | Genuine hang | Stop, then instruct: continue, do not re-read, do not restart |

When a hang is interrupted, tell the reviewer explicitly not to re-read files it has
already read and not to restate its plan — otherwise it spends the whole retry
re-deriving context.

---

## Working style

**Do not present option menus.** The creator does not want to pick between rankings.
Decide, state the choice and the reason, and proceed. If they disagree they will say so,
and that is cheaper than a decision they never asked to make.

**Keep polling; do not pause to write up.** Stopping a running script to report
progress wastes the wait already paid for.

**Be blunt about outcomes.** If something is slower, say slower. If a fix is unverified
by the creator, say unverified. If a step was skipped, say so.

**Back up uncommitted work before touching a tree.** A `git reset --hard` in this
workspace once destroyed about thirty lines of someone else's unstaged work that had
been flagged as at-risk one message earlier; unstaged means unrecoverable, and
`git fsck` finds nothing. Take a `git diff` to a scratch file first, every time.

**Push the feature branch each turn**, so the reviewer always has a SHA to read.
