# Status: the lane narrowed

Recorded 2026-09-12, updated after working the list. This does not replace
`README.md` — the plan and its reasoning stand. It records what changed when the
plan's own first instruction ("verify the `@try-works/dsh-browser-agent` claim
independently before forking") was actually carried out, and then what happened
when the remaining slices were worked.

## What changed

`@try-works/dsh-browser-agent@0.6.0` is real, ISC-licensed, and already
implements most of the checklist. It is installed into the `web` profile on
`sloptop` and reconciled into `dsh.profile.bundles`. So this lane is no longer
"build an inline browser"; it is "use this one, and own the gaps it does not
cover".

The tarball ships full TypeScript source, so those audits were reading code, not
trusting a README. Everything marked **verified** below was measured on the
running system, not inferred.

## Slice-by-slice

| # | Slice | Status |
| --- | --- | --- |
| 1 | Plugin shell and lifecycle | **read** — `ctx.effect` generator wraps registration and disposal |
| 2 | CDP endpoint resolver | **verified** — launched with `--remote-debugging-port=0`; the live port is read from `DevToolsActivePort` in the profile, so the endpoint is discovered, never assumed |
| 3 | Page-target catalog | **claimed** — `browser_tabs` / `tab-open` / `tab-switch` / `tab-close` |
| 4 | Authenticated live-event transport | **verified** — SSE `GET /browser-pane/stream`, HTTP 200, `text/event-stream` |
| 5 | Read-only screencast | **verified** — frames arrive on visual change (2 on attach, 4 after input) |
| 6 | Honest liveness and stale-image state | **verified** — `state` reports `{active, url, mode}`; a late subscriber is told the truth |
| 7 | Canonical coordinate transform | **verified** — see below |
| 8 | Measured coordinate proof | **verified** — see below |
| 9 | Mouse, drag and wheel | **claimed** — `Input.dispatchMouseEvent`, fractional wheel accumulation |
| 10 | Keyboard and text dispatch | **claimed** — `Input.dispatchKeyEvent`, held-key release on focus loss |
| 11 | Fail-closed per-tab ownership lease | **delivered** — see below, with one honest limit |
| 12 | Automation integration and visible handoff | **delivered** — see below |
| 13 | One-finger touch mapping | **blocked on hardware** — analysis done, phone disconnected before measurement |
| 14 | Mobile text entry | **blocked on hardware** — same |
| 15 | Tab loss, browser restart and endpoint change | **verified** — see below |
| 16 | Unmount, HMR and host teardown | **read** — the effect generator disposes routes, tools, screencast, held keys and Chrome |
| 17 | End-to-end acceptance gate | **delivered** — `pane-acceptance.mjs`, 5/5 |

Four of the seventeen remain unproven: 9 and 10 are the package's claims, and 13
and 14 need the phone.

## 7 and 8 — the coordinate proof

The transform is three steps, and only the middle one was ever in doubt:

- The screencast frame carries `metadata.deviceWidth`/`deviceHeight`, which is
  viewport CSS pixels. That is the canonical space.
- The client maps pointer position into it as
  `(clientX - rect.left) / rect.width * frame.width` — scaling the rendered
  `<img>` rect back to that space.
- The server passes `x`/`y` straight to `Input.dispatchMouseEvent` unmodified.

Measured rather than reasoned: a click dispatched through
`POST /browser-pane/input` at (480,270) landed on the top-left quadrant, whose
own handler recorded `clientX/clientY` of **exactly 480,270**. A second at
(1440,810) landed on the bottom-right, recording exactly 1440,810. Zero offset,
in both axes, at both extremes of the viewport.

The target page (`.dsh/probe/coord-test.html`) records coordinates rather than
just which element was hit, so an offset would show up as a number instead of
hiding behind a correct element.

## 11 and 12 — ownership, and what a lease can actually enforce

Two measured facts decided the design:

1. The pane's input route reads a CDP handle that only exists while an SSE client
   is streaming (`pane.ts`, "the screencast follows its subscribers"). Posting
   input with nobody watching returns `400 browser not ready`.
2. The package registers its routes directly on the web server and exposes **no
   hook** to make that route refuse input.

So a lease **cannot** stop a human clicking, and a design claiming otherwise
would be theatre. What it can do — and where the damage actually comes from — is
stop an **automation** driving while somebody else holds the page. That boundary
is ours, so it is enforceable there, and it fails closed.

`harness/pane-lease.mjs` keeps state in one JSON file taken atomically, so racing
acquirers cannot both win; leases expire, so a crashed run cannot wedge the page;
and unreadable, malformed or corrupt state reads as **held**, never free. Two of
its twelve checks exist solely to pin that last property: failing open is the one
bug that would make the whole thing worthless.

Evidence: 12/12 checks pass, and an A/B of the same automation at the same
coordinates produced **0 clicks while the lease was held** and **2 clicks at the
expected coordinates** once it was free.

The visible half lives in the page, not the GUI — `bannerScript(owner)` returns a
JS expression any driver can evaluate, so the human watching the pane sees who
has the page and until when. Measured: 1920x29 px, z-index max, and
`document.elementFromPoint` at its centre resolves to the page beneath it, i.e.
`pointer-events:none`. A takeover notice that swallowed clicks would be worse
than none.

## 15 — crash, tab loss and endpoint change

Killing all four processes of the plugin's browser produced a **new** instance:
`browser_tabs` returned two fresh blank tabs rather than the previous four, a
different `puppeteer_dev_chrome_profile-*` directory appeared, and a subsequent
navigation returned HTTP 200. The endpoint question is settled by fact: the
browser is launched with `--remote-debugging-port=0`, so the port is OS-assigned
and rediscovered from `DevToolsActivePort` on every launch. A fixed port was
never needed.

## Found while working it: an infinite redirect

The bridge signed a cookieless browser in with `303` + `Set-Cookie`. A client
that cannot retain cookies followed it to `/`, arrived cookieless again, and was
sent round: `curl -L` gave up after **50 redirects**, and Node's `fetch` just
failed. Browsers were unaffected, which is exactly why it went unnoticed.

Fixed by deleting the redirect: the bridge now proxies the GUI in one hop with a
session minted on the same response, so a cookieless client gets a real page and
browsers save a round trip. The cookie is signed **twice** per request, once per
hop, because the browser stores one bound to the name in its address bar while
DSH must receive one bound to the loopback authority it was launched on;
reusing a single signing for both is a 401.

A `Referer`-based loop guard was tried first and cannot work: the response set
`referrer-policy: no-referrer`, so the follow-up carries no Referer to detect.

## 13 and 14 — blocked on the phone, not on analysis

The phone disconnected (`adb devices` empty) before touch could be measured, so
neither slice is closed. What source reading predicts, to be tested when it
returns:

- The pane's page surface binds **mouse handlers only** (`onMouseDown`/`Up`/
  `Move`/`Wheel`); the pointer handlers belong to the resize handle. So touch
  must arrive via the browser's compatibility mouse events.
- `touchAction: 'none'` is set on the **resize handle**, not the image, so the
  page surface has default touch behaviour. A tap should work; a drag will pan
  the phone instead of dragging the remote page.
- The wire schema has no touch types at all — only mouse, wheel and key — so
  multi-touch and pinch have nowhere to go.
- Text entry is the likeliest real gap: soft keyboards frequently emit
  `key: "Unidentified"`, and there is no IME or composition handling.

A tool for the measurement is ready: `harness/phone-eval.mjs` evaluates JS in a
chosen tab of the phone's Chrome over the adb CDP forward.

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

Separately: the plugin declares `inject = ["tools","skills"]` but reads
`ctx.get("webServer")` synchronously and silently skips when it is not up yet, so
its pane routes never registered while its client row sat in the boot graph. That
is worked around with an entry-level `inject: [webServer]` in the profile's
`cordis.patch.yml`, commented for removal once upstream defers with
`ctx.inject(["webServer"], ...)`.

## Security posture, since this is a public repo

Recorded because the note is useful and the secret is not. No login key, cookie
secret, API key or tunnel hostname is recorded here.

The pane's routes (`/browser-pane/*`) are registered directly on the web server
and are therefore **not** under DSH's `/api` browser-trust fence. On the tailnet
they are reachable only through the loopback auth bridge; locally they are open
on `127.0.0.1:3080`, as is everything else on that port.

The bridge previously carried a hardcoded fallback for the browser-session
signing secret — a live session-forgery key in a file headed for a public repo.
It was never committed, and it now reads from `.credentials.yaml` and fails
closed.

The one-tap login key is gone entirely. It never denied anybody that automatic
sign-in did not already admit, because anything able to reach the bridge is on
the tailnet, and tailnet membership is the access boundary.

## Open decisions

Most are now settled by the package rather than by choice: transport is SSE,
endpoint policy is `DevToolsActivePort` discovery, and the frame budget is
Chrome's own screencast throttling. Still open: background-tab activation, phone
keyboard UX, and whether the ownership lease should ever move into the package
itself — it cannot be enforced from outside, so that is the only way it could
cover the human's input too.
