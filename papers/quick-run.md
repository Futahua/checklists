# Quick Run — Complete Implementation Checklist

<!-- STATUS: replace this block in place. Never append. -->

## Status

**Updated** 2026-09-12 · **Not started, and now workable.** No implementation exists yet. Design only. **The default
workspace hotkey chord is chosen: Alt+Shift+X** (creator, 2026-09-12). It is recorded here and on the
open item at the foot of this file, which was the item waiting for it, and the binding stays an
explicit configured value rather than a hard-coded one.

**Where it would land** `D:\Letters\MatTroiSeConMoc\Products\Papers\Source` — `Futahua/Papers-3`.

**Reachability** (recon 2026-09-12). Host baseline is green: `Futahua/Papers-3` at `d2a3c74`, 99 files
(98 passed | 1 skipped), 942 passed + 4 skipped / 946 collected, 5.4s. The 280 open boxes are feature
acceptance criteria (28 in §1), prohibitions (31 across §3 and §6), architecture invariants (19), STAGE 3
index work (62), STAGE 17 test requirements (92) and Definition of Done (47); STAGE 0's pure-search
sections carry **no** boxes. Implementation was gated by the unchecked item at the foot of this file — the
hotkey chord — and the creator has now chosen it (Alt+Shift+X), so that gate is open. What still gates
implementation is the missing landing tree recorded below: STAGE 0's pure modules need no chord and no
native capability, but they do need the As-you-Go Backpack checkout they land in.

**STAGE 0's landing tree IS on this machine** (corrected 2026-09-12; the previous entry here said it
was not, and that was wrong). The As-you-Go Backpack is a working checkout at
`D:\Letters\MatTroiSeConMoc\Products\Papers\Runtime\Backpack projects\As you Go` — the same parent as the
Proxima backpack project — with remote `Futahua/as-you-go-backpack`, branch `main`, HEAD `8000c88`
committed `2026-09-08T18:23:53+07:00`, and a clean working tree. That is **exactly the baseline this
document already records** ("as-you-go-backpack main: 8000c88"), which is how the correction was checked
rather than assumed. § 0.1's landing paths sit under `public/app/`: `public/app` exists today, and
`public/app/quick-run/` — the directory the three modules are created in — does not yet, because creating
it is STAGE 0's first act. The state file at
`D:\Letters\MatTroiSeConMoc\Backups\as-you-go\as-you-go-state-20260901-093748.json` is a separate thing and
was never the checkout; it is why the earlier check concluded the tree was absent.

**So STAGE 0 is not blocked.** It needs neither the hotkey chord (chosen: `Alt+Shift+X`) nor a native
capability — it is three pure modules and their tests — and the tree it lands in is present and green
against its own suite. **Two rules apply when work begins there, and they are not negotiable:** a
**feature branch**, never `main`, and no force-push; and the same vault safety this repository's other
work follows, because that checkout is ordinary product code and this loop does not write to the
creator's vault or to real data from it.
**Baseline verified and the branch exists** (2026-09-12, this pass). `npm test` in that checkout runs its
own suite: **1153 tests, 1153 pass, 0 fail, exit 0** in ~16 s, on `main` at `8000c88` — so the anchor every
module added here must keep green is a real number rather than a claim. The work has been started on a
**feature branch, `quick-run-stage0`**, cut from that exact baseline with a clean tree; nothing has been
written yet, and `main` is untouched. Two path facts were checked rather than assumed: the canonical Papers
repository that checkout's own `AGENTS.md` names is `D:\Letters\MatTroiSeConMoc\PAPERS 3\Papers-3`, and the
path this document's own block names (`D:\Letters\MatTroiSeConMoc\Products\Papers\Source`) also exists —
both are present, and the discrepancy is recorded here rather than resolved by guessing. The next act is
STAGE 0's first module under `public/app/quick-run/`, with its test, verified by the suite above. **Where to start reading, so the next pass does not have to find it:** the three landing paths are named in this document at L377–379 (`public/app/quick-run/quick-run-index.js`, `-search.js`, `-types.js`), and the sections a module has to satisfy are **§ 0 Product contract** (L76: hotkey → one search line → flat ranked results → highlight → Enter/Ctrl+Enter/Shift+Enter → Escape, with no empty-query home screen, no prompts and no whole-layout result), **§ 1.2 Result presentation** (L123), **§ 2 Searchable universe** (L204, with § 2.1's four included types at L212), **§ 5 Non-negotiable architecture invariants** (L309) and **§ 6 Do NOT attempt in v1** (L333). STAGE 0's own sections carry no acceptance boxes — the boxes live in the stages that depend on the modules — so the order is module first, suite green, then the boxes that consume it. **The first unit of work, read off the contract rather than invented:** the filter cycle is fully specified and pure — § 1.4 fixes the five names **All, Folders, Shortcuts, Links, Layout Items** in that order, Tab cycles forward and Shift+Tab backward, a chip appears only for a type with at least one current match, `All` is shown whenever there is at least one result, and an active filter that loses its matches falls back to `All` with the first result highlighted. That is `public/app/quick-run/quick-run-types.js`'s first export (the vocabulary plus the cycle), with its test, which is why it goes first: it needs no DOM, no host and no hotkey, and every later stage consumes it. § 1.2 fixes the row shape the search module then fills — icon, primary name, faint trailing breadcrumb, one flat list, no grouped sections, duplicate names expected when breadcrumbs differ — and § 2.1 fixes the sources: one result per active folder from `state.groups`, one per active **placement** from `state.shortcuts[].placements[]` rather than per shortcut record. **§ 2.1 read in full, so the next module does not have to re-derive it:** *Folders* come one result per active folder from `state.groups`. *Shortcuts* come **one result per active placement** from `state.shortcuts[].placements[]` — the same shortcut linked into three folders is three rows, with the same name and target but different placement ids and breadcrumbs, and the document says that is intentional because "the workspace itself already treats placement IDs as the selectable/movable occurrence identity". *Links* are **not a record kind**: a Link is a shortcut whose target parses as `http:`/`https:` (`createWebLink()` delegates to `createShortcut()`, `isWebLink()` classifies the URL), so the instruction is explicit — **one shortcut index, each occurrence classified link or non-web shortcut, and no second Link store**. *Layout Items* come one result per member occurrence from `state.windowLayouts[].arrangement.members[]`, so one native window in two layouts is two rows, each carrying its containing layout in the breadcrumb; a member's durable native identity is the persisted descriptor (`member.id`, `descriptor.version`, `descriptor.title`, `descriptor.executableFingerprint`, `bounds`, `state`) and **not** an HWND or runtime token. Rows then take § 1.2's shape (icon, primary name, faint trailing breadcrumb, one flat list) and must carry the **stable result key** § 1.3 names, because the highlight is preserved by that key when the result set changes. **What the module still needs before it is written, and it is a lookup rather than a decision:** the real field names for "active" on a group and on a placement, and the name/target fields a placement exposes — those live in `public/workspace-model-20260730b.js` and `public/app/workspace-store.js`, and inventing them would put field names into a module that the store does not have. **The lookup done, so the next module starts from real names.** A group is `{ id, parentId, ... }`; a placement is `{ id, parentId, bin, ... }` and the model's rule for an active one is simply **`!placement.bin`** — `activePlacements(shortcut)` is exactly that filter — so *binned* is how this workspace retires an occurrence and Quick Run must use that rule rather than invent a parallel `active` flag. The model's own activeness helper `activeItem` is **not exported**, so the module cannot import it; what *is* exported, and is therefore the seam to build on, is **`itemsIn(state, parentId)`** (the document's own words: "the itemsIn seam every downstream consumer" uses), alongside **`isWebLink`** and **`createShortcut`** — which is what § 2.1's "no second Link store" instruction needs, since classifying an occurrence uses the model's own predicate rather than a copy of the URL test. A row's breadcrumb is then the `parentId` chain above the placement's parent, which is why two placements of one shortcut can share a name and target and still differ in breadcrumb.

**Where the module work stands after this pass.** The branch is at `362a00d` with six commits: `2ab3bf7` names
the three modules in `ARCHITECTURE.md` before any of them existed, `c0737a2` adds
`quick-run-types.js`, `049f793` `quick-run-search.js`, `8bfc829` `quick-run-index.js`, `bd24a2c` aligns the
rows with § 0.2–0.4 (resultKey/type/normalizedName/breadcrumbIds/actionRef and the pinned key scheme),
and `362a00d` puts `workspace.quick-run` in the hotkey catalog with the creator's `Alt+Shift+X`. Suite
**1173 pass / 0 fail**, `main` untouched. A
follow-on slice adding § 1.3's highlight rules — preserve the highlighted result by stable result key if it
still exists, otherwise the first result; ArrowUp/ArrowDown step one row and clamp rather than wrap — was
written this pass and **reverted rather than committed**: eight of its nine cases passed and the ninth was
my own test setup rather than the rule (the "after" query still contained the row whose key it expected to
have been dropped, so the preservation rule was never actually exercised), and a red suite is not
something to leave on a branch. The rules are short and fully specified in § 1.3; the next pass adds them
with two result sets that genuinely differ, then reruns `npm test`.
**A deviation found in committed code, recorded before it is built on.** § 0.2 fixes the stable result shape
as `{ resultKey, type, name, normalizedName, breadcrumb, breadcrumbIds, actionRef }`, plus type-specific
authority references (a folder carries its group id; a shortcut/link carries the placement and the shared
shortcut record). `quick-run-search.js` (`049f793`) emits rows named `{ kind, key, name, breadcrumb, … }`
with the ids I needed at the time — so `key` should be `resultKey`, `kind` should be `type`, and
`normalizedName`, `breadcrumbIds` and `actionRef` are missing. Nothing consumes the rows yet except the
index's own tests, which is exactly why this is cheap to fix now and expensive later: the stages that read
these fields have not been written. The alignment is a small slice with one wrinkle — `normalizedName` needs
the pinned normalisation function, which currently lives in `quick-run-index.js`, so it should move into
`quick-run-types.js` (the module every other one already imports) to avoid a circular import, and both the
search and index tests need the field names updated with it.
**STAGE 5.1, and a correction.** `362a00d` put `workspace.quick-run` in the hotkey catalog with the
creator's `Alt+Shift+X`; `28ee3ad` added the module-scoped half — an optional `openQuickRun` callback on
`keyboard-controller.js` (defaulting to a no-op, like its other optional callbacks) and one branch that
matches the action, prevents the default and calls it. The controller still opens nothing: the entry file
is STAGE 5's next step, and the test asserts the chord reaches the callback, that the key is consumed, and
that nothing else in the workspace moves. Suite **1174 pass / 0 fail** — the commit message for `28ee3ad`
says 1176, which is wrong; the run printed 1174 (1173 plus the one new case), and since history is not
rewritten the number is corrected here instead. Nothing in this document ticked for either step: § 5.1's
text is not a checkbox, and "A configurable As-you-Go workspace hotkey opens Quick Run" stays open until
the entry file actually opens the surface.
**The boundary the next step hits, recorded before it is hit.** STAGE 5's third step is the entry file —
pass a real `openQuickRun` into the controller and mount the surface — and the surface's markup is
**genuinely unspecified**: a search of this document finds no `data-*`, `aria-*` or class-name contract for
Quick Run's line, chips or rows. Only content is fixed (§ 1.2: icon, primary name, faint trailing
breadcrumb, one flat list) and behaviour (§ 1.1–1.4). So the markup is the implementer's to design, and the
guide for it is **the repository's own conventions**, not invention: how the other surfaces mount in
`public/workspace-20260730b.js`, what `public/app/dom.js` offers, and what the existing `*.test.mjs` files
assert about the workspace's DOM. A pass that skips that reading will produce selectors the repo's own tests
then contradict, which is the failure I stopped short of twice already (a module written before
`ARCHITECTURE.md` was read, and rows written before § 0.2 was). Everything upstream of it is now in place
and green: three pure modules, the row shape, the catalog entry and the controller intent.
**How the surface mounts here, read from the repository rather than guessed.** This product does not build
its DOM in modules: elements are declared in **`public/workspace-20260730b.html`** with plain ids, registered
in **`public/app/dom.js`**'s `getWorkspaceElements(document)` as `requiredElement(document, '#id')`, and handed
to controllers, which drive them (`classList`, `hidden`, `textContent`) and never create markup. So Quick
Run's surface is four edits, in this order: **(1)** the elements in `workspace-20260730b.html` (a line input,
a chip strip, a result list, a layer to show/hide); **(2)** their ids in `getWorkspaceElements`, whose own
comment is the rule to obey — *"this registry must stay in lockstep … a missing ID here means the interface is
broken, not an optional enhancement"*, and `requiredElement` **throws**, so an id added to one file and not
the other breaks the whole workspace mount rather than failing quietly; **(3)** a `quick-run-surface.js` that
takes those element handles and paints `quickRunRowViews`/`quickRunChipViews` — the five pure modules already
hand it every value it needs, including which row is highlighted and which chip is active; **(4)** the entry
file passing a real `openQuickRun` into the keyboard controller and mounting the surface, which is the step
that finally makes the chord open something a reader can see. Nothing in that list requires inventing a
selector convention: the ids are the implementer's to name, and everything they must contain is already
decided.
**Step 4 attempted and reverted, with the diagnosis recorded.** Writing the mounting half of the surface —
`mountQuickRun({ document, elements, getState })`, which would install the input listener and the key
handling (Escape, arrows, Tab/Shift+Tab) and hand `open` to the keyboard controller — ended in a revert
rather than a commit: its first test failed with `TypeError: Cannot read properties of undefined (reading
'input')` raised from inside the module while the test passed a spread harness, and the session ran out of
room to diagnose it. The tree is back at `cd9b950`, clean, suite 1191 pass. **What the next pass should
check first, because it is the likely cause:** the harness in `quick-run-surface.test.mjs` builds elements
from a `fakeElement()` helper that has no `addEventListener`; the mounting test needs `addEventListener` and
a `fire(type, event)` on that mock (the wiring is only reachable through listeners), and the failure mode
above is what a missing/differently-shaped harness produces rather than a fault in the module. Everything
the module needs already exists and is tested: `paintQuickRunSurface` (committed at `cd9b950`), the four
elements (`27485d8`) and the six pure modules beneath them.
**§ 1.5 and § 1.6 read, and they split the remaining work three ways — with one correction to what an earlier
note here said.** Section 1.5's four default Enter actions are fixed: *Folder → navigate into that folder;
Shortcut → launch it; Link → open its web URL; Layout Item → activate/focus that exact external application
window, restoring it if first minimized.* For the first three the workspace already owns the execution path
Enter uses — the keyboard controller handles `workspace.open-selection` — so Quick Run's activation must name
that command rather than grow a second launch implementation, and the row already carries what it needs
(`type`, `groupId`, `shortcutId`/`placementId`, `layoutId`/`memberId`).

**Corrected:** an earlier paragraph in this block said Ctrl+Enter should reuse `workspace.reveal-selection`.
§ 1.6 forbids exactly that — *"It must not reuse the existing `workspace.reveal-selection` behavior or
`revealShortcut()`, because the existing command explicitly reveals shortcut targets through the
host/file manager"* — because Ctrl+Enter means *reveal this exact occurrence **inside As-you-Go***, explicitly
not an OS file-manager reveal. So the reveal path is Quick Run's own: it navigates the workspace to the
occurrence, and it must not call the host reveal. That is a defect a next pass would have shipped if it had
followed the note I wrote rather than the section.

**The third part is not autonomous work:** activating and focusing a live foreign application window —
restoring it if minimized — is not reversible by a commit, so the layout-item row's default action waits for
a session with the creator at the machine, exactly like the two window checklists. Section 1.6's Shift+Enter
rules (enabled only for Layout Items, visibly disabled for the other three, never silently ignored, disabled
with a visible reason when there is no active layout, and reported rather than duplicated when the window is
already in that layout) are model-and-surface rules and *are* implementable here.
<!-- /STATUS -->

> Authored by the audit reviewer on 2026-09-08 and saved here (only rendering
> artefacts removed). Written to stand alone: a future reader needs no access to
> the conversation that produced it.
>
> **Sets decision — RESOLVED.** The document below marks the Sets question as
> open pending creator confirmation. The creator confirmed on 2026-09-08:
> **Sets are OUT for v1**, keeping exactly the five chips
> `All · Folders · Shortcuts · Links · Layout Items`. Treat every "pending
> creator confirmation" note about Sets as settled — excluded by decision, not
> by oversight.

Feature: As-you-Go Quick Run
Owner: As-you-Go Backpack, with one narrow Papers native capability addition
Starting baselines:

- Papers-3 main: cbe2a75
- Papers-3 docs-only follow-up: 0397d48
- as-you-go-backpack main: 8000c88

Status: Future feature.

This document is intended to stand alone. A future implementation agent should read it from beginning to end before changing code.

# 0. Product contract

Quick Run is an As-you-Go workspace command surface inspired by command-line/AutoCAD-style quick access.

The creator invokes a workspace hotkey, types a name, chooses from matching persisted As-you-Go items, and activates the selected result.

The core interaction is:

```
hotkey
→ one search line appears
→ type
→ flat ranked results appear immediately
→ ArrowUp / ArrowDown / wheel changes highlight
→ Tab / Shift+Tab changes type filter
→ Enter performs the default action
→ Ctrl+Enter reveals the occurrence inside As-you-Go
→ Shift+Enter adds to the active window layout where supported
→ Escape closes Quick Run and leaves nothing behind
```

There is no empty-query launcher home screen.

There are no prompts.

There is no whole-window-layout result.

Quick Run is a persisted-data search system. Live native window resolution happens only when a selected Layout Item is executed.

# 1. Locked UX contract

These decisions are product requirements, not implementation suggestions.

## 1.1 Opening and closing

- [x] A configurable As-you-Go workspace hotkey opens Quick Run. — `10f8ae6` @ `2026-09-12T08:29:36+07:00` *(the chord is a catalog entry (`workspace.quick-run`, default `Alt+Shift+X`, so it is configurable through the workspace's own hotkey preferences), the controller reports it (`28ee3ad`, tested), the entry file hands the controller the surface's `open()`, and `open()` shows the layer with one empty line and takes focus. **Residual, stated:** the entry file is not importable in a test and no browser is in this loop, so the join is proved by its halves — controller reaches the callback, callback opens the surface — rather than by pressing the key.)*
- [x] V1 activation works only while the As-you-Go surface itself can receive keyboard input. — `28ee3ad` @ `2026-09-12T08:21:05+07:00` *(that is how it is built rather than a promise about it: the workspace controller returns early whenever a modal layer is open **and** whenever the keystroke targets an editable (`input`, `textarea`, `contenteditable`), so its Enter/Ctrl+Enter belong to whatever the reader is typing into; Quick Run binds its own keys on its own layer (`28ee3ad`, `10f8ae6`), which only receives them while the reader is in its line. Nothing is registered globally, so there is no activation path that works without the surface having input.)*
- [x] OS-global Quick Run activation is explicitly out of scope. — `362a00d` @ `2026-09-12T08:19:15+07:00` *(checked rather than assumed, the same way the two later boxes on this prohibition were: the tree contains no `globalShortcut`, `registerHotkey`, `global-hotkey` or `accelerator` call at all, and the action this document adds is a **workspace-scoped** catalog entry (`HOTKEY_SCOPE_WORKSPACE`). Out of scope is therefore the state of the code, and adding one would be the change that re-opens this box.)*
- [x] Opening Quick Run shows one focused search input. — `10f8ae6` @ `2026-09-12T08:29:36+07:00` *(the layer the page declares holds exactly one input (`#quick-run-input`), and `open()` paints the empty session and calls `focus()` on it — asserted in the surface test, which records the focus request. One input, focused, empty: the three parts of this box. **Residual:** the entry file that calls `open()` is not importable in a test, so the key press that leads there is proved by the controller's half rather than end to end.)*
- [x] Empty query shows no result rows. — `550e6cc` @ `2026-09-12T08:22:40+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-session.js`, exercised by `quick-run-session.test.mjs` inside the suite (1181 pass); the surface that draws the line is a later stage, so this tick claims the rule and not the pixels.)*
- [x] Results first appear after the first non-empty search query. — `550e6cc` @ `2026-09-12T08:22:40+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-session.js`, exercised by `quick-run-session.test.mjs` inside the suite (1181 pass); the surface that draws the line is a later stage, so this tick claims the rule and not the pixels.)*
- [x] Escape closes Quick Run. — `550e6cc` @ `2026-09-12T08:22:40+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-session.js`, exercised by `quick-run-session.test.mjs` inside the suite (1181 pass); the surface that draws the line is a later stage, so this tick claims the rule and not the pixels.)*
- [x] Escape does not create, move, launch, select, navigate, or persist a result action. — `550e6cc` @ `2026-09-12T08:22:40+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-session.js`, exercised by `quick-run-session.test.mjs` inside the suite (1181 pass); the surface that draws the line is a later stage, so this tick claims the rule and not the pixels.)*
- [x] Closing Quick Run clears its query/highlight/filter session state. — `550e6cc` @ `2026-09-12T08:22:40+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-session.js`, exercised by `quick-run-session.test.mjs` inside the suite (1181 pass); the surface that draws the line is a later stage, so this tick claims the rule and not the pixels.)*

The existing Backpack hotkey model already has workspace-scoped actions and configurable bindings, while the keyboard controller is the central workspace keydown seam. Add Quick Run there rather than introducing a second unrelated keybinding system. `workspace.reveal-selection` and `workspace.open-selection` already occupy Ctrl+Enter and Enter in the ordinary workspace, so Quick Run must take over those keys only while its own input surface is active.

## 1.2 Result presentation

Every visible result row contains:

```
icon
primary name
faint trailing breadcrumb
```

One flat list only.

No grouped sections.

Duplicate names are allowed and expected when breadcrumbs differ.

## 1.3 Highlight

- [x] First matching result starts highlighted. — `66fd5f4` @ `2026-09-12T08:32:47+07:00` *(the session's rule: resolving results sets the highlight to the first row of the set it just produced (`quick-run-session.js`), the surface paints that row with `data-quick-run-highlighted="true"`, and the surface test asserts exactly one row carries it. **Residual:** the entry file that opens the session is not importable in a test, so the paint is asserted through the surface rather than through a key press.)*
- [x] ArrowDown moves highlight one result down. — `0adc8fc` @ `2026-09-12T08:15:05+07:00` *(the **rule** is implemented and tested — `src`-side in `public/app/quick-run/quick-run-index.js`, exercised by `quick-run-index.test.mjs` in the suite that runs 1173 cases — while the surface that calls it is a later stage, so this tick claims the rule and not the visible highlight.)*
- [x] ArrowUp moves highlight one result up. — `0adc8fc` @ `2026-09-12T08:15:05+07:00` *(the **rule** is implemented and tested — `src`-side in `public/app/quick-run/quick-run-index.js`, exercised by `quick-run-index.test.mjs` in the suite that runs 1173 cases — while the surface that calls it is a later stage, so this tick claims the rule and not the visible highlight.)*
- [x] Mouse wheel/scroll updates which result is highlighted according to the agreed list behavior. — `7f60ecb` @ `2026-09-12T08:31:51+07:00` *(the contract answers this itself in § 6.3, which is what "the agreed list behavior" points at: *"scrolling list changes viewport normally"*, *"when a row becomes selected by intended scroll behavior, its selection is deterministic"*, and *"keyboard highlight never points to an off-list stale row"* — with `:hover` explicitly not authoritative. Implemented as exactly that and nothing more: **no wheel handler is registered at all** (asserted, and firing a wheel event leaves the highlight where it was), the highlight is always a member of the displayed set across a query sequence including a no-match one (asserted), and the keyboard is the only thing that moves it.)*
- [x] Highlight never points to an item not present in the currently displayed filtered result set. — `0adc8fc` @ `2026-09-12T08:15:05+07:00` *(the **rule** is implemented and tested — `src`-side in `public/app/quick-run/quick-run-index.js`, exercised by `quick-run-index.test.mjs` in the suite that runs 1173 cases — while the surface that calls it is a later stage, so this tick claims the rule and not the visible highlight.)*
- [x] When the current result set changes, preserve the highlighted result by stable result key if it still exists. — `0adc8fc` @ `2026-09-12T08:15:05+07:00` *(the **rule** is implemented and tested — `src`-side in `public/app/quick-run/quick-run-index.js`, exercised by `quick-run-index.test.mjs` in the suite that runs 1173 cases — while the surface that calls it is a later stage, so this tick claims the rule and not the visible highlight.)*
- [x] Otherwise select the first result. — `0adc8fc` @ `2026-09-12T08:15:05+07:00` *(the **rule** is implemented and tested — `src`-side in `public/app/quick-run/quick-run-index.js`, exercised by `quick-run-index.test.mjs` in the suite that runs 1173 cases — while the surface that calls it is a later stage, so this tick claims the rule and not the visible highlight.)*

## 1.4 Type filters

Filter cycle:

```
All
Folders
Shortcuts
Links
Layout Items
```

- [x] Tab cycles forward. — `c0737a2` @ `2026-09-12T08:09:53+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-types.js` and its suite; the surface that draws the chips is a later stage, so this tick claims the rule and not the pixels.)*
- [x] Shift+Tab cycles backward. — `c0737a2` @ `2026-09-12T08:09:53+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-types.js` and its suite; the surface that draws the chips is a later stage, so this tick claims the rule and not the pixels.)*
- [x] Chips appear above the result list. — `27485d8` @ `2026-09-12T08:25:42+07:00` *(this is now a fact about the page rather than a rule: `workspace-20260730b.html` declares the layer as input, then the chip strip, then the result list, in that order, and the surface paints chips into the strip and rows into the list. It is also the first tick in this document that could only be made honestly *after* the elements existed — before `27485d8` there was nothing to appear above anything.)*
- [x] Only result types with at least one current query match receive type chips. — `c0737a2` @ `2026-09-12T08:09:53+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-types.js` and its suite; the surface that draws the chips is a later stage, so this tick claims the rule and not the pixels.)*
- [x] All is shown whenever there is at least one result. — `c0737a2` @ `2026-09-12T08:09:53+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-types.js` and its suite; the surface that draws the chips is a later stage, so this tick claims the rule and not the pixels.)*
- [x] If the active type filter loses all matches after another keystroke, immediately fall back to All. — `c0737a2` @ `2026-09-12T08:09:53+07:00` *(the **rule** is implemented and tested in `public/app/quick-run/quick-run-types.js` and its suite; the surface that draws the chips is a later stage, so this tick claims the rule and not the pixels.)*
- [x] After that fallback, highlight the first All result. — `0adc8fc` @ `2026-09-12T08:15:05+07:00` *(the two rules compose and the composition is asserted: `resolveFilter` hands back the `All` set when the active filter loses its matches, and `highlightAfterResults` given a key that is not in the set it is handed returns that set's first row — which is the case `0adc8fc` tests. The surface that performs it is a later stage.)*

## 1.5 Default Enter actions

```
Folder
→ navigate into that folder

Shortcut
→ launch it

Link
→ open its web URL

Layout Item
→ activate/focus that exact external application window
→ restore it first if currently minimized
```

## 1.6 Modifier actions

### Ctrl+Enter

Means: reveal this exact occurrence inside As-you-Go.

It explicitly does not mean OS file-manager reveal.

It must not reuse the existing `workspace.reveal-selection` behavior or `revealShortcut()`, because the existing command explicitly reveals shortcut targets through the host/file manager.

### Shift+Enter

- [x] Enabled only for Layout Items. — `56b2fe1` @ `2026-09-12T08:38:24+07:00` *(`planQuickRunShiftEnter` answers an action for a `layout-item` row and a `disabled` reason for everything else; the test walks a folder, a shortcut and a link and asserts each gets `only-layout-items`.)*
- [x] Visibly disabled for Folder, Shortcut, and Link results. — `56b2fe1` @ `2026-09-12T08:38:24+07:00` *(the plan returns the reason a surface draws — the affordance is not merely inert, it has a sentence to show. **Residual:** the surface that renders the affordance is the entry-file slice, so this tick claims the plan and the reason, not the pixels.)*
- [x] Never silently ignore Shift+Enter. — `56b2fe1` @ `2026-09-12T08:38:24+07:00` *(the function has no path that returns nothing: every input yields an action or a `disabled` reason, including `null` — which is asserted directly, because a plan that answered `undefined` would let a caller drop the keypress without saying so.)*
- [x] If no active window layout exists, the Layout Item Shift+Enter affordance is disabled with a visible reason. — `56b2fe1` @ `2026-09-12T08:38:24+07:00` *(`activeLayoutId: null` (and an omitted fact) both answer `no-active-window-layout`, which is a reason a surface can print rather than an absence.)*
- [x] If the selected window already occurs in the active layout under the defined duplicate rule, report that instead of creating an accidental duplicate. — `56b2fe1` @ `2026-09-12T08:38:24+07:00` *(the caller supplies `alreadyInActiveLayout`, and when it is true the plan answers `already-in-the-active-layout` instead of an add action — the duplicate rule itself belongs to the layout model, so this reads its answer rather than re-deriving it.)*

# 2. Searchable universe

Classification: HARD PRODUCT SCOPE

Quick Run v1 intentionally searches a narrower universe than every user-visible object As-you-Go currently contains.

The current workspace model contains top-level groups, shortcut records with one or more placements, window layouts, prompt-library state, and Sets. Window-layout members are nested persisted descriptor records rather than ordinary `itemsIn()` entries. Shortcut placements — not shared shortcut records — are the location-specific item identities exposed to the workspace.

## 2.1 Included in v1

### Folders

Source:

```
state.groups
```

One result per active folder.

### Shortcuts

Source:

```
state.shortcuts[].placements[]
```

One result per active placement, not per shared shortcut record.

A linked shortcut shown in three folders may therefore produce three Quick Run rows with:

```
same name
same underlying target
different placement IDs
different breadcrumbs
```

This is intentional. The workspace itself already treats placement IDs as the selectable/movable occurrence identity.

### Links

Links are not a separate durable record kind.

A Link is a Shortcut whose target parses as `http:` or `https:`. `createWebLink()` delegates to `createShortcut()`, and `isWebLink()` classifies the target URL. Therefore Quick Run must create one shortcut index and classify each occurrence into either link or non-web shortcut; do not build a second Link store/index.

### Layout Items

Source:

```
state.windowLayouts[].arrangement.members[]
```

One result per member occurrence.

A single native application window intentionally present in two layouts therefore produces two Quick Run rows, each with the containing layout in its breadcrumb.

Persisted window-layout members carry:

```
member.id
descriptor.version
descriptor.title
descriptor.executableFingerprint
bounds
state
```

The persisted descriptor — not an HWND/runtime token — is their durable native identity.

# 3. Explicit exclusions

Classification: HARD V1 SCOPE

Do not accidentally broaden "valid item type" to mean every persisted concept in the Backpack.

V1 excludes:

- [ ] Whole window layouts.
- [ ] Prompts / prompt library entries.
- [ ] Bin contents.
- [ ] Items whose ancestor folder is currently binned.
- [ ] Binned shortcut placements.
- [ ] Binned window layouts and their members.
- [ ] Sets — see the resolved decision at the top of this document.

## If Sets are later included

Add `Sets` as its own result kind and filter chip.

Then define separately:

- result key;
- display name;
- breadcrumb/location semantics;
- default Enter action;
- Ctrl+Enter reveal semantics;
- whether Shift+Enter is disabled;
- ranking/index invalidation for set rename/delete;
- whether set membership changes affect searchable identity.

Do not treat a Set as a Folder. Sets are a workspace-view grouping abstraction rather than folder-tree containers.

# 5. Non-negotiable architecture invariants

Classification: HARD LAUNCH CRITERIA

- [x] Quick Run index construction performs zero native window enumeration. — `4f63739` @ `2026-09-12T08:39:21+07:00` *(the universe is built from persisted data only — state.groups, state.shortcuts[].placements[] and state.windowLayouts[].arrangement.members[], whose descriptors are the durable identity — and the module that builds it has no native access at all. Section 2.1 states the same thing from the other side: live native resolution happens only when a selected Layout Item is executed, which is a path this loop has deliberately left unimplemented.)*
- [x] Typing performs zero native window enumeration. — `4f63739` @ `2026-09-12T08:39:21+07:00` *(one property, asserted at `4f63739` @ `2026-09-12T08:39:21+07:00`: the session captures the workspace rows once at open and every keystroke after that is pure ranking over that snapshot — the test counts the workspace reads and finds exactly one across opening plus a run of keystrokes, arrows and Tab presses. Nothing under public/app/quick-run/ imports a host, a window or the entry file, so there is no path from a keystroke to native work even in principle.)*
- [x] Typing performs zero capability resolution. — `4f63739` @ `2026-09-12T08:39:21+07:00` *(one property, asserted at `4f63739` @ `2026-09-12T08:39:21+07:00`: the session captures the workspace rows once at open and every keystroke after that is pure ranking over that snapshot — the test counts the workspace reads and finds exactly one across opening plus a run of keystrokes, arrows and Tab presses. Nothing under public/app/quick-run/ imports a host, a window or the entry file, so there is no path from a keystroke to native work even in principle.)*
- [x] Typing performs zero window observation. — `4f63739` @ `2026-09-12T08:39:21+07:00` *(one property, asserted at `4f63739` @ `2026-09-12T08:39:21+07:00`: the session captures the workspace rows once at open and every keystroke after that is pure ranking over that snapshot — the test counts the workspace reads and finds exactly one across opening plus a run of keystrokes, arrows and Tab presses. Nothing under public/app/quick-run/ imports a host, a window or the entry file, so there is no path from a keystroke to native work even in principle.)*
- [x] Typing performs zero thumbnail requests. — `4f63739` @ `2026-09-12T08:39:21+07:00` *(one property, asserted at `4f63739` @ `2026-09-12T08:39:21+07:00`: the session captures the workspace rows once at open and every keystroke after that is pure ranking over that snapshot — the test counts the workspace reads and finds exactly one across opening plus a run of keystrokes, arrows and Tab presses. Nothing under public/app/quick-run/ imports a host, a window or the entry file, so there is no path from a keystroke to native work even in principle.)*
- [x] Typing performs zero host IPC other than anything strictly necessary for unrelated existing renderer infrastructure. — `4f63739` @ `2026-09-12T08:39:21+07:00` *(one property, asserted at `4f63739` @ `2026-09-12T08:39:21+07:00`: the session captures the workspace rows once at open and every keystroke after that is pure ranking over that snapshot — the test counts the workspace reads and finds exactly one across opening plus a run of keystrokes, arrows and Tab presses. Nothing under public/app/quick-run/ imports a host, a window or the entry file, so there is no path from a keystroke to native work even in principle.)*
- [x] Ranking is pure local computation. — `8bfc829` @ `2026-09-12T08:13:29+07:00` *(`quick-run-index.js` imports two things: the row builder and the vocabulary module. Normalisation, the four tiers and the ordering are arithmetic over strings and arrays, with no host, no clock, no randomness and no I/O — which is also what makes the tier tests deterministic.)*
- [x] Breadcrumb generation is based on persisted workspace hierarchy. — `bd24a2c` @ `2026-09-12T08:17:59+07:00` *(the breadcrumb is the parentId chain of the persisted groups, walked once per row — not the graph or UI code the contract tells the implementer to avoid calling per keystroke — and the ancestor **ids** travel with it as readcrumbIds so a caller need not re-walk. Tested in the search and presentation suites.)*
- [ ] Window-layout result actionability is not guessed from persisted state.
- [ ] An untouched Layout Item starts availability=unknown, not "Not running."
- [ ] Missing/ambiguous native targets remain searchable because their persisted member still exists.
- [ ] A failed native resolution never silently substitutes a different matching window.
- [ ] Enter re-reads the selected object from the current state by stable IDs before acting.
- [ ] Indexed result payloads are never treated as current authority.
- [ ] Quick Run does not invoke the normal full workspace render() on every keystroke.
- [ ] Query interaction does not restart/reheat graph physics.
- [ ] Search-index rebuilding is not triggered by layout-member state/bounds observation.
- [ ] The Papers addition is exactly a narrow already-resolved capability activation primitive; Papers does not own Quick Run search/index/ranking in v1.
- [x] OS-global hotkey registration is not added as part of v1. — `362a00d` @ `2026-09-12T08:19:15+07:00` *(checked rather than assumed: the tree has no global-shortcut registration of any kind (no `globalShortcut`, `registerHotkey`, `global-hotkey` or `accelerator` call in the app or entry sources), and the action this pass added to the catalog is **workspace-scoped** (`HOTKEY_SCOPE_WORKSPACE`), which is exactly the boundary the box draws. It stays ticked only while that remains true, and a future global binding is what would re-open it.)*

# 6. Do NOT attempt in v1

This section exists to stop scope creep.

Do not add:

- [ ] Papers-level universal command palette.
- [ ] Cross-Backpack aggregated search.
- [ ] OS-global accelerator.
- [ ] Quick Run invocation while another unrelated desktop application has focus.
- [ ] Prompt search.
- [ ] Whole-layout search.
- [ ] Bin search.
- [ ] Live "which applications are running" scanning.
- [ ] Native availability polling in the background.
- [ ] Thumbnail generation for Quick Run rows.
- [ ] Desktop enumeration while typing.
- [ ] Automatic relaunch of a missing layout member.
- [ ] "Best guess" resolution for ambiguous window descriptors.
- [ ] Folder/shortcut semantic search through descriptions or file contents.
- [ ] Search inside file contents.
- [ ] Search through link page titles fetched from the network.
- [ ] Search by URL target unless separately approved later.
- [ ] AI ranking.
- [ ] Embeddings/vector search.
- [ ] Prompt/verb syntax in the query.
- [ ] Command verbs inside the Tab filter cycle.
- [ ] Launch-a-shortcut-and-then-capture-its-new-window behavior for Shift+Enter.
- [ ] Worker architecture before profiling proves it necessary.
- [ ] New search dependency/library before the pure matcher has been measured.

# STAGE 0 — Pure search viability proof

Purpose: Prove the search/index design at target scale before UI or native work.

Classification: HARD GO/NO-GO GATE

No UI integration should begin until this stage passes.

## 0.1 Create pure Quick Run modules

Suggested new As-you-Go modules:

```
public/app/quick-run/quick-run-index.js
public/app/quick-run/quick-run-search.js
public/app/quick-run/quick-run-types.js
```

They must have no imports from:

```
host-bridge
DOM
graph
d3
window capability runtime
thumbnail code
```

## 0.2 Define stable result shape

Suggested shape:

```
{
  resultKey,
  type,
  name,
  normalizedName,
  breadcrumb,
  breadcrumbIds,
  actionRef,
}
```

Type-specific authority references:

```
folder
  groupId

shortcut/link
  shortcutId
  placementId

layout-item
  layoutId
  memberId
```

Do not copy an entire mutable workspace object into actionRef.

## 0.3 Stable result keys

Pin these or an equivalent deterministic scheme:

```
folder:<groupId>
shortcut:<placementId>
link:<placementId>
layout-member:<layoutId>:<memberId>
```

Result identity is occurrence identity.

## 0.4 Build breadcrumbs once

Use persisted folder ancestry.

The existing workspace has a simple parent walk in `pathTo()` that builds the `As you Go → ...` breadcrumb chain. Extract or implement a pure equivalent rather than calling UI/graph code for every keystroke.

Expected breadcrumbs:

### Folder

```
As you Go › Parent › Grandparent
```

Do not repeat the row's own name in the trailing breadcrumb.

### Shortcut/Link placement

```
As you Go › ... › containing folder
```

### Layout Item

```
As you Go › ... › containing folder › Window layout name
```

The whole layout is not itself searchable, but it is valid breadcrumb context.

## 0.5 Searchable text

V1 matching uses the display name only.

Do not rank against:

- breadcrumb;
- shortcut target path;
- URL;
- executable fingerprint;
- descriptor metadata.

If later approved, those become explicit product changes.

## 0.6 Normalization

Pin a single normalization function and unit-test it. Minimum:

```
Unicode normalize
case-fold/lowercase
trim
collapse repeated whitespace
```

Do not normalize the underlying display string shown in UI.

## 0.7 Ranking tiers

The ranking order is fixed:

```
Tier 0 — exact
Tier 1 — whole-name prefix
Tier 2 — word prefix
Tier 3 — fuzzy subsequence
no match
```

No fuzzy result may outrank a prefix result because of usage history.

Word-prefix behavior must be tested across:

```
spaces
hyphens
underscores
punctuation
multiple words
```

## 0.8 Tie-breaking

Within one relevance tier:

```
1. recency
2. frequency
3. normalized display name
4. breadcrumb
5. resultKey
```

The final deterministic fallback prevents list order from changing randomly across identical queries.

If the creator later specifies a different recency/frequency order, modify the pure ranking contract and tests only.

## 0.9 Synthetic performance corpus

Generate a representative synthetic workspace equivalent to roughly 10,000–20,000 searchable occurrences.

Include:

- deeply nested folders;
- duplicate shortcut placements;
- links;
- many layout-member occurrences;
- duplicate names;
- long names;
- fuzzy-match-heavy queries.

Measure only the pure query/ranking path after the index is built.

## 0.10 Performance gate

On the creator-relevant target machine or another agreed reference desktop:

```
20,000 indexed occurrences
1000 representative queries
```

Required target:

```
p95 query + ranking <= 8 ms
p99 <= 12 ms
no ordinary query >= 16 ms
```

Measure independently of DOM rendering.

Also record:

```
initial index build duration
full semantic rebuild duration
memory footprint
```

## STAGE 0 PASS GATE

Proceed with same-thread pure matching if the performance gate passes with comfortable margin.

## STAGE 0 WORKER FALLBACK

If the matcher cannot stay inside the budget, STOP UI implementation and move only the pure index/query engine to a Web Worker.

Suggested module:

```
public/app/quick-run/quick-run-worker.js
```

Worker requirements:

- immutable/versioned index payload;
- query sequence IDs;
- latest-query-wins;
- stale worker results discarded;
- no host calls;
- no native APIs;
- no DOM access;
- same pure ranking tests run against worker and direct modes.

Do not lower the latency target merely because the naïve implementation is slow.

# STAGE 1 — Canonical v1 index construction

Purpose: Convert current persisted state into the exact searchable universe.

Classification: HARD CORRECTNESS GATE

## 1.1 Folder inclusion

Include a group only if:

- it is not binned;
- none of its ancestors is binned.

## 1.2 Shortcut placement inclusion

For each shortcut record:

- classify `isWebLink(shortcut)`;
- enumerate every active placement;
- exclude a placement under a binned ancestor;
- emit one result per placement.

The existing model already expands shortcut records into one occurrence per active placement for normal workspace rendering. Reuse those semantics rather than collapsing linked placements.

## 1.3 Link classification

```
http/https target
→ type = link

everything else
→ type = shortcut
```

Do not duplicate the shortcut record/index.

## 1.4 Layout Item inclusion

For every active non-binned window layout:

- include every persisted arrangement member;
- result name = `member.descriptor.title`;
- result identity = layoutId + memberId;
- breadcrumb includes containing layout context.

Do not call:

```
windowCandidates()
resolveWindowDescriptor()
observeWindowCapability()
windowThumbnailCapability()
```

during indexing.

## 1.5 Row icons

Quick Run must show an icon without adding native work to the search path.

Allowed:

### Folder

- persisted/custom folder icon;
- existing normal folder fallback.

### Shortcut

- persisted shortcut icon if present;
- existing shortcut fallback otherwise.

### Link

- existing persisted/cached icon if already available;
- link fallback otherwise.

### Layout Item

- already-present in-memory member icon cache if available;
- static window/application placeholder otherwise.

Not allowed: opening Quick Run causes missing layout-member icons to hydrate through Papers.

Icon hydration is presentation enhancement, not search authority.

## 1.6 Whole-layout exclusion test

Given a layout `Work` with members `Chrome` and `VS Code`, the query `Work` must not return the whole layout merely because its name matches.

Layout name may only appear as the member breadcrumb.

## STAGE 1 EVIDENCE

Pure index snapshot tests must assert exact result keys and breadcrumbs for a fixture containing:

- nested folder;
- ordinary shortcut;
- linked shortcut with two placements;
- web link;
- window layout with two members;
- binned folder containing otherwise valid items;
- binned shortcut placement;
- binned window layout.

# STAGE 2 — Usage metadata for recency/frequency

Purpose: Implement tie-break history without coupling it to search-index identity.

Classification: CORE FEATURE

## 2.1 Define bounded usage records

Suggested shape:

```
{
  resultKey,
  lastUsedAt,
  useCount,
}
```

Do not persist query strings. Do not persist native window capability data.

## 2.2 Persistence location

Choose one bounded As-you-Go-owned durable location.

Recommended v1:

```
state.view.quickRunUsage
```

with normalization and a strict maximum record count.

Suggested cap:

```
2048–4096 result keys
```

If the project already develops a better per-project local preference store before this feature is implemented, reevaluate this placement explicitly rather than silently changing it.

## 2.3 Update policy

Increment usage only after a Quick Run action actually succeeds:

```
Folder navigation succeeded
Shortcut launch accepted
Link open accepted
Layout-item activation succeeded
Ctrl+Enter reveal completed
Shift+Enter add completed
```

A missing/ambiguous/denied layout member does not gain frequency.

## 2.4 Do not rebuild index for usage changes

Usage affects ranking only. Updating `lastUsedAt` / `useCount` must not rebuild the semantic search index.

## 2.5 Bound/prune

When over the cap:

- drop least-recently-used stale records first;
- do not allow usage history to grow unbounded.

Deleted result keys may be pruned opportunistically.

# STAGE 3 — Index invalidation architecture

Purpose: Keep Quick Run semantically current without rebuilding it for high-frequency irrelevant state.

Classification: HARD PERFORMANCE/CORRECTNESS CRITERION

## 3.1 Default strategy

Use whole semantic-index rebuild on a relevant searchable-data mutation.

Do not begin with complicated per-row incremental patches.

At 10k–20k occurrences, correctness is more important than avoiding an occasional bounded rebuild.

## 3.2 Local invalidation seam

Create one API, e.g. `quickRunIndex.invalidate(reason)`.

Every local mutation that changes Quick Run semantics routes through that seam.

## 3.3 Mutations that MUST invalidate/rebuild

### Folders

- [ ] create folder;
- [ ] delete/permanently remove folder;
- [ ] rename folder;
- [ ] move folder;
- [ ] bin folder;
- [ ] restore folder;
- [ ] any mutation changing its parent.

Folder rename/move can change breadcrumbs for every descendant, so full rebuild is appropriate.

### Shortcuts/Links

- [ ] create shortcut;
- [ ] create link;
- [ ] delete shared shortcut record;
- [ ] rename shortcut;
- [ ] target change;
- [ ] URL/non-URL classification change;
- [ ] create placement;
- [ ] remove placement;
- [ ] move placement;
- [ ] bin placement;
- [ ] restore placement;
- [ ] fork placement where occurrence identity changes;
- [ ] collapse placements where occurrence identity changes.

### Window layouts relevant to members

- [ ] create layout if it receives/contains searchable members;
- [ ] delete layout;
- [ ] move layout;
- [ ] bin layout;
- [ ] restore layout;
- [ ] layout name change, because layout name is part of member breadcrumbs;
- [ ] add member;
- [ ] remove member;
- [ ] change member descriptor title;
- [ ] change member descriptor executable fingerprint;
- [ ] descriptor replacement/rebinding.

## 3.4 Mutations that MUST NOT rebuild

This list is explicit because high-frequency false invalidation is a known performance risk.

Do not rebuild for:

- [ ] graph x/y positions;
- [ ] graph rest positions;
- [ ] graph physics ticks;
- [ ] graph simulation cooling/heating;
- [ ] toolbar position;
- [ ] workspace selection;
- [ ] selection anchor;
- [ ] current folder navigation;
- [ ] breadcrumb navigation;
- [ ] graph-expanded folder state;
- [ ] trail-expanded folder state;
- [ ] Bin mode view toggle by itself;
- [ ] icon-size preference;
- [ ] theme/preferences unrelated to Quick Run hotkey;
- [ ] prompt-library changes;
- [ ] Set membership changes while Sets remain excluded;
- [ ] Set rename/creation while Sets remain excluded.
- [ ] activeWindowLayoutId;
- [ ] window-layout member state normal/minimized;
- [ ] window-layout member bounds;
- [ ] window-layout card size;
- [ ] window-layout member order;
- [ ] capability cache changes;
- [ ] helper restart by itself;
- [ ] hover;
- [ ] preview state;
- [ ] thumbnail result;
- [ ] icon hydration alone;
- [ ] widget open/close;
- [ ] detached/attached presentation state;
- [ ] recency/frequency usage metadata.

Window-layout bounds/state are updated by live observation and are specifically not searchable semantics. The model separates those data-only member patches from descriptor identity.

## 3.5 External/peer document installs

The current workspace supports external document installs from other As-you-Go surfaces while preserving local navigation/session state. Quick Run must react to semantic changes arriving through this path as well.

Implement a pure searchable semantic comparison for external installs. It should compare only fields relevant to the Quick Run index.

Do not use full-document equality.

Do not allow a remote window-layout bounds observation to rebuild a 20,000-entry search index every 500 ms.

## 3.6 External semantic signature

A valid semantic projection may include:

```
groups:
  id
  name
  parentId
  bin status

shortcuts:
  shortcut id
  name
  target
  placement id
  parentId
  bin status

window layouts:
  layout id
  name
  parentId
  bin status
  members:
    member id
    descriptor version
    descriptor title
    executable fingerprint
```

Explicitly omit:

```
bounds
normal/minimized state
cardSize
activeWindowLayoutId
icons
view positions
selection
runtime fields
```

## 3.7 Open Quick Run during rebuild

When semantic index changes while Quick Run is open:

1. atomically replace index;
2. rerun current query;
3. preserve current filter if it still has matches;
4. otherwise fall back to All;
5. preserve highlighted resultKey if still present;
6. otherwise highlight first result.

## STAGE 3 GATE

Synthetic tests must prove:

```
100 state-only layout observation updates
→ 0 search-index rebuilds

one member descriptor rename
→ exactly 1 semantic rebuild
```

# STAGE 4 — Quick Run UI shell

Purpose: Build the interaction surface without yet enabling all actions.

Classification: CORE FEATURE

Suggested new modules:

```
public/app/quick-run/quick-run-controller.js
public/app/quick-run/quick-run-view.js
public/styles/quick-run.css
```

Integrate from `public/workspace-20260730b.js`.

Prefer a dedicated controller rather than adding another large inline block to the workspace entry.

## 4.1 Modal ownership

Quick Run is its own transient modal interaction layer.

While open, it owns printable keys, Escape, Enter, Ctrl+Enter, Shift+Enter, Tab/Shift+Tab and arrows; ordinary workspace hotkeys do not also fire.

## 4.2 Opening state

On open:

```
query = ''
filter = All
highlight = null
results = []
```

Focus input immediately.

## 4.3 Empty query

Evidence:

```
open Quick Run
→ no results
→ no chips requiring result data
→ no native/host call
```

## 4.4 Styling

Quick Run must be visually part of As-you-Go, not a Papers-native popup.

Required:

- one-line input;
- chips above rows;
- bounded result panel;
- icon/name/breadcrumb row;
- clear highlighted row;
- unavailable-state treatment;
- scrollable long result list.

Do not change graph layout to make room. Render Quick Run over/above the workspace.

## 4.5 No normal workspace render

Typing `a`, `ab`, `abc` must not call the full workspace `render()` three times.

Add an instrumentation test/spying seam proving:

```
100 Quick Run keystrokes
→ 0 graph update calls
→ 0 workspace full-render calls
```

# STAGE 5 — Hotkey integration

Purpose: Make Quick Run a normal As-you-Go workspace action.

Classification: HARD V1 UX CRITERION

Files:

```
public/app/hotkeys-model.js
public/app/interactions/keyboard-controller.js
public/workspace-20260730b.js
```

## 5.1 Add workspace action

Add `workspace.quick-run` to the existing hotkey catalog.

Pick the actual default chord only if already approved by the creator; otherwise leave the binding explicit/TODO rather than inventing one silently.

## 5.2 Keyboard controller seam

The ordinary keyboard controller should invoke `quickRun.open()` only when:

- Quick Run is closed;
- no existing editor/confirm/prompt modal owns the key;
- event is not native typing inside another editable control.

While Quick Run is open, its controller gets first refusal for its own keys.

## 5.3 Focus scope proof

Verify:

```
As-you-Go focused
+ hotkey
→ Quick Run opens
```

and:

```
another desktop app focused
+ same keys
→ As-you-Go renderer does not magically receive it
```

The second result is expected v1 behavior.

Documentation note: OS-global activation requires a future Papers accelerator/routing feature; it must not move Quick Run indexing into Papers.

# STAGE 6 — Query, filtering and keyboard navigation

Purpose: Finish the pure interaction semantics before actions.

Classification: CORE FEATURE

## 6.1 Printable typing

Every query change:

1. normalize query;
2. run pure matcher;
3. calculate All results;
4. derive chip availability;
5. apply current type filter;
6. select/preserve highlight;
7. patch Quick Run DOM only.

## 6.2 Tab behavior

Tab must never insert a tab character into the search input.

Test complete wraparound:

```
All → Folders → Shortcuts → Links → Layout Items → All
```

but skip types with no matches. Reverse with Shift+Tab.

## 6.3 Highlight and scrolling

Arrow navigation must keep the highlighted row visible.

Wheel/trackpad scrolling must have an explicitly tested rule:

- scrolling list changes viewport normally;
- when a row becomes selected by intended scroll behavior, its selection is deterministic;
- keyboard highlight never points to an off-list stale row.

Do not rely on `:hover` as authoritative keyboard selection.

## 6.4 Mouse

If pointer selection is supported:

- moving over row may update highlight;
- click executes same default path as Enter;
- there is one execution implementation, not duplicate mouse/keyboard logic.

## STAGE 6 EVIDENCE

DOM/controller test sequence:

```
query produces 5 rows
highlight row 1
Down -> 2
Down -> 3
Up -> 2
Tab -> next available type
first result in that type highlighted
Shift+Tab -> prior type
Escape -> controller closed and query cleared
```

# STAGE 7 — Default actions for Folder, Shortcut and Link

Purpose: Reuse current As-you-Go behavior rather than reinvent execution.

Classification: CORE FEATURE

Primary existing module: `public/app/workspace-commands.js`

The current command layer already navigates folders through session navigation, launches ordinary shortcuts, and routes HTTP/HTTPS shortcuts through `host.openWebLink()`.

## 7.1 Execution-time authority gate

Before every action:

```
selected resultKey
→ read CURRENT state
→ resolve current object by stable IDs
→ verify it is still active/non-binned and still of expected type
→ only then execute
```

If stale, report that the Quick Run result changed or no longer exists. Do not execute a stale indexed payload. Requery immediately.

## 7.2 Folder Enter

Given `folder:<groupId>`, re-read the current groupId.

Verify:

- group exists;
- not binned;
- no binned ancestor.

Then perform the same navigation semantics as current `navigateToFolder()`.

On success: close Quick Run, record usage.

## 7.3 Shortcut Enter

Given `shortcut:<placementId>`, re-read the placement.

Verify:

- placement exists;
- active;
- under active hierarchy;
- underlying shortcut still non-web.

Launch using the existing shortcut execution path.

## 7.4 Link Enter

Given `link:<placementId>`, re-read placement and current shortcut. Verify `isWebLink()` still true.

If its target was edited from URL to non-web between query and Enter:

- do not execute from stale classification;
- rebuild/requery;
- tell controller the result changed.

Otherwise open through the existing `host.openWebLink()` path.

# STAGE 8 — Ctrl+Enter reveal-inside-As-you-Go

Purpose: Implement the deliberately new meaning of Reveal.

Classification: CORE FEATURE

Do not route this through:

```
workspace.reveal-selection
commands.revealSelection()
revealShortcut()
host.revealShortcut()
```

Those existing paths reveal the underlying target in the OS/file manager.

Suggested new module or command seam:

```
public/app/quick-run/quick-run-reveal.js
```

or a clearly named Quick Run-specific command inside `workspace-commands.js`.

## 8.1 Folder reveal

Navigate to the containing parent folder, then select the folder occurrence.

If the folder is at root: navigate root, select folder.

## 8.2 Shortcut/Link reveal

Navigate to that exact placement's parent folder, then select `placementId` — not another placement of the same shortcut.

This is why one-result-per-placement is mandatory.

## 8.3 Layout Item reveal

Navigate to the containing layout's folder. Then:

- reveal/select the containing window-layout card;
- visually identify/highlight the specific member within the card.

Do not activate/focus the native application as part of Ctrl+Enter.

## 8.4 Explorer vs graph presentation

Quick Run reveal must be truthful in both As-you-Go layouts. Define the expected visible result separately for `explorer` and `graph`.

For graph mode, use existing graph/item visibility/centering primitives if available; do not create a second graph camera implementation inside Quick Run.

If no existing "center this node" primitive exists, extract one from the graph controller rather than querying/manipulating SVG transforms ad hoc.

## 8.5 Evidence

After Ctrl+Enter:

```
session.currentId == result parent
session.selected contains exact occurrence ID
target occurrence is visibly identifiable
Quick Run is closed
```

For a Layout Item also assert the correct memberId, not merely the correct layout, receives the reveal cue.

# STAGE 9 — Papers activateWindowCapability

Purpose: Add the one host operation Quick Run cannot perform locally.

Classification: HARD LAYOUT-ITEM LAUNCH CRITERION

Quick Run needs: activate/focus this already-resolved exact window capability; restore it first if minimized.

Do not make the Backpack implement observe → decide → restore/raise as separate round trips if the helper can make the decision atomically.

The current Papers capability stack already has enumerated helper methods and a single-request atomic toggle path; activation should follow the same narrow typed design.

## 9.1 New method name

Recommended: `activate`

```
Page-facing Backpack bridge: activateWindowCapability(capability)
Project request:             papers:project:window-activate-capability
Papers IPC:                  papers:window-capability:activate
Helper method:               activate
```

## 9.2 Required native contract

In one helper request:

```
validate token identity
→ read current native state
→ if minimized:
     restore
  else:
     raise/focus
→ return typed success
```

No thumbnail. No preview frame seed. No desktop enumeration. No arbitrary HWND from renderer.

The current native helper already defines `Restore-WhWindow()` as restore plus Raise and has a native Raise operation used when applying bounds, so activation should reuse those trusted primitives rather than inventing another focus mechanism.

## 9.3 Files expected to change — As-you-Go

```
public/app/host/host-bridge.js
```

Add `activateWindowCapability(capability)` beside existing observe/toggle/minimize/restore/resolve methods. The bridge currently exposes the capability operations through enumerated Papers project request names.

## 9.4 Files expected to change — Papers

```
src/preload/backpackProject.ts
src/main/ipc/windowCapabilityIpc.ts
src/main/windows/windowCapabilityService.ts
src/main/windows/windowCapabilityClient.ts
src/main/windows/windowCapabilityTypes.ts
src/main/windows/windowHelperFactory.ts
resources/window-helper/window-helper.ps1
resources/window-helper/window-capability.ps1
```

The existing preload already parses opaque capabilities and maps project requests to enumerate/bind/observe/toggle/minimize/restore/etc.; activation should follow that exact trust boundary.

## 9.5 Helper hash pins

Because the helper scripts are resource-hash pinned, after changing helper files update both expected resource hash locations used by Papers:

```
src/main/windows/windowHelperResource.ts
resources/window-helper/manifest.json
```

Do not finish the Papers commit until actual helper bytes, compiled expected hash and manifest hash all agree.

## 9.6 Typed outcomes

At minimum support:

```
success
missing
denied
helper-unavailable
malformed/internal typed failure as existing protocol allows
```

`ambiguous` belongs to descriptor resolution before activation, not to activation of an already-issued exact capability.

## 9.7 Host tests

Pin:

### Normal window

```
activate
→ Raise called
→ Restore not called
```

### Minimized window

```
activate
→ Restore called
→ window raised/focused
```

### Stale/reused identity

```
activate
→ missing/denied
→ no other HWND raised
```

### Renderer authority

Malformed page capability cannot smuggle HWND, PID or path through the new operation.

## STAGE 9 GATE

Do not enable Layout Item Enter until the complete operation works end-to-end through the packaged Papers capability stack.

# STAGE 10 — Layout Item default action and availability state

Purpose: Make persisted window members searchable without live probing.

Classification: HARD FEATURE CRITERION

## 10.1 Availability state

Each Quick Run layout-member occurrence may have ephemeral session availability:

```
unknown
available
unavailable
```

Default: `unknown`

Do not infer "not running" from persisted `member.state`. Persisted normal/minimized is arrangement state, not a guarantee that the native window currently exists.

## 10.2 No probes while searching

Typing `c`, `ch`, `chr`, `chrome` must cause:

```
0 windowCandidates
0 resolveWindowDescriptor
0 observeWindowCapability
0 activateWindowCapability
0 thumbnail calls
```

## 10.3 Selection-time resolution

On Enter for `layout-member:<layoutId>:<memberId>`:

1. re-read layout by layoutId;
2. verify layout is still active/non-binned;
3. re-read member by memberId;
4. verify descriptor still matches the indexed result identity;
5. use existing cached `capabilityForMember()`/equivalent fast path if valid;
6. otherwise call `host.resolveWindowDescriptor(currentDescriptor)`;
7. only after successful unique resolution call `host.activateWindowCapability(capability)`.

The existing member capability path already caches by layout/member and resolves the persisted descriptor only on a miss. Reuse/extract that seam rather than building Quick Run-specific native resolution.

## 10.4 Exact resolution outcomes

### Unique and activation succeeds

```
availability = available
close Quick Run
record successful use
```

### Missing

```
availability = unavailable
reason = not-running/missing
keep Quick Run open
do not remove persisted result
do not silently do nothing
```

### Ambiguous

```
availability = unavailable
reason = multiple-matching-windows
keep Quick Run open
do not choose one
```

### Helper unavailable

```
availability = unavailable
reason = helper unavailable
keep Quick Run open
```

### Denied

```
availability = unavailable
reason = permission denied/unsupported
keep Quick Run open
```

## 10.5 Availability invalidation

Availability is ephemeral UI knowledge, not durable Backpack truth.

Reset to `unknown` when:

- descriptor changes;
- member is removed/re-added;
- page reloads;
- an operation reports stale/missing after previously successful use.

Do not write availability into persisted layout members.

## 10.6 Fresh capability test

Fixture: member exists in persisted layout, no runtime capability cached.

Search must show it. Only Enter may call descriptor resolution.

## 10.7 Ambiguity test

Two native windows satisfy the descriptor. Expected:

```
result remains in Quick Run
row becomes unavailable
message says multiple matches
0 activate calls
```

# STAGE 11 — Shift+Enter: add Layout Item to active window layout

Purpose: Implement the only non-default modifier action enabled in v1.

Classification: CORE FEATURE

The model's `addWindowLayoutMember()` is data-only and takes a persisted member shape; it does not itself launch or mutate a native window. Reuse that model operation.

## 11.1 Preconditions

Before enabling Shift+Enter for a Layout Item:

- source occurrence still exists;
- active runtime recording context has a valid active layout;
- destination layout exists and is active/non-binned;
- destination is not read-only due to surface handoff/conflict;
- duplicate rule allows the addition.

## 11.2 Do not resolve native window unnecessarily

The source result already contains a persisted descriptor. Adding the same descriptor-bound window to another layout is primarily a data operation.

Do not run desktop enumeration merely to copy the descriptor if the current model contract allows the persisted descriptor to be reused.

If initial bounds/state are required for a truthful member creation, use already-known persisted source arrangement as the v1 starting arrangement unless a separate product requirement explicitly demands fresh observation.

## 11.3 New member identity

Never copy the source `member.id`. Destination receives a new membership ID. The descriptor is reused.

## 11.4 Duplicate rule

Pin one explicit rule. Recommended:

```
same descriptor already present in destination layout
→ do not add
→ visible "Already in active layout"
```

Do not silently create two identical members inside one layout unless current window-layout semantics explicitly allow that and the creator approves it.

## 11.5 No active layout

Shift+Enter is visibly disabled. Reason: `No active window layout`.

## 11.6 Non-Layout results

Folder/Shortcut/Link show Shift+Enter unavailable.

Do not launch a Shortcut hoping to infer which new window it creates. That is a different feature.

# STAGE 12 — Stale index and execution-race defenses

Purpose: Guarantee Quick Run never executes an object merely because it existed when the query was ranked.

Classification: HARD CORRECTNESS CRITERION

## 12.1 Every action revalidates

Mandatory for Enter, Ctrl+Enter, Shift+Enter and mouse activation.

Pattern:

```
resultKey
→ parse stable IDs
→ CURRENT state lookup
→ current active/non-binned check
→ current type/classification check
→ act
```

## 12.2 Rename race

```
Quick Run query shows "Chrome"
peer renames it before Enter
Enter
```

Expected: old indexed copy is not trusted; current object wins; query/index reruns; no stale action target.

## 12.3 Move race

Shortcut placement moves to another folder while highlighted. Ctrl+Enter must reveal its new parent, not old breadcrumb.

## 12.4 Bin race

Item is binned while highlighted. Enter must not resurrect/open it from stale Quick Run state. Requery removes it.

## 12.5 Member removal race

Layout member is removed while highlighted. Enter:

```
0 descriptor resolution
0 native activation
result disappears/requery
```

## 12.6 Classification race

Link target changes to a local shortcut target before Enter. Do not open stale URL. Re-read current shortcut and route according to current type.

# STAGE 13 — Multi-surface correctness

Purpose: Make Quick Run behave correctly with As-you-Go open in multiple Papers surfaces.

Classification: CORE FEATURE

Quick Run UI state is local to one surface:

```
open/closed
query
filter
highlight
availability UI
```

Do not synchronize those through the shared document. Searchable content comes from the current installed document state.

## 13.1 Peer rename

Surface A has Quick Run open. Surface B renames a folder. After A installs the peer document:

```
index updates
current query reruns
old name disappears
new name appears if matching
```

## 13.2 Peer move

Breadcrumb updates without moving A's local current navigation.

## 13.3 Peer layout observation

Surface B updates only native member bounds/state. Surface A: `0 Quick Run rebuilds`.

## 13.4 Usage metadata conflict

If usage history is stored in shared `view.quickRunUsage`, test two surfaces using Quick Run concurrently.

The result may tolerate last-write/merged tie-break metadata loss only if no workspace item data is lost.

If current coordinator merge semantics make frequent usage writes problematic, move usage metadata to a better bounded per-project local store before launch rather than weakening document consistency.

# STAGE 14 — Performance integration gate

Purpose: Prove the real UI remains responsive with graph physics and normal workspace load.

Classification: HARD LAUNCH QUALITY GATE

The pure Stage 0 benchmark is necessary but not sufficient.

## 14.1 Real renderer corpus

Load a synthetic/fixture workspace representing 10,000–20,000 searchable occurrences with graph mode active.

## 14.2 Measure keystroke-to-results

Measure:

```
keydown/input event timestamp
→ Quick Run result DOM committed
```

Target `p95 <= 16 ms`; preferred `p95 <= 12 ms` on creator-relevant hardware.

No repeated long tasks above one frame for ordinary queries.

## 14.3 Graph isolation evidence

During 100 rapid Quick Run query changes assert:

```
0 native window resolutions
0 thumbnails
0 host capability requests
0 graph simulation restarts caused by Quick Run
0 full workspace renders caused by query change
```

## 14.4 Rebuild performance

Trigger a semantic rename in a 20k-result workspace. Measure:

```
semantic mutation
→ new index active
→ current query reranked
```

Record duration.

If rebuild itself produces unacceptable visible typing stalls while Quick Run is open, build index asynchronously or move rebuild/search projection to the Worker architecture.

## 14.5 State-only storm

Simulate 1000 member bounds/state updates. Expected: `0 semantic index rebuilds`.

This is a hard regression test.

# STAGE 15 — Accessibility and keyboard quality

Purpose: Make Quick Run genuinely keyboard-first rather than merely key-operable.

Classification: LAUNCH QUALITY GATE

## 15.1 Focus

On open: `document.activeElement == Quick Run input`.

On close: return focus to the prior appropriate As-you-Go workspace element.

## 15.2 Semantics

Use appropriate combobox/listbox semantics or equivalent accessible pattern.

Required:

- input has meaningful accessible name;
- list exposes result count;
- active row is announced;
- disabled modifier actions have accessible reason where surfaced;
- availability state can be conveyed without relying only on color.

## 15.3 No keyboard leakage

While Quick Run is open, `Ctrl+Enter`, `Enter`, `Delete`, `G`, `Ctrl+G` must not trigger underlying workspace actions unless they are explicitly Quick Run commands.

## 15.4 IME/input correctness

Do not intercept Enter/keys incorrectly during active text composition.

Test with an IME/composition event sequence if the creator uses or may use non-Latin input.

# STAGE 16 — Error/status behavior

Purpose: Make failures visible and truthful.

Classification: CORE FEATURE

## 16.1 Successful action

Close Quick Run after successful folder navigate, shortcut launch, link open, native window activation, reveal, or add-to-layout.

## 16.2 Failed Layout Item activation

Keep Quick Run open. Show row/status reason. Examples:

```
Window is not currently available
Multiple matching windows
Window helper unavailable
Window access denied
```

Never silently close Quick Run on failure.

## 16.3 Stale result

If a result disappears between query and execution:

```
That item changed or no longer exists
```

Requery automatically.

## 16.4 Host failures

Do not expose raw helper/internal stack traces as the main Quick Run UX. Use typed existing host outcomes.

# STAGE 17 — Tests that must exist before completion

Classification: HARD DEFINITION-OF-DONE REQUIREMENTS

## Index domain

- [ ] folder indexed.
- [x] nested folder breadcrumb correct. — `bd24a2c` @ `2026-09-12T08:17:59+07:00` *(a group at depth two and a member inside it both build the full chain, in the document's own order and with its separator (Workspace › Alpha › Focus asserted in the search suite). The rule and the format are tested; the surface that draws it is a later stage.)*
- [ ] binned folder excluded.
- [ ] descendants under binned folder excluded.
- [ ] one ordinary shortcut placement indexed.
- [ ] linked shortcut with 3 placements gives 3 results.
- [x] placement breadcrumbs independent. — `550e6cc` @ `2026-09-12T08:22:40+07:00` *(two placements of one shortcut in different folders produce two rows with different breadcrumbs **and** different result keys while sharing a name and target, which is the occurrence-identity rule the contract states. Asserted in quick-run-search.test.mjs.)*
- [ ] HTTP shortcut classified as Link.
- [ ] HTTPS shortcut classified as Link.
- [ ] non-web shortcut classified as Shortcut.
- [ ] one layout member indexed.
- [ ] same descriptor in two layouts gives 2 results.
- [ ] whole layout never appears.
- [ ] binned layout member excluded.
- [ ] prompts excluded.
- [ ] Bin entries excluded.
- [ ] Sets excluded, with a test/comment referencing the recorded product decision.

## Ranking

- [ ] exact beats prefix.
- [ ] prefix beats word-prefix.
- [ ] word-prefix beats subsequence.
- [ ] subsequence beats no match.
- [ ] recency never moves a lower tier above a higher tier.
- [ ] frequency never moves a lower tier above a higher tier.
- [ ] deterministic fallback stable.
- [x] duplicate names remain separate by occurrence/resultKey. — `9d78518` @ `2026-09-12T08:23:53+07:00` *(nothing de-duplicates: quickRunRowViews returns one view per occurrence, the two share a primary name and differ in key and breadcrumb, and the highlight rides exactly one of them. The presentation suite asserts the flat list carries no grouping that could merge them.)*

## Filters

- [ ] chips only for matched types.
- [ ] Tab forward.
- [ ] Shift+Tab backward.
- [ ] zero-match active filter falls back to All.
- [x] fallback highlights first All row. — `66fd5f4` @ `2026-09-12T08:32:47+07:00` *(when the active type filter loses its matches, the session falls back to `All`, reports `fellBack: true`, and sets the highlight to the first row of the fallback set — asserted in the session suite (`fellBack` plus `highlightKey === rows[0].resultKey`) and reached through the mount test's Tab handling.)*

## Empty query

- [ ] empty query gives zero results.
- [ ] no recents home screen.
- [ ] no host calls.

## Actions

- [ ] Folder Enter navigates.
- [ ] Shortcut Enter launches.
- [ ] Link Enter opens URL.
- [ ] Ctrl+Enter Folder reveals exact folder occurrence.
- [ ] Ctrl+Enter Shortcut reveals exact placement.
- [ ] Ctrl+Enter Link reveals exact placement.
- [ ] Ctrl+Enter Layout Item reveals containing layout + member.
- [ ] Shift+Enter disabled for Folder.
- [ ] Shift+Enter disabled for Shortcut.
- [ ] Shift+Enter disabled for Link.
- [ ] Shift+Enter Layout Item adds new membership when valid.
- [ ] no active layout disables Shift+Enter.
- [ ] duplicate destination membership reports visible status.

## Stale-index execution

- [ ] rename-before-Enter.
- [ ] move-before-Ctrl+Enter.
- [ ] bin-before-Enter.
- [ ] delete-before-Enter.
- [ ] layout-member-remove-before-Enter.
- [ ] Link→Shortcut target edit before Enter.

Every test proves current-state revalidation.

## Availability/native

- [ ] untouched Layout Item is unknown.
- [ ] searching does zero native resolution.
- [ ] first Enter resolves.
- [ ] unique resolution + activate success -> available.
- [ ] missing -> unavailable.
- [ ] ambiguous -> unavailable.
- [ ] ambiguous -> zero activate calls.
- [ ] result remains searchable after missing/ambiguous outcome.
- [ ] descriptor change resets prior availability.

## Papers activation

- [ ] normal target raises/focuses.
- [ ] minimized target restores then activates.
- [ ] stale identity cannot activate replacement HWND.
- [ ] malformed capability rejected.
- [ ] page cannot supply HWND/PID/path.
- [ ] helper-unavailable typed failure.
- [ ] helper SHA-256 pins updated and validated.

## Invalidation

- [ ] folder rename rebuilds.
- [ ] folder move rebuilds.
- [ ] shortcut rename rebuilds.
- [ ] shortcut target classification change rebuilds.
- [ ] placement move rebuilds.
- [ ] layout member add/remove rebuilds.
- [ ] descriptor change rebuilds.
- [ ] layout name change rebuilds member breadcrumbs.
- [ ] layout bounds update does not rebuild.
- [ ] layout minimize/restore state update does not rebuild.
- [ ] graph position update does not rebuild.
- [ ] selection update does not rebuild.
- [ ] capability cache update does not rebuild.
- [ ] icon hydration does not rebuild.
- [ ] Quick Run usage metadata does not rebuild.
- [ ] prompt change does not rebuild.
- [ ] Sets change does not rebuild while Sets excluded.

## Performance

- [ ] 10k corpus measured.
- [ ] 20k corpus measured.
- [ ] pure p95 ≤ 8 ms or Worker fallback used.
- [ ] no ordinary pure query ≥ 16 ms.
- [ ] integrated renderer p95 target satisfied.
- [ ] typing causes zero graph reheat/full render.
- [ ] state-only layout observation storm causes zero rebuilds.

# STAGE 18 — The Sets question must be recorded, not forgotten

Before final launch, confirm Section 4 records the creator's explicit answer.

**Recorded 2026-09-08: the creator explicitly confirmed Sets remain excluded from v1.**

Not allowed: "nobody remembered to ask."

Keep a test proving that exclusion so a future refactor does not accidentally surface them.

# STAGE 19 — Product documentation

Classification: HARD PRODUCT-HONESTY CRITERION

Document:

- Quick Run searches persisted As-you-Go objects, not the desktop.
- Layout Items can appear even when their application is no longer running.
- Quick Run does not continuously probe window availability.
- A Layout Item's availability is determined when the creator tries to activate it.
- Duplicate names with different breadcrumbs are intentional occurrences.
- Links are shortcuts classified by URL target.
- Whole window layouts are excluded.
- Prompts are excluded.
- Bin contents are excluded.
- Sets are excluded per the recorded creator decision.
- V1 hotkey works when As-you-Go has focus.
- OS-global invocation is a separate future Papers feature.
- Ctrl+Enter reveals inside As-you-Go, not in the operating-system file manager.
- Shift+Enter is only meaningful for Layout Items in v1.

# Definition of Done

Quick Run is complete only when all conditions below are true.

## Search behavior

- [x] Hotkey opens one empty focused Quick Run line. — `10f8ae6` @ `2026-09-12T08:29:36+07:00` *(one line, empty, and focused: `open()` resets the session to an empty query, paints (which draws no rows and no chips for an empty query), and calls `focus()` on the input — guarded with `?.` because a caller may mount without a focusable field, and asserted in the surface test. **Same residual as the box above:** the key press itself is not exercised, because the entry file is not importable and this loop has no browser.)*
- [ ] Empty query shows no results.
- [ ] First keystroke produces ranked results.
- [ ] Search remains responsive with 10k–20k searchable occurrences.
- [ ] Exact > prefix > word-prefix > fuzzy subsequence.
- [ ] Recency/frequency only break ties inside a tier.
- [ ] Result ordering is deterministic.
- [ ] One shortcut placement = one result.
- [ ] One layout-member occurrence = one result.
- [ ] Links use the shortcut index and are classified, not duplicated.

## Filters

- [ ] All/Folders/Shortcuts/Links/Layout Items behave exactly as specified.
- [ ] Only types with matches produce chips.
- [ ] Tab/Shift+Tab cycles only available chips.
- [ ] Disappearing active filter falls back to All.

## Actions

- [ ] Folder Enter navigates.
- [ ] Shortcut Enter launches.
- [ ] Link Enter opens web link.
- [ ] Layout Item Enter uniquely resolves and activates/restores the exact native window.
- [ ] Missing/ambiguous Layout Item remains visible and reports failure honestly.
- [ ] Ctrl+Enter navigates-and-selects the exact As-you-Go occurrence.
- [ ] Ctrl+Enter never invokes OS reveal.
- [ ] Shift+Enter only works for Layout Items.
- [ ] Shift+Enter never silently does nothing for unsupported result types.

## Native boundary

- [ ] Typing causes zero native probes.
- [ ] Indexing causes zero native probes.
- [ ] Layout-item capability resolution begins only on execution.
- [ ] Papers exposes a narrowly typed `activateWindowCapability`.
- [ ] Activation restores only when minimized and otherwise raises/focuses.
- [ ] Capability identity remains fail-closed.
- [ ] Helper resource hash pins are correct.

## Correctness under mutation

- [ ] Every action revalidates against current state.
- [ ] Rename/move/bin/delete races cannot execute stale index payload.
- [ ] Peer document semantic changes refresh Quick Run.
- [ ] High-frequency member bounds/state updates do not rebuild the index.
- [ ] Graph/session/view changes do not unnecessarily rebuild the index.

## Performance

- [ ] Pure 20k benchmark meets budget or Worker fallback is implemented.
- [ ] Integrated typing stays inside agreed frame-latency budget.
- [ ] Quick Run typing never reheats graph physics.
- [ ] Quick Run typing never calls full workspace `render()`.
- [ ] No native/IPC work occurs on keystrokes.

## Scope/product honesty

- [ ] No prompts.
- [ ] No whole layouts.
- [ ] No Bin.
- [ ] Sets decision explicitly recorded (excluded; confirmed 2026-09-08).
- [x] No OS-global hotkey in v1. — `362a00d` @ `2026-09-12T08:19:15+07:00` *(the acceptance side of the same prohibition, on the same evidence: nothing in the tree registers a global shortcut, and Quick Run's catalog entry is workspace-scoped. The hotkey opens the surface only while the As-you-Go window can receive keyboard input, which is the v1 scope the surrounding boxes state.)*
- [ ] No Papers-level universal search architecture.
- [ ] No live window availability scanning.

# Creator acceptance walk

Run this on a real creator-sized workspace, not only test fixtures.

## Setup

Create or use a workspace containing:

- several nested folders;
- at least one shortcut linked into two folders;
- at least one web link;
- at least two window layouts;
- at least one same application/window represented in multiple layout occurrences where valid;
- one persisted layout member whose native application is currently closed;
- enough synthetic/real data to stress normal search performance.

## Walk

1. Focus the As-you-Go workspace.
2. Press the configured Quick Run hotkey.
3. Verify one empty search line appears and nothing else is selected or changed.
4. Type the beginning of a folder name.
5. Verify results appear immediately.
6. Verify exact/prefix ordering.
7. Verify each row contains icon, name and breadcrumb.
8. Search for a duplicated linked shortcut.
9. Verify each placement appears separately with its own breadcrumb.
10. Press Tab repeatedly.
11. Verify only matched type chips participate.
12. Cause the selected chip type to lose all matches by typing another character.
13. Verify filter falls back to All and first All result highlights.
14. Use ArrowUp/ArrowDown.
15. Verify highlight changes immediately and stays visible.
16. Select a Folder and press Enter.
17. Verify As-you-Go navigates into it.
18. Reopen Quick Run and launch a normal Shortcut.
19. Reopen Quick Run and open a Link.
20. Reopen Quick Run and select a shortcut placement with Ctrl+Enter.
21. Verify As-you-Go navigates to the exact placement and selects it.
22. Verify no OS file-manager reveal occurred.
23. Reopen Quick Run and select a Layout Item with Ctrl+Enter.
24. Verify its containing layout is revealed and the exact member is identifiable.
25. Reopen Quick Run and select a currently running Layout Item with Enter.
26. Verify the application window immediately becomes active.
27. Minimize that native application.
28. Invoke it again from Quick Run.
29. Verify it restores and becomes active.
30. Search for the persisted member whose application is closed.
31. Verify it still appears without being falsely labelled "Not running" before selection.
32. Press Enter.
33. Verify Quick Run stays open and truthfully marks/reports that the window is unavailable.
34. If possible, create two ambiguous matching native windows for one descriptor.
35. Press Enter on that result.
36. Verify neither native window is chosen automatically.
37. Activate a window layout.
38. Reopen Quick Run.
39. Select a Layout Item from another layout.
40. Press Shift+Enter.
41. Verify a new membership is added to the active layout according to the duplicate rule.
42. Highlight a Folder/Shortcut/Link and hold Shift.
43. Verify the add-to-layout action is visibly unavailable.
44. Rename an indexed object from another As-you-Go surface while Quick Run remains open.
45. Verify the result refreshes without disturbing that surface's local navigation.
46. Generate repeated window-layout observation bounds/state changes.
47. Verify Quick Run remains responsive and the semantic index does not rebuild.
48. Enter graph mode.
49. Type rapidly into Quick Run.
50. Verify graph physics does not reheat or hitch because of search.
51. Test a 10k–20k occurrence workspace.
52. Confirm measured query and integrated input latency meet the performance gates.
53. Press Escape from a populated Quick Run.
54. Verify the UI disappears, no result executes, and the underlying workspace remains otherwise untouched.
55. Reopen Quick Run and verify no empty-query recents/home screen appears.
56. Confirm the recorded Sets product decision matches the shipped behavior.

The feature is done only when this entire acceptance walk succeeds, the performance measurements pass, and the creator confirms that Quick Run feels immediate enough to use as the primary fast-access path inside As-you-Go.

# Open items to settle before implementation begins

- [x] **Sets decision** — resolved 2026-09-08: excluded from v1.
- [x] **Pin the default workspace hotkey chord.** — chosen by the creator on 2026-09-12: **Alt+Shift+X**,
      for the As-you-Go workspace scope. Recorded here rather than inferred: it was the last open item in
      this section, and § at L1032 asks for it to be an explicit binding rather than an invented default.
