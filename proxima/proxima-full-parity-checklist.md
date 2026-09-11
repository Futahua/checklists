# Proxima Backpack — Full-Parity Implementation Checklist

<!-- STATUS: replace this block in place. Never append. -->

## Status

**Updated** 2026-09-11 · **Repo** Futahua/proxima-backpack

**Where everything is.** Windows paths. The short names beside these are symlinks into
`Products\<Name>\<Role>` and both forms work, so a tool reporting one when you typed the
other is not a wrong directory. Use `D:/...` in scripts: Windows Python cannot resolve msys
`/d/...` and fails *silently*, which once produced a no-op edit that looked like a pass.

| | |
| --- | --- |
| Working tree | `D:\Letters\MatTroiSeConMoc\Products\Papers\Runtime\Backpack projects\Proxima` |
| Fixture vaults | `<working tree>\fixtures\` — `vault-basic`, `vault-duplicates`, `vault-legacy`, `vault-malformed` |
| This checklist | `D:\Letters\MatTroiSeConMoc\LongHorizon` — `Futahua/long-horizon` |
| Original plugin | `D:\LapSlop brotherhood\Local\.obsidian\plugins\proxima` — `Futahua/Proxima-Obsidian` at `c1af9cb`, the SHA the interaction trace was written from. **Read-only reference: it is a live plugin inside the creator's vault. Do not write to it.** |

| | |
| --- | --- |
| Accepted branch | `stage7-record-store-contract` @ `be3efdf` — pushed, creator-accepted through Stage 8 slice 2 durable identity reconciliation / duplicate-candidate planning foundation |
| Accepted host Gate 9.3 | `Futahua/Papers-3` branch `proxima-gate9-native-source-handoff` @ `67b7fa2` — pushed |
| Accepted host Gate 10.1 | `Futahua/Papers-3` branch `gate10-native-presentation-reconcile` @ `5451bbf` — pushed, creator-accepted |
| Accepted host Gate 10.2 | `Futahua/Papers-3` branch `gate10-host-truth` @ `9e6304b` — pushed, creator-accepted |
| Accepted host Gate 10.3 | `Futahua/Papers-3` branch `gate10-relay` @ `d2a3c74` — pushed, creator-accepted |
| Unaccepted work | none |
| Suite at `be3efdf` | typecheck 0, build 0, `git diff --check` 0, vitest 0 via `--no-file-parallelism`, 153 files / 912 tests; Stage 8 import-planner focused 1 file / 6 tests passed; `bridgeDisclosure` isolated 1 file / 3 tests passed |

**Done** Stage 0's spine, HARD GATE 0 closed at `5d5cebf`. Stage 1 at `2450828`. Stage 2,
the Elastic execution cockpit, at `57860d3`. Stage 3: the Timekeeping shell and Deadline
Calendar at `760e54d`, Timeline/Gantt at `fb67685`, the Gantt interaction contract at
`c1f8c93`, Countdowns at `2b8a145`, and the two acceptance proofs at `37e722b` — **Stage 3 is
complete except panel sizing/layout**. Stage 4 slice 1, Schedule Day/4-Day/Week, at
`7357b4d`, slice 2, the Day/4-Day/Week interaction contract, at `7292075`, and slice 3,
Schedule empty-cell creation, at `2e74059`, and slice 4, Schedule Month/Year/Agenda
projection, at `5d97cdc`. Nothing anywhere writes a record. Six Stage 0
projection, at `5d97cdc`, and slice 5a, Schedule shared navigation and filtering, at
`fc460f6`, slice 5b, Schedule recurrence projection, at `448c65f`, and Stage 5 slice 1,
Projects Hub read-only inventory, at `d83e158`, and Stage 5 slice 2, New Project provisional
modal with typed-unavailable Save, at `68e11b6`, and Stage 5 slice 3, project lifecycle refusal
controls, at `dbea424`, Stage 5 slice 4, read-only project workspace panels, at `dadd610`,
Stage 5 slice 5, detailed Notes tree/preview interactions, at `fa5bb33`, and Stage 5 slice 6,
detailed Task Board interactions, at `c8e35c3`, and Stage 5 slice 7, detailed Backlog interactions,
at `b281cab`, Stage 5 slice 8, detailed Deadlines interactions, at `d3dbb59`, and Stage 5
slice 9, detailed Schedule interactions, at `36fcc08`, and Stage 5 slice 10, workspace
ownership closeout, at `cb92cae`.
Stage 6 slice 1, Canvas selection and read-only node inspection, at `ace9bac`.
Stage 6 slice 2, Canvas geometry preview refusal, at `4e8bed7`.
Stage 6 slice 3, Canvas removal intent/confirmation/refusal, at `8e20d0d`.
Stage 6 slice 4, Canvas semantic action + inspection seam, at `6f93de2`.
Stage 6 slice 5, semantic source refresh/reload seam, at `839d1b7`.
Stage 6 slice 6, structured diagnostic code catalog, at `7844264`.
Stage 6 slice 7, structured diagnostic payload bounds, at `7313025`.
Stage 6 slice 8, structured frontmatter parse-failure diagnostics, at `4f5f063`.
Stage 6 slice 9, unsupported-frontmatter diagnostic policy, at `20764d4` (existing bridgeDisclosure full-suite timing exception accepted; isolated test passes).
Stage 6 slice 10, structured duplicate-ID diagnostics, at `fe4a6c9`.
Stage 6 slice 11, structured missing-relationship diagnostics, at `7a7018f`.
Stage 6 slice 12, structured invalid date/number diagnostics, at `1081aa2`.
Stage 6 slice 13, renderer-failure diagnostics, at `a888988`.
Stage 6 slice 14, filesystem/repository failure diagnostics, at `92e4fa3`.
Stage 6 slice 15, credential/token-safe diagnostic disclosure, at `7d6ea75`.
Stage 6 slice 16, real-machine-path-safe diagnostic disclosure, at `987daac`.
Stage 6 slice 17, headless programmability, at `35b20e4`.
Stage 6 slice 18, UI semantic-action parity, at `cb012d1`.
Stage 6 slice 19, renderer-independent inspection, at `4801bad`.
Stage 6 slice 20, deterministic events and evidence, at `ab9ca57`.
Stage 6 slice 21, optional Papers control, at `83ea8e1`.
Gate 9.1, native open/reveal acceptance gap, at `ac7daaf`.
Gate 9.2, smallest host capability, at `f6b49d1`.
Gate 9.3, native open/reveal execution and acceptance, accepted on Papers branch
`proxima-gate9-native-source-handoff` at `67b7fa2` (Proxima remains at `f6b49d1`).
Gate 10.1, live-agent-control gap proof, accepted on Papers branch
`gate10-native-presentation-reconcile` at `5451bbf`: real stdio `papers_control`, exact
same-project split target, DOM-only per-group proof, both exact canonical native presentations
visible, exact singular `inspect.surface` equality, C1 inspection/capture and refusal proofs;
Papers default suite 99 files (98 passed | 1 skipped), 940 passed + 4 skipped / 944 collected.
Gate 10.2, host-truth contract, accepted on Papers branch `gate10-host-truth` at `9e6304b`:
an unbound sender cannot claim Backpack authority; a mismatched claimed Backpack is refused
without crossing the downstream seam; a matching request crosses exactly once with the
host-resolved live project identity; and a retired logical surface makes that sender stale
and refused. Production is unchanged from Gate 10.1. Papers default suite 99 files
(98 passed | 1 skipped), 941 passed + 4 skipped / 945 collected.
Gate 10.3, bounded relay proof, accepted on Papers branch `gate10-relay` at `d2a3c74`:
the accepted host-resolved project identity reaches the real `DelegateWaveRelay`; the
read-only operation is fixed to `GET /v1/overview`, credentials come from relay configuration
rather than page parameters, caller-supplied path/token values cannot redirect or authorize
the request, and no mutation body or mutation operation is emitted. Production remains
unchanged. Papers default suite 99 files (98 passed | 1 skipped),
942 passed + 4 skipped / 946 collected.
HARD GATE A / A1, Stable opaque identity, accepted on Proxima branch
`hard-gate-a1-opaque-identity` at `71b0a2b`: task, project, event, schema and workflow-stage
records share one versioned opaque canonical-ID contract; display names, physical filenames,
source paths and legacy Markdown IDs are explicitly non-identity; rename stability, duplicate
display names, duplicate-ID refusal and legacy explicit-ID alias/provenance treatment are
proven. Existing Markdown compatibility reading is unchanged; no persistence, import
execution or mutation capability exists. Proxima full suite 135 files / 789 tests.
HARD GATE A / A2, Separate execution state from workflow stage, accepted on Proxima branch
`hard-gate-a2-task-state-separation` at `07d4926`: canonical tasks independently carry
`executionState` (`backlog`, `running`, `finished`) and opaque `workflowStageId`; the Elastic
execution and project-workflow projections remain separate, moving either dimension leaves
the other unchanged, and workflow-stage rename preserves membership through stable stage
identity. Legacy `Task.status` compatibility behavior remains unchanged; no persistence,
write, import execution or mutation capability exists. Proxima full suite 136 files / 794 tests.
HARD GATE A / A3, Scoped ordering, accepted on Proxima branch
`hard-gate-a3-scoped-ordering` at `bf56679`: canonical Elastic execution order and project
workflow order are independent durable scopes; workflow ordering is scoped by exact project
and workflow-stage IDs; reordering either surface leaves the other unchanged; calendar order
is chronology-derived rather than manually ranked; and Gantt row placement is LOCAL STATE
rather than a third durable task-order field. The typed `task.timeline.change.targetRowIndex`
contract remains present while its durable mutation leg remains unavailable. Legacy
`Task.orderIndex` compatibility behavior remains unchanged; no persistence, write, import
execution or mutation capability exists. Proxima full suite 137 files / 801 tests.
HARD GATE A / A4, Project-type silo removed, accepted on Proxima branch
`hard-gate-a4-project-capabilities` at `795f019`: active projects may associate with tasks
and events simultaneously; task/calendar visibility and selection no longer depend on the
legacy `projectType` label; capabilities derive from available task/event/workspace data;
inspection schema v5 exposes those capabilities rather than `projectType`; and legacy
`projectType` remains import/presentation metadata only. Obsolete pre-A4 silo assertions
were corrected without altering the legacy reader. No persistence, write, import execution
or mutation capability exists. Proxima full suite 138 files / 804 tests.
HARD GATE A / A5, Schema is canonical data, accepted on Proxima branch
`hard-gate-a5-canonical-schema` at `289754d`: property-schema definitions are canonical
opaque-ID `schema` records; select and multi-select options have stable opaque identity
separate from labels; formula, rollup and relation definitions are canonical semantic data;
and presentation-only option colors, column widths and collapsed state are explicitly
LOCAL STATE. Legacy schema types remain compatibility-only and the legacy reader is unchanged.
No persistence, write, import execution or mutation capability exists. Proxima full suite 139
files / 811 tests.
HARD GATE A / A6, Relations are ID-based, accepted on Proxima branch
`hard-gate-a6-id-relations` at `26c84d4`: canonical relation values contain only the opaque
relation-schema ID and opaque target-record IDs; resolution is entirely by canonical record
identity with schema target-kind enforcement; duplicate, missing and disallowed targets fail
explicitly; title changes and legacy source moves leave relation identity intact; and
wikilink/filename-shaped values are refused at the canonical boundary. Canonical relation
semantics contain no target filename, source path or `targetFolder`; existing legacy
compatibility code remains untouched. No persistence, write, import execution or mutation
capability exists. Proxima full suite 140 files / 817 tests.
HARD GATE A / A7, Names are independent from storage representation, accepted on Proxima
branch `hard-gate-a7-name-storage-separation` at `270f8cb`: task, project and event titles are
ordinary canonical fields rather than storage identity; filename-hostile and YAML-sensitive
text remains valid canonical title data; moving or renaming a legacy representation changes
provenance without changing canonical name or identity; and canonical structured task data
round-trips through standard JSON without Markdown/frontmatter/YAML interpretation. Existing
legacy reader behavior remains unchanged. No persistence, write, import execution or mutation
capability exists. Proxima full suite 141 files / 822 tests.
HARD GATE A / A8, Project/filesystem association is explicit, accepted on Proxima branch
`hard-gate-a8-explicit-artifact-association` at `1c87f24`: canonical Proxima records retain
their `pxr_...` identity while external vault/filesystem artifacts use a distinct `pxa_...`
identity namespace; project associations explicitly reference artifact/root IDs rather than
paths; mutable locators remain reference/provenance data; moving an artifact leaves project
and task identities unchanged; and one artifact may be referenced by multiple projects.
Legacy `linkedFolders` remains compatibility-only. No filesystem API, persistence, write,
import execution or mutation capability exists. Proxima full suite 142 files / 828 tests.
HARD GATE A / A9, Recurrence becomes explicit domain data, accepted on Proxima branch
`hard-gate-a9-canonical-recurrence` at `ed147ea`: recurrence rules are closed typed domain
structures; recurrence series use stable opaque `pxs_...` identity distinct from owner record
identity; ordinary occurrences are semantically addressed by series identity plus scheduled
start without forced record materialization; cancelled, rescheduled and detached exceptions
carry explicit occurrence identity and state; and occurrence-versus-series action scope is
explicit without filename or source-layout dependence. Detached special occurrences retain
their original series identity while referencing a separate canonical record when required.
No persistence, write, import execution or mutation capability exists. Proxima full suite
143 files / 835 tests.
HARD GATE A / A10, No hidden second database, accepted on Proxima branch
`hard-gate-a10-no-hidden-database` at `efdfa11`: domain schema version 2 classifies
retained information into canonical Proxima record/schema data, disposable Backpack-local
state, or external vault-artifact reference/provenance; no canonical semantic value is
allowed to survive only in local state; the architecture/import mapping records how legacy
status, ordering, project type, schema, relations, names, artifact associations and
recurrence cross the future import boundary; and dedicated fixtures prove combined task+event
projects plus independent execution/workflow movement. No Record Store, persistence, write,
import execution or mutation capability exists. Proxima full suite 144 files / 842 tests.
HARD GATE A is closed.
Stage 7 / slice 1, Record-store contract and headless JSON adapter, accepted on Proxima
branch `stage7-record-store-contract` at `3b1af20`: the pathless RecordStore port and JSON
adapter provide opaque-ID filenames, mandatory codec validation, typed read metadata,
conditional create/update/delete, visible corrupt-file failures, and explicit separation from
creator-vault FSA authority. No physical backing location or mutation authority was selected.
Proxima full suite 145 files / 853 tests.
Stage 7 / slice 2, canonical-domain-v2 RecordStore codec/validation, accepted on Proxima
branch `stage7-record-store-contract` at `a8c1b1e`: complete runtime validation now covers
task, project, event, schema and workflow-stage records, all accepted canonical property and
recurrence families, opaque IDs and scoped ordering; the canonical JSON RecordStore factory
always supplies this codec, and malformed, legacy/local and path-bearing shapes fail visibly.
No physical backing location or mutation/recovery authority was selected. Proxima full suite
146 files / 869 tests.
HARD GATE B, physical Proxima-owned Record Store location, creator-accepted on Proxima
branch `stage7-record-store-contract` at `a08340c`: canonical records are assigned to
the OPFS owned by the stable Proxima Backpack origin
`papers-backpack://bp-954ea2cd-6261-410d-baf8-0d1fbd8ca0b1`, with fixed
`record-store/records/` and `record-store/recovery/` namespaces. Authority is reacquired
programmatically from the origin with `navigator.storage.getDirectory()`; no picker,
creator-vault path, project-root database, direct agent storage access or Papers capability is
introduced.
Stage 7 / slice 3, browser OPFS RecordStoreFileBackend, creator-accepted on Proxima branch
`stage7-record-store-contract` at `e7e7362`: the accepted HARD GATE B decision now has a
physical browser backend for `record-store/records/`. It reacquires the stable Backpack
origin's OPFS programmatically, creates/opens only the fixed record namespace, exposes only
the pathless RecordStoreFileBackend seam, rejects non-opaque/path-shaped target names, keeps
raw handles private, and preserves conditional create/update/delete, observed revisions,
stale refusal and visible corrupt/schema-invalid failures. The reserved
`record-store/recovery/` namespace remains unimplemented. No semantic mutation action,
recovery coordinator, restart proof, process-kill proof, multi-caller race policy or import
exists. Proxima full suite 147 files / 879 tests using the accepted serialized full-suite
command; `bridgeDisclosure` isolated 1 file / 3 tests passed.
Stage 7 / slice 4, real Papers restart retention, creator-accepted on Proxima branch
`stage7-record-store-contract` at `a91b2de`: OPFS acquisition was corrected to preserve the
real StorageManager receiver, and an isolated real-host evidence harness created one disposable
canonical record through the accepted backend, closed the first Papers Electron application,
launched a second Papers process against the same isolated userData under a different PID,
returned to the exact stable Proxima Backpack origin, instantiated a fresh OPFS backend and
canonical RecordStore, reread the exact record, and conditionally deleted it. Papers source
remained unchanged and clean. Proxima full suite remains 147 files / 879 tests using the
accepted serialized command; `bridgeDisclosure` isolated 1 file / 3 tests passed.
Physical RecordStore writes remain infrastructure-only. No human or agent semantic mutation
path reaches them. Mutation/recovery authority, process-kill behavior, multi-caller conflict
handling, semantic-action containment and import remain open. Six Stage 0 boxes remain open
where record revisions, bulk-action results and UI-versus-agent equivalence require real
semantic mutation callers. Every ticked box names the commit that closed it.
Stage 7 / slice 5, crash-durability coordinator/journal foundation, creator-accepted on
Proxima branch `stage7-record-store-contract` at `4d61e20`: the fixed
`record-store/recovery/journal.json` OPFS backend now reuses the existing recovery-store
semantics, and a pathless record update/delete coordinator durably persists `prepared`
before the checked physical effect and `committed` after a successful effect. Definite
stale/missing refusal is recorded as `recovered` rather than successful; uncertain
post-effect journal finalization returns `recovery-required`; semantic mutation authority
remains unavailable. Proxima full suite is 148 files / 887 tests using the accepted
serialized command; `bridgeDisclosure` isolated 1 file / 3 tests passed.
Stage 7 / slice 6, durable startup journal loading and bounded restart reconciliation,
creator-accepted on Proxima branch `stage7-record-store-contract` at `d07fa61`: the
record-specific startup gate now loads and reconciles the existing durable recovery journal
before returning any RecordMutationCoordinator. Journal-load or reconciliation failure
blocks authority and exposes no coordinator. Prepared/recovery-required record entries
reuse the existing recovery semantics: an already-present intended effect becomes
`committed`, while unchanged prior bytes become `recovered`. No semantic action is wired
to this authority gate. Proxima full suite is 149 files / 891 tests using the accepted
serialized command; focused startup/recovery evidence is 4 files / 25 tests and
`bridgeDisclosure` isolated is 1 file / 3 tests.
Stage 7 / slice 7, record-recovery ambiguous/corrupt-state blocking, creator-accepted on
Proxima branch `stage7-record-store-contract` at `a937aa4`: the existing record startup
recovery path is proven to block rather than guess when unresolved record bytes match neither
the prior nor intended state, persisting that recovery entry as `blocked` and exposing no
mutation coordinator. Malformed durable recovery-journal data likewise blocks during load
before record access or authority exposure. This is tests-only evidence; production behavior
is unchanged. Proxima full suite is 149 files / 893 tests; focused record-recovery evidence
is 1 file / 6 tests and `bridgeDisclosure` isolated is 1 file / 3 tests.
Stage 7 / slice 8, process-death injection before commit, creator-accepted on Proxima
branch `stage7-record-store-contract` at `9bbedbd`: a real child process runs the accepted
record mutation coordinator to the durable-prepared boundary, with the recovery journal
fsynced while the coordinator remains inside `recovery.save()`. The parent kills that
process before the checked physical record commit is entered. Durable `prepared` state
survives, record bytes/revision remain unchanged, and fresh startup recovery classifies the
operation `not-applied`, persists it `recovered`, and only then restores mutation authority.
This is evidence-only; production behavior is unchanged.
Stage 7 / slice 9, process-death injection after physical record commit but before journal
finalization, creator-accepted on Proxima branch `stage7-record-store-contract` at `97970b7`:
a real child process reaches the complementary crash boundary after the checked record update
has durably committed `new @ record-r2` but while the durable recovery journal still contains
`prepared`. The parent kills the process before journal finalization reaches disk. Fresh
startup recovery observes the intended effect, classifies it `effect-present`, durably marks
the recovery entry `committed`, performs no rollback, and only then restores mutation
authority. This is evidence-only; production behavior is unchanged.
Stage 7 / slice 10, reconciliation idempotence, creator-accepted on Proxima branch
`stage7-record-store-contract` at `188209e`: repeated accepted startup reconciliation
is proven idempotent for terminal record-recovery states. `committed` remains available
with one observational already-committed outcome, `recovered` remains available with no
outcome, and `blocked` remains blocked with one observational blocked outcome. Repeated
startup performs no further journal status write or record access, creates no duplicate
recovery state/outcome, preserves terminal durable state, and returns the same
mutation-authority decision. This is tests-only evidence; production behavior is unchanged.
Stage 7 / slice 11, machine-readable recovery-required/blocked disclosure,
creator-accepted on Proxima branch `stage7-record-store-contract` at `155c736`:
an actual record-coordinator `recovery-required` result now maps into the existing schema-v4
typed ActionFailure vocabulary with stable `outcome/error.code = recovery-required`, while
an actual blocked record-startup result maps into a bounded pathless schema-v1 inspection
with stable code `record-recovery-blocked`. Neither disclosure exposes record filenames,
recovery paths, storage handles or direct record authority. No semantic action or UI mutation
path is enabled.
Stage 7 / slice 12, observed-revision same-record concurrency contract,
creator-accepted on Proxima branch `stage7-record-store-contract` at `052c3b4`:
the existing pathless update/delete mutation contract is proven to bind modifying callers
to an observed record revision. Two independent coordinators racing the same record from
the same observed `record-r1` cannot silently last-write-wins: exactly one conditional
update succeeds at `record-r2`, while the other returns typed `stale` with
`actualRevision = record-r2` and cannot overwrite the winner. This is tests-only evidence;
no semantic UI action, locking, retry or merge behavior is added.
Stage 7 / slice 13, different-record independence, creator-accepted on Proxima branch
`stage7-record-store-contract` at `10dc3c3`: two independent pathless record-mutation
coordinators are proven able to commit distinct records independently. Each caller binds to
its own observed revision, both conditional effects succeed, and both final records retain
their own intended bytes/revisions without cross-record blocking or overwrite. This is
tests-only evidence; no locking, retry, merge or semantic UI mutation behavior is added.
Stage 7 / slice 14, explicit caller refetch/retry with no silent storage-layer merge,
creator-accepted on Proxima branch `stage7-record-store-contract` at `eb0f3fe`: after a
same-record race returns one typed stale loser, the accepted storage/coordinator boundary
performs no automatic retry and leaves the winner untouched. The caller explicitly refetches
the winning revision and submits a new revision-bound mutation; only that new call performs
another conditional write. The retry commits exactly the caller-provided replacement bytes,
with no storage-layer merge, hidden retry, locking or semantic UI mutation behavior added.
Stage 7 / slice 15, aggregate process-kill classification/evidence closeout,
creator-accepted on Proxima branch `stage7-record-store-contract` at `7c89491`:
one aggregate executable matrix now invokes each of the two unchanged, previously accepted
real process-death harnesses exactly once and requires their complementary recovery
classifications. Death after durable `prepared` but before the checked physical effect is
`not-applied → recovered`; death after the checked physical effect but before durable journal
finalization is `effect-present → committed` without rollback. No production or accepted
crash-harness behavior changed.
Stage 7 / slice 16, creator-vault unchanged / Proxima-owned write-tree evidence closeout,
creator-accepted on Proxima branch `stage7-record-store-contract` at `4cdbeea`: the four
designated disposable vault fixture trees are proven unchanged across the record-store test
execution, while a separate disposable physical-tree probe changes exactly the opaque record
JSON and `record-store/recovery/journal.json` beneath the Proxima-owned record-store root.
A sibling creator-vault fixture remains unchanged. The actual creator vault is never read or
touched. Production storage behavior is unchanged.
Stage 7 / slice 17, semantic-action path containment, creator-accepted on Proxima branch
`stage7-record-store-contract` at `e961b94`: actual parsed record-mutation action shapes are
now composed with the accepted RecordStore boundary to prove that path-shaped semantic IDs
cannot reach its backend. Even when tests deliberately bypass the OpaqueRecordId TypeScript
brand, Windows, traversal-shaped and POSIX creator-vault paths are rejected by runtime
opaque-ID validation before any backend read/update/delete call. Backend call counts remain
zero and storage remains empty. No semantic/UI mutation authority is enabled.
Stage 8 / slice 2, durable identity reconciliation / physical-candidate duplicate planning,
creator-accepted on Proxima branch `stage7-record-store-contract` at `be3efdf`, committed
`2026-09-11T14:52:38+07:00`: the existing compatibility reader now exposes its readable
physical candidates before logical-id deduplication without changing ordinary compatibility
state. The dry-run importer assigns a separate HARD-GATE-A opaque candidate identity to every
physical source, emits a versioned durable provenance→identity manifest, reuses persisted
physical-candidate identities on replanning, records duplicate legacy aliases as collision
groups, and leaves references through multi-candidate project aliases explicitly ambiguous
with no selected canonical target. Legacy Markdown, canonical Record Store and staging
remain unwritten; unsupported-frontmatter remains policy-pending.

**In flight** Nothing. The tree is clean and the branch is pushed.

**Next operation** Stage 8 slice 3 — canonical conversion-plan semantics for successfully
decoded candidates: translate legacy task status into separate execution/workflow meaning,
translate legacy order into the accepted scoped-order model, and treat legacy projectType as
compatibility-only input, still without staging materialization or deciding the unresolved
unsupported-frontmatter policy.

**Slice 1 correction is closed in slice 3.** I had briefed the AUTHOR that an empty-slot
click must not create anything, which is right for Elastic and the Deadline Calendar but
wrong here. Slice 3 now seeds the event editor at the clicked time with a one-hour proposal;
the editor remains local-only until its typed-unavailable Save path.

**Two snapping models now coexist and must not be confused.** The Gantt is 42 whole-day
columns, pointer delta over one column width, ties away from zero, no time of day. Schedule
is 96 fifteen-minute slots per civil day, position from local minutes since midnight, height
from duration over 1440. Mixing them yields geometry that looks plausible and is wrong.

**HARD GATE B is closed** at Proxima `a08340c`: the physical backing API is the stable
Proxima Backpack origin's OPFS under `record-store/records/` plus
`record-store/recovery/`. The physical `record-store/records/` backend is accepted at
`e7e7362`. Real import still does not begin: the remaining Stage 7 restart,
mutation/recovery and concurrency acceptance must close first.

**`npm` cannot run on this machine.** The C: drive is at zero bytes free and npm dies with
ENOSPC before executing anything. Run the same steps directly instead —
`node tools/build-fixture-module.mjs`, `./node_modules/.bin/tsc -p …`,
`./node_modules/.bin/vitest run` — and say in the evidence that you did, because substituting
a command for the authored one has caused a real problem in this loop before. Nothing can be
installed until the creator frees space.

**Reviewer outages, 2026-09-10 ~09:50 and ~13:20.** The AUTHOR twice stopped answering:
replies die after a handful of words. Confirmed against the rendered page and reproduced in a
*fresh* thread, so it is the service, not thread length. The first outage had cleared within
about an hour. Try again before concluding anything.

**Reading the reviewer, hard-won, and this one cost hours.** Read a reply by walking the
assistant node's children yourself, taking `textContent` from each `pre code` for fenced
blocks. Do not trust `innerText` anywhere: **while the browser pane is hidden the page is not
laid out and `innerText` collapses to a fragment**, which reads exactly like the model being
cut off mid-sentence. Four complete answers were read as truncated and the AUTHOR was twice
told its replies were broken; it patiently restated the same answer each time. Worse, acting
on that false diagnosis I told it to stop using code blocks — which made the renderer decode
entities and strip backticks, genuinely corrupting the next packet. Fenced code blocks are
the *safe* transport, not the risky one. If a reply looks truncated: front the tab, take a
screenshot, and check before you say a word about it.

<!-- /STATUS -->

**Starting point:** `608bcdc`

**Target:** the old Proxima cockpit interaction model, backed by a cleaner Proxima-owned record database and fully operable by semantic agent actions.

**KeToan is permanently excluded.**

The current repo already has the right beginnings for programmability: `src/app/actionProtocol.ts` defines versioned typed actions/results, request IDs, accepted/rejected events and machine-readable errors. It currently supports only project selection, surface selection, month shifting and fixture reset. The inspection contract is likewise machine-readable, but currently represents only the simplified board/calendar world and reports no real pending mutations.

The existing mutation coordinator already provides checked create/update/move/delete outcomes and structured conflict/refusal results, while the durable recovery store records prepared/committed/recovery-required/recovered/blocked states and reconciles uncertain operations without guessing.

That machinery is reused. **The Markdown-specific semantic writers are legacy-import compatibility code, not the future record database API.**

---

# Global completion rules

These apply to **every stage**.

- The Backpack remains disposable. No feature depends on preserving today's renderer structure or migrating old cockpit/view state.
- Durable **domain data** and disposable **cockpit state** remain explicitly separate.
- Tasks, projects, events, schemas, workflow definitions and relations use the Proxima-owned record store once cutover occurs.
- Notes, drawings and attachments remain ordinary vault files.
- Legacy task/project/event Markdown remains readable for import and historical compatibility but is never silently treated as canonical after cutover.
- No feature reintroduces Markdown syntax, paths, filenames, wikilinks or Obsidian APIs into `src/domain`.
- KeToan does not return through Tools, templates, schema work or generic "future utility" abstractions.
- H4 remains unclaimed. Do **not** add a Papers transaction capability merely because one might be useful someday.
- No gate may require the creator to click something and report the result. This requirement already exists in the repository's engineering ledger: post-enrollment acceptance must be programmatic and machine-readable.
- Every automated UI acceptance can be invoked without a human through a browser/test interaction driver.
- Every canonical mutation can be invoked without the UI through `actionProtocol`.
- Every canonical mutation returns a typed, machine-readable outcome.
- Human UI and agent calls invoke **the same semantic operation**, not parallel implementations.
- An agent is never granted direct write access to record JSON as an alternative to the semantic action protocol.
- Direct record-store modification behind Proxima's back is explicitly unsupported and not exposed as an agent capability.

## Binding agent-action invariant

For every interaction tagged **DATA WRITE** in the parity trace:

```
human gesture
      │
      ▼
typed Proxima semantic action
      │
      ├── UI caller
      └── agent caller
      │
      ▼
semantic validation
      │
      ▼
record/file mutation boundary
      │
      ▼
typed ActionResult
```

Never:

```
agent → filesystem → JSON record
```

That would create an uncoordinated second writer and destroy the very write serialization gained by moving records away from Obsidian.

A stage containing a human mutation is **not closed** until its equivalent action can be submitted programmatically and its effect confirmed through inspection.

---

# Stage 0 — Expand the automation/acceptance spine first

Do this before adding large amounts of UI.

The current action dispatcher is synchronous and typed but only understands four non-domain-writing actions. Its success result already supplies `requestId`, `changed`, `stateRevision` and snapshot; failures already have typed errors. Preserve that pattern.

## Work

- [ ] Establish one public versioned action union for:
  - [ ] presentation actions;
  - [ ] local-state actions;
  - [ ] record mutations;
  - [ ] vault-artifact gestures.

- [x] Extend the result taxonomy so mutation callers can distinguish at minimum: — `da7881f`
  adds `src/app/actionTaxonomy.ts` with the eight outcomes, `outcomeForErrorCode`, and a
  `categoryOf` that returns `undefined` for an unregistered type instead of defaulting;
  `4554fea` widens the error-code map. Reverting either leaves `actionProtocol.ts`'s
  compile-time union check without a taxonomy to match and typecheck fails loudly.
  - [x] `accepted`;
  - [x] validation refusal;
  - [x] not found;
  - [x] stale observed revision;
  - [x] semantic conflict;
  - [x] unavailable action;
  - [x] recovery required / ambiguous commit;
  - [x] storage failure.

- [x] Preserve a unique request ID through dispatcher → semantic operation → mutation journal → result/event. *(dispatcher → result/event only; the journal leg arrives with the record store.)*
  — `da7881f` threads `requestId` through every result shape. The journal leg is still
  absent, so this box will reopen when the record store lands.
- [x] Include affected logical record IDs in mutation results. *(`entityIds` is required on every result, empty rather than absent for presentation actions.)*
  — `da7881f`. Required, not optional: an absent `entityIds` would be indistinguishable
  from "touched nothing", so presentation actions carry an empty array.
- [ ] Include resulting record revision(s) where a record changed.
- [ ] Define bulk-action results per entity so partial success can never be mistaken for complete success.
- [x] Make the inspection contract expose: — `2a2ff0c` raises `src/app/inspection.ts` to
  schema 3 and makes the projection state what it does not know; `2450828` adds the cockpit
  `localState` (surface, selection, modes, tab, calendar month). Reverting `2a2ff0c` returns
  the projection to claims it cannot support, which is what the schema bump exists to stop.
  - [x] current surface and submode;
  - [x] local cockpit state needed for test assertions;
  - [x] record revisions;
  - [x] pending operations;
  - [x] latest action/mutation event sequence; *(action sequence real; mutation is `null`
        because no mutation stream exists — a fabricated `0` would read as a quiet one.)*
  - [x] settled/busy state.

- [x] Replace the current permanently empty `pendingOperations: []` implementation with actual state once asynchronous mutation exists. — `2a2ff0c`. *(Now `{ tracking: 'unavailable', items: [] }` — "there is no tracking" rather than "nothing is pending". The guard refuses a projection claiming unavailable tracking while carrying items. Becomes a real list when mutation exists.)*
- [x] Provide a programmatic browser interaction harness capable of: — `5d5cebf` adds
  `src/browser/interactionHarness.ts` against a real DOM (happy-dom), all nine gestures on
  `InteractionHarness`. This is the commit that closed HARD GATE 0; reverting it reopens the
  gate and Stages 1–6 lose their only non-visual acceptance route.
  - [x] click;
  - [x] pointer down/move/up;
  - [x] drag/drop;
  - [x] resize gestures;
  - [x] Shift modifier;
  - [x] keyboard entry;
  - [x] Escape;
  - [x] context-menu invocation;
  - [x] hover.

- [x] Give important interactive geometry stable machine keys independent of visual text.
  — `5d5cebf` defines `data-c1-key` and makes `machineTarget` throw on zero or multiple
  matches, so an ambiguous key fails the test instead of silently picking one; `2450828`
  emits the keys from the renderer.
- [x] Tests can assert provisional drag/resize state **before** pointer release. — `5d5cebf`.
  Pointer down, move and release are separate calls returning the live gesture, so a test
  reads mid-drag geometry rather than only the settled result.

## Acceptance

- [ ] An action submitted through the UI and the equivalent action submitted through the agent/programmatic entry point produce the same semantic operation/result shape.
- [x] Invalid action input performs zero durable writes. — `4554fea`, proven by hashing every
  fixture byte before and after a rejected dispatch.
- [x] Unknown action type returns a typed refusal. — `4554fea`.
- [x] Every action result can be runtime-validated at the boundary. — `4554fea` makes the
  guard refuse a result whose category contradicts the registry, so a mislabelled result
  cannot cross the boundary even when the dispatcher believes it succeeded.
- [x] Test code can perform a real drag sequence without creator input and inspect the intermediate state. — `5d5cebf`.
- [x] Test code can wait for `settled` rather than relying on sleeps. — `2a2ff0c` reports busy
  state directly on the projection, so callers poll inspection instead of guessing a delay.
- [x] No test requires visual inspection by the creator. — holds as of `5d5cebf`; every suite
  since asserts through the harness or inspection. Any commit that breaks this unticks it.

## Evidence

- [x] Action parser/guard tests. — `tests/actionTaxonomy.test.ts`, 14 tests, on
  `proxima-backpack` branch `stage0-action-spine` at `da7881f`. Full suite 93 files /
  588 tests, typecheck clean.
- [ ] UI-versus-agent equivalence tests. *(nothing to compare yet: no action has two callers.)*
- [x] Programmatic pointer/keyboard harness tests. — `tests/interactionHarness.test.ts`,
  6 tests, at `5d5cebf`.
- [x] Machine-readable inspection snapshot fixtures. — `tests/inspection.test.ts` at
  `2a2ff0c`, extended at `2450828` with the cockpit `localState`.
- [ ] A test proving malformed agent requests never reach mutation storage. *(partially:
  malformed input is proven to leave dispatcher state untouched; there is no mutation
  storage to reach yet.)*

### Progress

Categories and outcomes exist and are enforced at the boundary. The action union itself
still contains only presentation actions, so the local-state, record-mutation and
artifact-mutation rows above stay open until actions of those categories are registered.
`categoryOf` returns undefined for an unregistered type rather than defaulting, and
`resultFor` throws rather than accept an action whose cost nobody declared.

### HARD GATE 0

**Stages 1–6 may begin only when programmatic UI acceptance exists.**

Otherwise the project will accumulate "looks right when I click it" behavior that cannot be closed autonomously later.

---

# Stage 1 — Restore the cockpit shell and navigation

Presentation/local state only. No storage migration dependency.

## Work

- [x] Replace the simplified Board / Calendar / Canvas-only navigation with the Proxima cockpit hierarchy: — `2450828` adds
  `src/browser/cockpitNavigation.ts` and rewires `main.ts` onto it. Canvas is kept as a
  fourth surface rather than folded into the three, so nothing the Backpack already did is
  lost. Reverting returns the app to Board/Calendar/Canvas and every Stage 2+ surface has
  nowhere to mount.
  - [x] Tasks;
  - [x] Schedule;
  - [x] Projects Hub;
  - [x] retain Canvas as a Backpack capability without displacing old Proxima surfaces.

- [x] Tasks contains: — `2450828`, `TasksMode = 'elastic' | 'timekeeping'`.
  - [x] Elastic Boards;
  - [x] Timekeeping.

- [x] Schedule exposes: — `2450828`, all six as `ScheduleMode`; 4-Day is `'four-day'` in
  code, and the label is rendered separately from the value so the machine key never depends
  on visible text.
  - [x] Day;
  - [x] 4-Day;
  - [x] Week;
  - [x] Month;
  - [x] Year;
  - [x] Agenda.

- [x] Projects Hub opens project workspaces. — `2450828`.
- [x] Project workspace exposes appropriate tabs from one project rather than treating selection as only a global filter. — `2450828`, `ProjectWorkspaceTab` = notes, task-board, backlog, deadlines, schedule.
- [x] Project selection remains view state. — `2450828`; it lives in the dispatcher snapshot,
  never in a record.
- [x] Current surface/subsurface remains local cockpit state. — `2450828`.
- [x] No migration framework is created for this state. — `2450828`; deliberately none.
- [x] Resetting/rebuilding the Backpack may discard it without affecting records. — `2450828`.

## Local/presentation actions

- `surface.select`
- `tasks.mode.select`
- `schedule.mode.select`
- `project.select`
- `project.workspace-tab.select`
- `calendar.navigate`
- `calendar.today`

These do not need to mutate durable records.

## Acceptance

- [x] Every old top-level destination is programmatically reachable. — `2450828`,
  `tests/cockpitNavigation.test.ts` walks all four surfaces and every submode by machine key.
- [x] Project selection does not alter any record JSON/source data. — `2450828`.
- [x] Reload/reset of local cockpit state leaves canonical records byte-identical. —
  `2450828`, `tests/actionProtocol.test.ts:196` hashes every durable fixture byte before and
  after a full navigation walk. This is the test that would catch a future surface quietly
  writing to the vault.
- [x] Inspection identifies exactly which surface/subsurface/project/tab is active. —
  `2450828` adds `localState` to the projection.

## Evidence

- Navigation contract tests.
- Headless browser tests for every navigation target.
- Before/after durable-store hash proving navigation does not write records.

---

# Stage 2 — Elastic presentation and local execution session

No record writes yet.

The current domain already contains weights, fixed/max duration and Elastic concepts, but its execution-column membership is derived through status definitions. Do not deepen that coupling; the structural replacement happens before import.

## Work

### Board rendering

- [x] Restore Backlog / Running / Finished appearance. — `57860d3` replaces the simplified
  board renderer with the Elastic cockpit while retaining status-derived Backlog, Running
  and Finished membership.
- [x] Restore proportional Running-card height. — `57860d3` sizes Running cards from the
  calculated execution allocation for the current target horizon rather than using one
  fixed card height.
- [x] Restore task-property pills/chips. — `57860d3` renders schema-labelled task properties
  as keyed pills on Elastic cards and scopes modal copies so machine keys remain unique.
- [x] Restore hover affordances. — `57860d3` restores an explicit interactive hover treatment
  on Elastic task cards instead of leaving clickable/draggable cards visually inert.
- [x] Restore clickable task cards opening a modal. — `57860d3` routes keyed Elastic card
  clicks through the real DOM interaction boundary into the task quick-editor state.
- [x] Render read-only task values in that modal even before Save is enabled. — `57860d3`
  exposes current task values in the quick editor while Save and Delete remain explicitly
  unavailable before write parity.

### Execution planning

- [x] Restore editable execution target date/time. — `57860d3` adds a datetime-local execution
  target whose browser-local wall time round-trips to the canonical instant through
  `elastic.target.set`. An earlier draft printed UTC into that local-time field, which would
  have mis-set the target by the machine's offset; reverting reintroduces that.
- [x] Restore default future execution horizon behavior matching old Proxima. — `57860d3`
  restores the four-hours-from-now default using the injected clock rather than a hard-coded
  wall time.
- [x] Recalculate Running allocations immediately as the target changes. — `57860d3` rerenders
  Elastic allocation geometry from the newly dispatched target, with deterministic tests
  proving a changed target changes allocations.
- [x] Restore Lock. — `57860d3` adds `elastic.lock`, capturing the injected clock instant and
  freezing target editing for the active local execution run.
- [x] Restore Unlock. — `57860d3` adds `elastic.unlock`, clearing the local lock without
  changing task records or the selected execution target.
- [x] Restore live elapsed-progress visualization. — `57860d3` derives elapsed run progress
  from lock time and target and advances the live cockpit on its one-second external-mode
  tick.
- [x] Restore per-task allocation/progress during a locked run. — `57860d3` exposes
  deterministic allocation minutes and sequential per-task progress from the locked Elastic
  timeline.
- [x] Lock information is **LOCAL STATE**, not task data. — `57860d3` keeps target and lock
  timestamps in dispatcher/inspection cockpit state and registers their actions as
  `local-state`.
- [x] No task JSON/legacy Markdown is touched when: — `57860d3` hashes the durable fixture
  before and after the full target/lock/clock-advance/unlock/local-state lifecycle and
  proves the bytes are identical.
  - [x] target time changes;
  - [x] run locks;
  - [x] time advances;
  - [x] run unlocks.

### Drag feel without committing data yet

- [x] Implement card pickup. — `57860d3` gives keyed Elastic cards a real drag-start pickup
  state and clears that visual state on drag completion or cancellation. Clearing is split
  between `clearDragFeedback` (per pointer move) and `clearDragPickup` (per drag); folding
  them back together erases the pickup state on the first move.
- [x] Correctly sized insertion placeholder. — `57860d3` matches the original drag geometry by
  sizing the insertion placeholder to `min(90px, dragged card height)` while preserving full
  card geometry separately.
- [x] Placeholder moves during drag. — `57860d3` clears the prior insertion slot and exposes
  the newly targeted keyed slot as the pointer moves before drop.
- [x] Destination-column highlight/feedback. — `57860d3` makes the active drag destination
  visibly styled, not merely marked by an otherwise inert DOM class.
- [x] Invalid/outside drop restores visual source state. — `57860d3` clears pickup, placeholder
  and destination feedback when the drag ends outside a valid insertion slot without
  changing task state.
- [x] During this stage successful state-changing drop remains disabled/refused with a typed "mutation unavailable before record-store cutover" result rather than silently pretending to save. — `57860d3` routes drop through `task.execution.move` as a `record-mutation` and returns `action-not-available` before record-store cutover without mutating the task.

## Local-state actions

- `elastic.target.set`
- `elastic.lock`
- `elastic.unlock`
- optional `elastic.session.reset`

## Acceptance

- [x] Changing target changes card allocation deterministically. — `57860d3` deterministic
  Elastic geometry tests compare different targets and prove the resulting allocation
  changes predictably.
- [x] Lock survives ordinary rerender within the same Backpack session if local persistence is intended. — `57860d3` keeps lock state outside disposable render markup and proves a normal rerender preserves the active lock and target.
- [x] Destroying local state does not alter any domain record. — `57860d3` resets/discards
  Elastic cockpit state under before/after durable-source hashing and proves domain bytes
  remain unchanged.
- [x] Locked run advances under injected clock. — `57860d3` deterministic clock tests advance a
  locked run and prove overall and per-task progress advance without wall-clock sleeps.
- [x] Programmatic drag shows placeholder before release. — `57860d3` the real-DOM interaction
  harness inspects the keyed insertion placeholder after drag movement and before
  drop/release.
- [x] Pre-storage DATA WRITE drop refuses visibly rather than updating only the DOM. —
  `57860d3` programmatic drop receives the typed unavailable result, renders the refusal in
  the cockpit, and leaves canonical task state unchanged.

## Evidence

- Deterministic clock tests.
- Elastic geometry tests.
- Programmatic drag mid-state assertions.
- Record-source before/after hashes proving zero durable writes.

---

# Stage 3 — Restore Timekeeping presentation

No storage migration dependency.

## Work

### Composition controls

- [x] Calendar panel toggle. — `760e54d` adds Calendar as independently visible Timekeeping
  panel local state through `timekeeping.panel.set-visible`.
- [x] Timeline/Gantt panel toggle. — `760e54d` adds Timeline/Gantt as an independently
  toggleable composition slot without making Timekeeping panels exclusive. The panel itself
  renders empty until its own slice.
- [x] Countdowns panel toggle. — `760e54d` adds Countdowns as an independently toggleable
  composition slot, likewise reserved until its own slice.
- [x] Multiple panels can be visible simultaneously. — `760e54d` makes Timekeeping panel
  visibility compositional local state, so Calendar, Timeline/Gantt and Countdowns can all
  be visible at once. This is the box that stops the surface degenerating into tabs.
- [ ] Panel sizing/layout is local state only. *(visibility is local state as of `760e54d`;
  no sizing exists yet, so this stays open rather than being closed by a technicality.)*

### Deadline Calendar

- [x] Month navigation. — `760e54d` reuses the local calendar cursor for deterministic
  previous/next month navigation.
- [x] Current-day styling. — `760e54d` marks the injected-clock civil day as the current day
  with a stable machine-addressable cell.
- [x] Deadline task placement. — `760e54d` projects tasks with real deadlines deterministically
  onto their civil-date cells; tasks without deadlines are not invented onto the calendar.
- [x] Overdue/urgency styling. — `760e54d` projects and styles incomplete deadlines before the
  injected clock as overdue, and reuses the existing deadline-pressure hue model so urgency
  tracks remaining time rather than a second, parallel threshold system.
- [x] Click task → task modal. — `760e54d` routes deadline cards through the existing task-modal
  affordance, exercised through `data-c1-key` real-DOM interaction. The modal still lives in
  `elasticCockpit.ts`; extract it when Timekeeping makes that awkward, not before.
- [x] Do not invent empty-day task creation if the old deadline surface did not have it. —
  `760e54d`; empty cells carry no creation action or affordance, and a test asserts it.

### Timeline/Gantt

- [x] Render task range from effective start to deadline. — `fb67685` projects truthful task
  spans from effective start through deadline, clipped to the visible civil-day window
  without inventing missing bounds. A task with only one bound draws a one-day milestone
  rather than a span; reverting reintroduces the temptation to invent the other end.
- [x] Render row structure. — `fb67685` renders machine-addressable task rows carrying span,
  start-only and deadline-only geometry as data, plus current-day marking, the panel's own
  month navigation and existing task-modal entry.
- [x] Hover/edge affordances. — `c1f8c93` gives the start and end boundaries separate
  machine-addressable 8px resize handles with 2px boundary rules and a col-resize
  affordance.
- [x] Normal pointer drag previews a bar move. — `c1f8c93` previews horizontal whole-day
  movement and vertical row movement live before release, with the picked bar following the
  gesture rather than jumping on drop.
- [x] Shift-modified edge manipulation previews resize. — `c1f8c93`; Shift is latched at
  pointer-down, so releasing the key mid-gesture does not silently turn a resize into a move.
- [x] Start-edge and end-edge geometry are distinct. — `c1f8c93` start-edge resize moves the
  start column and inversely changes width; end-edge resize holds the start column and
  changes width alone.
- [x] Proposed date values visible during interaction. — `c1f8c93` shows the proposed start and
  deadline beside the provisional geometry, before any semantic write is emitted.
- [x] Occupied row resolution matches the old continuous behavior rather than producing unnecessary modal errors. — `c1f8c93` resolves a drag into an occupied row to that row's
  insertion index and highlights it. **This is the box most likely to be undone by accident:
  the obvious-looking "fix" is to refuse the drop as invalid, and that is exactly the
  error-dialog behaviour the original did not have.** Continuous resolution is the parity
  requirement, not a convenience.
- [x] No canonical write yet; final drop is typed unavailable until cutover. — `c1f8c93` a valid
  release emits exactly one typed `task.timeline.change` record mutation and receives
  `action-not-available`. **Inverted or sub-one-day geometry emits zero write intents at
  all** — not a refused one — and restores the original geometry, so an invalid drag leaves
  no durable trace and nothing downstream ever sees a proposal the cockpit already knew was
  impossible.

### Countdowns

- [x] Overdue. — `2b8a145`; remaining time below zero.
- [x] under one day. — `2b8a145`; zero up to but excluding 24h.
- [x] under three days. — `2b8a145`; 24h up to but excluding 72h.
- [x] under one week. — `2b8a145`; 72h up to but excluding 168h.
- [x] later. — `2b8a145`; 168h and above. **The five boundaries are exactly `< 0`,
  `[0, 24h)`, `[24h, 72h)`, `[72h, 168h)` and `[168h, ∞)`** — written out because this is
  precisely the kind of thing a later agent re-derives slightly differently and never
  notices.
- [x] Live countdown progression. — `2b8a145`; the visible panel rerenders once per second
  from the current clock, updating displayed remaining time without touching records.
- [x] Automatic movement between buckets as injected clock advances. — `2b8a145`
  reclassifies from the clock on every tick rather than assigning a bucket once, so items
  move by themselves; advancing the injected clock 30h carries three tasks across three
  boundaries with no user action.
- [x] Click countdown item → task editor. — `2b8a145`; the same modal the calendar and the
  Gantt use, entered through the real-DOM harness, with durable state unchanged.

## Local/presentation actions

- `timekeeping.panel.set-visible`
- `timekeeping.panel.resize` if panel geometry is remembered.
- `timekeeping.timeline.viewport.set` if required for agent steering.

## Acceptance

- [x] Same task can be observed simultaneously in Calendar/Gantt/Countdown where applicable. — `37e722b` proves one qualifying task visible in all three panels at once, and proves both
  sides of "where applicable": start-only stays Gantt-only, no-deadline appears in none.
  Without those exclusions the row could be satisfied by a surface that showed everything
  everywhere.
- [x] Clock-only changes never write records. — `37e722b`; Countdowns visibility is established
  as render setup **before** the measurement, and after that there is no dispatch and no
  interaction at all — only the clock moving and the ticker firing. Presentation changes and
  the SHA-256 of durable state is identical. Proving this from adjacent before/after hashes
  would not have been the same claim.
- [x] Programmatic Shift-resize visibly changes provisional Gantt geometry. — `c1f8c93`;
  real-DOM Shift gestures change provisional start/end geometry before release, and the two
  edges produce distinct previews.
- [x] Invalid resize returns to authoritative geometry. — `c1f8c93`; an inverted resize is
  marked invalid, emits no `task.timeline.change` intent at all, and restores the original
  grid geometry on release.
- [x] Panel composition survives rerender only according to local-state policy. — `760e54d`;
  panel visibility lives in dispatcher local state, so composition survives an ordinary
  rerender while fixture reset destroys it and leaves durable records unchanged.

## Evidence

- Injected-clock urgency tests.
- Calendar projection tests.
- Gantt pointer/Shift tests.
- Zero-write proof for all presentation/local-state operations.

---

# Stage 4 — Restore Schedule presentation in all six modes

No record migration dependency.

## Work

### Shared navigation

- [x] Day. — `7357b4d`; one civil-day column.
- [x] 4-Day. — `7357b4d`; four adjacent civil-day columns.
- [x] Week. — `7357b4d`; seven. All three are one geometry family over the same vertical grid,
  differing only in column count.
- [x] Month. — `5d97cdc`
- [x] Year. — `5d97cdc`
- [x] Agenda. — `5d97cdc`
- [x] Previous. — `fc460f6`
- [x] Today. — `fc460f6`
- [x] Next. — `fc460f6`
- [x] Project/event filtering without mutation. — `fc460f6`

### Day / 4-Day / Week

- [x] 24-hour time grid. — `7357b4d`; 96 equal 15-minute slots per day, the same scale in all
  three modes. **This is not the Gantt's model** — that one is 42 whole-day columns. Two
  snapping models now coexist and confusing them yields plausible, wrong geometry.
- [x] Correct event vertical placement. — `7357b4d`; position derives from local minutes since
  midnight, and an event crossing midnight is segmented truthfully at the civil-day boundary
  rather than drawn as one impossible bar or dropped.
- [x] Correct duration height. — `7357b4d`; height is duration over the 1440-minute day.
- [x] Empty-cell click seeds event editor with clicked time. — `2e74059`; *(previously not
  built, and my fault:
  I briefed the AUTHOR that empty-slot click must NOT create, which is what the Elastic and
  Deadline Calendar surfaces require but the opposite of what this row asks. `7357b4d` renders
  empty slots deliberately inert. Seeding the editor from the clicked time is real work and
  is now owed.)*
- [x] Default one-hour event proposal. — `2e74059`; *(same mis-brief; goes with the row above.)*
- [x] Event click opens editor. — `7357b4d`; a read-only local event editor, the first modal in
  the codebase that is not the task modal.
- [x] Drag preview follows pointer. — `7292075`
- [x] Cross-day drag preview in multi-day modes. — `7292075`
- [x] 15-minute snap during drag. — `7292075`
- [x] Bottom-edge resize affordance. — `7292075`
- [x] 15-minute duration snapping. — `7292075`
- [x] Live resize preview. — `7292075`
- [x] Final save/drop remains unavailable until record-store mutation stage. — `7292075`

### Month

- [x] Month grid. — `5d97cdc`
- [x] Date-level occurrence projection. — `5d97cdc`
- [x] Event click opens editor. — `5d97cdc`
- [x] No Week-style time-height resize imported into Month. — `5d97cdc`

### Year

- [x] Twelve mini-month overview. — `5d97cdc`
- [x] Date navigation/drill-down. — `5d97cdc`
- [x] Event indicators. — `5d97cdc`

### Agenda

- [x] Chronological date groups. — `5d97cdc`
- [x] Event rows. — `5d97cdc`
- [x] Event click opens editor. — `5d97cdc`
- [x] No arbitrary drag ordering. — `5d97cdc`

### Recurrence projection

- [x] Existing recurring events expand into visible occurrences. — `448c65f`
- [x] Expansion itself writes nothing. — `448c65f`
- [x] Clicking a recurring occurrence can reach the later scope-choice modal. — `448c65f`
- [x] No generated ordinary occurrence is prematurely materialized as a separate record merely to display it. — `448c65f`

## Acceptance

- [ ] Same event projects correctly across all six views.
- [x] Day/4-Day/Week use 15-minute interaction geometry. — `7292075`
- [x] Month/Year/Agenda do not inherit invalid resize semantics. — `5d97cdc`
- [x] Recurrence expansion is deterministic under injected clock/date range. — `448c65f`
- [x] Empty-cell creation opens a form without modifying source data before Save. — `2e74059`

## Evidence

- Six-mode projection tests.
- Automated event drag/resize preview tests.
- Recurrence-expansion tests.
- Zero-write proof before Save.

---

# Stage 5 — Restore Projects Hub and read-only project workspaces

No record migration dependency.

## Projects Hub work

- [ ] Project cards display:
  - [ ] name;
  - [ ] description;
  - [ ] age;
  - [ ] task count;
  - [ ] overdue count;
  - [ ] P1/high-priority equivalent where represented;
  - [ ] next deadline;
  - [ ] archive state;
  - [ ] visual identity where available.

- [ ] Active/archived filtering.
- [ ] Clicking a project opens its workspace.
- [ ] New Project button opens its modal even before Save is enabled.
- [ ] Archive/restore/delete controls exist but refuse DATA WRITE until storage cutover.

## Workspace work

- [ ] Notes.
- [ ] Task Board.
- [ ] Backlog.
- [ ] Deadlines.
- [ ] Schedule capability can coexist with tasks instead of being hidden behind permanent task/schedule project silos once the corrected domain lands.

### Notes — read side

- [ ] Project-linked vault artifact tree.
- [ ] Folder expand/collapse.
- [ ] File selection.
- [ ] Markdown preview.
- [ ] Canvas preview.
- [ ] Excalidraw preview where supported.
- [ ] Hover affordances.
- [ ] Context menu opens programmatically.
- [ ] Read/open/reveal-like operations remain presentation.
- [ ] Drag targets can preview valid folder destinations without committing moves yet.

### Task Board — read side

- [ ] Project workflow columns.
- [ ] Card click.
- [ ] Column presentation colors.
- [ ] Local display order.
- [ ] Drag pickup/placeholders implemented.
- [ ] Durable workflow transition still disabled until corrected domain/store exists.

### Deadlines

- [ ] Reuse the Timekeeping interaction implementation project-scoped rather than independently reinventing it.

## Acceptance

- [ ] Opening a project changes the cockpit, not canonical data.
- [ ] Project Notes can inspect ordinary vault files without treating them as database records.
- [ ] Same task can be visible in project Board, Backlog and Deadlines.
- [ ] Project can eventually show both tasks and events; no new UI work assumes `projectType` is permanent.

## Evidence

- Programmatic project navigation tests.
- File-tree read/preview fixture tests.
- Cross-tab projection tests.
- Zero-write proof for all read-only project navigation.

---

# Stage 6 — Restore Backlog/database presentation and modal completeness

Still before migration.

## Backlog

- [ ] Search.
- [ ] Tag filtering.
- [ ] Property filters.
- [ ] Type-appropriate comparison operators.
- [ ] Multiple filters.
- [ ] Remove filter.
- [ ] Sort ascending/descending.
- [ ] Sort indicator.
- [ ] Custom-property columns.
- [ ] Resizable columns.
- [ ] Row selection.
- [ ] Select all.
- [ ] Multi-selection.
- [ ] Task row/name click opens editor.
- [ ] Relation display.
- [ ] Rollup display.
- [ ] Formula display.
- [ ] Bulk Complete control visible but unavailable until write cutover.
- [ ] Bulk Delete control visible but unavailable until write cutover.

## Task modal

All existing meaningful fields must be representable:

- [ ] name;
- [ ] project;
- [ ] execution state;
- [ ] workflow stage where project-scoped;
- [ ] weight;
- [ ] fixed-duration enable/value;
- [ ] maximum duration;
- [ ] start date;
- [ ] deadline;
- [ ] completion;
- [ ] custom text property;
- [ ] number;
- [ ] select;
- [ ] multi-select;
- [ ] date;
- [ ] checkbox;
- [ ] relation;
- [ ] derived rollup;
- [ ] derived formula;
- [ ] recurrence if task recurrence remains supported.
- [ ] Cancel/Escape discards provisional form state.
- [ ] Save is disabled/refused until the new record write path exists.

## Event modal

- [ ] name.
- [ ] description.
- [ ] project.
- [ ] start.
- [ ] end.
- [ ] color if event metadata supports it.
- [ ] recurrence controls.
- [ ] until/end condition.
- [ ] exception/scope UX.
- [ ] Save/Delete unavailable until write cutover.
- [ ] Cancel/Escape loses no data.

## Project modal

- [ ] name.
- [ ] description.
- [ ] metadata that survives the corrected model.
- [ ] Do **not** require task-versus-schedule type in the successor record shape.

## Recurrence-scope modal

- [ ] This occurrence.
- [ ] Entire series.
- [ ] Cancel.
- [ ] No mutation while simply choosing/opening scope.

## Template UI

- [ ] Paste/type.
- [ ] Parse.
- [ ] Preview.
- [ ] Structured parse errors.
- [ ] Execution disabled until record write actions exist.
- [ ] Exact old textual mini-language is not assumed immutable if the same presentation/workflow can be preserved cleanly.

## Acceptance

- [ ] Every old editor can be opened programmatically.
- [ ] Every unsaved field can be changed and cancelled without durable change.
- [ ] Search/filter/sort never mutate records.
- [ ] Relation/rollup/formula projection works without wikilink semantics leaking into UI code.
- [ ] All future Save/Delete buttons currently produce a typed unavailable result rather than fake success.

## Evidence

- Modal state tests.
- Query/filter/sort tests.
- Derived-property tests.
- Automated cancel/Escape tests.
- Durable-store/source no-write evidence.

---

# HARD GATE A — Fix the future database shape before importing anything

**No record-store import may start before this closes.**

The current domain still contains structural residue from the plugin: `Project.projectType` is `'task' | 'schedule'`; a task has one generic `status`; `StatusDefinition` maps that status into an Elastic column; task ordering is a single `orderIndex`; relation schema still has a `targetFolder` field.

If those shapes are copied into JSON first, the migration will preserve precisely the database constraints the creator approved removing.

## A1 — Stable opaque identity

- [x] Every task/project/event/schema/workflow-stage record has an opaque stable ID. — `71b0a2b`
- [x] Display name is not identity. — `71b0a2b`
- [x] Filename is not identity. — `71b0a2b`
- [x] Physical file location is not identity. — `71b0a2b`
- [x] Record lookup never derives meaning from JSON filename. — `71b0a2b`
- [x] Rename does not alter identity. — `71b0a2b`
- [x] Import policy for legacy explicit IDs is settled: — `71b0a2b`
  - [x] they become aliases/provenance only; — `71b0a2b`
  - [x] they must not silently defeat the opaque-ID requirement. — `71b0a2b`

### Acceptance

- [x] Change record name; ID unchanged. — `71b0a2b`
- [x] Change physical record filename if adapter permits; domain identity unchanged. — `71b0a2b`
- [x] Two records may have identical display names. — `71b0a2b`

---

## A2 — Separate execution state from workflow stage

Replace the old shared status concept.

- [x] Task has explicit execution state capable of: — `07d4926`
  - [x] Backlog; — `07d4926`
  - [x] Running; — `07d4926`
  - [x] Finished. — `07d4926`

- [x] Task independently has project workflow-stage identity. — `07d4926`
- [x] Workflow stage references stable stage ID, not display text. — `07d4926`
- [x] Moving a task into global Running does not erase project workflow stage. — `07d4926`
- [x] Moving a task from Review → Done-like workflow stage does not automatically change global execution state unless an explicit semantic rule is separately defined. — `07d4926`

### Acceptance

Fixture proves a task can simultaneously be:

```
execution = Running
workflow = Review
```

and appears correctly on both surfaces. — `07d4926`

---

## A3 — Scoped ordering

The single current `orderIndex` cannot remain the universal answer.

- [x] Define separate ordering semantics for: — `bf56679`
  - [x] Elastic execution queue; — `bf56679`
  - [x] project workflow stage; — `bf56679`
  - [x] any durable user-authored ordering elsewhere. — `bf56679` *(the canonical model currently admits no additional durable manual order scope; calendar chronology is derived and Gantt rows are local state)*

- [x] Workflow ordering is scoped at least by project + stage. — `bf56679`
- [x] Reordering Elastic cannot silently reorder the project's workflow board. — `bf56679`
- [x] Reordering the project board cannot silently alter Elastic order. — `bf56679`
- [x] Decide Gantt row placement explicitly: — `bf56679`
  - [x] preferred correction: treat pure row layout as LOCAL STATE; — `bf56679`
  - [ ] if creator declares it semantic priority, give it its own scoped field.

- [x] Even if Gantt row placement becomes LOCAL STATE, retain a typed programmatic action because the old DATA WRITE gesture must remain agent-operable. — `bf56679` *(existing typed `task.timeline.change.targetRowIndex` retained; durable mutation remains unavailable until record-store cutover)*

---

## A4 — Project-type silo removed

- [x] Project can associate with tasks and events simultaneously. — `795f019`
- [x] Project UI capabilities are determined by available data/workspace configuration, not immutable `task|schedule` type. — `795f019`
- [x] Existing legacy `projectType` is import metadata only if needed for faithfully reconstructing old presentation. — `795f019`
- [x] No selector filters task visibility merely because a project was formerly labeled schedule. — `795f019`
- [x] No selector filters event visibility merely because a project was formerly labeled task. — `795f019`

The inspection and selector contracts no longer use `projectType` as capability or visibility
authority; inspection schema v5 exposes data/workspace-derived capabilities instead. — `795f019`

---

## A5 — Schema is canonical data

- [x] Property-schema definitions are durable Proxima records. — `289754d`
- [x] Schema identity is opaque/stable. — `289754d`
- [x] Schema does not live in Backpack local settings. — `289754d`
- [x] Select-option identity is stable and separate from label. — `289754d`
- [x] Formula definitions are durable. — `289754d`
- [x] Rollup definitions are durable. — `289754d`
- [x] Relation definitions are durable. — `289754d`
- [x] Colors/column widths/collapsed UI state remain LOCAL STATE where they are only presentation. — `289754d`

---

## A6 — Relations are ID-based

- [x] Relation values contain logical record IDs. — `26c84d4`
- [x] Relation semantics do not contain wikilinks. — `26c84d4`
- [x] Relation semantics do not depend on target filenames. — `26c84d4`
- [x] Relation schemas do not use `targetFolder` as the conceptual target. — `26c84d4`
- [x] Rename/move of a human-facing record representation cannot break relation identity. — `26c84d4`
- [x] Markdown/wikilink conversion exists only inside legacy import/export compatibility code if required. — `26c84d4` *(canonical domain introduces no Markdown/wikilink conversion; existing compatibility code remains outside canonical relation semantics)*

---

## A7 — Names are independent from storage representation

- [x] Task/project/event titles are ordinary fields. — `270f8cb`
- [x] Any valid domain title can be represented without changing filename logic. — `270f8cb`
- [x] Colon/YAML quoting rules disappear from canonical record validation. — `270f8cb`
- [x] JSON encoding, not hand-authored source syntax, represents canonical structured values. — `270f8cb`

---

## A8 — Project/filesystem association is explicit

- [x] A project can explicitly reference its Notes/drawings/attachments roots or artifacts without asserting that filesystem location *is* project identity. — `1c87f24`
- [x] Moving a note does not mutate task/project IDs. — `1c87f24`
- [x] One artifact being referenceable from multiple projects is not structurally forbidden by "must live inside project directory" assumptions. — `1c87f24`
- [x] Exact external-artifact identity semantics are documented separately from Proxima record identity. — `1c87f24` *(canonical Proxima records use `pxr_...`; external artifact references use distinct `pxa_...` identity with mutable locator stored separately)*

---

## A9 — Recurrence becomes explicit domain data

- [x] Recurrence rule has a typed structure. — `ed147ea`
- [x] Series identity is explicit. — `ed147ea`
- [x] Occurrence identity can be addressed semantically. — `ed147ea`
- [x] Exception identity/state is explicit. — `ed147ea`
- [x] "this occurrence" and "entire series" actions do not depend on filenames or accidental source layout. — `ed147ea`
- [x] A detached/special occurrence can be represented without corrupting series identity. — `ed147ea`

---

## A10 — No hidden second database

Every durable piece of information is classified as one of:

- [x] canonical Proxima record/schema data; — `efdfa11`
- [x] disposable Backpack-local state; — `efdfa11`
- [x] external vault-artifact provenance/reference. — `efdfa11`

Nothing semantic is allowed to survive only in an opaque equivalent of Obsidian plugin settings. — `efdfa11`

### Evidence closing HARD GATE A

- [x] Revised domain types. — `71b0a2b` through `efdfa11`
- [x] New domain-schema version. — `efdfa11` *(canonical domain/record schema version 2)*
- [x] Tests covering every separation above. — `efdfa11` *(10-file / 61-test HARD GATE A closeout matrix)*
- [x] Architecture/import mapping document. — `efdfa11` *(`docs/canonical-domain-ownership.md`)*
- [x] A fixture demonstrating combined task+event project. — `efdfa11`
- [x] A fixture demonstrating independent execution/workflow movement. — `efdfa11`
- [x] ID-based relation test surviving title changes. — `26c84d4`
- [x] Scoped-order independence tests. — `bf56679`
- [x] No canonical-domain import of filesystem, Papers or Obsidian APIs. — `efdfa11` *(Gate 20B remains green)*

**HARD GATE A CLOSED** — `efdfa11`

### What breaks if this gate is skipped

The importer would freeze old mistakes into new JSON:

- shared execution/workflow status;
- global ambiguous ordering;
- project-type silos;
- wikilink relations;
- file-shaped schema;
- path-like identity.

Correcting those afterward means migrating the newly migrated database a second time.

---

# Stage 7 — Define and implement the Proxima-owned Record Store

This stage is storage infrastructure, not user parity yet.

## Record-store contract

- [x] One JSON file per durable record. — `3b1af20` *(adapter contract: one opaque-ID JSON file per record)*
- [x] Filename carries no human/domain meaning. — `3b1af20` *(opaque record ID only)*
- [x] Every JSON document validates against the current domain schema. — `a8c1b1e` *(canonical-domain-v2 codec is bound to the canonical JSON RecordStore factory; malformed, legacy/local and path-bearing record shapes fail at the boundary)*
- [x] Unknown/corrupt record files fail visibly. — `3b1af20`
- [x] No arbitrary partial JSON patch is exposed as the semantic application API. — `3b1af20`
- [x] Reader returns: — `3b1af20`
  - [x] typed record; — `3b1af20`
  - [x] opaque ID; — `3b1af20`
  - [x] kind; — `3b1af20`
  - [x] observed revision. — `3b1af20`

- [x] Writer supports: — `3b1af20`
  - [x] create-if-absent; — `3b1af20`
  - [x] update-if-unchanged; — `3b1af20`
  - [x] delete-if-unchanged. — `3b1af20`

- [x] Physical move/rename of a record JSON is not required for changing any human-facing record property. — `3b1af20`

## Single-writer boundary

- [x] Record-store write authority is explicitly distinct from creator-vault FSA write authority. — `3b1af20`
- [x] D51 remains intact for shared creator files. — `3b1af20` *(existing vault writer/co-writer boundary untouched)*
- [x] A new record-store boundary may enable writes because the record location is Proxima-owned and not a live Obsidian source. — `e7e7362` *(browser OPFS backend provides conditional physical record CRUD only; semantic mutation authority remains unavailable)*
- [x] The code makes it difficult to accidentally pass a creator-vault root into the record writer. — `3b1af20`
- [x] Record-store adapter never receives arbitrary user vault paths from semantic actions. — `e961b94` *(actual parsed `task.execution.move` and `project.delete` actions with Windows, traversal-shaped and POSIX creator-vault IDs are rejected by RecordStore opaque-ID validation before backend read/update/delete; backend call counts remain zero and semantic mutation authority remains unavailable)*

## Crash durability

Reuse the existing mutation/recovery semantics rather than inventing another journal.

The existing coordinator records the prior bytes, intended update bytes, revisions, request IDs and durable state, then classifies uncertain operations.

- [x] Record updates go through a coordinator with equivalent prepared → commit → committed semantics. — `4d61e20` *(pathless record update/delete coordinator durably prepares before the checked physical effect and commits the recovery entry only after successful effect; semantic mutation authority remains unavailable)*
- [x] Durable journal loads before record mutation authority becomes available. — `d07fa61` *(startup reconciliation completes before a RecordMutationCoordinator can be returned; load/recovery failure blocks authority and returns no coordinator)*
- [x] Prepared entries reconcile on restart. — `d07fa61` *(record startup reuses the existing durable recovery reconciler before authority exposure)*
- [x] `recovery-required` entries reconcile. — `d07fa61` *(record startup passes unresolved recovery-required entries through the existing reconciliation semantics before authority exposure)*
- [x] Effect-present operation classifies committed. — `d07fa61` *(prepared update with intended bytes already present is persisted as committed before coordinator exposure)*
- [x] Effect-absent operation classifies recovered/no-op. — `d07fa61` *(recovery-required update with unchanged prior bytes is persisted as recovered before coordinator exposure)*
- [x] Ambiguous/corrupt state blocks rather than guesses. — `a937aa4` *(record startup persists ambiguous third-party bytes as blocked and exposes no coordinator; malformed durable journal state blocks during load before record access or authority exposure)*
- [x] Process-death injection exists before commit. — `9bbedbd` *(real child process is killed after fsynced durable `prepared` state and before the checked record backend commit is entered; fresh startup observes unchanged prior bytes and reconciles `not-applied` → `recovered`)*
- [x] Process-death injection exists after file commit but before journal finalization. — `97970b7` *(real child process is killed after the checked record update durably commits `new @ record-r2` but while the durable journal still says `prepared`; fresh startup classifies effect-present → committed without rollback)*
- [x] Reconciliation is idempotent. — `188209e` *(repeated record startup over terminal committed/recovered/blocked journal state performs no further journal write or record access, creates no duplicate recovery state/outcome, and preserves the same mutation-authority decision)*
- [x] Agent receives machine-readable recovery-required/blocked outcome. — `155c736` *(actual coordinator `recovery-required` maps into the existing typed ActionFailure result vocabulary; actual blocked startup maps into bounded pathless inspection code `record-recovery-blocked`, with no direct storage authority exposed)*

## Multiple Proxima callers

Even with no Obsidian co-writer, UI surfaces and agents may observe stale revisions.

- [x] Every modifying action binds to an observed record revision where stale semantics matter. — `052c3b4` *(the pathless update/delete coordinator contract requires `expectedRevision`, and conformance callers bind it directly from the observed record revision; semantic UI actions remain unavailable)*
- [x] Two concurrent Proxima operations on the same observed revision cannot silently last-write-wins. — `052c3b4` *(two independent coordinators prepare against the same `record-r1`; the conditional store permits one `record-r2` winner and refuses the second operation as stale)*
- [x] Winner succeeds. — `052c3b4` *(exactly one same-record concurrent result succeeds and its returned revision becomes the stored revision)*
- [x] Loser receives typed stale/conflict. — `052c3b4` *(exactly one concurrent loser returns typed `reason: stale` with `actualRevision` equal to the winner's revision)*
- [x] Different records may commit independently. — `10dc3c3` *(two independent coordinators bind distinct record mutations to their own observed revisions; both conditional effects succeed and both records retain their own intended bytes/revisions without cross-record blocking or overwrite)*
- [x] Semantic caller may explicitly refetch/retry; storage layer does not silently merge. — `eb0f3fe` *(typed stale ends the original mutation with no automatic retry; caller explicitly refetches the winning revision and submits a new revision-bound mutation, which writes exactly the caller-provided replacement bytes without storage-layer merge)*

## Acceptance

- [x] Create/read/update/delete record through headless APIs. — `3b1af20`
- [x] Restart retains records. — `a91b2de` *(isolated real Papers profile; first Electron application closed; second Electron launch reused the same userData under a different PID and the same stable Proxima Backpack origin; a fresh accepted OPFS backend/RecordStore reread the exact disposable canonical record and conditionally deleted it)*
- [x] Corrupt JSON reports error. — `3b1af20`
- [x] Stale update refuses. — `3b1af20`
- [x] Two independent action callers race same revision: one winner. — `052c3b4` *(two independent pathless coordinator callers bind to the same observed revision; exactly one succeeds and the other returns typed stale without overwriting the winner)*
- [x] Process-kill tests classify every recovery state. — `7c89491` *(single-run aggregate executable matrix invokes both required real process-death windows: effect absent after before-commit death → `not-applied`/`recovered`; intended effect present after post-commit/pre-finalization death → `effect-present`/`committed`, with no rollback)*
- [x] No creator-vault file changed during record-store test suite. — `4cdbeea` *(all four designated disposable vault fixture trees remain byte/mtime-identical across focused record-store/recovery tests, isolated bridgeDisclosure and the serialized full suite; no live creator-vault access is used)*

## Evidence

- [x] RecordStore adapter tests. — `3b1af20` *(headless JSON adapter)*; `e7e7362` *(browser OPFS physical-backend/conformance coverage)*
- [x] Mutation coordinator conformance tests. — `4d61e20` *(prepared-before-effect ordering, committed-after-effect ordering, definite stale recovery, prepare-write refusal, uncertain post-effect journal failure and checked delete)*
- [x] Record startup recovery/authority conformance tests. — `d07fa61` *(durable load-before-authority, load-failure blocking, prepared effect-present → committed, and recovery-required effect-absent → recovered)*; `a937aa4` *(ambiguous peer bytes → durable blocked authority; corrupt recovery journal → blocked before record access)*; `188209e` *(repeated terminal committed/recovered/blocked startup is idempotent: no further journal writes, no record access, no duplicate state/outcomes, same authority decision)*
- [x] Machine-readable recovery disclosure contract tests. — `155c736` *(actual coordinator recovery-required → typed ActionFailure; actual blocked startup → bounded pathless blocked inspection; stable codes/fields and storage-target non-disclosure proven)*
- [x] Same-record observed-revision concurrency tests. — `052c3b4` *(update/delete caller shapes bind to observed revision; two independent same-revision coordinator callers produce one winner plus one typed stale loser, with winner bytes/revision preserved)*
- [x] Different-record independence concurrency tests. — `10dc3c3` *(two independent coordinator callers bind to distinct observed revisions; both different-record updates succeed and retain their own bytes/revisions without cross-record interference)*
- [x] Explicit refetch/retry no-silent-merge concurrency tests. — `eb0f3fe` *(stale refusal performs no automatic third write; explicit caller refetch observes the winner revision, and only a new revision-bound execute commits exact replacement bytes without merge)*
- [x] Semantic/UI mutation-containment closeout tests. — `b612cdb` *(all eleven registered record-mutation actions remain typed-unavailable through programmatic dispatch; ActionDispatcherOptions and dispatcher execution expose no RecordStore mutation authority; browser mutation intents route only through that dispatcher and browser source contains no RecordStore/coordinator/recovery mutation wiring)*
- [x] Process-death recovery evidence: `9bbedbd` *(before-commit kill: durable prepared survives; physical effect absent; startup → recovered)*; `97970b7` *(after-commit kill: intended physical effect survives while durable journal remains prepared; startup → committed without rollback)*; `7c89491` *(single-run aggregate executable matrix invokes both unchanged accepted harnesses exactly once and requires the exact `not-applied → recovered` / `effect-present → committed` classification pair)*
- [x] Durable recovery/process-kill tests. — `7c89491` *(single-run aggregate matrix executes both accepted real child-process death boundaries against durable recovery/record fixtures and requires the complete complementary classification pair)*
- [x] Tree diff showing writes confined to the Proxima-owned store. — `4cdbeea` *(disposable physical-tree probe changes exactly the opaque record JSON and `record-store/recovery/journal.json`, both beneath the Proxima-owned root; sibling creator-vault fixture remains unchanged)*
- [x] Explicit test that a creator-vault path cannot be supplied as a record-store target. — `3b1af20`; `e961b94` *(actual parsed record-mutation action IDs shaped as creator-vault paths cannot cross RecordStore update/delete identity validation; no backend mutation call occurs)*

---

# HARD GATE B — Physical store location must be settled before real import

The storage **format** and physical backing API are decided.

**Chosen location/API — `a08340c`:** the canonical Proxima Record Store is the
Origin Private File System of the stable Proxima Backpack origin
`papers-backpack://bp-954ea2cd-6261-410d-baf8-0d1fbd8ca0b1`, reacquired with
`navigator.storage.getDirectory()`. Its fixed namespace is
`record-store/records/` for canonical record JSON and `record-store/recovery/` for the
durable recovery journal. Chromium's private on-disk implementation path is not an
application path contract.

- [x] Backing location chosen. — `a08340c`
- [x] Authority restoration is programmatic after initial unavoidable enrollment, if any. — `a08340c` *(OPFS root is reacquired from the stable origin; no Record Store picker or external handle is required)*
- [x] Store survives normal Papers restart. — `a08340c` *(location is the stable Backpack origin in Papers' persistent profile; Stage 7's separate implemented restart-retention acceptance row remains open until the backend exists)*
- [x] Obsidian does not treat it as the live task/project/event database. — `a08340c` *(origin-private browser storage, not the creator vault)*
- [x] Agent access occurs through Proxima actions, not direct backing-store access. — `a08340c` *(OPFS handles remain adapter-private)*
- [x] Recovery journal survives wherever the record store survives. — `a08340c` *(same OPFS root, sibling `record-store/recovery/` namespace)*

**HARD GATE B CLOSED** — `a08340c`

Closing this decision gate does not itself implement the store and does not authorize real
migration. Complete Stage 7 physical-backend, restart, mutation/recovery and concurrency
acceptance before beginning real import.

---

# Stage 8 — One-time Markdown → Record Store importer

Legacy Markdown is input only.

## Import architecture

- [x] Importer uses the existing compatibility reader/parser rather than creating another Markdown interpretation. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(the dry-run planner calls `loadVaultState` directly and contains no Markdown/frontmatter/discovery parser)*
- [x] Import has a dry-run/planning phase. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(schema-v1 planner is explicitly `mode: dry-run` and has no writer authority)*
- [x] Import plan is machine-readable. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(plain JSON-serializable schema-v1 identity/reference/problem/census plan with explicit zero-write declaration)*
- [x] Import assigns final opaque record IDs according to HARD GATE A. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(every compatibility-loaded record receives a separately allocated `pxr_...` identity validated by the accepted opaque-ID and legacy-provenance boundary; invalid, reused and silently promoted legacy identity is refused)*
- [x] A durable import mapping records legacy provenance → new opaque record identity for reconciliation of relationships. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(versioned provenance→opaque-ID manifest is keyed by physical kind/source rather than ambiguous legacy alias, has an explicit durable load/save port, preserves prior reservations, and reuses persisted candidate identities on replanning; canonical staging remains separate)*
- [x] Project references are translated to new project IDs. — `0fd5f51` @ `2026-09-11T14:28:25+07:00`; `be3efdf` @ `2026-09-11T14:52:38+07:00` *(unambiguous task/event project aliases resolve through planned opaque project identity; absent aliases remain `missing`, while aliases backed by multiple physical project candidates are explicitly `ambiguous` with null selected target and all candidate opaque IDs disclosed)*
- [ ] Relations are translated to record IDs.
- [ ] Legacy status is translated separately into:
  - [ ] execution state;
  - [ ] workflow stage.

- [ ] Legacy ordering is translated into the appropriate scoped orders.
- [ ] Legacy project type informs import compatibility only; it does not create a permanent silo.
- [ ] Schema/settings needed to interpret custom properties become first-class schema records.
- [ ] Legacy wikilink relations never remain canonical relation values.
- [ ] Notes/drawings/attachments are **not copied** into the record store.
- [ ] Project references to external notes/files remain references to external artifacts.
- [ ] Legacy source files are never altered.

## Import staging

Use staged activation, not a half-cut-over live database.

- [ ] Import can materialize a staging record store.
- [ ] Valid records may be converted into staging while blockers are reported.
- [ ] Staging is not canonical until activation.
- [ ] Re-running the same import is idempotent with respect to already assigned import identities.
- [ ] An interrupted import resumes/replans without producing duplicate canonical records.
- [ ] No hidden "some records now JSON, some still Markdown" live mode is allowed unless explicitly designed and tested.

## Duplicate legacy IDs

Do **not** silently choose one source file.

- [x] Every physical legacy record involved in an ID collision is identified separately. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(import planning consumes the compatibility reader's pre-dedup physical candidate inventory; the dedicated duplicate fixture exposes both `proj-twin` sources and both `task-shared` sources separately)*
- [ ] Each decodable physical record can receive its own candidate opaque ID in staging.
- [x] The duplicate legacy alias is recorded as a collision. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(machine-readable collision groups retain the shared legacy alias plus every physical candidate's source provenance and separately allocated opaque identity)*
- [x] Any legacy relation/project reference that resolves through that duplicate alias remains explicitly unresolved/ambiguous. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(a project alias with multiple physical candidate mappings yields `resolution: ambiguous`, null selected project ID and the complete candidate-ID set; general non-project relation conversion remains open)*
- [x] No arbitrary filesystem/index order picks the target. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(all candidate identities may be deterministically listed, but a duplicate target alias never resolves by first/last/index order)*
- [ ] Canonical activation cannot claim the migration is clean while ambiguous references remain unacknowledged.
- [ ] A machine-callable import-resolution operation exists if ambiguous identities require explicit mapping.
- [ ] Resolution decisions are included in the import evidence.

## Malformed records

- [ ] Parse/validation-blocking malformed record produces a structured import failure containing:
  - [ ] source path/reference;
  - [ ] record kind if known;
  - [ ] problem code;
  - [ ] bounded diagnostic.

- [ ] No JSON record is created from guessed fields.
- [ ] Original malformed Markdown remains byte-identical.
- [ ] Other valid records may be prepared in staging.
- [ ] Canonical activation does not silently omit malformed records as though import were complete.
- [ ] A machine-readable unresolved-record count remains nonzero until deliberately resolved/skipped according to an explicit migration policy.

## Unsupported-frontmatter open question

The repository currently has a real unresolved semantic mismatch: repository loading can accept `unsupported-frontmatter` as a warning, while refresh treats that same code as blocking. The docs correctly preserve this as an open question. Do **not** invent an import rule for it.

- [ ] Before final migration activation, answer:

> Is an otherwise readable record containing `unsupported-frontmatter` importable using the interpreted fields with legacy source preserved as provenance, or must import block until the unsupported construct is resolved?

- [x] Until answered, importer reports it distinctly from an ordinary malformed record. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(`unsupported-frontmatter` is emitted as `unsupported-frontmatter-policy-pending`, while ordinary frontmatter parse failures remain separate reader problems; no importability policy is invented)*
- [ ] Tests encode the decided rule only after the decision exists.

## Byte-preservation proof

- [ ] Hash every legacy Markdown record before import.
- [ ] Run import.
- [ ] Hash every legacy Markdown record afterward.
- [ ] Every hash matches.
- [ ] Notes/drawings/attachments also remain untouched by the importer.
- [ ] No source "promotion" or ID injection is performed into legacy files.

## Import verification

Machine-check the legacy interpreted state against new-state semantics:

- [ ] same count of valid physical task records accounted for;
- [ ] same count of valid projects accounted for;
- [ ] same count of valid events accounted for;
- [ ] every imported source has explicit import disposition;
- [ ] names preserved;
- [ ] descriptions preserved;
- [ ] dates preserved;
- [ ] task durations/weights preserved;
- [ ] project associations mapped;
- [ ] custom property values mapped;
- [ ] relations either resolved to new IDs or explicitly unresolved;
- [ ] recurrence mapped where representable;
- [ ] archived/completed state preserved;
- [ ] no legacy `projectType` silo leaks into new capability filtering;
- [ ] no record filename is derived from record title.

## Programmatic import actions

The creator must not have to perform migration by clicking through a wizard.

- `import.plan`
- `import.inspect`
- `import.resolve`
- `import.commit`
- `import.status`

These are semantic administrative actions with typed results.

## Evidence closing import

- [x] Dry-run import planner contract tests. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(existing compatibility-reader reuse, machine-readable zero-write plan, HARD-GATE-A identity assignment/refusal, project-ID reconciliation, source byte/revision preservation, and unsupported-frontmatter policy-pending disclosure)*

- [x] Durable identity / duplicate-candidate planning contract tests. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(pre-dedup physical candidate enumeration, versioned provenance→opaque-ID manifest persistence/reuse, dedicated `vault-duplicates` collision accounting, and explicit ambiguous-project-reference refusal without staging writes)*

- Full import against all four existing fixture vaults.
- Dedicated duplicate-ID fixture assertions.
- Dedicated malformed-record fixture assertions.
- Legacy tree byte hashes before/after.
- Machine-readable import manifest/report.
- Restart after staged import.
- Restart after committed import.
- Idempotent rerun.
- No creator gesture.

---

# HARD GATE C — Canonical cutover

Do not enable any real record-editing UI until this gate closes.

## Work

- [ ] Startup chooses the Proxima record store as canonical tasks/projects/events/schema source after successful migration activation.
- [ ] Legacy Markdown record directories remain present but become **legacy source only**.
- [ ] Legacy Markdown task/project/event changes after cutover do not silently overwrite JSON records.
- [ ] Record-store mutations refresh every active Proxima surface.
- [ ] Read-only projection/source abstractions are generalized so UI does not care whether state originated from legacy import fixtures or record store.
- [ ] Current UI no longer labels the ordinary product as "Read-only workspace" once record mutations are enabled; at `608bcdc` that label is still hardcoded into the browser shell.
- [ ] Existing FSA creator-vault write boundary remains blocked for record files because record files are no longer creator-vault files at all.
- [ ] H4 remains untouched.

## Acceptance

- [ ] Modify a legacy task Markdown file after cutover; canonical Proxima task does not change.
- [ ] Execute semantic JSON-backed task update; every surface changes.
- [ ] Restart; JSON-backed state remains.
- [ ] Remove/rename legacy task source after cutover; canonical record remains.
- [ ] Notes continue reading from vault.
- [ ] Inspection identifies record-store source/revision rather than pretending JSON records are Markdown provenance.

## Evidence

- Cutover integration test.
- Cross-surface convergence test.
- Legacy-source-isolation test.
- Restart test.
- Machine-readable source-mode inspection.

### What breaks if writes are enabled before this gate

UI/agents could mutate JSON while some surfaces still refresh from Markdown, yielding two apparent truths and making accepted actions appear to revert.

---

# Stage 9 — Task mutation parity and Elastic direct manipulation

First full DATA WRITE surface.

## Required semantic actions

### Record editing

- `task.create`
- `task.update`
- `task.delete`
- `task.property.set`
- `task.property.clear`
- `task.relation.set` / equivalent typed relation mutation
- `task.recurrence.set`
- `task.recurrence.clear`

`task.update` must use a closed typed mutation schema, not arbitrary JSON patch paths.

### Elastic gestures

- `task.execution.move`
  - task ID;
  - target execution state;
  - optional scoped insertion target/order;
  - expected revision.

- `task.execution.reorder`
  - task ID;
  - execution scope;
  - before/after target or explicit semantic ordering intent;
  - expected revision.

## UI wiring

- [ ] New Task Save calls `task.create`.
- [ ] Card edit Save calls typed task mutation.
- [ ] Delete calls `task.delete`.
- [ ] Drag Backlog → Running calls `task.execution.move`.
- [ ] Drag Running → Finished calls same semantic family.
- [ ] In-column card reorder calls `task.execution.reorder`.
- [ ] UI uses provisional card/placeholder feedback during drag.
- [ ] UI does not update authoritative record until accepted.
- [ ] Stale refusal returns card to authoritative location and shows refusal feedback.
- [ ] Storage/recovery failure does not leave a card optimistically "saved."

## Agent parity

For every UI operation above:

- [ ] same action accepted through agent entry point;
- [ ] same validation;
- [ ] same stale behavior;
- [ ] same resulting record revision;
- [ ] same resulting inspection state.

Example required contract behavior:

```
Agent: move task T from Backlog to Running using observed revision R

Result:
- accepted + new revision, OR
- stale + actual/current revision information, OR
- typed refusal/failure
```

Never "200 OK but it didn't move."

## Acceptance

- [ ] Human-style drag and direct semantic action produce identical durable task state.
- [ ] Two agents/surfaces race same task revision: one wins, stale caller learns it lost.
- [ ] Elastic lock/progress remains local and does not increment task revision.
- [ ] Completion semantics are consistent when moving into/out of Finished.
- [ ] Reordering Elastic does not alter workflow-stage order.

## Evidence

- Semantic action tests.
- UI/agent equivalence tests.
- Stale race tests.
- Automated drag tests.
- Restart/read-back tests.
- Mutation journal request-ID attribution.

---

# Stage 10 — Project workflow Board and Backlog mutation parity

## First-class workflow schema

Because workflow stages are now semantic, distinguish their semantic definition from local presentation.

### DATA WRITE actions

- `workflow-stage.create`
- `workflow-stage.rename`
- `workflow-stage.delete`
- explicit remap/refusal semantics when deleting a stage containing tasks
- `task.workflow.move`
- `task.workflow.reorder`

### LOCAL STATE actions

- workflow column color if treated only as cockpit decoration;
- displayed column order if purely presentational;
- column width;
- collapsed state.

If stage order itself is determined to have semantic workflow meaning, move that one item into canonical schema explicitly rather than accidentally persisting UI order.

## Board UI

- [ ] Drag task between project workflow stages.
- [ ] Drag task within stage.
- [ ] Placeholder during drag.
- [ ] Destination feedback.
- [ ] Stale refusal restores authoritative state.
- [ ] Moving workflow stage does not alter Elastic execution state.

## Backlog mutation actions

- `task.bulk.complete`
- `task.bulk.delete`

Bulk contracts must identify every requested task and outcome.

- [ ] zero silent omissions;
- [ ] no "overall success" if some members failed unless result explicitly reports partial success;
- [ ] stale member behavior defined;
- [ ] retry is caller-controlled.

## Task-property edits

- [ ] All editable custom property types round-trip through semantic operations.
- [ ] Relations use IDs.
- [ ] Rollup/formula values are derived, not independently writable unless their schema says otherwise.
- [ ] Schema validation occurs before record writer call.

## Schema-management actions

Because the creator does not manually maintain wiring:

- `schema.property.create`
- `schema.property.update`
- `schema.property.delete`
- semantic option management for select/multi-select fields
- relation target-schema update
- formula-definition update
- rollup-definition update

## Acceptance

- [ ] Running + Review task remains Running after workflow drag.
- [ ] Project-board reorder leaves Elastic order unchanged.
- [ ] Search/filter/sort remain presentation only.
- [ ] Bulk complete from UI and agent produce same results.
- [ ] Bulk delete survives restart.
- [ ] Relation survives target title change.

## Evidence

- Cross-dimension status tests.
- Scoped-order tests.
- Schema-record tests.
- Bulk mutation tests.
- UI/agent parity matrix.

---

# Stage 11 — Project lifecycle parity

## Actions

- `project.create`
- `project.update`
- `project.archive`
- `project.restore`
- `project.delete`

No `projectType` mutation should survive as an ordinary successor operation unless a new separate product decision explicitly reintroduces it.

## UI

- [ ] New Project.
- [ ] Edit project fields.
- [ ] Archive.
- [ ] Restore.
- [ ] Delete.
- [ ] Project card/hub updates immediately after accepted mutation.
- [ ] Combined task/event project remains valid throughout lifecycle.

## Delete semantics

Must be explicit before implementation:

- [ ] Define whether deleting a project:
  - [ ] leaves tasks/events uncategorized;
  - [ ] requires explicit cascading action;
  - [ ] or refuses while members exist.

- [ ] Do not infer old plugin filesystem behavior as the answer.
- [ ] Whatever choice is made appears identically in UI and agent actions.

This is an **open semantic question**; source cannot answer what the creator wants after removing the old storage model.

## Acceptance

- [ ] Agent can create/archive/restore/delete without UI.
- [ ] UI buttons call the same actions.
- [ ] Project deletion has deterministic typed effect/refusal.
- [ ] Archive does not silently delete records.
- [ ] Project with both tasks and events behaves correctly.

## Evidence

- Lifecycle action tests.
- Cross-surface hub/workspace tests.
- UI/agent equivalence.
- Restart/read-back.

---

# Stage 12 — Schedule DATA WRITE parity

## Required actions

- `event.create`
- `event.update`
- `event.delete`
- `event.reschedule`
- `event.resize`

### `event.reschedule`

Typed intent must carry:

- event ID;
- proposed new start;
- proposed new end or preserved duration rule;
- expected revision.

### `event.resize`

Typed intent must carry:

- event ID;
- new end/duration;
- expected revision.

The semantic operation, not the agent, owns date validation.

## UI

### Empty cell

- [ ] Click seeds form.
- [ ] Save → `event.create`.

### Event editor

- [ ] Save → `event.update`.
- [ ] Delete → `event.delete`.

### Drag

- [ ] Actual block follows pointer provisionally.
- [ ] 15-minute snapping.
- [ ] Cross-day behavior.
- [ ] Release → `event.reschedule`.
- [ ] Stale refusal snaps back to authoritative location.

### Resize

- [ ] Bottom edge visible on hover.
- [ ] Live provisional height.
- [ ] 15-minute snap.
- [ ] Release → `event.resize`.
- [ ] Invalid duration refused before storage.

## Agent parity

An agent must be able to state:

> Move event E to 2026-09-10 14:30, retaining its current duration.

and get a typed accepted/stale/refused result without manipulating pixels.

- [ ] Agent does not need to know calendar geometry.
- [ ] UI geometry converts gesture → same semantic request.

## Acceptance

- [ ] Day/4-Day/Week drag writes correct record.
- [ ] Month/Agenda editor writes same record.
- [ ] Resized event appears consistently in every view.
- [ ] Race between UI drag and agent edit produces explicit stale loser.

## Evidence

- Semantic event tests.
- 15-minute snapping tests.
- Pointer integration tests.
- UI/agent race test.
- Restart/read-back.

---

# Stage 13 — Recurrence and occurrence-scope write parity

## Actions

- `event.recurrence.set`
- `event.recurrence.clear`
- `event.occurrence.update`
- `event.occurrence.delete` if old delete behavior requires occurrence scope
- series-scoped update/delete remains explicit rather than inferred.
- Equivalent task-recurrence actions if task recurrence is retained.

Every occurrence-level request identifies:

- series ID;
- occurrence identity/date;
- expected series revision;
- operation scope.

## UI

- [ ] Click recurring occurrence.
- [ ] Show scope modal.
- [ ] This occurrence.
- [ ] Entire series.
- [ ] Cancel.
- [ ] Save selected scope through semantic action.
- [ ] Occurrence exception reprojects immediately.
- [ ] Series update reprojects all affected future/visible occurrences.

## Agent parity

Agent never answers a hidden modal.

Its request contains the scope explicitly.

Example:

```
event.occurrence.update
seriesId = …
occurrence = …
scope = occurrence
…
```

or series action equivalent.

## Acceptance

- [ ] Occurrence-only edit does not rewrite unaffected occurrences.
- [ ] Series edit changes derived occurrences consistently.
- [ ] Stale series revision refuses occurrence update.
- [ ] UI scope selection and agent scope request produce identical state.
- [ ] No ordinary generated occurrence is incorrectly persisted merely because it was displayed.

## Evidence

- Recurrence-domain tests.
- Exception tests.
- Scope UI/action equivalence.
- Restart/read-back.

---

# Stage 14 — Timekeeping/Gantt DATA WRITE parity

## Actions

- `task.timeline.move`
- `task.timeline.resize`

`task.timeline.resize` explicitly identifies:

- task ID;
- edge = `start | end`;
- target date;
- expected revision.

`task.timeline.move` explicitly identifies:

- task ID;
- resulting date range or semantic delta;
- expected revision.

If vertical row position was reclassified as LOCAL STATE:

- `timeline.row.move` still exists programmatically but mutates only local cockpit state.

If creator later declares it semantic:

- it gets its own scoped canonical field rather than reusing workflow/Elastic order.

## UI

- [ ] Drag whole Gantt bar → semantic move.
- [ ] Shift + start edge → resize start.
- [ ] Shift + end edge → resize deadline.
- [ ] Live provisional bar geometry.
- [ ] Dates preview during manipulation.
- [ ] Invalid/inverted ranges visibly refuse.
- [ ] Stale commit restores authoritative bar.
- [ ] Collision/row handling retains old fluid interaction feel.

## Acceptance

- [ ] Agent can express exact same date mutation without pointer coordinates.
- [ ] UI and agent operations produce identical task dates.
- [ ] Gantt date changes update Countdowns and deadline Calendar immediately.
- [ ] Scoped local row movement cannot alter project workflow/Elastic ordering.

## Evidence

- Gesture-to-action tests.
- Shift-modifier tests.
- Cross-Timekeeping convergence.
- UI/agent equivalence.
- Stale refusal test.

---

# Stage 15 — Notes, drawings and attachments workspace

This is deliberately separate from the record store.

## Read parity

- [ ] File/folder tree.
- [ ] Markdown preview.
- [ ] Canvas preview.
- [ ] Excalidraw preview.
- [ ] Folder expansion.
- [ ] Selection.
- [ ] Context menu.
- [ ] Hover.
- [ ] Attached existing file navigation.

These are not blocked by record-store migration.

## Explicit file DATA WRITE actions

Every file gesture still requires an agent semantic action:

- `artifact.create-note`
- `artifact.create-folder`
- `artifact.create-canvas`
- `artifact.create-drawing`
- `artifact.rename`
- `artifact.move`
- `artifact.delete`
- `project.artifact.attach`
- detach action if the UX supports detaching without deleting.

The agent supplies logical/project-relative intent, not arbitrary unrestricted machine paths.

## UI

- [ ] Create controls call same actions.
- [ ] Drag file to folder calls `artifact.move`.
- [ ] Drag folder to folder calls same semantic family.
- [ ] Rename calls `artifact.rename`.
- [ ] Delete calls `artifact.delete`.
- [ ] Attach existing artifact calls project-association action.
- [ ] Valid destination visibly highlights.
- [ ] Invalid/self-descendant folder drops refuse.
- [ ] Failed move leaves tree at authoritative location.

---

# HARD GATE D — unresolved shared-file write question

This is the one part of the supplied storage decision that does **not** automatically follow from moving records to Proxima-owned storage.

Moving **records** eliminates the Obsidian co-writer race for task/project/event JSON.

It does **not** by itself eliminate concurrent access to **Notes/drawings/attachments**, because the decision explicitly leaves those as ordinary vault files owned by Obsidian.

At `608bcdc`, native creator-vault writes are still blocked specifically because ordinary browser FSA cannot guarantee an atomic checked commit.

Therefore the following must be answered before Stage 15's file mutations can be called safe:

> What semantics are acceptable if Obsidian edits a note while Proxima explicitly renames, moves or deletes that same ordinary vault file?

Creating a brand-new unique file and moving/deleting an existing file are not identical conflict cases.

Do not silently treat "explicit gesture" as concurrency control.

Possible resolution could be a deliberately accepted single-writer convention for those explicit operations, stronger native capability later, or narrower safe operations—but **this checklist does not invent the creator's answer.**

Until answered:

- [ ] Notes/files **read parity can close**.
- [ ] File-write actions can be implemented/tested on disposable roots.
- [ ] Native shared-vault rename/move/delete cannot be declared fully safe merely because record JSON is now private.
- [ ] H4 remains unclaimed unless creator later explicitly chooses it.

This does **not** block task/project/event parity.

---

# Stage 16 — Template execution

The old compact template syntax is less important than the resulting operation.

## Work

- [ ] Parser remains separate from executor.
- [ ] Preview produces a typed intended-operation plan.
- [ ] No mutation occurs on parse.
- [ ] Invalid template produces structured errors.
- [ ] Execution translates the plan into the same semantic actions normal UI/agents use.
- [ ] Do not give TemplateExecutor direct RecordStore write authority.
- [ ] Batch creation uses stable opaque IDs.
- [ ] Relations between simultaneously created records use those IDs.
- [ ] Project can contain both tasks and events.
- [ ] Relative dates use injected clock.

## Agent action

- `template.execute`

Result identifies:

- created project IDs;
- task IDs;
- event IDs;
- failures;
- whether operation was complete or partial.

Prefer atomic plan semantics where required; do not report full success after partial creation without explicit result representation.

## Acceptance

- [ ] Same semantic record set can be produced manually and through template execution.
- [ ] Invalid plan causes no hidden partial writes.
- [ ] Agent can execute template without opening modal.
- [ ] Restart reproduces created state.

## Evidence

- Parser fixtures.
- Plan tests.
- Execution/action equivalence tests.
- Partial-failure tests.
- Restart/read-back.

---

# Stage 17 — Full DATA WRITE action coverage audit

Before calling UX parity complete, make the interaction trace itself executable as a conformance matrix.

## Required canonical/action coverage

### Tasks

- [ ] create;
- [ ] edit every mutable ordinary field;
- [ ] delete;
- [ ] set/clear dates;
- [ ] weight/duration edits;
- [ ] execution-state move;
- [ ] execution reorder;
- [ ] workflow-stage move;
- [ ] workflow reorder;
- [ ] Gantt date move;
- [ ] Gantt start resize;
- [ ] Gantt end resize;
- [ ] custom property set/clear;
- [ ] relation edit;
- [ ] task recurrence if retained;
- [ ] bulk complete;
- [ ] bulk delete.

### Projects/workflow/schema

- [ ] project create;
- [ ] project edit;
- [ ] archive;
- [ ] restore;
- [ ] delete;
- [ ] workflow stage create;
- [ ] stage rename;
- [ ] stage delete/remap;
- [ ] property schema create/update/delete;
- [ ] schema options;
- [ ] formula/rollup/relation schema edits.

### Events

- [ ] create;
- [ ] edit;
- [ ] delete;
- [ ] reschedule;
- [ ] resize;
- [ ] recurrence set/clear;
- [ ] occurrence-specific change;
- [ ] series-specific change.

### External project artifacts

- [ ] create note;
- [ ] create folder;
- [ ] create Canvas;
- [ ] create drawing;
- [ ] rename;
- [ ] move;
- [ ] delete;
- [ ] attach existing.

Shared-vault safety qualification from HARD GATE D applies.

### Templates

- [ ] execute.

## For every row above

- [ ] typed request exists;
- [ ] runtime validation exists;
- [ ] typed success exists;
- [ ] typed stale/conflict where applicable;
- [ ] typed validation refusal exists;
- [ ] typed storage/recovery failure exists;
- [ ] request ID exists;
- [ ] affected entity IDs returned;
- [ ] state/revision observable afterward;
- [ ] event/audit record exists;
- [ ] agent invocation test exists;
- [ ] UI invocation test exists;
- [ ] equivalence test exists.

### HARD GATE E

**No DATA WRITE interaction is considered shipped if only its UI route works.**

Trigger for reopening the gate:

> A human can perform a durable operation that an agent cannot express semantically through Proxima.

That is a release-blocking defect.

---

# Stage 18 — Interaction-feel conformance pass

This is not an architecture audit. It verifies the cockpit actually behaves like old Proxima.

## Elastic

- [ ] click card opens editor;
- [ ] drag pickup;
- [ ] correctly sized placeholder;
- [ ] column feedback;
- [ ] invalid drop restoration;
- [ ] successful drop persists;
- [ ] Lock/Unlock;
- [ ] live run progression.

## Timekeeping

- [ ] Calendar/Gantt/Countdown independent toggles;
- [ ] simultaneous panels;
- [ ] live countdown buckets;
- [ ] Gantt bar follows pointer;
- [ ] Shift resize;
- [ ] accepted drop remains;
- [ ] refused drop visibly reverts.

## Schedule

- [ ] six modes;
- [ ] Today/Previous/Next;
- [ ] empty-cell event creation;
- [ ] event click;
- [ ] 15-minute drag;
- [ ] 15-minute resize;
- [ ] cross-day move;
- [ ] recurring occurrence scope.

## Projects Hub

- [ ] cards expose pressure/summary;
- [ ] clicking enters workspace;
- [ ] create/archive/restore/delete have visible feedback.

## Notes

- [ ] file/folder click;
- [ ] expand;
- [ ] context menu;
- [ ] hover actions;
- [ ] drag destination;
- [ ] move/rename/create/delete feedback as far as HARD GATE D permits.

## Task Board

- [ ] custom workflow columns;
- [ ] card click;
- [ ] card drag;
- [ ] placeholder;
- [ ] workflow transition independent of Elastic execution state.

## Backlog

- [ ] search;
- [ ] filters;
- [ ] sort;
- [ ] resizable columns;
- [ ] selection;
- [ ] select-all;
- [ ] bulk actions;
- [ ] relation/rollup/formula display.

## Modals

- [ ] every meaningful field accessible;
- [ ] Save;
- [ ] Cancel;
- [ ] Escape;
- [ ] Delete;
- [ ] recurrence scope;
- [ ] invalid form refusal;
- [ ] stale-save refusal.

## Feedback

- [ ] provisional UI never masquerades as committed state;
- [ ] accepted action visibly settles;
- [ ] stale/refused action visibly restores authoritative state;
- [ ] operation failures are not swallowed;
- [ ] no gesture depends on opening raw JSON/Markdown to finish the operation.

## Evidence

- Automated interaction recording/report covering every trace row.
- Every expected DOM/state transition machine-asserted.
- No "creator visually confirmed" evidence.
- Full action/inspection trace retained for the run.

---

# Stage 19 — Cross-surface and agent convergence

The cockpit must behave as one system, not a collection of independently updated surfaces.

## Work

- [ ] Task changed on Elastic updates:
  - [ ] Backlog;
  - [ ] project Task Board;
  - [ ] Timekeeping;
  - [ ] task modal;
  - [ ] project metrics.

- [ ] Deadline changed in Gantt updates:
  - [ ] Countdowns;
  - [ ] deadline Calendar;
  - [ ] task modal;
  - [ ] project Hub next-deadline metric.

- [ ] Event changed in Week updates:
  - [ ] Day;
  - [ ] 4-Day;
  - [ ] Month;
  - [ ] Year;
  - [ ] Agenda.

- [ ] Project archive updates navigator/Hub/workspace everywhere.
- [ ] Relation/schema changes reproject Backlog without restart.
- [ ] Agent write appears on human cockpit without a manual Refresh click.
- [ ] Human cockpit write becomes visible to agent inspection without manual refresh.
- [ ] Multiple independent Proxima surfaces converge to the same record revision.
- [ ] Each surface may keep independent local view state.

Current action dispatch already has state revisions and source-replacement semantics; preserve that concept while moving canonical state to the record store.

## Acceptance

- [ ] Agent modifies task while Board and Backlog are open; both converge.
- [ ] UI and agent race one record; stale loser explicit.
- [ ] Separate records update independently.
- [ ] Local surface selections do not bleed into canonical storage.
- [ ] No manual source-refresh control is required for normal record-store coherence.

## Evidence

- Multi-surface integration tests.
- UI+agent concurrent-operation tests.
- Revision convergence report.
- Local-state isolation report.

---

# Stage 20 — Remove transitional read-only scaffolding from the product surface

Only after parity writes are genuinely working.

At `608bcdc`, the visible page still contains fixture/FSA acceptance controls, build evidence panels and a `"Read-only workspace"` identity. These are useful engineering surfaces but are not the final old-Proxima cockpit.

## Work

- [ ] Ordinary user surface no longer leads with acceptance-probe chrome.
- [ ] Engineering diagnostics remain programmatically available.
- [ ] FSA disposable-probe controls are not confused with ordinary record ownership.
- [ ] "Read-only workspace" disappears from normal record-backed operation.
- [ ] Build/source/recovery health remains inspectable without dominating the cockpit.
- [ ] Canvas remains available as the Backpack capability already ahead of the old plugin.
- [ ] Legacy import controls disappear/retire after successful migration if they are no longer needed operationally.
- [ ] No migration ceremony becomes permanent UX.

## Acceptance

- [ ] Starting ordinary Proxima shows the cockpit, not the audit harness.
- [ ] Agents can still inspect build/source/recovery state.
- [ ] Removing user-visible diagnostics does not remove machine-readable diagnostics.
- [ ] Rebuilding/discarding the Backpack does not threaten record data.

## Evidence

- Browser acceptance.
- Inspection contract test.
- Restart/rebuild test against existing record store.

---

# Final release gate — "Feels like Proxima and agents can do everything"

Full parity is closed only when all of the following are true.

- [ ] Elastic is again an active execution cockpit rather than a read-only projection.
- [ ] Timekeeping again provides Calendar + Gantt + Countdowns.
- [ ] Schedule again provides all six modes and direct event manipulation.
- [ ] Projects are workspaces, not just filters.
- [ ] Notes remain ordinary vault artifacts.
- [ ] Task Board and Elastic no longer fight over one status field.
- [ ] Backlog behaves as a database view.
- [ ] Recurrence has occurrence/series semantics.
- [ ] Every human DATA WRITE gesture has one semantic Proxima action.
- [ ] Every such action has typed success/refusal/stale/failure.
- [ ] UI and agent paths share implementation.
- [ ] Agents never directly modify Proxima record JSON.
- [ ] Legacy Markdown record files remain untouched after migration.
- [ ] Changing legacy record Markdown after cutover cannot silently change canonical state.
- [ ] Record filenames carry no semantic meaning.
- [ ] IDs survive names/storage changes.
- [ ] Relations survive renames.
- [ ] Schema survives disposal/rebuilding of the Backpack.
- [ ] Project may contain both tasks and events.
- [ ] Scoped ordering no longer cross-contaminates surfaces.
- [ ] Crash during record mutation has deterministic restart classification.
- [ ] Multiple Proxima callers cannot silently last-write-wins a stale record.
- [ ] No Papers change is claimed.
- [ ] H4 remains unclaimed.
- [ ] KeToan remains out.
- [ ] No acceptance row requires creator manual interaction.

---

# Open questions that must remain open

These should not be silently "resolved" by whoever implements the checklist.

### Unsupported frontmatter during import

> Is `unsupported-frontmatter` importable when the compatibility reader produced a usable record, or is it an import blocker?

This must be answered before real migration activation.

### Durable all-day intent

> `CalendarEvent` has no all-day flag. Stage 4 infers all-day purely from bounds: both ends
> valid local midnights, end later than start. Before cutover, must explicit all-day intent
> become canonical data, so a user-authored all-day event stays distinguishable from an
> ordinary timed event that merely happens to run midnight to midnight?

Inference is adequate while the store is read-only. At import it stops being adequate,
because the two cases become indistinguishable and the author's intent is lost.

### Project deletion semantics

> When a project containing tasks/events is deleted, are members retained and unassigned, is cascade explicitly available, or must deletion refuse until empty?

Must close before project-delete parity.

### Gantt row order

> Is vertical Gantt row arrangement meaningful durable priority, or merely cockpit layout?

The old plugin persisted it, but that alone is not evidence that it belongs in the database. Either answer is supportable; do not reuse generic task order.

### External vault-artifact identity

> For project Notes/drawings/attachments that remain ordinary files, what exactly identifies an association across a rename performed outside Proxima?

Do not claim stronger identity than the filesystem integration can actually provide.

### Shared Notes-file mutation concurrency

> If Obsidian edits an ordinary note while Proxima explicitly renames/moves/deletes it, what behavior is acceptable?

Moving record data into private JSON does not answer this separate ordinary-file race. Read parity is unaffected; native shared-file mutation parity cannot be called closed until this is settled.

---

The most important sequencing rule is:

**Restore presentation first → correct the domain before import → build the private store → import once → cut over → enable semantic writes surface by surface.**

And the most important architectural rule is:

**The agent never becomes another storage writer. It becomes another caller of Proxima.**
