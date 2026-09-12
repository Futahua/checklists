# Inline browser pane — research and implementation checklist

Lane: **special-lane-dont-touch**. Reserved for this work; other agents and
runs should not modify files under this directory.

Source: a design review conducted 2026-09-12 against a live ChatGPT session over
CDP, given the full DSH plugin brief (host/client halves, the slot registry as
the only UI contribution mechanism, /api route inheritance of the Host fence and
session cookie, the reload matrix, hashed class names versus data-slot hooks,
and mobile breakpoints), plus the established CDP findings.

Contents, in order:
1. Ranked research on existing work to reuse rather than rebuild.
2. A 19-slice implementation checklist, each slice with an observable acceptance
   check and the failure it prevents.
3. The decisions reserved for the human owner.

Read the research first: its top recommendation is that the screencast and input
machinery should NOT be built from first principles.

---
I found enough prior art that you should not implement the screencast/input machinery from first principles. The closest existing work is surprisingly close to your DSH shape.

Research result — what to reuse
Rank by work saved	Existing work	Frames + input	Coordinate/mobile handling	Licence / status	Recommendation
1	@try-works/dsh-browser-agent
	Yes. DSH-native pane; SSE Page.startScreencast; mouse, wheel, keyboard input; tab switching; cleanup	Its current client scales pane coordinates directly to screencast dimensions. That is simpler than Chromium DevTools' mapping and should not be accepted without your measurement gate.	ISC; npm 0.6.0 published 19 days ago. 
npm
+1
	Best source/fork. Reuse the DSH lifecycle, SSE, ACK, held-key and cleanup mechanics. Replace its coordinate and ownership model.
2	Vercel agent-browser streaming
	Yes. WebSocket frames plus input_mouse, input_keyboard, input_touch; can attach to existing Chrome/CDP and auto-discover dynamic ports	Sends full screencast metadata; already has input pacing/ACK and touch protocol	Apache-2.0; npm 0.37.1, published days ago; very active. 
GitHub
+2
agent-browser
+2
	Best complete sidecar. Consider only if an extra daemon is acceptable. Otherwise mine its protocol/reconnect behavior.
3	duongdev/cdp-browser
	Yes. JPEG screencast, canvas, mouse/keyboard/scroll, tabs; also has a web build	Adaptive viewport and input scaling	MIT; active in 2026. 
GitHub
	Excellent reference implementation, but its Electron/browser shell is much larger than your plugin needs.
4	browserface
	Yes. Explicitly designed as a human face for an agent-controlled CDP browser	Good touch implementation: tap vs drag-scroll, remote/local scale, mobile keyboard handling. Its client maps displayed frame coordinates into a tracked CSS viewport.	No licence found in the current repository/package metadata. The repo is active, but treat the source as all-rights-reserved unless that changes. 
GitHub
	Behavioral prior art only. Do not copy code.
5	chrome-remote-interface
	CDP transport only	No pane or coordinate translation	MIT; 0.34.0; ~1.3M weekly npm downloads. 
npm
	Best small embedded dependency if you build the host yourself.
—	Playwright / Puppeteer	CDP/session primitives, not a ready interactive pane	Automation APIs, but no drop-in remote pane transform	Apache-2.0; both actively maintained. 
npm
+1
	Too large if all you need is CDP transport.
—	Browserless	Live debugger/browser infrastructure	Product handles the hard parts	SSPL-1.0 or commercial licence; very active. 
GitHub
+1
	Far too much infrastructure/licence coupling for one local Chrome.
—	noVNC	Yes, full desktop video + input	Mature scaling, mouse emulation and mobile gestures	Mainly MPL-2.0. 
GitHub
	Only sensible if Chrome lives in an isolated desktop/session. Wrong fit for your real local Chrome because it can contend for OS pointer/focus.

The canonical coordinate reference is Chrome DevTools itself, not any of those projects. CDP defines Input.dispatchMouseEvent.x/y in main-frame viewport CSS pixels, while screencast metadata gives offsetTop, pageScaleFactor, device dimensions in DIP, and scroll offsets in CSS pixels. 
Chrome DevTools
+1
 DevTools computes a screenZoom, divides pointer coordinates and wheel deltas by it, subtracts offsetTop from Y, and latches the offset during a drag. For document hit-testing it additionally divides by pageScaleFactor and adds scroll offsets. 
Chromium Git Repositories
+2
Chromium Git Repositories
+2

For prior-art UX, Browserbase's Live View is almost exactly the product surface: watch/click/type/scroll, iframe embedding, multitab and explicit disconnect signaling. It is a hosted product rather than reusable local code. 
Browserbase Documentation
 Browserface goes further toward your automation/human-handoff semantics, but its present licensing makes it unsuitable as a source dependency.

For alternatives: stay with CDP screencast for v1. WebRTC would improve video transport but Chrome does not give you a WebRTC stream of an arbitrary CDP target; you would need another capture layer while still using CDP for input. VNC provides both pixels and input but at desktop level and undermines your non-interference requirement. An iframe/header-stripping proxy gives native input but cannot faithfully reproduce an arbitrary already-authenticated Chrome target—origin, cookies, service workers, CSP, CORS and cross-origin frames make that a different architecture.

Inline Browser Pane — Complete Implementation Checklist
Status

Implementation target: new DSH plugin; no shipped-bundle patches.

Reference implementation policy:

 ISC-licensed @try-works/dsh-browser-agent may be reused with attribution.

 Chromium DevTools' BSD-licensed screencast/input algorithms may be adapted.

 browserface source must not be copied while it has no usable licence.

 Browserless/Browserbase/noVNC are not runtime dependencies for v1.

 Use chrome-remote-interface unless the existing raw-CDP code is materially smaller.

Phase A — read-only observer
Slice 1 — Plugin shell and lifecycle

Build

 Create the plugin host half in index.js.

 Create the lib/client.js window.__ModuleLoader__.load(...) bundle.

 Add the composition row to cordis.patch.yml.

 Register one pane component into a root-scope slot; prefer the existing shell.overlay seat if present.

 Give every DOM node owned by this plugin its own data-dsh-inline-browser-* hook.

 Do not query or style DSH CSS-module class names.

 Add one host disposer that owns every route, timer, CDP connection and subscription created by the plugin.

Acceptance check

 Start dsh web, refresh once after adding the new client row, and assert exactly one pane root exists.

 Rewrite lib/client.js; assert the pane HMRs without creating a second pane root.

 Change index.js; assert the change is absent until dsh web is restarted and present after restart.

 Toggle the pane at viewport widths above and below 768 px; assert it remains reachable at both.

Failure prevented

Duplicate client mounts, reliance on unstable host classes, incorrect assumptions about DSH host HMR, and a desktop-only pane.

Slice 2 — CDP endpoint resolver

Build

 Support a configured static endpoint such as 127.0.0.1:9222.

 Also support a configured dedicated Chrome user-data-dir.

 When a profile directory is configured, read DevToolsActivePort and derive the current browser WebSocket endpoint from it.

 Treat endpoint identity as a generation; increment the generation whenever the browser endpoint changes.

 Bind only to loopback/private configured endpoints; never expose the raw CDP port through DSH/Tailscale.

 While disconnected, retry with bounded backoff.

 On a changed DevToolsActivePort, abandon the old socket before attaching to the new one.

agent-browser uses this same dynamic-port discovery strategy for existing Chrome, so the mechanism is already proven in current tooling. 
GitHub

Acceptance check

 Start Chrome on port A; query a plugin diagnostic endpoint and assert connected=true.

 Stop Chrome.

 Start the same dedicated profile on port B where B != A.

 Without restarting DSH, assert the diagnostic endpoint eventually reports endpoint generation N+1, port B, and connected=true.

 Assert no connection remains open to port A.

Failure prevented

A pane permanently tied to 9222, reconnecting to a dead browser, or driving the wrong Chrome after restart.

Slice 3 — Page-target catalog

Build

 Enable browser-level target discovery.

 Maintain targets keyed by CDP target ID, never array index.

 Admit user-visible page targets only.

 Exclude browser_ui, workers, DevTools surfaces, extension/background targets and other non-tab targets.

 Expose title, URL and target ID to the client.

 Add an exact /api/inline-browser/select operation accepting a target ID.

 Selection must not send input or activate the target.

 If the selected target disappears, clear selection rather than silently selecting another tab.

Acceptance check

 With two ordinary tabs plus at least one non-page target, fetch the catalog.

 Assert the two page target IDs appear and the non-page target does not.

 Select tab B.

 Close tab A and assert B remains selected by ID.

 Close B and assert selectedTargetId=null; assert another tab was not selected automatically.

Failure prevented

Index drift, accidentally attaching to Chrome internals, and silently switching the controlled tab after a close.

Slice 4 — Authenticated live-event transport

Build

 First prove whether an exact connection.fetch.register /api route can hold a streaming text/event-stream response.

 If yes, implement /api/inline-browser/stream as SSE.

 If exact-route streaming is unsupported, implement an exact authenticated long-poll route /api/inline-browser/events?after=<seq> rather than bypassing the Host fence.

 Event records carry a monotonically increasing sequence number.

 Define state, targets, selected, frame, owner, and heartbeat events.

 Reconnect from the last observed sequence where transport permits.

 Do not expose a second unauthenticated streaming server merely for convenience.

Acceptance check

 Open one authenticated request and observe at least three separately framed events without reopening the request; otherwise assert the long-poll fallback returns immediately when a later sequence appears.

 Make the same request without the DSH browser-session credentials and assert it is rejected.

 Disconnect/reconnect the browser client and assert event sequence remains monotonic within the current host generation.

Failure prevented

Turning a privileged Chrome-control stream into an unauthenticated side channel, or falling back to screenshot polling because streaming was assumed rather than tested.

Slice 5 — Read-only screencast

Build

 Attach a dedicated flattened CDP session to the selected target.

 Enable Page.

 Start Page.startScreencast.

 ACK every Page.screencastFrame immediately, including frames not delivered to the UI.

 Keep only the newest undisplayed frame; never queue an unbounded series of JPEGs.

 Preserve the complete metadata required later:

offsetTop

pageScaleFactor

deviceWidth

deviceHeight

scrollOffsetX

scrollOffsetY

timestamp

 Tag every frame with endpoint generation, target ID, target generation and frame sequence.

 Render the selected tab into an <img> or canvas without installing any input handlers yet.

 Do not enable focus emulation merely because someone is observing.

The first-subscriber/last-subscriber screencast ownership and ACK pattern can be lifted conceptually from the existing DSH browser plugin. 
npm

Acceptance check

 Select a page containing an animation or incrementing counter.

 Assert at least 10 increasing frame sequences arrive.

 Stop the visual change; assert the last rendered pixels remain but CDP health remains independently reported.

 Inspect the host diagnostic state and assert no pending frame queue can exceed one replacement frame.

Failure prevented

Screencast deadlock from missing ACKs, memory growth under a slow phone, and accidental behavioral changes to a tab that is only being watched.

Slice 6 — Honest liveness and stale-image state

Build

 Track CDP connection health independently from frame freshness.

 Send a host heartbeat while the selected target/session is healthy.

 Track lastFrameAt.

 Track Page.screencastVisibilityChanged if available.

 Give the client distinct visible states for:

disconnected endpoint,

reconnecting,

no tab selected,

selected tab closed,

attaching,

connected with fresh frame,

connected with static/old frame,

screencast inactive/backgrounded,

stream transport stale.

 Never show an old frame without an age/status overlay once liveness is lost.

 Keep old pixels dimmed for context rather than clearing them immediately.

Acceptance check

 Freeze frame delivery in a test while leaving heartbeat delivery active; assert UI says the last visual frame is old/static without claiming Chrome disconnected.

 Freeze both heartbeat and frames; assert the pane displays a stale/disconnected overlay within the configured health deadline.

 Kill Chrome; assert the last frame is visibly marked non-live.

 Restart Chrome; assert the stale state clears only after a new session/target is established.

Failure prevented

A frozen screenshot being mistaken for the current state of a live browser.

Phase B — desktop input plumbing

Do not expose interactive pane listeners to the user during this phase. Exercise the input primitives through integration tests until the ownership gate exists.

Slice 7 — Canonical coordinate transform

Build

 Compute coordinates from the rendered image content rectangle, not the pane rectangle.

 If the element uses object-fit: contain, exclude its letterbox area.

 Let:

screenZoom = rendered-frame-width-in-local-CSS-px / metadata.deviceWidth

inputX = localX / screenZoom
inputY = localY / screenZoom - metadata.offsetTop

 Clamp only after conversion to the valid remote viewport.

 Do not multiply inputX or inputY by the local phone/desktop devicePixelRatio.

 Do not add page scroll offsets to Input.dispatchMouseEvent; CDP wants viewport CSS coordinates. 
Chrome DevTools

 For wheel deltas, divide displayed-pixel deltas by screenZoom.

 On mouse-down, latch the current screenZoom and offsetTop until mouse-up so a frame arriving during a drag cannot move the coordinate system. This matches DevTools' own InputModel. 
Chromium Git Repositories

 Retain pageScaleFactor and scroll offsets for document-space inspection only:

documentX = inputX / pageScaleFactor + scrollOffsetX
documentY = inputY / pageScaleFactor + scrollOffsetY

This is the same distinction used by DevTools' screencast inspector. 
Chromium Git Repositories
+1

Acceptance check

 Unit-test the transform with synthetic metadata covering nonzero offsetTop, fractional zoom, local DPR 1 and DPR 2, and two letterboxed aspect ratios.

 Assert identical remote CSS coordinates for the same visual target under local DPR 1 and 2.

 Assert changing metadata after mouse-down does not alter the transform used before mouse-up.

Failure prevented

The classic “looks correct at 1× but clicks drift on phone/zoom/resize” failure.

Slice 8 — Measured coordinate proof

Build

 Add a deterministic local test page containing a labelled grid of small hit targets distributed near all four edges and the center.

 Make the document taller than the viewport and horizontally scrollable.

 Install a page listener that records:

target id
clientX/clientY
pageX/pageY
scrollX/scrollY
devicePixelRatio
innerWidth/innerHeight
visualViewport values

into a known test variable.

 Aim through the same coordinate-transform path the pane will use.

 Dispatch a real mousePressed + mouseReleased.

 Read the page's record back through Runtime.evaluate.

 Also call document.elementFromPoint(record.clientX, record.clientY) and return its test ID.

Run this matrix:

 default viewport, DSF 1;

 Emulation.setDeviceMetricsOverride, DSF 2;

 substantially different viewport width/height;

 vertical scroll;

 horizontal scroll;

 non-1 page/visual viewport scale where reproducible;

 narrow rendered pane;

 wide rendered pane.

Acceptance check

 For every case, machine output must report expectedTargetId === actualTargetId.

 elementFromPoint(...) must return the same target.

 Recorded clientX/clientY must be within ±2 CSS px of the requested target center.

 The slice fails on any matrix member; visual inspection is not an acceptable substitute.

Failure prevented

Shipping mathematically plausible coordinate code that is empirically wrong.

Slice 9 — Mouse, drag and wheel dispatch

Build

 Implement host-side mouseMoved, mousePressed, mouseReleased and mouseWheel.

 Carry modifiers, button, buttons, and click count.

 Throttle hover-only move events to a bounded rate.

 Do not discard intermediate drag movement solely because of hover throttling.

 Capture the pointer locally or listen for release outside the frame so a drag cannot leave the remote mouse permanently pressed.

 Normalize DOM wheel deltaMode.

 Preserve fractional wheel remainder rather than losing subpixel input.

 Keep this path inaccessible from ordinary pane UI until the lease gate is complete.

Acceptance check

 Integration test single click, double click, drag and wheel against the deterministic page.

 Assert the remote page records the exact expected event ordering.

 Drag outside the local frame before releasing and assert the remote receives mouseup.

 Scroll 500 local CSS px at two different pane scales and assert the resulting remote scroll displacement is equal within tolerance.

Failure prevented

Stuck mouse buttons, scale-dependent scrolling, broken selection drags and event floods.

Slice 10 — Keyboard and text dispatch

Build

 Use Input.dispatchKeyEvent for key-down/up and navigation/control keys.

 Carry key, code, modifiers, repeat/location information where available.

 Use Input.insertText for committed text, paste, Unicode, emoji and IME output.

 Do not synthesize printable text solely from keydown.

 Track held keys locally and remotely.

 Release every held key on blur, client loss, target change and CDP disconnect.

 Keep interactive client listeners disabled pending Phase C.

Acceptance check

 Focus a remote test input.

 Type ASCII, Vietnamese text, and an emoji through the text path; assert its exact final .value.

 Test Backspace, arrows, Shift selection, Ctrl+A and Enter through the key path.

 Simulate local focus loss while Shift is held and assert the remote records a matching key-up.

Failure prevented

Broken mobile/IME input, duplicated characters, and modifiers getting stuck in Chrome.

Phase C — ownership and automation coexistence
Slice 11 — Fail-closed per-tab ownership lease

Build

 Default every selected target to observer.

 Create a host-owned lease keyed by target ID and target generation.

 Lease record contains at minimum:

kind = human | automation
holderId
opaque token
acquiredAt
lastHeartbeatAt
expiry

 Add exact authenticated acquire, heartbeat and release operations.

 Require targetId, target generation and valid lease token on every input request.

 Re-check the lease immediately before CDP dispatch.

 Return conflict, not success, when another owner holds the tab.

 A human “Take control” operation must never silently displace automation.

 If force takeover is supported, make it a separate operation requiring an explicit confirmation gesture.

 Revoke the lease on target close, browser disconnect, generation change or expiry.

 Streaming remains available to observers regardless of owner.

Acceptance check

Run two synthetic clients:

acquire target as automation=A;

attempt human=H;

assert H receives conflict;

submit input without token and assert rejection;

submit input with H's nonexistent/stale token and assert rejection;

submit with A and assert accepted;

release A;

acquire H and assert accepted;

attempt input with old A token and assert rejection.

 While A owns the tab, H must continue receiving frames.

 No rejected input may appear in the page's event log.

Failure prevented

Two independent actors driving one tab and producing irreproducible, dangerous mixed input.

Slice 12 — Automation integration and visible handoff

Build

 Expose the same lease contract to the automated browser driver.

 Before an automated run first mutates the selected tab, it acquires automation.

 It heartbeats while active and releases on completion/cancellation.

 The pane shows Watching automation while that lease exists.

 Human controls remain inert while automation owns the target.

 After human ownership begins, show a persistent You control this tab state.

 Releasing human control removes input listeners/focus state before announcing observer mode.

 Do not call Target.activateTarget, inject focus, or emulate focus while merely observing.

Acceptance check

 Start a scripted automated sequence that continuously owns the lease.

 Click the pane's normal Take Control control.

 Assert no CDP input from the human appears and automation continues unchanged.

 Release automation.

 Acquire human ownership.

 Assert automation now receives the same ownership conflict if it attempts a mutating action.

 Release human ownership and assert automation can acquire again.

Failure prevented

A UI that claims to have an ownership gate while the actual automated path bypasses it.

Hard gate: if the CUA/automation stack cannot participate in this lease protocol, the implementation cannot truthfully guarantee non-contention. In that case the pane must require an explicit external-automation-paused acknowledgement before human acquisition.

Phase D — phone support
Slice 13 — One-finger touch mapping

Build

Implement a touch state machine only after human ownership has been acquired:

 one active touch ID at a time;

 save start and previous coordinates on touchstart;

 movement below approximately 10 local CSS px remains a tap candidate;

 movement above threshold becomes remote scrolling;

 tap emits left mousePressed then mouseReleased;

 scroll emits mouseWheel;

 convert drag delta through the same remote/local scale used for mouse coordinates;

 finger up means page scroll in the opposite direction, matching ordinary touchscreen behavior;

 call preventDefault() during remote one-finger scrolling;

 clear state on touchcancel;

 cancel the mouse-emulation gesture if a second touch appears;

 leave pinch behavior local for v1 rather than pretending it is a remote gesture.

This is the same high-level gesture split proven by browserface and noVNC, but implement it independently. 
GitHub

Acceptance check

On a real phone or mobile-browser automation surface:

 tap each of five remote test buttons and assert the intended ID receives the click;

 drag upward 200 px and assert remote scrollY increases;

 drag downward and assert it decreases;

 perform a 5 px movement and assert it remains a click, not scroll;

 initiate two touches and assert no remote click is accidentally emitted;

 assert the DSH page itself does not scroll while the gesture is classified as remote scroll.

Failure prevented

Every phone gesture becoming a click, every drag scrolling the DSH GUI instead of Chrome, and accidental gestures during pinch.

Slice 14 — Mobile text entry

Build

 Add a local text-entry surface capable of summoning the phone's software keyboard.

 For the reliable first implementation, provide an explicit Type affordance while human ownership is active.

 Send committed local text through Input.insertText.

 Send Backspace, Enter, arrows and other controls through the key path.

 Preserve composition/IME text as committed text rather than manufacturing keycodes.

 Do not keep the keyboard helper focused after ownership is released.

Optional later enhancement:

 probe whether the touched remote element is editable on touchstart;

 use that early probe to decide whether to focus the local keyboard helper during the same user gesture;

 do not make this asynchronous convenience path a prerequisite for v1.

Browserbase explicitly documents mobile Live View keyboard handling as a separate concern rather than something video streaming solves automatically. 
Browserbase Documentation

Acceptance check

 On the phone, tap a remote input.

 Open the local typing surface.

 Enter DSH Việt Nam 🙂.

 Assert the remote input's .value exactly equals DSH Việt Nam 🙂.

 Backspace one character and press Enter; assert the remote event log records both operations.

 Release ownership and assert further local typing generates zero CDP input.

Failure prevented

A pane that technically handles desktop keyboard events but is unusable from iOS/Android soft keyboards.

Phase E — recovery and lifecycle hardening
Slice 15 — Tab loss, browser restart and endpoint change

Build

 On Target.targetDestroyed for the selected tab:

stop screencast;

detach the page session;

clear the latest frame's live status;

revoke ownership;

leave selection empty.

 On browser-WebSocket disconnect:

increment connection generation;

revoke all leases;

cancel the target session;

broadcast disconnected;

start endpoint rediscovery.

 On reconnection, rebuild the target catalog from scratch.

 Do not restore a target by old numeric index.

 Do not assume an old target ID survives a browser restart.

 Require a new explicit tab selection if identity cannot be proven.

Acceptance check

Run one automated test sequence:

select tab B;

close B;

assert selected=null and lease absent;

select a newly opened tab;

kill Chrome;

restart its profile on a different port;

assert browser state reconnects;

assert fresh targets appear;

assert no input is accepted against the old generation/token.

Failure prevented

Driving a replacement tab using stale identity or stale authority after browser/session churn.

Slice 16 — Unmount, HMR and host teardown

Build

Client disposer must:

 close EventSource or abort pending long-poll;

 cancel reconnect/freshness timers;

 remove window/document listeners;

 cancel pointer/touch state;

 release held keys best-effort;

 release human lease best-effort;

 clear local frame references.

Host disposer must:

 cancel endpoint retry timers;

 unsubscribe browser/target events;

 stop screencast;

 detach target CDP session;

 close the CDP client without terminating the user's Chrome;

 revoke leases;

 unregister every route;

 end open SSE responses;

 clear client/subscriber sets.

 Add diagnostic counters for active stream clients, target sessions, screencasts, subscriptions and retry timers.

Acceptance check

 Record all diagnostic counters at baseline.

 Mount/unmount the pane 20 times; assert all counters return to baseline each cycle.

 HMR lib/client.js 20 times; assert there is still exactly one stream client and one set of document/window listeners.

 Restart dsh web; assert Chrome remains running.

 Assert old CDP and SSE connections disappear after the host exits.

Failure prevented

Each HMR adding another input dispatch, abandoned screencasts consuming resources, and plugin teardown killing the user's browser.

Slice 17 — End-to-end acceptance gate

Execute the full scenario without development-only input bypasses.

 Start dedicated-profile Chrome.

 Open at least two tabs.

 Load DSH desktop UI.

 Assert both tabs appear by target ID.

 Select tab A.

 Assert live frame progression.

 Assert pane begins read-only.

 Acquire automation ownership.

 Assert human takeover is rejected and observation continues.

 Release automation.

 Acquire human ownership.

 Run the complete coordinate matrix from Slice 8.

 Click a remote control.

 Drag.

 Scroll.

 Type text.

 Release ownership.

 Assert further input is rejected.

 Close tab A and verify honest closed state.

 Kill Chrome and verify stale/disconnected overlay.

 Restart Chrome on a different debug port.

 Verify endpoint rediscovery and new target list.

 Open the same DSH surface on the phone.

 Acquire human ownership.

 Verify tap, scroll and exact Unicode text entry.

 Release ownership.

 Run the 20× mount/HMR leak check.

 Assert zero leaked screencasts, CDP target sessions, input leases or event subscribers.

Failure prevented

Passing isolated unit tests while the actual DSH + Chrome + phone + automation system remains unsafe or misleading.

Decisions still requiring you

Reuse strategy: fork the ISC-licensed DSH browser plugin and remove what you do not need, or build a smaller plugin around chrome-remote-interface. I would fork/reference its lifecycle but keep your own narrow state/ownership model.

Automation ownership integration: whether CUA/other automated drivers can be changed to acquire the same per-target lease. This determines whether mutual exclusion can be guaranteed rather than merely requested.

Endpoint policy: fixed debug port as a fallback versus making the dedicated profile's DevToolsActivePort the normal authority. Your restart/port-change requirement favors the latter.

Background-tab policy: never activate a selected tab automatically, or allow an explicit human-owner-only “Activate tab” action when Chrome stops compositing a background tab.

Phone keyboard UX: ship the explicit reliable Type control first, or spend the extra work on seamless tap-an-input → software-keyboard behavior.

Frame budget: JPEG quality/FPS ceiling for phone use. Keep it configurable; do not make coordinate correctness depend on resolution.

Transport: authenticated exact-route SSE if DSH's fetch route really streams; otherwise authenticated long-poll. That should be decided by Slice 4's executable probe, not by design assumption.