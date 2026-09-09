# The loop

**AUTHOR** — the browser. Writes the change. No hands, cannot run anything.
**EXECUTOR** — whoever writes to disk. Applies it and runs it. Does not redesign.
**The creator** — says yes or no. Nobody else does.

```
AUTHOR writes → EXECUTOR applies and runs → it worked?
                                             yes → creator decides
                                             no  → back to AUTHOR
```

That is the workflow. The rest of this page is the handful of things that go wrong.

## Five rules

1. The creator decides what is done. Neither agent decides it.
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

## Two habits

Commit at an accepted slice, not per edit. Keep big files out of context — read the part
you need.

## Elsewhere

[BROWSER.md](BROWSER.md) is the AUTHOR's brief; hand it that URL at session start.
[reference/](reference/) is how all this was worked out, including every failure behind a
rule. Read it if you want the reasoning. It is not law.

A script gets written only after the same failure has cost a round trip twice. So far:
none, correctly.
