# How these documents get made

This repository holds plans, not code. Every document here was produced by the same
workflow, and this file exists so that workflow can be repeated without rediscovering
its failure modes.

Read this before adding or updating a checklist.

The companion document is [`BROWSER.md`](BROWSER.md) — the same workflow written for the
AUTHOR, which reads it in a browser session and cannot read this one. Hand it that URL at
the start of a session instead of re-explaining the rules in chat:

```
https://raw.githubusercontent.com/Futahua/checklists/main/BROWSER.md
```

---

## Why there is a second model at all

> Throughout the browser-facing sections below, "the reviewer" is the **AUTHOR** role
> defined under *Authorship, execution, and acceptance* at the end of this file. The
> older name is kept where it describes how the browser session is driven; the role
> definition governs who owns what.

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

---

## Context economy and pacing

The creator owns the project; the agent owns pacing. Never ask them to shorten useful
prompts, manage context by hand, or ration ordinary discussion of their own work. The
objective is not minimum token cost — it is not exhausting their access partway through
something useful.

### The accounting, correctly

Four quantities, and conflating them produces the wrong fix:

- **cache read** — an existing prompt prefix reused. The cheap path.
- **cache creation / write** — prompt material newly written or *re*written to cache.
- **uncached input** — input processed with no cache hit.
- **output** — generated text.

A large live conversation raises the **cache-read** floor. It does not, on its own, mean
the whole conversation is cache-*written* every turn: with a healthy prefix hit, only the
newly added suffix is created. So a very large cache-creation number on a turn that added
almost nothing is **a cache miss or invalidation event**, not the ordinary price of a long
session. Measured here: turns of ~481k cache-creation returning ~200 tokens of reply.

Do not optimise output length while hundreds of thousands of tokens of unnecessary live
context accumulate. Output is secondary — but not free, because every long answer becomes
future input.

**Flag `CACHE_MISS_LARGE`** when a turn introduced under ~10k tokens of genuinely new
material yet reports over 100k of cache creation. The 100k figure is an operational alarm
derived from this workflow's observed 100k–481k events, not a provider guarantee. Two of
them inside one short work phase means stop carrying the session into the next phase.

Do not derive a quota formula from these counters. How a five-hour access ceiling weights
cache creation, uncached input, cache reads, output, request count and model class is not
published. Measure consumption; do not invent the rule behind the limit.

### Keep large material out of context in the first place

**Never stream a large artifact through the model merely to save it.** Write the bytes to
disk with the tool that produced them, then return only a path, a byte or line count, a
status, a hash where provenance matters, and a short summary.

```bash
command > /tmp/out.log 2>&1; status=$?
printf 'exit=%s lines=%s bytes=%s\n' "$status" "$(wc -l < /tmp/out.log)" "$(wc -c < /tmp/out.log)"
tail -n 120 /tmp/out.log
```

in preference to piping through `tee`, which feeds everything back through context. Same
for fetches: download to a file, then search the ranges that matter.

**Saving a document to disk after it has already entered the conversation does not evict
it.** Later turns may cache-read it cheaply, but it still occupies context and enlarges
the next cache miss. Only deliberate compaction or a fresh session removes it. Do not
pretend otherwise — this workflow made exactly that mistake, writing 60k-character
reviewer answers to disk *after* pulling them through context in slices.

Treat a single tool result or inserted artifact above **10k tokens** as large, and before
admitting it ask: will most of this be needed verbatim over the next several turns? If
not, it belongs on disk with a compact representation returned instead.

Read files narrowly by default — a grep with line numbers, a bounded `sed` range, `head`,
`tail`. For an audit: inspect the tree, locate definitions, read bounded ranges, widen
only when cross-file context forces it. Never concatenate a repository into a prompt just
because the window can hold it.

### Keep the cached prefix stable

Tool definitions sit *before* system and message content in the cached prefix, so changing
the tool set can invalidate a large amount downstream. Do not add or remove tools inside a
big live session for convenience; do it at a phase boundary. Put stable instructions early
and volatile per-turn material late. When cache behaviour changes right after a
configuration change, suspect the change before blaming conversation growth.

### Poll outside the model

Two different things wear the same name:

- **Orchestrator polling** — waiting in the browser or network layer without asking the
  model for another turn. No context cost. Prefer it always.
- **Agent polling** — the model calls a tool, gets a small result, reasons, calls again.
  Not free because the result is small: each iteration is another continuation over the
  entire live prefix, and another chance to miss cache.

So never run 10–16 model-driven sleep/probe turns where one in-page wait would do. Install
the observer or listener once and return to the model only on completion, explicit error,
a known blocker, a meaningful state change, or a watchdog timeout needing judgement.

Batch independent shell and file queries into one invocation rather than alternating
model → tool → model → tool, provided the batch's own output stays bounded.

### Continue, compact, or start fresh

Do not start fresh merely because a conversation is long — a hot large cache can be
cheaper and more coherent than rebuilding context.

**Continue** when the phase is still running, recent detail is genuinely needed, cache
hits look healthy, no long idle gap is imminent, and only one or two substantive turns
remain. Never pay a handoff cost just before finishing.

**Compact** at a coherent boundary when much of the old material is no longer needed
verbatim, continuity still matters, and several turns remain. A useful trigger: live
context above ~100k tokens, more than five iterations expected, and at least half the
accumulated context is history rather than working state. Afterwards, verify from actual
telemetry that cache activity dropped — do not assume the command worked because it
returned success.

**Start fresh** when a phase has ended, durable truth is already on disk, the next phase
can be re-established in a handoff of 10k tokens or less, the old conversation holds large
reports the next phase does not need verbatim, and at least three substantive iterations
are expected. Strongly prefer it once live context exceeds ~250k tokens and a small
handoff suffices — chosen to keep any single cold recreation well below the ~481k worst
turns measured here.

**Do not restart when reconstruction is worse.** A "fresh" session carrying a 100k-token
reconstructed handoff is not fresh. Carry context only when its information value exceeds
the cost of carrying it.

A handoff contains durable working state only: goal, repo and SHA and branch, governing
decisions and invariants, work completed, where the detailed evidence lives, current
findings, unresolved questions, and the exact next operation. Never paste old transcripts
into it; point at the reports on disk.

### The one-hour cache TTL

TTL runs from the **start of the request** that used or refreshed the cache, and use
refreshes it — so a long generation eats part of the hour before anyone is idle. Expiry is
a minimum-lifetime policy, not a promise of deletion at exactly sixty minutes.

For a session above ~100k live tokens, an expected idle gap of **45 minutes or more** is
the trigger to write the handoff before the gap — deliberately under the hour because
generation time counts inside it. Returning after the window to a large old session,
assume the prefix may need recreation: resume from the handoff rather than waking the
whole conversation with a trivial message. Do not send artificial keepalive turns to
refresh a cache.

### What to tell the creator

Do not narrate token counts, cache statistics or context housekeeping. Compaction, bounded
reads, output redirection, batching and handoffs are handled silently.

Speak up only when context economy **changes the work**: a fresh session is being used and
the discontinuity would otherwise be surprising; a large cache miss means continuing this
way risks their access; required evidence exists only in context and cannot be compacted
without losing it; a limit has actually been imposed or is imminent; or scope must be cut
because the remaining access cannot safely finish the phase.

Say the concrete thing, not "we are using a lot of tokens":

> A trivial turn just recreated over 100k tokens of cache, so the large prefix is no
> longer hitting reliably. I am not going to spend more tool turns against it — the next
> phase resumes from the saved handoff.

Never make the creator solve pacing by withholding useful project context.

### Priority order

1. Keep unnecessary large artifacts out of context entirely.
2. Drop obsolete context at natural phase boundaries.
3. Preserve cache-prefix stability.
4. Avoid model-driven polling and needless tool round-trips.
5. Batch bounded tool work.
6. Avoid repeating material that is already persisted.
7. Only then, answer length.

**Do not spend expensive live context on information that already has a durable home.**

---

## Authorship, execution, and acceptance

"Reviewer" was the wrong name and it cost real money. A reviewer produces advice; advice
has to be re-derived into intent by whoever holds the keyboard; and re-deriving intent is
exactly the expensive thinking the arrangement exists to move off the metered agent. The
name quietly handed authorship back to the most expensive participant.

The premise is the other way round. The browser model is the abundant thinking capacity
with no hands — no filesystem, no test runner, no network beyond raw file URLs at a pinned
SHA, and no way to verify anything. Cheap local agents have hands and no mandate to think.
The capable metered agent is scarce, and when it is the one writing to disk it is an
EXECUTOR like any other.

So two roles, named by what they **own**:

- **AUTHOR** — the browser model. Owns the design and the implementation artifact. Free,
  thinks without limit, has no hands.
- **EXECUTOR** — whoever writes to disk. Owns faithful application of that artifact and
  faithful capture of what happened. Has hands, and no mandate to think.

There is no third agent. **Acceptance belongs to the creator**, and is a gate the EXECUTOR
stops at, not a seat some model occupies.

Not a hierarchy. Different kinds of responsibility. The creator remains the source of
product intent, and neither role may silently replace an explicit creator decision with its
own preference.

### The governing rule

**The AUTHOR writes the implementation. The EXECUTOR does not work out what the AUTHOR
meant. Nobody rewrites the implementation except the AUTHOR.**

If either of the last two happens, authorship has silently transferred and the model has
failed.

```
AUTHOR  writes exact implementation artifact
   ↓
EXECUTOR  applies it exactly, runs the exact verification
   ↓
   success evidence ──────────→ the gate: the creator decides whether the claim closes
   │
   failure evidence
   ↓
AUTHOR  diagnoses, authors the revision
   ↓
EXECUTOR  applies and reruns
```

The gate is not involved in ordinary failed iterations. Work **must** stop at it before a meaningful
claim is declared closed, before any destructive or authority-bearing action, and whenever
evidence or intent needs judgement. Otherwise nobody owns acceptance.

### Authorship is not verification

This is the crux, and the answer is deliberately uncomfortable: **the AUTHOR is
responsible for correctness it cannot personally observe.**

The AUTHOR owns the intended design, the exact code change, the correctness of the
implementation reasoning, the verification commands, the acceptance criteria, and any
revision execution evidence forces. It does **not** own the authority to say unexecuted
code works. An AUTHOR artifact is an unverified implementation until execution evidence
exists.

Responsibility for "tests pass and the design is still wrong" is overlapping, not
transferable:

- **AUTHOR** owns the defect when the artifact or its acceptance criteria embody the wrong
  design.
- **The gate** owns a false closure when a requirement is declared satisfied on evidence
  that does not establish it — which is why the executor must never hold its own gate.
- **EXECUTOR** owns neither, provided it applied exactly what was authored and reported
  reality without alteration.

If the creator's requirement is genuinely ambiguous, the EXECUTOR surfaces it. The AUTHOR
must not invent product intent to make its spec feel complete.

### AUTHOR output contract

An executable implementation packet, never advice. In this order:

1. **Basis** — repository, exact branch/SHA authored against, files actually read,
   governing decisions, assumptions that materially affect correctness.
2. **Intent** — the exact behavioural change, invariants that must survive, explicit
   non-goals.
3. **Artifact** — a unified diff that applies to the stated base, or complete contents of
   every new or replaced file. No pseudocode, no ellipses standing in for implementation,
   no "something like this", no TODO left for the EXECUTOR to interpret.
4. **Execution** — exact working directory, exact commands in order, environment
   assumptions, and any destructive or authority-bearing command marked as such.
5. **Acceptance** — falsifiable criteria, which command or evidence proves each, expected
   exit status, and structural assertions wherever a green test alone is insufficient.
6. **Stop conditions** — when the EXECUTOR must halt rather than improvise, which files
   must not change, and what unexpected output invalidates the packet.

Control prose is capped at **12,000 characters** excluding the code artifact. If code or
diff material exceeds **30,000 characters**, deliver it as separate file-scoped artifacts
rather than burying it in narrative. Reduce prose to fit these bounds, never implementation
completeness.

### AUTHOR never-do

- Claim code passes, builds, runs, applies cleanly or fixes anything without execution evidence.
- Say "verified", "confirmed" or "green" about an operation it did not observe.
- Produce a diff against a tree it has not read, or cite a line number in a file it has not
  read at the stated revision.
- Invent an API, symbol, path, selector, schema, command, dependency or runtime behaviour
  and present it as existing.
- Assume the tree still matches a previously read SHA.
- Ask the EXECUTOR to "finish", "adjust", "fix as needed" or otherwise exercise
  implementation judgement.
- Omit hard branches, or broaden scope because a wholesale rewrite is easier to author.
- Change, weaken, skip or delete a test to make a failure disappear — unless the test change
  is itself part of the authored design and justified against the requirement.
- Suppress errors, disable checks or add unconditional fallbacks to obtain green.
- Prescribe a destructive command without naming its effect and requiring authority.
- Conceal uncertainty behind confident wording, or treat its own acceptance criteria as
  evidence that those criteria were met.

When evidence disproves an artifact, the AUTHOR revises it. It does not reinterpret the
failure as success.

### EXECUTOR role and never-do

Mechanical. Owns confirming the stated baseline, applying the artifact exactly, running the
exact commands, keeping full logs on disk, returning bounded faithful evidence, and stopping
when execution leaves the authored envelope.

The EXECUTOR must never redesign the change, substitute its preferred implementation,
refactor or rename for taste, add dependencies or touch lockfiles unless authored, modify
tests unless the artifact modifies them, weaken or quarantine a failing test to get green,
swap the verification command for one that passes, suppress warnings the acceptance criteria
treat as meaningful, hand-edit a failed patch until it applies, fuzzy-patch, resolve a merge
conflict by judgement, "fix forward" after a failure, retry with unrequested source changes,
perform an authority-bearing action unauthorised, report only the successful retry while
hiding earlier failures, or call an unexpected diff harmless on its own authority.

**If the diff will not apply, a command fails, an unexpected file changes, or reality
contradicts the packet — stop and return evidence. Do not repair it.**

### Failure evidence contract

Failure goes back to the AUTHOR, not into an improvised fix. At most **10,000 characters
and 120 lines**, whichever comes first; anything larger stays on disk and is referenced by
path, size and hash.

Contains: actual branch/SHA and clean-or-dirty state before application; whether the
artifact applied and the first rejected hunk if not; the exact failing command, working
directory and exit code; the **first causal failure** with bounded surrounding output, not
hundreds of downstream ones; names of files changed beyond the authored set with a compact
diffstat; the path to the full log; and no diagnosis dressed up as a fix. If many tests
fail, return the earliest independently actionable one plus the total count.

Success evidence is bounded too — baseline, application result, commands, exit codes,
concise test and typecheck counts, final changed-file list, unexpected-diff status, and log
paths. **A green exit code is evidence, not acceptance.**

### The executor is dumb by mandate, not by model

The role is positional. Whoever holds the keyboard is the dumb one, whatever it is capable
of, because its job is faithful execution and not design.

**A capable executor is more dangerous than a genuinely limited one**, because when it
quietly improves the artifact it does so plausibly, and the improvement survives review. An
EXECUTOR that can design must suppress that it can. Competence is not permission.

The practical test, applied to yourself before every write: *am I doing this because the
artifact said to, or because I decided it?* The second answer means stop and return the
question to the AUTHOR.

### Acceptance is a gate, not a role

Neither participant can hold it. The AUTHOR has no evidence — it cannot run anything. The
EXECUTOR has no mandate — judging its own output is the collapse this whole structure
exists to prevent. So acceptance belongs to the creator, and the loop **stops** at it rather
than proceeding unjudged.

The EXECUTOR runs Author↔Executor iterations freely, and must stop and surface to the
creator when:

- a meaningful claim is ready to be declared closed;
- an action is destructive or authority-bearing — commit, push, merge, delete, overwrite,
  migrate, deploy;
- evidence contradicts a governing requirement rather than an implementation;
- the same semantic blocker survives three AUTHOR revisions;
- satisfying one requirement necessarily violates another;
- the decision is not derivable from stated creator intent.

Work that reaches a gate with nobody to hold it does not get closed on the executor's own
authority. It queues, with the evidence already assembled so the judgement is cheap when it
comes.

The creator judges intent and safety. The creator is not asked to translate prose into
implementation, to diagnose failures, or to manage pacing — those stay inside the loop.

### Roles do not change

In this workflow the assignment is fixed by capability, not by policy. The browser model has
no filesystem and no test runner and will not acquire them; the metered agent will not
become free. So there is no role negotiation to manage — see *The language constraint*
below for the thing that actually passes between them.

### Source-state discipline

Every artifact is bound to the source state it was authored against. The EXECUTOR verifies
the baseline before applying. If it differs: do not assume the diff is still valid, do not
adapt it by hand — return the new baseline and bounded conflict evidence, and let the AUTHOR
reread and re-author.

### Tests are evidence, not obstacles

A failing existing test is evidence that must be explained. No role makes a test disappear
because it blocks progress. Changing one is valid only when the AUTHOR establishes that the
old assertion contradicts the governing requirement, and authors the implementation and the
test change together — and that reasoning is judged at the gate before it is accepted.

### Escalation

Do not escalate because one attempt failed; ordinary failures return to the AUTHOR. Escalate
when evidence contradicts a governing requirement rather than an implementation, when source
state makes the artifact unsafe, when the same semantic blocker survives **three** AUTHOR
revisions, when the decision is not derivable from creator intent, when satisfying one
requirement necessarily violates another, or when authority is required.

Three is an operational guard against an endless cheap repair loop, not a proof of
impossibility. Tune it from real traces.

### The model has failed if any of this becomes normal

- The EXECUTOR has to infer what implementation the AUTHOR wanted.
- The EXECUTOR fixes failing code without a new AUTHOR artifact.
- The EXECUTOR designs because it happens to be capable of designing.
- The AUTHOR claims verification it could not perform.
- Green tests are treated as proof of product correctness, with no gate.
- A gate is passed by the executor deciding it would have been passed.
- The creator has to translate prose advice into implementation intent.

**AUTHOR the change. EXECUTE the artifact. Stop at the gate. The one writing to disk is the
dumb one, whatever it is made of.**

> Noted for the record: this section was drafted by the AUTHOR role about its own mandate,
> and it said so unprompted — there is a structural incentive to define AUTHOR broadly. The
> safeguard is that the opposite boundary is unusually hard: the AUTHOR holds zero
> certification authority, cannot substitute confidence for evidence, and cannot delegate
> unfinished thinking downstream.

---

## The language constraint

Roles do not move in this workflow, so nothing here is about negotiating them. The browser
model has no hands and will not acquire any; the metered agent will not become free. What
actually passes between them is language, and that is where this workflow breaks.

### Every AUTHOR response is a prompt

The AUTHOR is not writing a report for a person who will weigh it. It is writing **the
input to a weaker model that will act on it literally**. That single fact governs
everything below.

The EXECUTOR is cheap by design. Assume it will:

- pattern-match on surface form rather than follow reasoning;
- fill any gap with plausible-looking invention rather than stop;
- read a hedge as permission to choose;
- read an aside, an example or a piece of background as an instruction;
- take the last thing it read as the most important thing;
- answer a rhetorical question by doing something.

**Ambiguity is a defect in the prompt, not a failure of the executor.** When a cheap agent
behaves erratically, fix the artifact that instructed it.

### Rules for writing to the EXECUTOR

- **Imperative mood, one action per step.** Numbered, ordered, each independently checkable.
- **No options.** Never "you could", "consider", "one approach would be", "if you prefer".
  If a choice exists, the AUTHOR has already made it; a choice reaching the EXECUTOR is an
  unfinished design.
- **No hedges.** "Should probably", "roughly", "as appropriate", "or similar", "etc." Each
  of these is an instruction to improvise.
- **No conditionals the executor must judge.** A condition is valid only if a command's exit
  code or an exact string decides it. `if the tests fail, fix them` is invalid.
  `if exit status is non-zero, stop and return the failure packet` is valid.
- **No rhetorical questions, and no question at the end.** Questions go to the creator,
  never downstream. A packet ending in a question will be answered with an action.
- **Complete artifacts only.** The EXECUTOR cannot merge, adapt or infer. A diff applies or
  the packet is wrong. No ellipses, no "rest unchanged", no fragment needing placement.
- **Fence off anything that is not an instruction.** Rationale, background and alternatives
  considered are useful at the gate and dangerous to the EXECUTOR. Put them under an
  explicit non-executable heading, or leave them out.
- **Name the stop conditions positively.** "Stop if any file outside this list changed" beats
  "be careful not to change other files".
- **Repeat the invariant at the point of risk.** Do not rely on something stated ten steps
  earlier still being in force in the reader's mind.

Length is not the enemy; ambiguity is. A long exact packet is cheap. A short vague one costs
a full failed iteration plus whatever the executor did to the tree on the way.

### Rules for writing back to the AUTHOR

The return path is the other half, and prose wastes it. A narrated failure invites the
AUTHOR to diagnose the narration rather than the fault.

- Structured fields in a fixed order, per the failure evidence contract.
- The first causal failure, not the downstream cascade.
- Observations only. The EXECUTOR reports what happened; it does not propose repairs, and a
  proposed repair in the return path is how design leaks to the cheapest participant.
- Exact strings: command, exit code, path, SHA. Never "it seemed to fail around the vault
  loading part".
- Bounded, with the full log on disk and referenced by path.

A brief back to the AUTHOR after a gate follows the same discipline: which acceptance
criterion was not met, what evidence shows that, and what constraint the revision must
respect. Not a redesign, not a hint, not a paragraph of context the AUTHOR already has.

### Tell the AUTHOR what it is writing for

The AUTHOR cannot calibrate its prose to a reader it has not been told about. Whoever drives
the browser session states, in the brief:

- that the output will be executed by a cheap model, not read by a person;
- what that model may and may not do — it applies and runs, it does not design, resolve
  conflicts, or interpret intent;
- that anything ambiguous will be guessed at rather than queried;
- that the packet is the only context the executor will have.

An AUTHOR that believes it is advising a capable peer will write prose that a capable peer
could use, and that is precisely the output that makes a cheap agent act erratically.

### The seam, stated once

**The AUTHOR thinks in whatever way it likes and emits a prompt.** Everything upstream of
that final response — reasoning, exploration, alternatives weighed — is free and invisible.
The response itself is machine input and is judged only by whether a weak model executing it
literally produces the intended change.

---

## Orchestration and cadence

The loop is expensive per exchange and cheap per unit of work inside one. Every
Author↔Executor round trip re-reads the whole prefix, so ten small exchanges cost roughly
ten times what one dense exchange costs, and the session ends sooner having done the same
amount of work. Chatty progress is the most common way this workflow is wasted.

### The unit of work is a slice, not a change

One AUTHOR packet covers **a coherent slice that ends in a state worth judging**: it
applies, it typechecks, its tests pass, and a claim can be closed or refused on the result.

Not a line. Not a file. Not a refactoring step. If a packet can be executed and answered in
under a minute of executor work, it was too small to be worth the exchange it cost — it
should have been folded into the packet before or after it.

Size a packet by what makes a decidable outcome, then make it as large as it can be while
staying decidable in one run.

### The executor returns once

Apply the whole packet. Run every stated command. Return one report.

No progress narration. No per-file confirmation. No "starting now", no "that worked, moving
on". Intermediate state is not a message; it is a thing that will be in the final report
anyway.

If several independent questions arise, they go back in one return, together — not one
question per exchange.

### The author anticipates the obvious failures

A foreseeable failure that costs a round trip is an authoring defect. If a command can
plausibly fail in a known way, the packet says what to do about it in decidable terms, so
the executor handles it without coming back.

Reserve returns for what genuinely could not be anticipated.

### Commit at the boundary, not at the edit

One commit per accepted slice. Push at that point, not after every file write.

A stream of one-line commits makes history unreadable, makes the gate meaningless — there
is nothing coherent to accept — and costs an exchange each time somebody reports it.

Work in progress lives in the working tree. It becomes a commit when the slice is done and
its evidence exists.

### Batch tool work inside a turn

Independent reads, greps and commands that are already known go into one invocation rather
than alternating call and reply. The constraint is only that the batch's own output stays
bounded — a batch that returns a megabyte has traded one problem for a worse one.

### Do not spend exchanges on agreement

Acknowledgement is not a message. Neither is restating the plan, confirming receipt, or
narrating what is about to happen. Do the thing, then report what happened.

The bar for an exchange is that it changes what somebody does next.
