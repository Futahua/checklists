# Status: the checklist worked

Recorded 2026-09-12. Supersedes the earlier revision of this file; `README.md`
still holds the original plan and its reasoning, which stands.

Everything marked **verified** was measured on the running system. Where a slice
was the package's claim, it was tested rather than taken on trust, and two of
those claims turned out to be wrong in ways that matter.

## Slice-by-slice

| # | Slice | Status |
| --- | --- | --- |
| 1 | Plugin shell and lifecycle | **read** — `ctx.effect` generator wraps registration and disposal |
| 2 | CDP endpoint resolver | **verified** — launched with `--remote-debugging-port=0`; the live port is read from `DevToolsActivePort`, so the endpoint is discovered, never assumed |
| 3 | Page-target catalog | **verified** — `browser_tabs` plus `tab-open` / `tab-switch` / `tab-close`, each exercised; close reindexes and promotes a new active tab |
| 4 | Authenticated live-event transport | **verified** — SSE `GET /browser-pane/stream`, HTTP 200, `text/event-stream` |
| 5 | Read-only screencast | **verified** — frames arrive on visual change (2 on attach, 4 after input) |
| 6 | Honest liveness and stale-image state | **verified** — `state` reports `{active, url, mode}` |
| 7 | Canonical coordinate transform | **verified** — see below |
| 8 | Measured coordinate proof | **verified** — exact, zero offset |
| 9 | Mouse, drag and wheel | **verified** — see below |
| 10 | Keyboard and text dispatch | **verified** — see below |
| 11 | Fail-closed per-tab ownership lease | **delivered** — with one honest limit |
| 12 | Automation integration and visible handoff | **delivered** |
| 13 | One-finger touch mapping | **verified — WORKS**, on the real phone |
| 14 | Mobile text entry | **verified — DOES NOT WORK**, on the real phone |
| 15 | Tab loss, browser restart and endpoint change | **verified** — crash test |
| 16 | Unmount, HMR and host teardown | **partial** — HMR and browser lifecycle verified; route/tool disposal by inspection only |
| 17 | End-to-end acceptance gate | **delivered** — `pane-acceptance.mjs`, 5/5 |

Sixteen of seventeen are closed with measurement. Slice 16 is two-thirds
measured and one-third inspection, for a reason given below rather than for lack
of trying.

## 7 and 8 — the transform, proven

`metadata.deviceWidth`/`deviceHeight` from the screencast defines the space
(viewport CSS px); the client scales the rendered `<img>` rect into it; the
server passes coordinates to `Input.dispatchMouseEvent` unmodified.

A click at (480,270) landed on the top-left quadrant, whose handler recorded
`clientX/clientY` of **exactly 480,270**; a second at (1440,810) recorded exactly
1440,810. The probe page records coordinates rather than just which element won,
so an offset would surface as a number instead of hiding behind a correct hit.

## 9 and 10 — input, proven

Through the same `POST /browser-pane/input` route a human gesture uses:

- drag released at exactly (520,430); element moved (200,200) → (420,380), the
  precise +220/+180 delta, across four intermediate moves
- wheel: scrollY 0 → 120 → 240 → 360 → 480 → **600** for five 120-deltaY events
- typing: field held exactly `"Hi 42"`, five keydowns observed
- `Enter/Enter` and `A/KeyA` delivered by key **and** code, not just text

## 11 and 12 — ownership, and what a lease can enforce

The pane's input route needs a live SSE subscriber (it reads a CDP handle that
only exists while streaming), and the package exposes no hook to make that route
refuse input. So a lease **cannot** stop a human clicking. What it can do — and
where the damage comes from — is stop an **automation** driving while somebody
else holds the page. That boundary is ours, so it fails closed.

`harness/pane-lease.mjs`: one JSON file taken atomically (racing acquirers cannot
both win), leases expire (a crashed run cannot wedge the page), and corrupt or
malformed state reads as **held**, never free — two of its twelve checks exist
solely to pin that, because failing open is the one bug that would make it
worthless. A/B on the same automation at the same coordinates: **0 clicks** while
held, **2 clicks** at the expected coordinates once free.

Visible handoff lives in the page, not the GUI: a banner any driver can evaluate,
measured at 1920×29 px with `pointer-events:none`, verified by
`document.elementFromPoint` at its centre resolving to the page beneath.

## 13 — touch works

Measured on the phone over the adb CDP forward, aiming by **fraction of the
rendered image** so the expected coordinate comes from measured geometry rather
than hand arithmetic:

A touch at image fraction (0.6, 0.4) — screen (211,181) — made the pane post
`x=1152.34 y=429.52`, and the page recorded a hit on `#tr` at (1152,429),
matching the prediction to rounding. Android does synthesise the compatibility
mouse events the pane listens for, and the transform is correct under touch.

One trap worth recording: an early read showed **0 hits** and looked like
failure. The input round-trip simply had not finished. Reading state immediately
after a dispatched gesture gives a false negative — wait, or verify the request
completed, before concluding anything.

## 14 — mobile text entry does NOT work

Measured two independent ways, both with the pane image's DOM focus verified as
`document.activeElement === img` (`tabIndex: 0`):

- real IME text injection (`adb shell input text`)
- raw hardware key events (`adb shell input keyevent`), which bypass the IME

Both produced **zero keydowns** in the shared page. The pane binds
`onKeyDown`/`onKeyUp` to a non-editable `<img>`; a soft keyboard cannot be raised
for a non-editable element, and the raw-keyevent result shows the gap is not
merely IME-related. **A phone user has no way to type into the page.** This was
flagged in the plan as the likeliest real gap, and it is confirmed.

## Also found on the phone: the pane overflows and cannot be resized back

Measured: the pane renders **521 px wide in a 419 px viewport** (`left:
-101.67px, right: 0`), and its resize handle sits at `x=-101, width 8` —
`handleOnScreen: false`. The width persists, so on mobile the pane is stuck at a
size that overflows the screen with its drag handle entirely off-screen. The
right 80% of the remote page stays visible and tappable; the left 20% and the
only means of resizing it do not.

## 16 — why one third is inspection only

Two of its three concerns are measured:

- **HMR works.** Editing a linked plugin's client bundle changed its revision
  hash in the boot graph (`ad61b2423377` → `209fd218c280`). The edit was reverted
  and the hash returned to exactly the original value, which proves the file was
  restored byte-identically — the revision *is* a content hash, so it is a
  self-check rather than a hope.
- **The browser does not leak.** No orphaned `chrome.exe`: the only live headless
  instance postdates `dsh web` and is parented to it, while four earlier browsers
  closed and left only temp profile directories.

**Route and tool disposal is inspection only.** Exercising it means unloading the
plugin, and re-enabling requires loading a module again — which `dsh-base`
disables module HMR for — so a failed re-enable would leave the pane down until a
restart. That is a real cost to a working feature for a code path that reads
correctly (`ctx.effect` yields disposers for the tools, the routes, the
screencast, the held keys and the browser). It is left unexercised deliberately,
not overlooked; a `dsh web` restart with no orphaned browser afterwards is the
cheap way to close it.

## Found while working it: an infinite redirect

The bridge signed a cookieless browser in with `303` + `Set-Cookie`. A client
that cannot retain cookies followed it to `/`, arrived cookieless, and was sent
round: `curl -L` gave up after **50 redirects**, Node's `fetch` simply failed.
Browsers were unaffected, which is why it hid.

Fixed by deleting the redirect: the bridge proxies the GUI in one hop with the
session minted on the same response. The cookie is signed **twice** per request,
once per hop, because the browser stores one bound to the name in its address bar
while DSH must receive one bound to the loopback authority it was launched on;
reusing a single signing for both is a 401. A `Referer`-based loop guard cannot
work — the response sets `referrer-policy: no-referrer`.

## Compatibility finding worth keeping

The package declares `dsh.client.inject: ["@deepseek-ai/dsh-client-runtime"]`,
and that module does not exist in this harness build. It is benign:
`dsh-client-modules` resolves that list with `if (dependency !== void 0)`, so an
id with no graph row is skipped rather than awaited. The built `lib/client.js`
requires only `react` and `react-dom`, both platform-seeded.

Separately, the plugin declares `inject = ["tools","skills"]` but reads
`ctx.get("webServer")` synchronously and silently skips when it is not up yet, so
its pane routes never registered while its client row sat in the boot graph. It
is worked around with an entry-level `inject: [webServer]` in the profile's
`cordis.patch.yml`, commented for removal once upstream defers with
`ctx.inject(["webServer"], ...)`.

## Security posture, since this is a public repo

No login key, cookie secret, API key or tunnel hostname is recorded here.

The pane's routes (`/browser-pane/*`) register directly on the web server and are
therefore **not** under DSH's `/api` browser-trust fence. On the tailnet they are
reachable only through the loopback auth bridge.

The bridge previously carried a hardcoded fallback for the browser-session
signing secret — a live session-forgery key in a file headed for a public repo.
It was never committed, and it now reads from `.credentials.yaml` and fails
closed. The one-tap login key is gone entirely: it never denied anybody that
automatic sign-in did not already admit.
