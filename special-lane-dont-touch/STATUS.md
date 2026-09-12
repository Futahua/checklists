# Status: the lane narrowed

Recorded 2026-09-12. This does not replace `README.md` — the plan and its
reasoning stand. It records what changed when the plan's own first instruction
("verify the `@try-works/dsh-browser-agent` claim independently before forking")
was actually carried out.

## What changed

`@try-works/dsh-browser-agent@0.6.0` is real, ISC-licensed, and already
implements most of the checklist. It is now installed into the `web` profile on
`sloptop` and reconciled into `dsh.profile.bundles`. So this lane is no longer
"build an inline browser"; it is "use this one, and own the gaps it does not
cover".

The tarball ships full TypeScript source, so the audit was reading code, not
trusting a README.

## Slice-by-slice

Evidence grades: **read** = confirmed in the package's source; **claimed** =
stated in its README and not yet independently exercised; **gap** = not
addressed by the package and still ours.

| # | Slice | Status |
| --- | --- | --- |
| 1 | Plugin shell and lifecycle | **read** — `src/index.ts` wraps registration in a `ctx.effect` generator |
| 2 | CDP endpoint resolver | **partial** — it launches its own Chrome from `chromePath`; `connectUrl` is a fixed URL, so no `DevToolsActivePort` discovery for an external browser |
| 3 | Page-target catalog | **claimed** — `browser_tabs` / `tab-open` / `tab-switch` / `tab-close` routes exist in `src/pane.ts` |
| 4 | Authenticated live-event transport | **read** — SSE `GET /browser-pane/stream` registered on `ctx.webServer` |
| 5 | Read-only screencast | **claimed** — `Page.startScreencast`, JPEG on visual change |
| 6 | Honest liveness and stale-image state | **partial** — subscriber lifecycle and last-frame replay are claimed; no explicit stale/liveness affordance confirmed |
| 7 | Canonical coordinate transform | **unverified** — the pane→viewport mapping has not been read or measured |
| 8 | Measured coordinate proof | **gap** — proving it by click plus `document.elementFromPoint` readback is still ours |
| 9 | Mouse, drag and wheel | **claimed** — `Input.dispatchMouseEvent`, fractional wheel accumulation |
| 10 | Keyboard and text dispatch | **claimed** — `Input.dispatchKeyEvent`, held-key release on focus loss |
| 11 | Fail-closed per-tab ownership lease | **gap** — nothing prevents the pane and an automated run fighting over one tab |
| 12 | Automation integration and visible handoff | **gap** |
| 13 | One-finger touch mapping | **unverified** — pointer events are handled; touch fidelity on a real phone is untested |
| 14 | Mobile text entry | **unverified** — same |
| 15 | Tab loss, browser restart, endpoint change | **partial** — crash/relaunch handled; endpoint change is not |
| 16 | Unmount, HMR and host teardown | **read** — the effect generator disposes routes, tools, screencast, held keys and Chrome |
| 17 | End-to-end acceptance gate | **gap** |

Slices 8 and 11 remain the two that matter most, and both are gates rather than
features: correctness proven by measurement, and a fail-closed ownership lease.

## Compatibility finding worth keeping

The package declares `dsh.client.inject: ["@deepseek-ai/dsh-client-runtime"]`,
and that module **does not exist** in the harness build here. It is benign, and
the reason is worth recording because it is not obvious:

```
dsh-client-modules/lib/client.js:265
  for (const packageName of row.inject) {
      const dependency = this.graphRows.get(packageName)
      if (dependency !== void 0) await this.arriveGraphRow(dependency, [], visited)
  }
```

An id with no matching graph row is skipped, not awaited. No hang, no throw. The
built `lib/client.js` requires only `react` and `react-dom`, both platform-
seeded, so nothing is missing at materialization.

## Security posture, since this is a public repo

Recorded because the note is useful and the secret is not: the pane's routes
(`/browser-pane/*`) are registered directly on the web server and are therefore
**not** under DSH's `/api` browser-trust fence. On the tailnet they are reachable
only through the loopback auth bridge, which requires a valid browser-session
cookie for every path except the login and manifest. Locally they are open on
`127.0.0.1:3080`, as is everything else on that port.

No login key, cookie secret, API key or tunnel hostname is recorded here or in
the repository.

## Open decisions still not made

Unchanged from the original list, and now sharper because the package fixes some
of the variables: endpoint policy (fixed port vs `DevToolsActivePort`),
background-tab activation, phone keyboard UX, frame budget, and SSE versus
long-poll — the last of which the package answers in favour of SSE.
