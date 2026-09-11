# Proxima Backpack — Full-Parity Implementation Checklist

<!-- STATUS: replace this block in place. Never append. -->

## Status

**Updated** 2026-09-12 · **Repo** Futahua/proxima-backpack

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
| Accepted branch | `stage7-record-store-contract` — creator-accepted through Stage 8 slice 18 at `97c9dd9`; slices 19–47 are pushed at `bd64a34`, `394179c`, `c62a7dc`, `d7e6a6c`, `d66622f`, `a31c74c`, `9b59d16`, `bdea4a1`, `7ec8d17`, `7825d20`, `e88e193`, `b20cdca`, `fef3b8a`, `d7e6270`, `9d6062c`, `1ffdd55`, `d21f434`, `8cadd24`, `3fa16bc`, `ba50cc6`, `7f96a71`, `ead7927`, `215777a`, `08e505d`, `8dc3841`, `d9d8c5e`, `738bb53`, `06c0702`, `d6e2b30`, `e898a04`, `abf8204`, `e62e8f4`, `ed09e3d`, `cab1627`, `18c2e48`, `9a04451`, `e4e319b`, `c74003f`, `1029a25` and `6dfad33` and **await acceptance** |
| Accepted host Gate 9.3 | `Futahua/Papers-3` branch `proxima-gate9-native-source-handoff` @ `67b7fa2` — pushed |
| Accepted host Gate 10.1 | `Futahua/Papers-3` branch `gate10-native-presentation-reconcile` @ `5451bbf` — pushed, creator-accepted |
| Accepted host Gate 10.2 | `Futahua/Papers-3` branch `gate10-host-truth` @ `9e6304b` — pushed, creator-accepted |
| Accepted host Gate 10.3 | `Futahua/Papers-3` branch `gate10-relay` @ `d2a3c74` — pushed, creator-accepted |
| Unaccepted work | none |
| Suite at `6dfad33` | fixture generation 0, source/test typecheck 0, build 0, `git diff --check` 0, vitest 0 under **default parallelism**, 193 files / 1299 tests; committer `2026-09-12T04:05:45+07:00`. At `1029a25` the same steps were 192 files / 1291 tests, committer `2026-09-12T03:59:36+07:00`; at `c74003f` 191 files / 1286 tests, committer `2026-09-12T03:54:01+07:00`. At `e4e319b` they were 189 files / 1271 tests, committer `2026-09-12T03:44:25+07:00`; at `9a04451` 188 files / 1269 tests, committer `2026-09-12T03:40:29+07:00`. At `18c2e48` they were 187 files / 1265 tests, committer `2026-09-12T03:37:24+07:00`; at `cab1627` 187 files / 1260 tests, committer `2026-09-12T03:31:18+07:00`. At `ed09e3d` they were 186 files / 1250 tests; committer `2026-09-12T03:25:34+07:00`. At `e62e8f4` the same steps were 186 files / 1246 tests, committer `2026-09-12T03:21:44+07:00`; at `abf8204` 186 files / 1245 tests, committer `2026-09-12T03:20:05+07:00`. At `e898a04` they were 185 files / 1235 tests; committer `2026-09-12T03:10:20+07:00`. At `d6e2b30` the same steps were 184 files / 1230 tests. At `06c0702` the same steps were 183 files / 1225 tests, at `738bb53` 182 / 1220, at `d9d8c5e` 181 / 1214, at `8dc3841` 180 / 1210, at `08e505d` 179 / 1207, at `215777a` 179 / 1205, at `ead7927` 179 / 1203, at `7f96a71` 179 / 1192, and at `ba50cc6` 178 / 1185, `3fa16bc` 178 / 1184, `8cadd24` 178 / 1172, `d21f434` 178 / 1167, `1ffdd55` 177 / 1147, `7825d20` 174 / 1105. **One test was load-sensitive and was fixed, not tolerated:** `tests/bridgeDisclosure.test.ts` starts a real bridge child process and allowed it five seconds to print `listening`; under parallel load that expired while the file passed alone in half a second, which is a flake that makes the whole suite untrustworthy. The bound is now thirty seconds. **The same flake class recurred and was fixed the same way at `d6e2b30`:** that file had raised its *bridge-start* bound to thirty seconds but left its three cases on vitest's five-second default, so with the suite at 184 files one case timed out under parallel load while passing alone. All three now carry `30_000`. The rule this keeps teaching: when a case spawns a process whose start it bounds, the case's own timeout must be at least that bound, or the bound is decoration. The slice-30 commit message says "177 files"; that is wrong — two existing files each gained a case, so the file count did not move then. At the last accepted point `97c9dd9`: 168 files / 1011 tests, Stage 8 focused 16 files / 105 tests, committer `2026-09-11T20:42:20+07:00` |

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
ownership closeout, at `cb92cae`, and Stage 5 slice 39, the Notes read side, the Timekeeping
reuse and the workspace acceptance boxes, at `ead7927` — **Stage 5 is complete.** Stage 4's
`## Acceptance` section is complete as of `215777a`, which also closed Stage 0's action-union
box and annotated the two of its four kinds that remain vocabulary rather than implementation.
**Stage 18's interaction-feel pass is complete on its read half as of `08e505d`** — 51 of its
58 boxes, with the remaining seven named and gated individually. **Stage 19's convergence claim
is proven on its read half as of `8dc3841`** — 18 of its 28 boxes, and every box left open names
the write, the agent path or the un-extracted renderer that blocks it. **Stage 8 is down to its
two creator-decision boxes as of `d9d8c5e`**, which also proved the broad staging pass and the
byte-preservation proof against real trees on disk — so HARD GATE C, the canonical cutover, is now
the only thing between the tree and the write stages. **HARD GATE C is open and being worked as of
`738bb53`:** the projection from canonical records to the world the surfaces render now exists, so
a record-store source is a thing that can be built rather than a thing that cannot be represented.
**As of `06c0702` the gate's isolation half is proven** — a record-store session activates, projects,
refreshes and switches, and a legacy edit or a deletion moves neither the surfaces nor the store — and
**as of `d6e2b30` its choice half is too**: activation has a marker that can be refused, startup chooses
the store only for an intact activated one and reports every other answer, and the browser shell holds
nothing but a read-only source. The write stages are no longer gated; they are simply not written yet.
**As of `abf8204` the first of them is written**: an Elastic drop submits one accepted task mutation through
the operation layer and the surfaces then read the store, so the cutover is no longer a read-side claim only.
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
Stage 8 / slice 3, canonical conversion-plan semantics, creator-accepted on Proxima branch
`stage7-record-store-contract` at `173b45e`, committed `2026-09-11T15:04:55+07:00`: every
readable physical candidate now carries the compatibility interpretation needed for dry-run
conversion without creating a second Markdown parser. Legacy task status is split into the
accepted independent execution-state and project-workflow meanings; legacy order is expressed
as separate Elastic-execution and project/workflow-stage candidate scopes rather than surviving
as a universal canonical order; and legacy projectType is explicitly compatibility/import
metadata with canonical capabilities remaining data/workspace-derived. No canonical payload,
workflow-stage record, Record Store write or staging materialization occurs; unsupported-
frontmatter remains policy-pending.
Stage 8 / slice 4, first-class schema/settings conversion-plan foundation, creator-accepted on
Proxima branch `stage7-record-store-contract` at `368b3bf`, committed
`2026-09-11T15:37:49+07:00`: explicitly interpreted legacy task/per-project schema settings
now reconcile scoped stable opaque schema and select/multi-select option identities and emit
canonical-ready primitive, select, multi-select and non-empty-formula schema records. Option
colors remain local presentation state; relation targets, rollups and incomplete formulas stay
explicitly pending. The parent planner remains dry-run and zero-write, with no custom-property
values, staging or Record Store materialization.

Stage 8 / slice 5, legacy custom-property value capture and dry-run conversion-plan foundation,
creator-accepted on Proxima branch `stage7-record-store-contract` at `a360fa96c62b910a5865de962d6a150a2a4e6e4b`,
committed `2026-09-11T16:08:36+07:00`: already-interpreted task/event frontmatter is retained as
import evidence; ordinary task values map to slice-4 opaque schema/option identities, events remain
captured-but-untyped, and relation, rollup and formula values remain explicit deferred outcomes.
The parent and property-value plans remain dry-run/zero-write; the direct-binary evidence is used
because `npm` is ENOSPC on this machine.

Stage 8 / slice 6, relation target resolution and wikilink→canonical-record-ID dry-run conversion
planning, creator-accepted on Proxima branch `stage7-record-store-contract` at
`400ccfcd6c2d778b9d635287995c3ef5002b50e8`, committed `2026-09-11T16:24:16+07:00`: exact valid
legacy wikilinks resolve only through the complete physical-candidate inventory, existing opaque
record identities and canonical relation target-kind semantics. Unambiguous permitted targets become
canonical relation values containing only opaque schema/record IDs; missing, ambiguous, malformed,
disallowed-kind and duplicate-target outcomes remain explicit, while unknown relation folders remain
schema/value pending. Plans remain dry-run/zero-write; no derived-value, staging, Record Store, UI,
Papers or live-vault authority is introduced.

Stage 8 / slice 7, rollup canonical-reference resolution and derived rollup/formula dry-run
planning, creator-accepted on Proxima branch `stage7-record-store-contract` at
`57e8c169166d2142d14e5b6580699388ef49833b`, committed `2026-09-11T17:46:24+07:00`: legacy
rollup relation properties resolve to canonical relation-schema IDs and target properties resolve
to canonical schema identities within the permitted relation scope; missing, ambiguous and
incompatible references remain explicit; derived rollup/formula values are evidence-only and never
treated as authority. The parent planner remains dry-run/zero-write, with no staging, Record Store,
import UI/commit, HARD GATE C, Papers or live-vault authority introduced.

Stage 8 / slice 8, external-artifact association/reference dry-run planning, creator-accepted on
Proxima branch `stage7-record-store-contract` at `646d72e20b76e2f7cfa33c3e7e42e38448fbd551`,
committed `2026-09-11T18:49:42+07:00`: the existing compatibility interpretation of legacy
`linkedFolder`/`linkedFolders` data now produces canonical external-artifact references with opaque
`pxa_...` identities and explicit project associations. Exact legacy locators remain evidence-only;
machine-path versus vault-relative classification is explicit; shared exact locators reuse one
identity; out-of-band rename continuity remains unclaimed. The planner has no content-reader or
copy authority, and linked bytes, legacy Markdown, canonical Record Store, staging and external-
artifact writes remain zero. Browser-boundary and bridge-disclosure gates passed, and the full
serialized suite is 158 files / 944 tests.

Stage 8 / slice 9, isolated schema-record staging foundation, creator-accepted on Proxima branch
`stage7-record-store-contract` at `9c0c2dca72d6dd02959e480961ff629dfe8da6d2`, committed
`2026-09-11T19:01:24+07:00`: a staging-only seam now consumes the accepted zero-write dry-run
plan and creates or reuses only canonical-ready schema records after Canonical V2 validation.
Pending and conflicting schema conversions remain explicit blockers; reruns are idempotent and
partial attempts resume without duplicate records. Legacy Markdown, settings, canonical/live
Record Store, external-artifact and activation writes remain zero. Focused evidence is 7 files /
43 tests, browserBoundary 1 / 4, bridgeDisclosure 1 / 3, and full suite 159 files / 949 tests.
This is intentionally a schema-only staging foundation; broad physical task/project/event staging
and activation rows remain open.

Stage 8 / slice 10, durable workflow-stage identity reconciliation and canonical workflow-stage
staging, creator-accepted on Proxima branch `stage7-record-store-contract` at
`a2cbdddf28159ccd57b200b1741b4add9c261267`, committed `2026-09-11T19:08:44+07:00`:
workflow-stage identity is keyed exactly by (canonical project record ID, legacy status ID),
durably persisted before staging creation, reused across interruption/replan, and staged only
through the isolated staging seam. Missing/ambiguous projects and identity/payload conflicts remain
explicit blockers; task/project/event materialization, live Record Store writes and activation remain
absent. Focused evidence is 8 files / 50 tests, browserBoundary 1 / 4, bridgeDisclosure 1 / 3, and
full suite 160 files / 956 tests.

Stage 8 / slice 11, physical-candidate identity staging metadata, creator-accepted on Proxima
branch `stage7-record-store-contract` at `42a03610cea7b7d81a3c2df28a1b83d79b3a70b7`, committed
`2026-09-11T19:14:55+07:00`: every decodable physical source retains its already-authored opaque
candidate identity, including duplicate legacy-alias candidates, with complete collision evidence.
Only staging metadata is written; no canonical task/project/event payload, Record Store, artifact or
activation write is introduced. Focused evidence is 9 files / 55 tests, browserBoundary 1 / 4,
bridgeDisclosure 1 / 3, and full suite 161 files / 961 tests. The duplicate-candidate staging row
is now closed; broad physical payload staging and activation remain open.

Stage 8 / slice 12, durable malformed-record and unsupported-frontmatter staging evidence,
creator-accepted on Proxima branch `stage7-record-store-contract` at
`3846805f02aa421f33ae78955b99836a6d3f07ed`, committed `2026-09-11T19:22:40+07:00`: structured
frontmatter parse failures are grouped by physical source as unresolved malformed-record evidence
with exact source/kind/identity context, stable problem codes and the accepted bounded diagnostic;
unsupported-frontmatter remains a separate policy-pending disposition. Source bytes remain
unchanged, no canonical payload or record is guessed, and the idempotent interruption-safe problem
manifest is the only writable boundary. Focused evidence is 10 files / 61 tests, browserBoundary
1 / 4, bridgeDisclosure 1 / 3, and full suite 162 files / 967 tests. Activation omission,
unsupported-frontmatter policy, and valid physical payload staging remain open.

Stage 8 / slice 13, canonical project payload planning and isolated project-record staging,
creator-accepted on Proxima branch `stage7-record-store-contract` at
`b92b2d408f87fda332dec9b84dbc701cf4485c7f`, committed `2026-09-11T19:43:23+07:00`: already-
interpreted project fields and accepted external-artifact bindings now form canonical V2 project
payloads and eligible projects materialize through the staging-only seam. Malformed, unsupported,
duplicate and otherwise ineligible projects remain explicit blockers; live Record Store, activation,
task/event staging and import commit authority remain absent. Focused evidence is 11 files / 68
tests, browserBoundary 1 / 4, bridgeDisclosure 1 / 3, and full suite 163 files / 974 tests.

Stage 8 / slice 14, canonical task payload planning and isolated task-record staging,
creator-accepted on Proxima branch `stage7-record-store-contract` at
`27691bd9c1284fc8fbdcea1554e42abbd349e9af`, committed `2026-09-11T19:53:28+07:00`: eligible
tasks now carry canonical V2 payloads with execution/workflow identities, scoped ordering and
resolved property values, and materialize only through the staging-only seam. Missing, ambiguous,
malformed, unsupported and conflicting dependencies remain explicit blockers; live Record Store,
activation, event staging and import commit authority remain absent. Focused evidence is 12 files /
75 tests, browserBoundary 1 / 4, bridgeDisclosure 1 / 3, and full suite 164 files / 981 tests.

Stage 8 / slice 15, canonical event payload planning and isolated event-record staging,
creator-accepted on Proxima branch `stage7-record-store-contract` at
`0a89f534ff966b3757255210fcf0ea8d4fd695f5`, committed `2026-09-11T20:03:54+07:00`: eligible
events now form canonical V2 payloads with canonical associations and recurrence data and materialize
only through the staging-only seam. Malformed, unsupported, ambiguous and conflicting dependencies
remain explicit blockers; live Record Store, activation and import commit authority remain absent.
Focused evidence is 13 files / 82 tests, browserBoundary 1 / 4, bridgeDisclosure 1 / 3, and full
suite 165 files / 988 tests.

Stage 8 / slice 16, import source byte preservation, creator-accepted on Proxima branch
`stage7-record-store-contract` at `184765e2b125b85bccea18e13cba7966ef4371f4`, committed
`2026-09-11T20:19:14+07:00`: the import evidence boundary now proves source bytes and source hashes
remain unchanged across planning and staging for valid, malformed and unsupported inputs, without
granting content rewrite or live-vault authority. Focused evidence is 14 files / 89 tests,
browserBoundary 1 / 4, bridgeDisclosure 1 / 3, and full suite 166 files / 995 tests.

Stage 8 / slice 17, staged legacy import semantics, creator-accepted on Proxima branch
`stage7-record-store-contract` at `7ffa63f6a4ac37714bedb58c2bca76916cc95259`, committed
`2026-09-11T20:29:17+07:00`: staged project, task and event payloads are checked against the
legacy interpretation and canonical conversion contracts, with explicit refusal for malformed,
unsupported, duplicate and dependency-invalid records; staging remains isolated and no live-store
or activation authority is introduced. Focused evidence is 15 files / 97 tests, browserBoundary
1 / 4, bridgeDisclosure 1 / 3, and full suite 167 files / 1003 tests.

Stage 8 / slice 18, read-only legacy import actions, creator-accepted on Proxima branch
`stage7-record-store-contract` at `97c9dd9e68ad2e21222acf91a58502eecb278abd`, committed
`2026-09-11T20:42:20+07:00`: machine-callable read-only import inspection and status actions expose
the staged legacy plan and bounded evidence while import commit remains typed-unavailable. Invalid,
unknown and mutation-shaped requests return typed refusals without storage or activation writes.
Focused evidence is 16 files / 105 tests, browserBoundary 1 / 4, bridgeDisclosure 1 / 3, and full
suite 168 files / 1011 tests.

Stage 8 / slice 19, machine-callable read-only ambiguous-project resolution, pushed on Proxima branch
`stage7-record-store-contract` at `bd64a346c114144bdeb8768bc8aba6bc81a6b8cd`, committed
`2026-09-11T23:57:13+07:00` and **awaiting creator acceptance**: `import.resolve` takes the explicitly
selected candidate project record id and resolves every ambiguous project reference whose candidate set
contains it. The selection applies only while planning, so the resolved reference carries the chosen
project and everything derived from it follows rather than being patched afterwards: the task workflow
stage becomes a candidate, its workflow-order scope names the selected project, the event project
association resolves, and the reference counts are recomputed. An id that is a candidate of no ambiguous
reference is refused as `invalid-action-input` without re-planning, the verification that described the
pre-resolution plan is discarded so `import.inspect` re-verifies the resolved plan, and `import.commit`
remains typed-unavailable. Evidence: focused 16 files / 108 tests, full suite 168 files / 1014 tests
(which includes `browserBoundary` and `bridgeDisclosure`), every step exit 0, run directly rather than
through the npm scripts.

Stage 8 / slice 20, machine-visible remaining ambiguity, pushed on Proxima branch
`stage7-record-store-contract` at `394179c1137d16a26e2029ad430f3d695c34a3fa`, committed
`2026-09-12T00:02:14+07:00` and **awaiting creator acceptance**: `import.status` now reports the plan's
outstanding project references (`unresolvedProjectReferences`, `ambiguousProjectReferences`) and the
`appliedProjectSelection`, and `import.commit` refuses with those counts in machine-readable
`error.outstandingProjectReferences` while either is nonzero, instead of merely being typed-unavailable. A
fresh `import.plan` clears the applied selection, so status never describes a decision belonging to a
superseded plan, and once the references are acknowledged the ambiguity-specific reason disappears while
the policy refusal remains. **The administrative action envelope version is now 2** — the status payload
gained required fields, so a version-1 consumer would reject it and the version is the signal. Evidence:
focused 16 files / 109 tests, full suite 168 files / 1015 tests, every step exit 0.

Stage 8 / slice 21, unconvertible records visible before commit, pushed on Proxima branch
`stage7-record-store-contract` at `c62a7dcf06982b05ffedb1c2e7c5fb3efa686eca`, committed
`2026-09-12T00:05:59+07:00` and **awaiting creator acceptance**: `import.status` reports the plan's
`readerProblems` and `unsupportedFrontmatter`, and `import.commit` refuses carrying both in
machine-readable `error.outstandingRecords` whenever a record could not be converted. The two refusal
reasons are independent, which the test pins down on a fixture that carries an ambiguous project
reference *and* unconvertible records: acknowledging the references clears only the reference reason,
so clearing ambiguity can never make an incomplete import read as complete. The message names the
surviving reason instead of collapsing into the generic policy sentence. Evidence: focused 16 files /
110 tests, full suite 168 files / 1016 tests, every step exit 0.

Stage 8 / slice 22, legacy-import plan parity bundle, pushed on Proxima branch
`stage7-record-store-contract` at `d7e6a6c3be4bf8e6d1dbc7dee9166ae17db5e381`, committed
`2026-09-12T00:09:34+07:00` and **awaiting creator acceptance**: a dedicated `tests/importParity.test.ts`
proves thirteen census/parity boxes in one packet, which is the pace correction — one round closed
thirteen items instead of one. Against a plan built from one declared project, task and event with every
supported field set, it asserts: each kind's census reports `loadedRecords` equal to the plan's count,
`unaccountedCandidates` zero, and `loadedRecords + explicitlyRejected === recordCandidates`; every
declared source has a disposition and every conversion carries its `sourcePath`; names, descriptions and
dates survive (dates compared as instants, so a format normalisation cannot pass as data loss); task
weight, fixed/max durations survive; both `project:` and `projectId:` resolve to one canonical project
record id; `recurrence` is an explicit typed null rather than an omitted key; archived and completed state
survive without the record being dropped; `projectType` stays compatibility metadata and filters nothing;
and record identity is opaque with same-title records receiving distinct ids. Evidence: focused 17 files /
119 tests, full suite 169 files / 1025 tests, every step exit 0.

Stage 8 / slice 23, import identity idempotence, pushed on Proxima branch
`stage7-record-store-contract` at `d66622fb1c1f05d00b537d6d02e2426b70f0cee1`, committed
`2026-09-12T00:12:36+07:00` and **awaiting creator acceptance**: `tests/importIdempotence.test.ts` proves
that re-planning the same vault reuses every identity from the durable mapping, and that an interrupted
run resumed from the stored manifest alone comes back identical — through a duplicated legacy alias too,
and stable on a third pass. The proof rests on giving every run a *disjoint allocator range*: a shared
counter would have hidden exactly the failure under test, because a re-derived identity would still have
looked like reuse. Evidence: focused 18 files / 122 tests, full suite 170 files / 1028 tests, every step
exit 0.

**In flight** Nothing. The tree is clean and the branch is pushed.

Slice 48, Stage 9's first wiring, pushed on Proxima branch `stage7-record-store-contract` at `abf8204`,
committed `2026-09-12T03:20:05+07:00` and **awaiting creator acceptance**: an Elastic drop writes. The gesture is
`src/app/taskMoveGesture.ts` — it submits **one** accepted mutation (`execution-state` and `execution-order`
together, because a card in a new column at its old index is not a state a reader should ever observe) and only
then re-reads the source, so nothing is drawn as saved before the store says so, which is why a refusal needs no
undo path: the authoritative record never changed. A lost race is the one refusal where the board was showing a
revision the store no longer holds, so that case re-reads before the refusal is rendered and reports the revision
that beat the caller, while every other refusal leaves the world as it was and does not redraw. A refresh that
fails after an accepted write does not undo the write. The shell receives **operations, never storage**:
`src/adapters/browserTaskMutations.ts` composes the OPFS backend, the recovery journal, Stage 7's recovery gate
and the activation marker, and returns three callables or a typed reason there are none (`not-activated`,
`recovery-blocked`, `store-unreadable`); a run still reading legacy Markdown has no record write path at all and
says so rather than appearing to work. Six UI-wiring boxes tick: both column drags, the in-column reorder, "UI does
not update authoritative record until accepted", the stale return-to-place with refusal feedback, and
"storage/recovery failure does not leave a card optimistically saved". `docs/DECISIONS.md` D55 records the choice
and its reversal condition. **Two guards were relaxed deliberately in the same commit, and neither assertion was
deleted**: `recordMutationContainment` now asserts the sharper rule — the drop is routed to operation layer and is
deliberately *not* dispatched, no file under `src/browser/` composes a store, and the sanctioned composition names
all three refusal reasons — and `uiSemanticActionParity` follows the two gesture names to
`src/app/taskMoveGesture.ts`, where the canonical vocabulary now lives.

Slice 49, the stage's two acceptance cases, at `e62e8f4`, committed `2026-09-12T03:21:44+07:00`: one task is moved
by a drop and a second by the equivalent submitted operation, and the two stored records are compared field by
field with only identity and the human-typed title removed — they are equal, down to completion, workflow order and
the resulting revision both callers are told. The Elastic lock case now also derives a progress presentation at a
tick moment: a real dispatcher over the store's own projection takes the target, locks, draws progress and unlocks,
and every task revision is byte-identical afterwards with the store holding exactly the records it held before.
Two acceptance boxes tick — "human-style drag and direct semantic action produce identical durable task state" and
"Elastic lock/progress remains local and does not increment task revision". The seventh UI-wiring box, provisional
drag feedback, was already built and tested rather than written here: `57860d3` @ `2026-09-10T09:14:42+07:00`
introduced `elastic-insertion-placeholder`, and `tests/elasticCockpit.test.ts` proves a correctly sized placeholder
is shown at the drop target during the drag while no move has been emitted, that it follows the pointer to a second
slot, and that exactly one semantic move is emitted on drop.

Slice 50, the same wiring made executable, at `ed09e3d`, committed `2026-09-12T03:25:34+07:00`: the sequence that
joins a binder's drop intent to the semantic write path lived inline in `main.ts`, where the only thing that could
check it was reading the file as text. It is now `src/app/elasticDropAction.ts`, and four cases execute it against a
real store — resolve, write, refresh, render, in that order, asserted — so nothing is drawn before the store has
answered and been re-read. The sinks are dependencies rather than globals, which is what makes the order checkable,
and the shell supplies no storage: the containment guard now asserts that of this module too. The four cases cover
the whole reachable surface of a drop: the accepted path, a run with no write path (refused by name, one render, no
refresh, record untouched), a card the board is not showing (no write path is even resolved and nothing is redrawn),
and a lost race, where the drop carries the revision the board was *rendering* rather than a fresher one.

Slice 51, the Task editor's write path, at `cab1627`, committed `2026-09-12T03:31:18+07:00`:
`planTaskEditorSave` compares the draft against the record it was seeded from and emits one typed
mutation per field that **actually changed** — nothing else, because a field nobody touched is a field a
concurrent editor may already have changed, and rewriting it would be this form overwriting work it never
saw. It refuses values the record could not hold (an empty name, an unreadable date, weight that is not a
number, a fixed duration with no minutes) instead of half-writing the form, and it refuses a column that is
not one of the three canonical execution states: a vault's own status id is not a column, and inventing one
is how two vocabularies start sharing a field. Custom properties are refused **by name** with the reason —
their values reached the editor through a compatibility projection, a select's option id having become its
label, so writing one back needs the canonical mapping Stage 10 owns; refusing loudly is the honest half of
that and dropping the edit silently would be the dishonest one. `saveTaskFromEditor` and
`deleteTaskFromEditor` are the sequence over the real store and the real recovery gate, carrying the
revision the card was read at, and the convergence rule the drop established is now one module
(`src/app/writeConvergence.ts`) that both callers share. Ten cases.

Slice 52, the editor's Save and Delete as real controls, at `18c2e48`, committed
`2026-09-12T03:37:24+07:00`: the modal is told what this run may do by the same resolution a gesture uses,
so the two cannot disagree — a resolved write path makes Save and Delete real, and anything else is the
typed reason they are not. Save is offered only when there is something to write, because a form matching
the record has no save and a disabled button saying so beats a click that comes back refused. What happens
to the form *after* a write is a rule rather than an accident, and it is testable because the sequences
report it instead of reaching for the shell's state: a **refused** save keeps the edits, so a reader retries
from the authoritative revision rather than retyping, and only an accepted one clears them. An accepted
delete closes the editor; a refused one leaves it open. The containment guard now covers this path too. Two
UI-wiring boxes tick — **Card edit Save calls typed task mutation** and **Delete calls `task.delete`** — and
the Timekeeping surface's copy of the modal keeps the typed-unavailable constant on purpose, because its
binder has no form handlers at all: its write parity is Stage 14's, and half-wiring a read-only form would
be worse than saying so.

Slice 53, what the product calls itself, at `9a04451`, committed `2026-09-12T03:40:29+07:00`: the
literal "Read-only workspace" is gone from the shell and the claim is derived —
`src/browser/workspaceIdentity.ts` says "Editable workspace" only when records come from the record
store **and** a record write path actually resolved. Deriving it from the capability rather than the
source mode is the point: a label tied to the mode would have claimed editability the moment a store
existed, before anything could write to it. The badge and the identity stay separate strings on
purpose — the badge names the source, because a reader needs to know whether they are looking at
fixture bytes or their own data, and the identity names the capability, because "read-only" is a
promise about what the product will do with that data. Three boxes tick: **HARD GATE C item 6**,
**HARD GATE C's "Execute semantic JSON-backed task update; every surface changes"** (the operation
now exists and two UI callers execute it, followed by the product's own refresh and the projection
every surface renders), and **Stage 20's "Read-only workspace disappears from normal record-backed
operation"**.

Slice 54, an audit rather than a feature, at `e4e319b`, committed `2026-09-12T03:44:25+07:00`: four boxes in
Stages 18 and 19 had been left open against a world that no longer exists — "the drop is refused, so there is
no accepted move to persist", "no modal has a save path to make stale", "an Elastic edit is refused", "a refresh
**is** the mechanism". Stage 9's write half answered all four, so the honest close was to assert it rather than
re-argue it. `tests/elasticChangeConvergence.test.ts` starts where a person does — a drop, then the product's
own re-read — and mounts the real renderers over that projection, so the Elastic column, the project Task
Board's column, the Task editor's field and the Backlog row's order all move together and the deadline and
completion deliberately do not (A2 from the surface side). One new case saves a name in the card editor and
finds it on the same surfaces. Ticks: Stage 18's **successful drop persists** and **stale-save refusal**, Stage
19's **Task changed on Elastic updates** (the parent whose five children were already ticked for a source-made
change) and **No manual source-refresh control is required for normal record-store coherence** — a write
converges the cockpit by itself, and the interval policy covers changes made elsewhere. The same audit narrowed
three boxes it could *not* close and said so: Stage 18's **Save** and **Delete** now name which modal is wired
and which two are not, and Stage 19's **UI and agent race** records that one of the two writers now exists.

Slice 55, the New Task form, at `c74003f`, committed `2026-09-12T03:54:01+07:00`: nothing in the tree
offered "new task" at all, so the last of Stage 9's three UI-wiring boxes needed *UI* rather than wiring.
The form is built in the shape the card editor established rather than a second idiom — a `FormDraft`, a
projection over the same `TaskEditorField` vocabulary, a plan that turns the draft into one closed typed
request, and a sequence that executes it through operations rather than a store — and its own hooks
(`data-new-task-field`), because both forms can be on the board at once and one binder answering the other's
keystroke is the failure those hooks exist to prevent. `planTaskCreate` refuses by field before the write path
is asked, the form offers only the fields the request can carry (custom properties are absent, not
shown-and-refused), and a new card lands at the top of its column because where it belongs among peers is a
drag. Save is a real control exactly when a write path resolved and is offered only once the form holds a
name; a refused create leaves the form open with what was typed. Fifteen cases. **Stage 9's UI-wiring half is
now complete: what remains in the stage is its five agent-parity boxes, which need an agent-facing caller.**

Slice 56, agent parity, at `1029a25`, committed `2026-09-12T03:59:36+07:00`, and **Stage 9 is complete — 20
of 20 boxes**. The five parity boxes compare a UI caller with the programmatic entry point, and the checklist
is explicit that the entry point is the semantic write path itself; what was missing was a case that drives
both. `tests/uiAgentMutationParity.test.ts` runs each claim twice, in two identical worlds — once through the
sequence the UI executes and once through a directly submitted typed request — and compares with record ids
normalised away, because the point is that the operation is identical rather than that two random ids are.
All five: the same action accepted (create, update, move, reorder, delete, with the affected records equal
field for field), the same invalid request refused in the same words, the same race lost the same way with
both callers told the revision that beat them, the same resulting revision, and the same inspection state
with the same record-store provenance. **Writing it found two real gaps rather than confirming the claim:**
the editor's plan said `invalid-value` where the write path said `validation-refused`, so the same refused
keystroke read differently depending on which caller asked, and the editor's refusals did not report
`actualRevision` although the drop's did. Both are fixed here, which is the whole argument for asserting
parity instead of reasoning about it.

Slice 57, the first of Stage 10, at `6dfad33`, committed `2026-09-12T04:05:45+07:00`: Stage 9 refused every
property edit by name and said Stage 10 would own the mapping, and this is the mapping.
`src/app/propertyMutationPlan.ts` reverses the compatibility projection against the canonical schema, with four
rules that each exist because the alternative loses data silently — a derived value is never written, an option
is matched by id first and by label second, a blank is a clear except on a checkbox (where false is a value),
and a relation holds ids rather than names (A6), refusing one it cannot resolve. The case that matters does the
whole loop through the real store and the real recovery gate — canonical values in, projection out, form edit,
mapping back, both ends read again — for all six editable types in one save, and asserts a declared rollup is
*absent* from the record because it is derived. **Four Stage 10 boxes tick**: all editable types round-trip,
relations use ids, rollups and formulas are not independently writable, and schema validation happens before
the writer is called (both refusal cases leave the record at its first revision).

Slice 27, the Backlog's query controls as values, pushed on Proxima branch
`stage7-record-store-contract` at `bdea4a18182d14d6e62805481e53aeaa2ab53901`, committed
`2026-09-12T00:34:29+07:00` and **awaiting creator acceptance**: `src/app/backlogControls.ts` makes every
control a value — set-search, add-filter, remove-filter, sort-by, clear-sort, clear-query — and
`applyBacklogControl` the whole of what one does, so nothing in the browser layer decides what a control
means and a control that cannot change the query returns that same query. The filter menu is built from
the engine's own tables (`BACKLOG_FIELDS`, `operatorsForField`, `valueTypeForField`), and a test walks
every field and every comparison it admits, builds the filter and puts it through `assertBacklogQuery`, so
the menu cannot offer a comparison the matcher would refuse. The Backlog now draws a search field, the
filter menu, a sort button per sortable column and a remove button on every chip, all disabled when the
view belongs to another project. Two boxes are ticked: **Remove filter** and Stage 6's **Search/filter/sort
never mutate records**.

**The controls are driven, not just called.** Every control carries a `data-c1-key`, so the happy-dom
harness runs the real loop — render, click or type, apply, render — against the production renderer and
binder. `tests/projectBacklog.test.ts` now proves that typing searches, that the menu adds the filter it
was left on, that the chip's remove button brings the hidden task back, that a mistyped number is refused
with its reason and leaves the query alone, that a column sorts ascending then descending then clears, and
that none of it writes to a record. That file was the last place the Backlog's binder was untested: it is
no longer character-identical on purpose, it is covered.

**What the Backlog still lacks.** Tag filtering stays open because tags have no model; Property filters
stay open because the engine filters the nine typed fields and not `task.properties`; Custom-property
columns stay open because the projection supplies the columns while the renderer still draws the legacy
list rather than a column table; Resizable columns, Row selection, Select all and bulk actions have no
implementation. Stage 18's lowercase `search;`/`filters;`/`sort;` items stay open on purpose — that
section is an *interaction-feel* pass, and the three capabilities existing is not the same as their feel
having been assessed, which needs a browser.

**Slice 28 is done**, in two commits: 28a, `src/app/taskEditor.ts` at `7ec8d17`, decides every field the
Task modal shows — the ten task fields, one field per schema property whether or not the task has set it,
and any record value the schema does not declare — and 28b, `7825d20` at `2026-09-12T00:44:55+07:00`, makes
the modal that editor: `renderTaskModal` consumes `projectTaskEditor`, draws a control per type, and holds
provisional form state that Cancel and Escape discard. `editorDraft` is threaded through
`ElasticCockpitRenderOptions` and `TimekeepingCockpitRenderOptions` (one modal, two surfaces) and owned by
`main.ts`. An edit is reported through `ElasticCockpitHandlers.editTask` and deliberately does **not**
re-render, so a keystroke cannot take the field away from the reader; the drawn draft updates on the next
render. Twenty § Task modal boxes are ticked.

**Slice 29 is done**, in two commits: 29a, `e88e193`, added `src/app/eventEditor.ts` and extracted the draft
mechanics both editors share into `src/app/formDraft.ts` (the Task editor re-exports them under its own
names, so its callers and tests are unchanged and the two editors cannot drift on what "dirty" means); 29b,
`b20cdca` at `2026-09-12T00:56:55+07:00`, made `src/browser/eventModal.ts` the one renderer for both event
editors — the month/year/agenda one and the time grid's, which before this were two copies of five read-only
inputs with no Save, no Delete and no recurrence at all. The modal shows name, description, project, start,
end and completion, the recurrence rule read by the schedule's own rule reader, and three statements where
the fields are: event records carry no colour, an event that does not recur still gets the controls, and a
recurrence the reader refuses is reported as unusable rather than shown as absent. Eleven § Event modal boxes
are ticked, including **color if event metadata supports it**, whose condition is false — nothing in the
record or the vault format declares a colour, and the modal says so rather than omitting silently.

**Two things this slice states for the next agent.** The event editor takes a narrow input
(`events` + `projectChoices`) rather than the loaded state, because the schedule surfaces carry a project
name lookup, not the schema — so event custom properties are deliberately *not* listed, and adding that
data path is a separate change no § Event modal box asks for. And every control in the event modal is
**inert**: the modal represents each field rather than accepting an edit, which is why **Cancel/Escape
loses no data** is ticked on the grounds that nothing can be lost yet. That box reopens the moment the
event editor becomes editable at the record-store cutover.

**Also corrected here:** the § Task modal box **recurrence if task recurrence remains supported** stays
open, but the earlier reason given for it was wrong. A canonical recurrence model exists
(`src/domain/canonicalRecurrence.ts`) and its owner kind is `'event' | 'task'`, with an exceptions model for
cancelled, rescheduled and detached occurrences. So the question is not whether recurrence can own a task —
it can — but whether the product wants task recurrence, which is the creator's decision. **workflow stage
where project-scoped** stays open because no project-scoped workflow stage model exists (HARD GATE A2 owns
it; the legacy status is not the same thing).

**Slice 30 is done**, `fef3b8a` at `2026-09-12T01:01:45+07:00` — an audit slice, no production code
changed. The § Project modal and § Recurrence-scope modal boxes were closable on evidence that already
existed but had never been assembled, and two of them had never been exercised at all: nothing had clicked
**Entire series** or pressed the scope modal's Cancel. The new cases drive both scopes, change the choice
back, cancel and reopen, asserting the whole loaded shape is byte-identical throughout; and assert the
project modal's controls are exactly `project-create-name` and `project-create-description`, with no
control for anything the corrected model drops. Eight boxes are ticked, and the ticks name the commits that
made each behaviour true (`68e11b6` for the project modal, `448c65f` for the scope modal) as well as this
one where the evidence is new. **The lesson worth keeping: some boxes are already satisfied and simply
untested — an audit is cheaper than an implementation, and the checklist does not distinguish the two.**

**Slice 31 is done**, `d7e6270` at `2026-09-12T01:06:10+07:00`, five § Backlog boxes: relation, rollup and
formula display, and the two bulk controls. A row now draws the property cells the projection already
computed, each carrying the kind the schema declares, so a computed value can be told from an entered one
and an unset property shows as empty rather than vanishing. Property columns are labelled with the schema's
name, falling back to the stored key — the projection had used the raw key, which disagreed with the Task
editor and the property pills. The bulk controls are drawn where a selection would act, disabled, carrying
the same typed refusal every other write carries.

**Slice 32 is done**, `9d6062c` at `2026-09-12T01:11:58+07:00`, three § Backlog boxes: Row selection, Select
all, Multi-selection. `BacklogViewState.selectedTaskIds` holds the marked tasks in the order they were
marked, and the projection reports three separate facts about it — how many *shown* rows are marked, how
many marked tasks the query hides, and whether every shown row is marked — so a bulk action can never be
read as covering a row nobody can see. Select all means the rows on screen; a hidden mark is left to
whatever marked it before; clearing clears hidden marks too. Each row carries a real checkbox keyed by task
and the binder reports which task it is for rather than deciding what that means. The transitions are pure
functions in `app/backlogControls.ts` beside the query controls.

**Deliberately not in slice 32: Task row/name click opens editor.** The Backlog's row click opens its own
inspector, and opening the Task editor modal from this panel needs a decision about where that modal is
mounted — the Backlog panel does not render it today. That is its own slice, and it is the one Backlog box
left that is a wiring decision rather than a feature.

**Slice 33 is done**, `1ffdd55` at `2026-09-12T01:19:47+07:00` — Stage 6's Acceptance section, all four
remaining boxes ticked, and the audit paid for itself. **It found two real violations and they are fixed:**
the Task editor's and the Event editor's Delete buttons were `disabled` with no stated reason, which is
indistinguishable from a broken button — both now carry a typed `action-not-available` refusal as their Save
buttons already did. `tests/modalAudit.test.ts` checks the invariant against the rendered document, and the
two controls that stay clickable (the project create Save and the create-event Save) each have a case that
clicks them and asserts the refusal *and* that no record was created.

**How the audit selects what to check is itself a finding.** The first version picked write controls by
their words and immediately failed on two controls that order and filter — the Backlog's sort button
labelled "Completed" and the Projects Hub's "Archived" filter. A label cannot tell a write from an order or
a view. It now selects by the product's own convention (a `*-refusal`, `*-write-action` or
`*-lifecycle-action` hook) with one narrow safety net for a button labelled exactly a write verb.

**And one flake fixed rather than tolerated.** `tests/bridgeDisclosure.test.ts` starts a real bridge child
process and allowed five seconds for `listening`; under parallel load that expired while the same file
passed alone in half a second. A flaky suite makes every tick in this file unverifiable, which is the one
thing an evidence-driven loop cannot afford, so the bound is now thirty seconds and slice 33 verified the
suite under default parallelism as well as on the evidence path.

**Slice 34 is done**, `d21f434` at `2026-09-12T01:26:26+07:00`, and it closed all six § Template UI boxes
in one slice rather than the two the previous handoff expected — the panel turned out to be small once the
model existed. `src/app/templateComposer.ts` parses a template into a plan with eleven typed, positioned
error codes and two bounds; `src/browser/templateComposerPanel.ts` is a panel the Backlog hosts, opened from
"Tasks from a template", with the text area, the preview and the complaint list side by side and an Execute
button refused with the typed result. Two decisions are worth carrying forward: **the format is this
project's own**, which is what the sixth box permits and asks for, and **the panel parses on every render**
rather than keeping a second copy of what the text means, because a preview that holds its own idea of the
text is exactly how a preview and a parser drift apart. Writing the tests found a real bug — value
complaints reported a zero-based column, so `weight: heavy` pointed one character early.

**Slice 35 is done**, `8cadd24` at `2026-09-12T01:31:08+07:00` — the deferral paid off. Slice 34's handoff
warned that rewriting the Backlog's row markup into a column table would break the evidence slices 26–32
built on it, so this slice drew the table *around* the rows instead: a header above the existing list, one
entry per custom-property column, and the cells the rows already drew now keyed to those columns by id and
sharing their width. Every earlier assertion about rows, drop slots, chips and controls still passes
untouched, and the two boxes are genuinely closed. **Custom-property columns** and **Resizable columns** are
ticked, with the design notes recorded: widths live in view state because they are how this reader looks at
the table rather than what it means, the clamp stops a drag from making a label unreadable or letting one
column swallow the table, and a resize edge needs no typed refusal because resizing is presentation, not a
write. The drag is driven end to end through the harness, clamps included.

**Slice 36 is done**, `3fa16bc` at `2026-09-12T01:41:25+07:00`, and it closed the last feature box in the
Backlog. The design landed differently from the sketch, and better: rather than widening `BacklogField`
(which would have let a *sort* name a custom property) or making `field` optional (which would leave a
required property that lies), the query gained a **second filter list** — so a property filter cannot be
mistaken for a field filter, and every field filter and every test that builds one is untouched. The
comparison itself moved out of `matchesFilter` into `compareValue`, driven by a value type rather than a
field, so a property and a field cannot compare the same kind of value two ways; the engine's 17 existing
cases passed before any new test existed, which is what makes that refactor safe to believe.

**The DOM test caught a real bug that no unit test could see.** Minting a filter id from one list only meant
a property filter and a field filter could both be `filter-1` — and since one chip id names one filter,
removing it would have removed *both*. That is the aliasing this project treats as an error rather than a
tiebreak, and it was invisible until two kinds of filter could exist in one query. Id minting now spans both
lists and the test asserts two filters have two distinct ids. Worth remembering as a pattern: the unit tests
each knew their own list, and only a test that drove the whole surface saw them meet.

**Slice 37 is done**, `ba50cc6` at `2026-09-12T01:48:47+07:00` — the last Backlog box, and **Stage 6 is now
down to three boxes that are not mine to close**: **Tag filtering** (tags have no model — the creator's
decision) and the Task modal's two deliberate opens (**workflow stage where project-scoped**, owned by HARD
GATE A2, and **task recurrence**, the creator's product choice, since the canonical recurrence model can
already own a task).

The row click opens the Task editor **in the panel**, not the board's modal, and the reason is worth
keeping: both binders listen on the application root, so rendering the board's modal here would have meant
two binders answering one keystroke and a Backlog edit landing in the board's draft. The Backlog draws the
same `projectTaskEditor` projection through a new `src/browser/taskEditorFields.ts` that takes the surface's
hook names — the extraction is markup-identical, which the Elastic suites proved by passing unchanged. The
read-only inspector is retired rather than duplicated: it was a placeholder for exactly this editor. Two
probes were rewritten rather than deleted — the row-click case now asserts the editor opens for that task
with the record's values, and the write-control audit's expectation for this surface moved from the
inspector's `Edit`/`Delete` to the editor's `Delete`/`Save`, both typed. The audit caught that change,
which is what it is for.

**Where the work goes next, by the numbers.** A count of open boxes per stage says the largest untapped
block is not a new feature at all: **Stage 5, "Restore Projects Hub and read-only project workspaces", has
40 open boxes and zero ticked** — yet the Status block records its slices 1–9 as pushed, and the workspace
panels (Notes, Task Board, Deadlines, Schedule, Backlog) exist and are covered by tests. Like Stage 6's
Project and Recurrence-scope modals in slice 30, those 40 boxes describe work that is already done and was
never ticked. Stage 3 is 1 box from complete and Stage 4 is 1 box from complete; HARD GATE A is 1 box from
complete. Everything else that is large (Stages 9–14's write halves, HARD GATE C, Stage 17's write coverage,
Stage 18's interaction-feel pass) is either gated on HARD GATE C or needs a browser. **As of `6dfad33` the
document stands at 600 ticked / 240 open**, and the open column is now: Stage 0 7, Stage 3 1, Stage 6 3,
HARD GATE A 1, Stage 8 2 (both the creator's unsupported-frontmatter answer), **HARD GATE C 3**, **Stage 9 0**,
**Stage 10 16**, Stage 11 18, Stage 12 20, Stage 13 13, Stage 14 12, Stage 15 18, HARD GATE D 4, Stage 16 14,
Stage 17 58, Stage 18 5, Stage 19 8, Stage 20 11 and the final release gate 26. **Stage 9 is the first write
stage to close**, and Stage 10 has started from its most self-contained end — the property mapping Stage 9
deferred — so what remains there is the workflow Board's drag, the Backlog's bulk actions and schema
management.

**Slice 38 is done**, `7f96a71` at `2026-09-12T01:52:46+07:00` — **nineteen boxes**, and the audit found the
same thing slice 30 did: the work was done, the evidence was not. `tests/projectsHub.test.ts` covered only
the New Project modal, so nothing asserted what a project card shows; `tests/projectsHubCards.test.ts` now
does — every field the checklist names, with the conditionals taken literally (the priority row only where a
priority is represented, the identity swatch only for a value that is a colour, an unreadable created date
as "Unknown" rather than an age of zero), the active/archived filter and its `aria-pressed` state, a card
opening its project's workspace and coming back, the lifecycle controls offering archive-or-restore plus
delete with typed refusals, and the pure card projection agreeing with the rendered one. **No production
code changed in this slice either.** Two of the seven new cases were wrong first: the `^=` attribute
selector matches a card's *shell* as well as its button, and I asserted an unknown age against the project
that has a valid one — both my mistakes, both caught by the suite rather than by review.

The five Workspace boxes needed no new evidence at all: `tests/projectWorkspacePanels.test.ts` renders all
five tabs, asserts no `projectType` gating and no record mutation, and each panel has its own suite. The
ticks name `d83e158` (hub inventory), `dbea424` (lifecycle refusals), `68e11b6` (create modal), `dadd610`
(workspace panels and the five-tab test) and the interaction slices, with this commit only where the
evidence is new — and `1ffdd55` for the lifecycle controls, because the write-control audit is what proved
they carry typed refusals.

**Slice 39 is done**, `ead7927` at `2026-09-12T02:02:58+07:00` — **twenty-one boxes**, which closes the read
half of Stage 5 outright, including its § Acceptance section and its four `## Evidence` bullets. The audit
repeated slices 30 and 38's finding: the panels existed and their suites were real, but specific claims had no
case behind them. Four new cases in `tests/projectNotes.test.ts` (nine now): expansion is driven through the
machine-key harness — a collapsed root renders no file buttons at all and `aria-expanded` tracks it — and the
linked root's toggle gained `data-c1-key="project-note-root-<projectId>-<path>"` so it is addressable like
every other control; the hover affordance is pinned as the stylesheet's `.project-note-entry:hover` on exactly
the interactive entries, so a hover reaches no handler and an unreadable root has nothing to hover; a drag over
a file previews nothing while the same drag over a folder previews `source -> target` and the drop clears it;
and the whole read side was run against a vault whose writer members throw, with every byte re-read unchanged.
Four cases in `tests/projectTaskBoard.test.ts` (eight now): a column is painted only for a validated hex value
(`#112233` yes, `  #abc  ` trimmed and yes, `red;display:none` and `url(...)` nothing), a status the vault does
not define still gets a column after the defined ones, display order survives tied and missing indices, and the
pickup report plus the placeholder geometry are asserted while the record stays byte-identical. **One
production change, and it removes a restatement rather than adding a feature:** `projectDeadlines.ts` derived
`remainingMs < 0` for the overdue/upcoming split even though it already imported the Timekeeping deadline
projection, so that split now runs through the exported `countdownBucketForRemaining`; the case asserts row
order, day, value and state against both Timekeeping functions, including the boundary where a deadline equal
to `now` is `upcoming`, not `overdue`. § Acceptance's two substantive boxes were argued where each claim could
be made once: a markdown file carrying record-shaped frontmatter is previewed byte-for-byte as text rather than
parsed, and the same five workspace panels render byte-identically for the same project typed `task` and typed
`schedule` — the A4 silo removal seen from the workspace side. Every other tick names the commit that made the
behaviour true (`fa5bb33` Notes, `c8e35c3` Task Board, `d3dbb59` Deadlines, `dadd610` workspace panels and the
cross-tab/zero-write acceptance case, `2450828` navigation keys) with `ead7927` only where the evidence is new.
Two of the new cases were wrong first and the suite caught both: a file key I meant to drag over was inside a
collapsed folder, and `localeCompare` orders `Deep/…` after `data.json`, which code-unit sort does not.

**Slice 40 is done**, `215777a` @ `2026-09-12T02:11:10+07:00` — the loose ends that Stage 5's closeout exposed:
Stage 0's action-union boxes and Stage 4's six-view acceptance. Stage 0's parent box is ticked because the union
genuinely exists and is genuinely versioned and public — `ProximaAction` with `ACTION_SCHEMA_VERSION = 4`,
`parseAction` as the one gate, and a compile-time check (`ACTION_TAXONOMY_MATCHES_PROTOCOL`) that the union and the
category registry name exactly the same types, so adding an action without a category fails typecheck. The new
runtime case states what that proof protects: which of the four kinds the product populates. Two of them are
**vocabulary, not implementation**, and their boxes stay open with the reason written on them: nothing is a pure
presentation action (every gesture that changes what is shown also records which way the reader left it), and no
action mutates an ordinary vault file yet. § Acceptance's six-view box is ticked by one case that mounts a single
fixture set through both renderers the application chooses between and compares each view against the same
canonical occurrence projection clipped to the dates that view shows — Day/4-Day/Week through `scheduleVisibleDays`,
Month through its own non-empty cells, Agenda against everything, Year as per-date counts because it draws no
per-event element. Five boxes are annotated rather than ticked, each with what would close it: per-record revisions
in action results and per-entity bulk results both wait for a semantic record action that can actually run (HARD
GATE C, Stage 10 for bulk), UI-versus-agent equivalence waits for an agent-facing action submission path — the
loopback bridge is a read-only vault reader, so today the equivalence is structural (one parser, one dispatcher)
rather than proven — and panel sizing is still unbuilt, though the Backlog's column widths are local state now.

**Slice 41 is done**, `08e505d` @ `2026-09-12T02:16:06+07:00` — Stage 18's interaction-feel pass, **fifty-one of
its fifty-eight boxes**, and the same finding as slices 30, 38 and 39 for the fourth time: the interactions were
built and asserted, and the boxes had simply never been read against the suites. Every tick names the case that
asserts it and the commit that added that case, resolved with `git log -S` on the case title rather than by
memory — `57860d3` for the Elastic cockpit, `760e54d`/`c1f8c93`/`2b8a145`/`37e722b` for Timekeeping,
`7292075`/`2e74059`/`fc460f6`/`448c65f`/`7357b4d` for Schedule, `7f96a71` for the hub cards, and the slice 26–39
commits for the Backlog, Notes, Board and modals. **Two claims genuinely had no evidence and now do:** the New
Project modal answered every form with the same refusal, so a new case shows an empty or whitespace name refused
as `invalid-action-input` by the boundary it really dispatches through while a valid name still gets the
unavailable answer; and the Notes preview pane could fail silently, so a new case asserts idle, loading,
unavailable-with-its-reason and ready-in-the-file's-own-bytes as four distinct states. The seven boxes left open
are named and gated individually rather than annotated as a block: a successful Elastic drop, an accepted Gantt
drop, the Board's workflow transition, bulk actions, and the modals' Save, Delete and stale-save refusal — every
one of them needs a record write to exist. Stage 18's `## Evidence` bullets are annotated too, and the first of
them is **not** claimed: making the interaction trace itself an executable conformance matrix is Stage 17's own
line, not something a pass over the suites can assert.

**Slice 42 is done**, `8dc3841` @ `2026-09-12T02:22:54+07:00` — Stage 19, **eighteen of its twenty-eight
boxes**, and the first slice this session that had to *build* its evidence rather than find it. Nothing can write
a record, so the change a surface must notice can only arrive the way another program makes it — in the vault — and
`tests/surfaceConvergence.test.ts` does exactly that: it edits a task's file behind an open cockpit (a later
deadline and a move to the Running column), reloads it the way the application does, and asks eight surfaces what
they show. The project Task Board's card, the Backlog row, the project Deadlines list, the Task editor's field, the
Countdowns, the deadline Calendar and the Timeline/Gantt all report the new deadline, the Elastic card is in the
running column, the Hub's next-deadline metric follows the earliest deadline to the *other* task, and the old value
is gone from every surface rather than joined by the new one. The second case does the same for an event moved and
renamed: Day, 4-Day, Week, Month and Agenda all draw it, the time grids name the new instant, and Year is excluded
with its reason rather than asserted false. The third case is the one that keeps view state honest: a query and a
selection survive the data changing underneath them, the marked-but-hidden row is still reported, and the vault
holds the peer's edit and nothing else. Ten boxes stay open and each names its blocker — the three group parents
because their *origin* is a refused write (Stage 9, 12 and 14), the archive box because the navigator list is
rendered inline by `main.ts` with no exported surface for a test to mount, schema reprojection because the legacy
reader returns `taskSchema: []` and property definitions arrive with the record store, the two agent directions
because the bridge is a read-only reader, and the manual-refresh box because today a refresh *is* the mechanism the
checklist's own paragraph preserves. Stage 19's `## Evidence` bullets are annotated, and the UI+agent concurrency
bullet is explicitly **not** claimed.

**Slice 43 is done**, `d9d8c5e` @ `2026-09-12T02:35:31+07:00` — **eleven boxes**, and the first slice
this session that closed a stage's *implementation* half rather than auditing evidence that already existed.
Stage 8's staging and byte-preservation sections were the ones I had written off as gated; re-reading HARD GATE
C showed the dependency runs the other way — the cutover waits on the import, not the reverse — and none of this
work needs a write to the creator's vault. `tests/importStagingBytePreservation.test.ts` materializes every record
kind into slice 9's isolated staging store over disposable copies of all four fixture vaults, with
`runLegacyImportBytePreservationProof` around the operation and `node:crypto` hashing the tree independently
before and after: verdict `preserved`, zero changed paths, zero verifier writes, and every digest the verifier
reports equal to the filesystem's own. Three findings came out of writing it rather than reading the boxes. The
malformed fixture's fifteen problems are **all warnings** — the reader is tolerant, so those records enter state
and stage, while four candidates are blocked with typed reasons in the same pass, which is the "valid records
prepared while blockers are reported" pair in one run. A duplicate legacy id is **staged as its own candidate**
rather than excluded, which is the duplicate section working as designed and which contradicted my first
assertion (a blanket "rejected records are never staged" would have been wrong). And a store that claims canonical
authority is **refused** by every materializer, which is what makes "staging is not canonical until activation" a
mechanism rather than a hope. The unsupported-frontmatter question is annotated with what I now know it costs: the
reader treats `unsupported-frontmatter` and `frontmatter-parse-failure` as warnings, so the answer decides whether
the *existing* conversion is correct by default or must be withheld — it is not a question about the machinery.

**Slice 44 is done**, `738bb53` @ `2026-09-12T02:45:43+07:00` — **two boxes of HARD GATE C**, and the one that
mattered: the cutover's missing piece was that nothing turned `CanonicalRecordV2` into `ProximaState`, so a
record-store source could not even be *represented*, let alone wired. `src/app/recordStateProjection.ts` is that
projection, `recordStoreStateLoad.ts` is the store-side load in the same shape as the vault-side one, and
provenance gained a `record-store` origin so inspection names where a record came from — which is also the gate's
own acceptance box about not pretending JSON records are Markdown. The projection deliberately invents nothing: a
project's legacy `projectType` is reconstructed from what the project holds, because A4 removed that label from
capability decisions; and a workflow stage is reported as having no slot in the readable world rather than folded
into a board column, because A2 keeps project workflow and Elastic execution independent. Six cases, and the one
that says the most compares the real Task Board rendered from a legacy load with the same board rendered from the
store: **the same cards in the same three Elastic columns**, with the third column called `review` by a vault's
vocabulary and `finished` by the canonical model — a difference a projection must show, not paper over. Writing it
also caught a boundary the type change surfaced: `importPlanner` copies a source's `idOrigin` into fields that can
only mean a legacy Markdown answer, so those four sites now go through `legacyIdOriginOf`, which refuses a
record-store record instead of letting one claim a vault origin. The other twelve HARD GATE C boxes are annotated
individually with what each is waiting for; none of them is waiting on an unknown.

**Slice 45 is done**, `06c0702` @ `2026-09-12T02:53:45+07:00` — **six boxes**, and HARD GATE C's isolation half is
now proven rather than argued. The refresh seam only knew how to reload a vault, so a record-store source had
nowhere to plug in; `src/app/stateSource.ts` introduces the seam (a source says what kind it is and answers one
question — read the world now, and the revisions), `RefreshController` takes either a source or a vault so the
thirty existing call sites are untouched, `SourceMode` gains `record-store`, and a candidate in that mode carries
**both** a source for records and a reader for notes, drawings and attachments — which is why "notes continue
reading from the vault" is asserted in the mode that could have broken it. The five new cases cover activation,
refresh-on-store-change, switching in both directions, refusal of a record-store candidate with no record source,
and the one that matters: with records coming from the store, the source Markdown is renamed **and then deleted**,
nothing the surfaces read changes, the refresh stays `unchanged`, and `store.list()` returns the same records with
the same observed revisions — while the vault's own note read returns the edited text. Two ticks proved more than
their boxes asked: the "legacy changes do not overwrite JSON records" protection is unconditional today (the
store's boundary is the only writer, and `legacyIdOriginOf` refuses a record-store provenance from the import
planner), and the machine-readable source-mode inspection now has a third mode to carry. The main shell also stops
calling a record-store session a fixture: the badge names both halves, "Record store records · vault notes".

**Slice 46 is done**, `d6e2b30` @ `2026-09-12T03:02:30+07:00` — **four boxes, including HARD GATE C's item 1**, which was
the last thing between the tree and the write stages. The gap was not wiring but meaning: "activated" had none, so the
only available rule was "the store holds records, so trust it" — and a staging store holds records too. Activation is
now an act with a marker (when, which import, how many per kind) stored beside `records/` and `recovery/` in the
store's own namespace and validated on read rather than trusted; `activateRecordStore` refuses an empty store, refuses
to steal a store another import activated, and refuses to overwrite a marker this build cannot read. `chooseStartupSource`
names every answer — no marker, unreadable marker, emptied after activation, short of what it activated, unreadable
store — and every one of them keeps the product on the legacy reader *and says why*, because an empty canonical store
renders an empty application and that is worse than reading Markdown. `startupSession` keeps a restored vault handle as
the record-store candidate's **artifact** reader rather than letting it become a competing source; otherwise a remembered
folder would silently undo the cutover on every launch. **The guard caught me and was right:** a first attempt imported
the store into `main.ts`, and `recordMutationContainment` failed on it — the shell must hold no RecordStore authority, so
the composition moved to the adapter layer and `main.ts` receives only a `StateSource`, whose type has no mutation method
at all. Two more findings: the same load-sensitive flake class recurred (`bridgeDisclosure`'s cases were on the 5s default
while the start they wait for allows 30s — now all three carry `30_000`), and the real-vault acceptance report was
collapsing a record-store run into `fixture`, which it no longer does.

**Slice 47 is done**, `e898a04` @ `2026-09-12T03:10:20+07:00` — **three acceptance boxes**, and the first slice that
writes a canonical record rather than reading, projecting or activating one. Stage 9's required semantic actions are
now real code in `src/app/taskMutations.ts`: `task.create`, `task.update` and `task.delete`, with property set and
clear (relations ride the property value union), dates, weight, fixed and maximum duration, both orderings,
execution-state moves and recurrence set/clear. Three rules shaped it — the request is closed and typed rather than a
JSON patch, every refusal happens before a byte moves, and existing records change through the recovery coordinator
while creates use the store's own idempotent `createIfAbsent` — and failures speak the action taxonomy's vocabulary
so one operation can be reported identically to a human and an agent. Two of the rules were **found in the canonical
codec rather than invented here**, and are now enforced with sentences instead of store rejections: a task in a
workflow stage must carry its position in that stage while a task with no stage must not, and a project change may not
leave a stage behind from another project. Completion is derived from the execution state on every move, so "moved
into Finished" and "is complete" cannot disagree. The five cases attack the path: a dozen typed refusals that leave
every revision untouched, closed-field updates including clears, completion and both orderings, a contested write
where the loser is told the revision that beat it and can retry, and a delete that honours its revision. The UI half
of the stage is deliberately untouched: no gesture dispatches these yet, and `recordMutationContainment` still
asserts every registered record-mutation action is typed-unavailable through the dispatcher.

**Next operation** Slice 58 — Stage 10's workflow Board, which is now the largest unblocked block after the
property mapping landed: its Board UI boxes (drag between project workflow stages, drag within a stage,
placeholder, destination feedback, stale refusal restoring authoritative state, and moving a stage without
altering the Elastic execution state) plus the two acceptance claims that name them. Two facts shape the work
and neither is a surprise: `src/app/taskMutations.ts` already carries a `workflow-stage` mutation that moves a
stage and its position together and refuses to leave a foreign stage behind, and `src/domain/canonicalOrdering.ts`
already scopes workflow order by project and stage — but the **readable world has no slot for a stage**, which
`recordStateProjection` reports as `workflow-stage-has-no-legacy-slot` on purpose (A2). So the first step is a
deciding one rather than a wiring one: either the readable `Task` gains a workflow-stage field and the project
board groups by it, or the board reads stages from a projection of their own. The projection's current refusal
to invent a slot is the reason this is a decision and not a detail. Nothing in Proxima or LongHorizon is parked
or uncommitted; both trees are clean and both branches are pushed.
So the loop moves to the next unfinished checklists under `D:\Letters\MatTroiSeConMoc\LongHorizon`: the three Papers
documents whose titles say `Complete Implementation Checklist`. **All three are blocked, and this is now checked
rather than assumed.** `adopted-window-surfaces.md` and `window-layout-consistency-and-auto-tracking.md` both
manipulate **live foreign windows** on the creator's desktop — moving, hiding and Z-ordering other applications'
windows — which is not reversible by a later commit and is the one line this loop does not cross unattended; the
second also has an unanswered reviewer item (the window-tag lifetime contradiction) standing before its Stage 1.
`quick-run.md`'s 280 boxes are gated by the creator's hotkey-chord decision, and the one part that is not — STAGE 0's
pure modules — lands at `public/app/quick-run/` in the **As-you-Go Backpack** tree, which is not checked out on this
machine: the only trace is `Backups\as-you-go\as-you-go-state-20260901-093748.json`, a state file with no `.git` and
no `public/`. That fact is now recorded in `papers\quick-run.md`'s own Status block. Nothing in Proxima or
LongHorizon is parked or uncommitted; both trees are clean, both branches are pushed.

Slice 26, the Backlog view projection and query-aware rendering, pushed at `9b59d16`, committed
`2026-09-12T00:23:35+07:00`: `src/app/backlogView.ts` turns loaded state plus a view state into everything
the Backlog draws — rows, the eight field columns plus one per custom property the data declares, cells
formatted per type, both counts, the sort indicator, the filter chips, and why the list is empty — and
`renderProjectBacklog` consumes it instead of filtering inline with its own comparator. Five § Backlog
boxes were ticked: Search, Type-appropriate comparison operators, Multiple filters, Sort
ascending/descending, Sort indicator. `src/browser/` gained unit coverage there, which is what turned
those five boxes into evidence rather than claims.

Slice 25, the Backlog query surface, pushed on Proxima branch `stage7-record-store-contract` at
`a31c74c9d1c78436e542523823c5e94f5b045ca2`, committed `2026-09-12T00:19:34+07:00` and **awaiting creator
acceptance**: `src/domain/backlogQuery.ts` with `tests/backlogQuery.test.ts` (17 tests) gives search over
name and description, nine filter fields restricted to the operators their type admits, conjunction of
multiple filters, removal by filter id, ascending/descending ordering with a missing value last ascending
and first descending, and a total order — ties fall through `orderIndex` then `id`, so equal keys never
swap between runs. A numeric field compared against a non-number does not match: `9` is not `"9"`, which
the engine coerced until the test caught it. Evidence: full suite 171 files / 1045 tests, every step
exit 0.

**Papers checklists recon, 2026-09-12 (slice 24).** All three are greenfield: every Status reads "Not
started. No implementation exists. Design only." Their boxes are feature-level acceptance criteria,
test-stage requirements and Definition-of-Done gates — not verification gaps — so no read-only pass can
close them. Each of the two largest also carries an explicitly unresolved pre-implementation gate that
only the creator can close: Quick Run — "Pin the default workspace hotkey chord. Not chosen yet; do not
invent one silently."; Window Layout — "Resolve the window-tag lifetime contradiction … record the answer
before Stage 1." Two of the three (adopting foreign windows, window layout and auto-tracking) require
moving and Z-ordering *live foreign windows*, which must not be attempted autonomously on the creator's
desktop overnight under a non-destructive mandate. Papers host baseline is green: `Futahua/Papers-3` at
`d2a3c74`, 99 files (98 passed | 1 skipped), 942 passed + 4 skipped / 946 collected, 5.4s.

**The AUTHOR loop changed on 2026-09-11, by creator instruction.** The browser reviewer is retired: it
was too slow, and it existed mainly to keep an agent working through the creator's night rather than to
judge the work. The executing agent is now author and executor at once, and the judgement that used to
come from a reviewer reading evidence now comes from the project's own suite — fixture generation, both
typechecks, build, `git diff --check`, and the full vitest run, each recorded by exit code. That is
stronger than the browser on correctness, which could run nothing; it is weaker on whether a slice is the
right *product* decision, so a genuine product choice is left stated and open rather than self-approved.
The reviewer-tab machinery in AGENTS.md is inert until the creator says otherwise.

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

**`npm` blocked this loop once; C: was freed.** The original note was that the C: drive sat at zero
bytes free and npm died with ENOSPC before executing anything. As of 2026-09-11 C: has roughly 5.4 GB
free and `npm ls` completes, so the blocker is gone. This loop still runs the steps directly rather
than through the npm scripts — `node tools/build-fixture-module.mjs`,
`./node_modules/.bin/tsc -p …`, `./node_modules/.bin/vitest run --no-file-parallelism` — because it is
faster and because the substitution has to be declared either way. Say in the evidence that the
commands were run directly, because substituting a command for the authored one has caused a real
problem in this loop before.

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

- [x] Establish one public versioned action union for: — `da7881f` and `4554fea` built the
  taxonomy and its registry, and `215777a` @ `2026-09-12T02:11:10+07:00` added the runtime
  case below; `actionProtocol.ts` declares `ProximaAction` and
  `ACTION_SCHEMA_VERSION = 4`, both exported, with `parseAction` as the single gate for
  anything entering from outside — a UI click handler and a programmatic caller hand it the
  same shape. The union and the registry cannot drift apart: `ACTION_TAXONOMY_MATCHES_PROTOCOL`
  is a compile-time check that each names exactly the types the other does, so adding a type
  to the union without a category fails typecheck. `tests/actionTaxonomy.test.ts` states at
  runtime what that check protects — which of the four kinds the product actually populates.
  Two of the four kinds are vocabulary rather than implementation, and the two child boxes
  say which and why.
  - [ ] presentation actions; *(no action is registered as one: every cockpit gesture that
        changes what is shown also has to record which way the reader left it, so it is
        local state. `presentation` is the category an unregistered type is deliberately
        **not** defaulted into, because defaulting a durable write to it is how a write
        crosses a boundary that believes nothing durable happens.)*
  - [x] local-state actions;
  - [x] record mutations;
  - [ ] vault-artifact gestures. *(ordinary vault-file writes — Notes rename/move/delete and
        the canvas file — are refused today and arrive with the Notes/drawings write stage,
        which HARD GATE C gates. The category exists, is carried by
        `isMutationCategory`, and has no member yet.)*

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
- [ ] Include resulting record revision(s) where a record changed. *(The result carries
  `stateRevision` for the cockpit as a whole and `entityIds`, but no per-record revision: the
  dispatcher's record-mutation leg is refused as `action-not-available` and nothing in the
  product produces one, so there is no "a record changed" case to fill in. The record store's
  own mutation results do carry per-record revisions, so this closes with the first semantic
  record action the product dispatcher can actually run — HARD GATE C.)*
- [ ] Define bulk-action results per entity so partial success can never be mistaken for complete success. *(The selection half exists: the Backlog marks rows, reports how many the query is hiding, and refuses Bulk Complete and Bulk Delete with a typed reason rather than acting on part of a selection. A per-entity result shape belongs with the first bulk action that can run — Stage 10's write parity, under HARD GATE C. A shape no producer fills is vocabulary a reviewer cannot check.)*
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

- [ ] An action submitted through the UI and the equivalent action submitted through the agent/programmatic entry point produce the same semantic operation/result shape. *(Half of it is now asserted, and the half that is not is named. For **record mutations** the equivalence exists and is tested: `1029a25` runs each task operation twice — once through the sequence the UI executes, once through a submitted typed request — and compares acceptance, refusal vocabulary, stale behaviour, resulting revision and inspection state (`tests/uiAgentMutationParity.test.ts`), with two real gaps found and fixed rather than confirmed. What the box still asks for is that equivalence over the **action protocol**: `parseAction` plus the dispatcher, whose record-mutation actions are typed-unavailable and which has no agent-facing submission path, because the loopback bridge is a read-only vault reader (list/read/walk, writes refused). Closes with the first action an agent can submit, which Stage 17's agent parity owns under HARD GATE C.)*
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
- [ ] UI-versus-agent equivalence tests. *(the mutation half now exists — `1029a25` @ `2026-09-12T03:59:36+07:00` drives each task operation through both callers and compares the five things the parity boxes name — but the box's vocabulary is the action union's, and the union still has one caller: dispatch is what the UI does, and nothing an agent can reach submits an action. `215777a` @ `2026-09-12T02:11:10+07:00` added runtime coverage of the union's four kinds, which is the vocabulary this box would exercise rather than the equivalence itself.)*
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
  no sizing exists yet, so this stays open rather than being closed by a technicality. The
  cockpit has since gained one piece of sizing that is local state — Backlog column widths at
  `8cadd24`, clamped to 96–640 and never written — but panel sizing itself is still unbuilt,
  and Stage 18's interaction-feel pass is where the panels that need it are named.)*

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

- [x] Same event projects correctly across all six views. — `215777a` @ `2026-09-12T02:11:10+07:00` *(one fixture set — a timed event, one crossing midnight, and two others in other months — is mounted through both renderers the application chooses between, and each view is asserted against the same canonical occurrence projection restricted to the dates that view shows: `scheduleVisibleDays` for Day/4-Day/Week, the grid's own non-empty cells for Month, everything for Agenda, and per-date occurrence counts for Year, which draws no per-event element. The case also asserts the fixture is unchanged.)*
- [x] Day/4-Day/Week use 15-minute interaction geometry. — `7292075`
- [x] Month/Year/Agenda do not inherit invalid resize semantics. — `5d97cdc`
- [x] Recurrence expansion is deterministic under injected clock/date range. — `448c65f`
- [x] Empty-cell creation opens a form without modifying source data before Save. — `2e74059`

## Evidence

- [x] Six-mode projection tests. — `5d97cdc`, `7292075` and `215777a` @ `2026-09-12T02:11:10+07:00` *(`tests/scheduleProjection.test.ts` mounts Month, Year and Agenda against fixture events, `tests/scheduleTimeGrid.test.ts` covers Day, 4-Day and Week geometry, and the six-view case added at `215777a` reads one fixture set through all six in a single case so the modes cannot drift apart: each view's occurrences are compared against the same canonical projection, clipped to what that view shows.)*
- Automated event drag/resize preview tests.
- Recurrence-expansion tests.
- Zero-write proof before Save.

---

# Stage 5 — Restore Projects Hub and read-only project workspaces

No record migration dependency.

## Projects Hub work

- [x] Project cards display: — `d83e158` @ `2026-09-10T17:07:59+07:00` and `7f96a71` @ `2026-09-12T01:52:46+07:00` *(the projection `cardForProject`/`projectsHubCards` decides every field and the renderer draws it; until this slice `tests/projectsHub.test.ts` covered only the New Project modal, so nothing asserted what a card shows. `tests/projectsHubCards.test.ts` now does, for a project whose data exercises every field and one whose data does not — including the conditionals: an unreadable created date shows as "Unknown" rather than as an age of zero.)*
  - [x] name; — `d83e158`, evidence `7f96a71` *(the card's heading, asserted against the record's name)*
  - [x] description; — `d83e158`, evidence `7f96a71` *(the card's paragraph, with one sentence where the record has none)*
  - [x] age; — `d83e158`, evidence `7f96a71` *(whole days since creation, carried as `data-project-age-days` and shown as `Nd`; an unparseable date is unknown, not zero)*
  - [x] task count; — `d83e158`, evidence `7f96a71` *(every task in the project, completed or not)*
  - [x] overdue count; — `d83e158`, evidence `7f96a71` *(unfinished tasks whose deadline has passed — a completed task with a past deadline is not late, and the fixture contains exactly that task)*
  - [x] P1/high-priority equivalent where represented; — `d83e158`, evidence `7f96a71` *("where represented" taken literally: a priority property in the schema or on a task is what makes the count exist, and a project without one has no priority row rather than a zero nobody's data supports)*
  - [x] next deadline; — `d83e158`, evidence `7f96a71` *(the earliest future deadline among unfinished tasks, ties broken by task id, shown as "None" when there is none)*
  - [x] archive state; — `d83e158`, evidence `7f96a71` *(as `data-project-archive-state` and as the Active/Archived chip; the workspace's eyebrow says the same about the project that is open)*
  - [x] visual identity where available; — `d83e158`, evidence `7f96a71` *(a swatch built from the project's tab colours, and only from values that parse as colours — a string carrying CSS is no swatch, which a hostile fixture asserts)*

- [x] Active/archived filtering. — `d83e158` @ `2026-09-10T17:07:59+07:00`, evidence `7f96a71` *(the cards are filtered by the project's own status, the two buttons carry `aria-pressed` for the filter in effect, the header counts what is listed, and a filter with nothing in it says "No archived projects" rather than showing an empty grid)*
- [x] Clicking a project opens its workspace. — `dadd610` @ `2026-09-10T17:32:11+07:00`, evidence `7f96a71` *(a card is a button carrying the project id; opening it replaces the hub's grid with that project's workspace — asserted by the cards being gone, the workspace being there and naming the project's status, and the Projects button coming back to the grid)*
- [x] New Project button opens its modal even before Save is enabled. — `68e11b6` @ `2026-09-10T17:19:10+07:00` *(the button opens a provisional modal whose Save routes through `project.create` and answers the typed `action-not-available` while creating no record — `tests/projectCreateModal.test.ts`, plus this slice's assertion that the modal's controls are exactly name and description)*
- [x] Archive/restore/delete controls exist but refuse DATA WRITE until storage cutover. — `dbea424` @ `2026-09-10T17:25:25+07:00`, verified at `1ffdd55` @ `2026-09-12T01:19:47+07:00`, evidence `7f96a71` *(all three exist: an active project offers Archive and Delete, an archived one Restore and Delete, each disabled with a typed `action-not-available` refusal and the reason written beside them. The write-control audit is what proved every one of them carries a typed refusal rather than being silently inert, and this slice asserts which control a project's status gets.)*

## Workspace work

- [x] Notes. — `dadd610` @ `2026-09-10T17:32:11+07:00` *(the workspace's Notes tab renders the project's note tree; `tests/projectWorkspacePanels.test.ts` renders all five tabs and asserts no `projectType` gating and no record mutation, and `tests/projectNotes.test.ts` covers the panel itself)*
- [x] Task Board. — `dadd610` @ `2026-09-10T17:32:11+07:00` and `c8e35c3` @ `2026-09-10T19:54:34+07:00` *(the panel and its interactions, with `tests/projectTaskBoard.test.ts` covering the read-only inspector, the drag placeholders and the refused transition)*
- [x] Backlog. — `dadd610` @ `2026-09-10T17:32:11+07:00` and `b281cab` @ `2026-09-10T20:04:42+07:00` *(the panel and its interactions; slices 25–37 have since rebuilt its query, controls, selection, column table, property filters, template composer and task editor on top of it)*
- [x] Deadlines. — `dadd610` @ `2026-09-10T17:32:11+07:00` and `d3dbb59` @ `2026-09-10T20:15:12+07:00` *(the panel and its interactions, and the workspace test asserts the projection is the Timekeeping one reused rather than reinvented — which is also § Deadlines' own box below)*
- [x] Schedule capability can coexist with tasks instead of being hidden behind permanent task/schedule project silos once the corrected domain lands. — `dadd610` @ `2026-09-10T17:32:11+07:00` and `36fcc08` @ `2026-09-10T20:30:21+07:00` *(the workspace switches on the tab and never on `projectType`, so a project typed as a task still has a Schedule tab and one typed as a schedule still has a Backlog; `tests/projectWorkspacePanels.test.ts` renders a mixed project — both tasks and events — through all five tabs and asserts no gating. `Project.projectType` survives only as legacy import metadata, and HARD GATE A4 owns removing it from capability decisions.)*

### Notes — read side

- [x] Project-linked vault artifact tree. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(`loadProjectNotesTree` walks each `linkedFolders` root and nothing else, so a vault file outside those roots is absent from the snapshot rather than filtered out later; a root whose path is not vault-relative is typed `unavailable` and an absent one `missing`, and the panel draws all three states. `tests/projectNotes.test.ts` pins the entry list, the exclusion of a file outside the roots, and both degraded roots.)*
- [x] Folder expand/collapse. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(`expandedPaths` decides both `aria-expanded` and whether the children are rendered at all, so a collapsed folder emits no file buttons; the linked root's own toggle now carries `data-c1-key="project-note-root-<projectId>-<path>"`, so it is addressable like every other control. The slice-39 case drives the root and a nested folder open and shut through the machine-key harness and asserts all four DOM states, including that expanding selects nothing.)*
- [x] File selection. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(a click on a file reports its path and the renderer marks exactly that entry `selected` and `aria-current="true"`; selection is view state, so the panel is a pure function of it rather than of the DOM.)*
- [x] Markdown preview. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(`.md` and `.markdown` render the stored text verbatim as `kind:'markdown'`; slice 39 adds that a file whose frontmatter looks like a record (`id:`, `status:`, `weight:`) is still previewed byte-for-byte and never parsed into one, which is what keeps the Notes read side out of the record store.)*
- [x] Canvas preview. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(`.canvas` is summarised as node and edge counts plus a bounded node list (`MAX_PROJECT_CANVAS_PREVIEW_NODES`), and a canvas that is not JSON, or that lacks node/edge arrays, fails as `canvas-invalid` instead of drawing an empty canvas; the fixture asserts 2 nodes and 1 edge.)*
- [x] Excalidraw preview where supported. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(`recogniseExcalidraw` decides by file content, not by extension, and a scene that cannot be read fails as `excalidraw-unavailable` — the "where supported" clause is a typed failure rather than a silent omission; the fixture asserts the `excalidraw` preview kind and that it carries the rendered SVG and its element census fields.)*
- [x] Hover affordances. — `ead7927` @ `2026-09-12T02:02:58+07:00` *(`public/index.html` styles `.project-note-entry:hover`; the slice-39 case asserts that every interactive entry the renderer emits carries that class, that a root the vault cannot read carries none because there is nothing to hover, that only files are `draggable`, and that a hover reaches no handler — the affordance is the stylesheet's, not a second code path.)*
- [x] Context menu opens programmatically. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(a context-menu event on any entry reports its path and the panel renders the menu from `contextPath` under `data-project-note-context-path`; Escape closes it. Its three write verbs — Rename, Move, Delete — are drawn disabled with `action-not-available`, so opening the menu cannot write.)*
- [x] Read/open/reveal-like operations remain presentation. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(the read side is handed a `VaultReader` and the panel's handlers only set view state — selection, expansion, context, drag. Slice 39 runs the whole read side against a vault whose writer members throw and re-reads every file byte-identical afterwards, so the strongest available statement is not "it did not write" but "it had no way to".)*
- [x] Drag targets can preview valid folder destinations without committing moves yet. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(`dragover` reacts only to an element carrying `data-project-note-directory-path`, so a file is not a destination: slice 39 asserts that a drag over another file previews nothing while the same drag over a folder previews `source -> target` on the panel and reports it, and that `drop` clears the preview and reports a refusal instead of a move.)*

### Task Board — read side

- [x] Project workflow columns. — `c8e35c3` @ `2026-09-10T19:54:34+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(`renderProjectTaskBoard` draws one column per vault status definition in declaration order, then appends a column for any status a project task actually uses but the vault does not define — slice 39 pins that orphan column, its label and its drop slot — and the panel is scoped to the project, so another project's card is not drawn.)*
- [x] Card click. — `c8e35c3` @ `2026-09-10T19:54:34+07:00` *(a click on a card opens the read-only inspector for that task (`data-project-board-inspector-task-id`), which escapes the task's own text — the fixture's `<script>` description renders as text — and Escape closes it.)*
- [x] Column presentation colors. — `c8e35c3` @ `2026-09-10T19:54:34+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(a column is painted only when the status colour is a validated hex value: slice 39 asserts that `#112233` becomes `border-top:3px solid #112233` plus the echoed `data-project-status-color`, that a padded `  #abc  ` is trimmed and accepted, and that `red;display:none` and a `url(...)` value paint nothing and echo empty.)*
- [x] Local display order. — `c8e35c3` @ `2026-09-10T19:54:34+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(cards sort by `orderIndex` with the task id as the tiebreak; slice 39 adds that equal indices fall back to id order and that a missing index is treated as zero. The order is display only — `orderIndex` in the record is never rewritten by this panel.)*
- [x] Drag pickup/placeholders implemented. — `c8e35c3` @ `2026-09-10T19:54:34+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(`dragstart` reports the picked-up task, `dragover` marks the slot (`data-project-board-preview="true"`) and opens its insertion placeholder to 54px, and the drop reports the move intent; slice 39 pins the pickup report and the placeholder geometry. The slots are drawn before, between and after the cards, so the reported index is a real position rather than a column append.)*
- [x] Durable workflow transition still disabled until corrected domain/store exists. — `c8e35c3` @ `2026-09-10T19:54:34+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(the panel declares `data-project-board-write-authority="unavailable"`, its Edit and Delete controls are disabled with `action-not-available`, and a drop reports a refusal whose text says the task data was not changed; slice 39 asserts the record state is byte-identical across the whole drag-and-refuse sequence.)*

### Deadlines

- [x] Reuse the Timekeeping interaction implementation project-scoped rather than independently reinventing it. — `d3dbb59` @ `2026-09-10T20:15:12+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(the panel imports `deadlineCalendarProjection` from `timekeepingCockpit` for the deadlines themselves and declares `data-project-deadline-projection="timekeeping"`; slice 39 removes the last restatement of Timekeeping semantics by routing the overdue/upcoming split through the exported `countdownBucketForRemaining` instead of re-deriving `remainingMs < 0`, and asserts row order, day, value and state against those two functions — including the boundary where a deadline equal to `now` is `upcoming`, not `overdue`.)*

## Acceptance

- [x] Opening a project changes the cockpit, not canonical data. — `dadd610` @ `2026-09-10T17:32:11+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(opening a project decides which project the five workspace panels project: the slice-39 case opens one project and then another, sees the board's `data-project-board-project-id` and its cards change, and asserts the state JSON is byte-identical after each render. Separately, `tests/projectNotes.test.ts` runs the notes read side against a vault whose writer members throw and re-reads every byte unchanged. `tests/projectWorkspacePanels.test.ts` asserts the same state-JSON invariant per tab, and `tests/zeroWriteWitness.test.ts` proves the disk-level witness fails when it should.)*
- [x] Project Notes can inspect ordinary vault files without treating them as database records. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(a linked folder's ordinary files are listed whatever they are — `.md`, `.canvas`, `.excalidraw`, and files no previewer claims — and the snapshot is a tree (`projectId`, `roots`, `fileCount`), not a record set. Slice 39 asserts that a markdown file carrying record-shaped frontmatter is previewed verbatim as text, that an unclaimed `.json` is still listed but fails as `unsupported-format`, and that the whole read side runs against a vault whose writer members throw with every byte unchanged.)*
- [x] Same task can be visible in project Board, Backlog and Deadlines. — `dadd610` @ `2026-09-10T17:32:11+07:00` *(`tests/projectWorkspacePanels.test.ts` renders one project's `shared-task` in the Task Board, the Backlog and the Deadlines tab of the same cockpit, with a second project's task absent from all three.)*
- [x] Project can eventually show both tasks and events; no new UI work assumes `projectType` is permanent. — `dadd610` @ `2026-09-10T17:32:11+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(the acceptance fixture is a `schedule` project whose Task Board, Backlog and Deadlines are populated and whose Schedule tab carries the events; slice 39 adds the other half — rendering the same five panels for the same project typed `task` produces byte-identical panel HTML — so the panels branch on nothing but the records they are given. The legacy label survives only as a presentation caption (`src/browser/projectPresentation.ts`) and an import concern.)*

## Evidence

- Programmatic project navigation tests. — `2450828` @ `2026-09-09T21:49:58+07:00` *(the four surfaces, both Tasks modes, all six Schedule modes and the five project tabs are pinned by machine key in `tests/cockpitNavigation.test.ts`, with `cockpitSubmode` asserted per surface)*; `dadd610` @ `2026-09-10T17:32:11+07:00` *(each workspace tab is opened and read back through its own `data-project-workspace-panel` in `tests/projectWorkspacePanels.test.ts`)*
- File-tree read/preview fixture tests. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(tree shape, Markdown/Canvas/Excalidraw previews, unsafe roots and unsupported formats, all against real fixture bytes in a memory vault)*; `ead7927` @ `2026-09-12T02:02:58+07:00` *(nine cases in `tests/projectNotes.test.ts`: expansion states, hover affordances, valid and invalid drop targets, and ordinary files that are not records)*
- Cross-tab projection tests. — `dadd610` @ `2026-09-10T17:32:11+07:00` *(one project's task is read in the Task Board, the Backlog and the Deadlines tab and its event in the Schedule tab, each scoped against a second project)*
- Zero-write proof for all read-only project navigation. — `dadd610` @ `2026-09-10T17:32:11+07:00` *(every workspace tab render in `tests/projectWorkspacePanels.test.ts` is asserted to leave `JSON.stringify(state)` identical)*; `ead7927` @ `2026-09-12T02:02:58+07:00` *(opening another project is asserted the same way in that file, and `tests/projectNotes.test.ts` runs the whole notes read side against a vault whose writer members throw and re-reads every file unchanged)*; `7c0c69d` @ `2026-09-06T22:18:57+07:00` *(`tests/zeroWriteWitness.test.ts` proves the witness records a smuggled write, fails when it was never wired to anything, and detects a file changed behind its back)*

---

# Stage 6 — Restore Backlog/database presentation and modal completeness

Still before migration.

## Backlog

- [x] Search. — `9b59d16` @ `2026-09-12T00:23:35+07:00` *(`renderProjectBacklog` renders exactly the rows the query matched — asserted by a filtered-out task id being absent from the output — and echoes the active query in `data-project-backlog-search`; the matcher reads name and description case-insensitively and treats an all-whitespace query as empty. What is verified is the Backlog's behaviour under a query: the shell owns `ProjectBacklogViewState.query` and supplies it, so the interactive control that types one is the remaining piece.)*
- [ ] Tag filtering. *(Blocked on a product decision, not on effort: Proxima has no tag model. A tag could be a schema property, a list in the record's own frontmatter, or its own record, and each answer changes what the filter means and which part of A5's canonical schema owns it. The Backlog's field and property filters are already driven by the engine's own tables, so the cheap version exists the moment the creator says which of the three a tag is.)*
- [x] Property filters. — `3fa16bc` @ `2026-09-12T01:41:25+07:00` *(the query gained a second filter list rather than widening `BacklogField`: a property filter carries its `propertyKey` and its `valueType`, `assertBacklogQuery` validates it against `operatorsForValueType` (the same tables the fields use, reached by type), `applyBacklogQuery` conjoins it with the field filters and the search, and `removeBacklogFilter` finds the id in either list. The comparison itself moved out of `matchesFilter` into `compareValue`, driven by a value type rather than a field, so a property and a field cannot compare the same kind of value two ways — a refactor the engine's 17 existing cases passed before any new test existed. What is compared is what a cell shows: a multi-select property compares as the text its cell joins, a numeric property compared against text still matches nothing, and a boolean never equals its spelling. The menu offers a property because the project's tasks declare it, with only its declared type's comparisons.)*
- [x] Type-appropriate comparison operators. — `9b59d16` @ `2026-09-12T00:23:35+07:00` *(nine filter fields each admit only the operators their type supports, decided in one place so a menu and the matcher cannot disagree; a numeric field compared against a non-number does not match instead of coercing, dates compare as instants, a boolean never equals its string spelling, and a query naming an operator its field does not admit is refused by name rather than silently skipping the filter)*
- [x] Multiple filters. — `9b59d16` @ `2026-09-12T00:23:35+07:00` *(filters conjoin — a task must satisfy every one — and the projection exposes each as a chip carrying its id, field, operator and a readable label, which the renderer draws. Raising new filters from the UI is part of the unwired control work.)*
- [x] Remove filter. — `bdea4a1` @ `2026-09-12T00:34:29+07:00` *(`applyBacklogControl({kind:'remove-filter'})` drops the filter the chip names and returns the same query when the id is already gone, so removing a filter twice is harmless; the chip renders a remove button carrying `data-project-backlog-filter-remove`, the binder reads the id from it and nothing else, and `tests/projectBacklog.test.ts` drives the whole loop in happy-dom — a click on the rendered chip brings the task that filter was hiding back into the list. Removal is view state only: the query is replaced, never edited, and `tests/backlogControls.test.ts` asserts the state and every record are byte-identical after a session of controls.)*
- [x] Sort ascending/descending. — `9b59d16` @ `2026-09-12T00:23:35+07:00` *(ordering is ascending or descending on any field column, and it is a total order: ties fall through the legacy order index then the record id, so equal keys never swap between renders. A missing value sorts last ascending and first descending, which is stated because "no deadline" is not a deadline of zero.)*
- [x] Sort indicator. — `9b59d16` @ `2026-09-12T00:23:35+07:00` *(the renderer emits `data-project-backlog-sort-indicator` carrying the sorted field and direction with a ▲/▼ mark, and omits the whole toolbar when no query is active so the unqueried markup is byte-identical to what it rendered before)*
- [x] Custom-property columns. — `8cadd24` @ `2026-09-12T01:31:08+07:00` *(the projection has supplied the columns and a `cells` array per row since slice 26; the renderer drew the legacy list. It now draws the table: a header above the list with one entry per custom-property column, labelled with the schema's name, and each row's cells keyed to those columns by id — so a value sits under its own heading. A column appears because the data declares it, which is the projection's rule and now the table's too; a project whose tasks declare no properties renders no header rather than an empty one. The **field** columns are deliberately not repeated: a row already shows its name, description and deadline on one line, and a header promising columns the body does not draw would be worse than no header.)*
- [x] Resizable columns. — `8cadd24` @ `2026-09-12T01:31:08+07:00` *(each column header carries a drag edge; the width lives in `ProjectBacklogViewState.columnWidths` because how wide this reader has a column is not a fact about the table, and `resizeBacklogColumn`/`clampBacklogColumnWidth` are pure functions beside the other controls. The clamp is what stops a drag off either edge from making a label unreadable (96px) or letting one column swallow the table (640px), and rounding to whole pixels keeps a rendered width and a stored width the same number. The drag follows the schedule's gesture shape — the pointer moves update what is on screen and only the release reports a width, because re-rendering mid-drag would replace the element the pointer is holding — and it is driven end to end through the interaction harness, including both clamps. A resize edge needs no typed refusal, because resizing is presentation rather than a write; that is the line slice 33's write-control audit draws.)*
- [x] Row selection. — `9d6062c` @ `2026-09-12T01:11:58+07:00` *(every row carries a real checkbox keyed by task id, and the binder reports which task it is for rather than deciding what that means; `toggleBacklogSelection` keeps the order the marks were made in, because that is the order a bulk action would act in. Selection is view state — `BacklogViewState.selectedTaskIds` — so no record is written, asserted.)*
- [x] Select all. — `9d6062c` @ `2026-09-12T01:11:58+07:00` *(Select all means the rows on screen: `selectAllBacklogVisible` adds the visible tasks and leaves a marked task the query hides to whatever marked it before, because a hidden row is not something the creator can see they are selecting. The control disables itself when every shown row is already marked, and when nothing is shown there is nothing to select.)*
- [x] Multi-selection. — `9d6062c` @ `2026-09-12T01:11:58+07:00` *(a selection is memory, not a filter: the projection reports how many shown rows are marked, how many marked tasks the query is hiding, and whether every shown row is marked — three separate facts, so a bulk action can never be read as covering a row nobody can see. `allVisibleSelected` is false when nothing is visible, because an empty list has nothing selected and saying otherwise would let a bulk action look safe to run. Clearing the selection clears hidden marks too.)*
- [x] Task row/name click opens editor. — `ba50cc6` @ `2026-09-12T01:48:47+07:00` *(clicking a row opens the Task editor for that task, in the Backlog panel. It draws the same `projectTaskEditor` projection the Elastic board's modal draws, through a new `src/browser/taskEditorFields.ts` that takes the surface's hook names: both binders listen on the application root, so shared attribute names would have meant two binders answering one keystroke and a Backlog edit landing in the board's draft. The extraction is markup-identical — the Elastic suites passed unchanged before the Backlog's editor existed. The read-only inspector is retired rather than duplicated, since it was a placeholder for exactly this editor; the fields it showed are now editable, with Save and Delete refused with a typed result and Cancel discarding the draft. A typed edit becomes a draft that Cancel discards while the loaded state stays byte-identical, asserted; and the write-control audit's expectation for this surface moved from the inspector's Edit/Delete to the editor's Delete/Save, both typed.)*
- [x] Relation display. — `d7e6270` @ `2026-09-12T01:06:10+07:00` *(a row now draws the property cells the projection already computed, so a relation property is visible where a reader looks for it, carrying `data-project-backlog-cell-kind="relation"` so a target id can be told from an entered value. Property columns are labelled with the schema's name for the property — the projection had used the raw stored key, which disagreed with how the Task editor and the property pills already name one.)*
- [x] Rollup display. — `d7e6270` @ `2026-09-12T01:06:10+07:00` *(shown with `data-project-backlog-cell-kind="rollup"`, displaying the value the record holds. Stated residual: computing a rollup from its relations is not this surface's job yet, so what is displayed is the stored value rather than a freshly aggregated one.)*
- [x] Formula display. — `d7e6270` @ `2026-09-12T01:06:10+07:00` *(shown with `data-project-backlog-cell-kind="formula"`, displaying the stored value; the same residual as the rollup — the expression is not evaluated here)*
- [x] Bulk Complete control visible but unavailable until write cutover. — `d7e6270` @ `2026-09-12T01:06:10+07:00` *(drawn where a selection would act, disabled, carrying `data-project-backlog-write-action="bulk-complete"` and the same typed `action-not-available` refusal every other write carries, with the reason beside it. It belongs to the project this view is for and is absent from a view belonging to another project — an existing no-leak case caught the first version, which rendered it unconditionally.)*
- [x] Bulk Delete control visible but unavailable until write cutover. — `d7e6270` @ `2026-09-12T01:06:10+07:00` *(as Bulk Complete, with `data-project-backlog-write-action="bulk-delete"`; clicking either changes no record, asserted)*

## Task modal

All existing meaningful fields must be representable:

- [x] name; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(the modal is now the editor `src/app/taskEditor.ts` describes: `renderTaskModal` consumes `projectTaskEditor` instead of six hard-coded read-only inputs, and each field is drawn with the control its type calls for. Name is a text input holding the record's value; typed edits are held as a draft and never reach the record.)*
- [x] project; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a select over the active projects plus "No project", so a task can be taken out of a project as well as moved between them)*
- [x] execution state; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a select over the vault's own status vocabulary, each option labelled with the Elastic column it maps to; a vault that declares no statuses gets a text field and a note saying so rather than an empty select)*
- [ ] workflow stage where project-scoped; *(The separation exists in the domain: HARD GATE A2 is accepted at `07d4926`, which is an ancestor of this branch, and `src/domain/canonicalRecordV2.ts`/`canonicalOrdering.ts` carry `executionState` and `workflowStageId` as independent dimensions. The Task modal edits the legacy compatibility `Task` in `src/domain/types.ts` — whose `status` field is commented "Not the future canonical execution/workflow model" — because the reader still loads legacy Markdown. The box closes when canonical records reach the modal, which is the record-store read path, not a modal change.)*
- [x] weight; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a number input, with the one sentence that says what weight does)*
- [x] fixed-duration enable/value; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(the enable flag is a checkbox and the minutes are their own number field; while the flag is off the minutes field says it is not counted, which is the relationship the record encodes as "only meaningful when true")*
- [x] maximum duration; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a number input, described as the cap on how far an elastic task may stretch)*
- [x] start date; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a text input holding the stored value on purpose: the vault stores ISO instants, and a date input would normalise `2026-03-10T00:00:00.000Z` to `2026-03-10` on sight and report a change nobody made. The same reasoning covers deadline and every date property.)*
- [x] deadline; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(as start date; an absent deadline shows as empty rather than as the word "null")*
- [x] completion; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a checkbox over `isCompleted`)*
- [x] custom text property; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(the property list comes from `state.taskSchema`, not from the record: a property the schema declares but this task has never set is still a field, because a field nobody can see is a field nobody can fill in. A record value with no schema entry is shown too, so an editor cannot silently drop it.)*
- [x] number; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a `number` schema type is a number input)*
- [x] select; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a select over the schema's own options, with the stored option selected)*
- [x] multi-select; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a checkbox group, one box per option; the binder reports the whole remaining selection rather than a removal the model would have to infer, which is asserted in happy-dom by unticking one of two chosen options)*
- [x] date; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a date-typed property is shown and edited as a date field of the same text-input kind the task's own dates use, for the ISO reason above)*
- [x] checkbox; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(only a stored `true` is ticked; any other value — including the string `"true"` — is not)*
- [x] relation; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(shown as a field holding the target record id, with the field itself saying there is no picker until relations are canonical (HARD GATE A6). Representable, and honest about what is not there yet.)*
- [x] derived rollup; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(shown with its aggregation and target property, with nothing to type in: a derived value is not the record's to set. Asserted by there being no `input` or `select` inside it.)*
- [x] derived formula; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(as the rollup, showing the expression)*
- [ ] recurrence if task recurrence remains supported. *(The condition is the creator's: event recurrence is explicit domain data with its own modal and scope choice, while a task has no recurrence model anywhere in the tree. If task recurrence remains a feature it becomes a Task-modal field built the way the Event modal's controls were; if it does not, the honest close is to say so and delete the box's condition rather than leave it waiting.)*
- [x] Cancel/Escape discards provisional form state. — `7825d20` @ `2026-09-12T00:44:55+07:00` *(a draft is `null` while nothing has been edited, so discarding is `null` rather than a rebuild that hopes to reproduce the record; `dirty` is the draft differing from the record it was seeded from, so an undone edit goes back to not dirty. Cancel and Escape both discard, asserted in happy-dom by typing, seeing the unsaved-changes line, pressing Escape and reading the record's value back. Deliberately, an edit does not re-render — a keystroke must not take the field away from the reader — so the drawn draft updates on the next render.)*
- [x] Save is disabled/refused until the new record write path exists. — `7825d20` @ `2026-09-12T00:44:55+07:00` *(the button is present and disabled, carrying `data-task-editor-save-refusal="action-not-available"`, with the reason next to it: a form that cannot save says so where the button is rather than hiding it. Delete carries the same refusal.)*

## Event modal

- [x] name. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(the Event modal is now the editor `src/app/eventEditor.ts` describes, rendered by `src/browser/eventModal.ts`: before this the month/year/agenda modal and the time-grid modal were two copies of five read-only inputs with no Save, no Delete and no recurrence at all. Name is a text input holding the record's value, readonly.)*
- [x] description. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(a textarea holding the record's description, readonly)*
- [x] project. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(a select over the project names the surface knows, plus "No project", with the held one marked selected; the choices are passed in rather than read from loaded state, which is why the editor takes a narrow input.)*
- [x] start. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(a text input holding the stored start, which is an ISO instant — the same reasoning the Task editor's dates use: a date input would normalise the value on sight and report a change nobody made)*
- [x] end. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(a text input holding the record's deadline, with a note saying that is what the field is)*
- [x] color if event metadata supports it. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(the condition is false, and the modal says so rather than omitting silently: `CalendarEvent` carries no colour field and no vault format declares one, so there is no colour control. The projection exposes `colourNote` and the modal renders it at `data-c1-key="schedule-event-colour-note"`; a test asserts the note, and asserts that no field id mentions colour. If event metadata ever grows a colour, this is the box to reopen.)*
- [x] recurrence controls. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(frequency, interval, end condition, end date and count, read from the record by the schedule's own rule reader so the editor and the projections cannot disagree about whether an event recurs. They are offered even for an event that does not recur, because the end-condition select includes "Does not recur" — one control answers both whether it recurs and how it ends. Recurrence the record carries that the reader refuses is reported as unusable rather than shown as absent.)*
- [x] until/end condition. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(the end-condition select carries the four answers — does not recur, never ends, ends on a date, ends after a number of times — and the two value fields say when they are the ones in use. Asserted against a weekly rule ending on a date, a monthly rule ending after a count, and a rule that never ends.)*
- [x] exception/scope UX. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(the choice itself is the existing occurrence/series scope modal, which `tests/scheduleRecurrence.test.ts` already drives — it renders for a recurring occurrence, reports its mode and records the chosen scope. What this slice adds is that the editor states the question where the fields are, so a reader is not left to discover that changing one occurrence is not changing the series.)*
- [x] Save/Delete unavailable until write cutover. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(both buttons are present and disabled, Save carrying `data-schedule-event-save-refusal="action-not-available"` with the reason beside it: a form that cannot save says so where the button is rather than hiding it)*
- [x] Cancel/Escape loses no data. — `b20cdca` @ `2026-09-12T00:56:55+07:00` *(every control in this modal is inert — text and date inputs are readonly, selects and checkboxes are disabled, asserted in happy-dom — so there is no provisional state for a cancel to lose and closing the modal cannot change a record. Stated residual: Escape is not bound to close this modal, which is an affordance rather than a data question; when the event editor becomes editable at the record-store cutover, this box must be re-examined, because that is when a draft starts to exist.)*

## Project modal

- [x] name. — `68e11b6` @ `2026-09-10T17:19:10+07:00` *(the project surface's modal is the New Project modal, and it has collected a name since Stage 5 slice 2: `tests/projectCreateModal.test.ts` types into `project-create-name`, and asserts that Cancel, Escape and a refused Save each leave the project list and the state revision untouched. A name here is canonical data, not identity — the modal never asks for an id or a filename.)*
- [x] description. — `68e11b6` @ `2026-09-10T17:19:10+07:00` *(a textarea, `project-create-description`, typed into by the same cases and empty when the modal is reopened, so a discarded draft cannot leak into the next one)*
- [x] metadata that survives the corrected model. — `a8c1b1e` @ `2026-09-11T08:54:12+07:00` and `fef3b8a` @ `2026-09-12T01:01:45+07:00` *(the corrected shape is `CanonicalProjectRecordV2` in `src/domain/canonicalRecordV2.ts`, which keeps the name, the description, `createdAt` and the active/archived lifecycle state; the modal asks for exactly name and description, and a new case asserts its controls are exactly those two and nothing else. Nothing the corrected model drops is required: no control exists for the legacy task-versus-schedule label, the tab background or text colours, the linked folders, the record id or its source path. This is the create modal — editing an existing project's name is not something these four boxes ask for, and does not exist.)*
- [x] Do **not** require task-versus-schedule type in the successor record shape. — `68e11b6` @ `2026-09-10T17:19:10+07:00` and `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(the modal has no type control — its own case asserts `[data-project-type]` is absent — and the successor shape never mentions the field: `projectType` appears nowhere in any `src/domain/canonical*.ts` module, and the HARD GATE A4 box saying the legacy label informs import compatibility only is ticked at `d7e6a6c`. `Project.projectType` survives in the legacy compatibility model, documented as removed from capability and visibility decisions.)*

## Recurrence-scope modal

- [x] This occurrence. — `448c65f` @ `2026-09-10T16:53:37+07:00` *(the scope modal renders a `This occurrence` button carrying `data-schedule-recurrence-scope="occurrence"`, and clicking it records that scope in the modal's own state — driven in `tests/scheduleRecurrence.test.ts` since Stage 4 slice 5b)*
- [x] Entire series. — `448c65f` @ `2026-09-10T16:53:37+07:00` and `fef3b8a` @ `2026-09-12T01:01:45+07:00` *(the button shipped with the modal, but nothing clicked it until this slice: the new case clicks `schedule-recurrence-scope-series`, asserts the modal reports `series` and that both buttons' `aria-pressed` follow the choice, then changes the choice back to `occurrence` — a choice, not a commitment)*
- [x] Cancel. — `448c65f` @ `2026-09-10T16:53:37+07:00` and `fef3b8a` @ `2026-09-12T01:01:45+07:00` *(the close control carries `data-schedule-recurring-action="close-occurrence"`, and the handler mirrors `main.ts`: it clears the occurrence and the chosen scope and re-renders. The new case presses it, asserts the modal is gone, then reopens the occurrence to prove the next visit starts with no scope chosen — a discarded choice cannot be inherited.)*
- [x] No mutation while simply choosing/opening scope. — `448c65f` @ `2026-09-10T16:53:37+07:00` and `fef3b8a` @ `2026-09-12T01:01:45+07:00` *(opening the occurrence, choosing `series`, changing to `occurrence` and cancelling are all asserted to leave the loaded shape byte-identical — projects, tasks, events, statuses and schema — rather than only the one event the older case inspected. The scope is view state in `main.ts` (`selectedScheduleRecurringScope`), and choosing it dispatches no action.)*

## Template UI

- [x] Paste/type. — `d21f434` @ `2026-09-12T01:26:26+07:00` *(`src/browser/templateComposerPanel.ts` is a panel the Backlog hosts, opened from "Tasks from a template" in its toolbar and carrying a real textarea at `data-template-text`. Typing re-renders — which is what makes the preview follow the text — and the caret is put back afterwards, the same arrangement the Backlog's search field uses. A textarea rather than a one-line field, because a template is multi-line by nature.)*
- [x] Parse. — `d21f434` @ `2026-09-12T01:26:26+07:00` *(`src/app/templateComposer.ts`, pure and tested in Node: one task per unindented line, one `field: value` per indented line, `#` for a comment, `property.<key>` for a custom property. The panel parses on every render rather than keeping a second copy of what the text means, because a preview that holds its own idea of the text is how a preview and a parser drift apart.)*
- [x] Preview. — `d21f434` @ `2026-09-12T01:26:26+07:00` *(every task the parser could read is listed with the line it came from and a one-line description of what it asks for — weight, status, dates, durations, completion, custom properties, in that order — so the preview says what the text *means* rather than repeating it. Empty text previews as "Nothing to plan yet" rather than as an empty list.)*
- [x] Structured parse errors. — `d21f434` @ `2026-09-12T01:26:26+07:00` *(eleven typed codes — a field before any task, an unknown field, a duplicate, a missing separator, an empty value, a tab, an invalid number, date or boolean, and the task and line bounds — each carrying the line, the column of the offending character, the line as written, and a sentence naming what a valid value looks like. Writing the tests found a real bug: value complaints reported a zero-based column, so `weight: heavy` pointed one character early; the column is now computed from the raw line, and `weight: heavy` and `weight:heavy` each point at their own character.)*
- [x] Execution disabled until record write actions exist. — `d21f434` @ `2026-09-12T01:26:26+07:00` *("Create tasks" is present and disabled, carrying the typed `action-not-available` result at `data-template-execute-refusal` with the reason beside it: execution is Stage 16's job, and a button that cannot run says so where it is rather than being hidden. A test clicks through to it, asserts the refusal and the note, and asserts no record changed.)*
- [x] Exact old textual mini-language is not assumed immutable if the same presentation/workflow can be preserved cleanly. — `d21f434` @ `2026-09-12T01:26:26+07:00` *(taken literally: the format is **this project's own** and nothing reproduces the legacy syntax or promises compatibility with it. The module says so in its own documentation, and the panel tells the reader the format inline. What is preserved is the workflow the box cares about — a person writes a shape once and gets tasks out of it — not the old characters. The presentation is therefore reconstructed rather than ported, which is what "not assumed immutable" permits.)*

## Acceptance

- [x] Every old editor can be opened programmatically. — `1ffdd55` @ `2026-09-12T01:19:47+07:00` *(five editors, each opened from state alone with no pointer: `tests/modalAudit.test.ts` renders the Task editor in the Elastic surface, the Event editor and the create-event variant in the time grid, the New Project modal, and the recurrence scope modal — and asserts each is present. The editors open because a view state names what is being edited (`elasticSelectedTaskId`, `selectedScheduleEventId`, `seededEvent`, `newProjectOpen`, `selectedRecurringOccurrence`), so a test or an agent drives them the same way a click does; the older suites that open each one by clicking remain as the second path.)*
- [x] Every unsaved field can be changed and cancelled without durable change. — `1ffdd55` @ `2026-09-12T01:19:47+07:00` *(three surfaces, three honest answers, all read-only in effect. **The Task editor** has real provisional state: a draft is `null` until something is typed, Cancel and Escape discard it, and a draft equal to its seed is not dirty (`tests/elasticCockpit.test.ts`, `tests/taskEditor.test.ts`). **The New Project modal** has provisional name and description that Cancel, Escape and a re-open all discard, with the state byte-identical throughout (`tests/projectCreateModal.test.ts`). **The Event editor** has no provisional state at all: every control is inert and reads the record, so there is nothing a cancel could lose (`tests/eventModal.test.ts`) — that is stated rather than dressed up as an editing form.)*
- [x] Search/filter/sort never mutate records. — `bdea4a1` @ `2026-09-12T00:34:29+07:00` *(the Backlog is Stage 6's only search/filter/sort surface, and the whole path is proven read-only: `tests/backlogControls.test.ts` drives projection and markup through a session of controls and asserts the loaded state is byte-identical, every task is the same object with the same keys, and the query's own filters array is replaced rather than edited; the happy-dom session in `tests/projectBacklog.test.ts` does the same after real clicks and typing. A modal that later gains a query surface must meet this same bar — this tick covers the query surfaces that exist.)*
- [x] Relation/rollup/formula projection works without wikilink semantics leaking into UI code. — `1ffdd55` @ `2026-09-12T01:19:47+07:00` *(`tests/boundaries.test.ts` now enforces it rather than describing it: `[[target]]` syntax or the word for it appears in exactly three modules — `domain/excalidraw.ts`, `domain/excalidrawAssets.ts` and `app/excalidrawAssetLoader.ts`, the one place a raw `![[asset]]` embed is really decoded — and nowhere in `src/browser/`. A relation is a record id: the Task editor shows the target id and says there is no picker until relations are canonical (HARD GATE A6), the Backlog draws relation, rollup and formula values from `task.properties` with the kind the schema declares, and nothing resolves a link out of text. The pattern demands a closing `]]`, because a nested array literal looks like `[[` too — the first version of the check flagged `app/inspection.ts` for an array of pairs.)*`
- [x] All future Save/Delete buttons currently produce a typed unavailable result rather than fake success. — `1ffdd55` @ `2026-09-12T01:19:47+07:00` *(audited and **two real violations found and fixed in this slice**: the Task editor's and the Event editor's Delete buttons were disabled with no stated reason, which is indistinguishable from broken — both now carry a typed `action-not-available` refusal as their Save buttons did. `tests/modalAudit.test.ts` checks the invariant against the rendered document for the Task editor, the Backlog inspector and bulk controls, the Projects Hub lifecycle controls and the Event editor; the two controls that stay clickable (`project-create-save`, the create-event Save) are routed to the dispatcher and each has a case that clicks it and asserts the refusal and that no record was created. The population is the product's own convention — a `*-refusal`, `*-write-action` or `*-lifecycle-action` hook — with a narrow safety net for a button labelled exactly "Save", "Delete", "Edit", "Archive", "Restore" or "Complete" that is enabled with no hook. Selection by words alone was tried and failed: the Backlog's completion *sort* button reads "Completed" and the Projects Hub's "Archived" is a filter.)*

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
- [x] Relations are translated to record IDs. — `400ccfc` @ `2026-09-11T16:24:16+07:00` *(unambiguous permitted legacy wikilinks become canonical relation values containing only opaque relation-schema and target-record IDs; missing, ambiguous, malformed, disallowed-kind, duplicate-target and unresolved-schema cases remain explicit)*
- [x] Legacy status is translated separately into: — `173b45e` @ `2026-09-11T15:04:55+07:00` *(the dry-run conversion plan preserves one legacy status input while independently deriving Elastic execution meaning and project-scoped workflow-stage-candidate meaning; no final workflow-stage record is materialized yet)*
  - [x] execution state; — `173b45e` @ `2026-09-11T15:04:55+07:00` *(existing compatibility Elastic classification becomes canonical `backlog|running|finished`, including completion override and unknown-valid-status → running behavior)*
  - [x] workflow stage. — `173b45e` @ `2026-09-11T15:04:55+07:00` *(resolved projects receive a project-scoped legacy-status stage candidate; absent/ambiguous project identity remains explicitly unresolved rather than choosing a stage target)*

- [x] Legacy ordering is translated into the appropriate scoped orders. — `173b45e` @ `2026-09-11T15:04:55+07:00` *(legacy order seeds independent validated Elastic-execution and, when resolvable, project/workflow-stage-candidate positions; no universal canonical `orderIndex` is emitted)*
- [x] Legacy project type informs import compatibility only; it does not create a permanent silo. — `173b45e` @ `2026-09-11T15:04:55+07:00` *(`task|schedule` is retained only as compatibility import metadata; both labels declare canonical capability authority as associated data/workspace rather than a type filter)*
- [x] Schema/settings needed to interpret custom properties become first-class schema records. — `368b3bf` @ `2026-09-11T15:37:49+07:00` *(explicitly interpreted task/per-project settings are converted through scoped stable opaque schema/option identities into canonical-ready primitive, select, multi-select and non-empty-formula records; option colors remain local-state; relation/rollup/incomplete-formula cases remain pending; planner and parent import remain dry-run/zero-write)*
- [x] Legacy custom-property values are captured from the existing interpreted task/event frontmatter and ordinary task families are dry-run mapped to canonical opaque schema/option identities. — `a360fa9` @ `2026-09-11T16:08:36+07:00` *(projects expose no property-value surface; events remain captured-but-untyped; absent, unresolved, relation-pending, rollup-pending and formula-pending outcomes remain explicit; parent/property plans remain zero-write)*
- [x] Legacy wikilink relations never remain canonical relation values. — `400ccfc` @ `2026-09-11T16:24:16+07:00` *(canonical-ready relation values are constructed through the canonical relation boundary and contain no wikilink text, legacy ID, path, basename, filename, display name, folder or `.md` value)*
- [x] Notes/drawings/attachments are **not copied** into the record store. — `646d72e` @ `2026-09-11T18:49:42+07:00` *(slice-8 artifact planner is reference-only and has no content-reader or copy authority)*
- [x] Project references to external notes/files remain references to external artifacts. — `646d72e` @ `2026-09-11T18:49:42+07:00` *(interpreted linked folders become explicit canonical `pxa_...` artifact references and project associations; legacy labels/paths remain evidence)*
- [x] Legacy source files are never altered. — `646d72e` @ `2026-09-11T18:49:42+07:00` *(the accepted slice proves zero legacy-Markdown, Record Store, staging and external-artifact writes)*

## Import staging

Use staged activation, not a half-cut-over live database.

- [x] Import can materialize a staging record store. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(one isolated store receives every kind the planners can prepare, in the order they require: projects, the workflow stages those projects scope, the tasks that resolve a stage through that mapping, events, and the schema records the plan declares — asserted by non-empty staged sets and a non-empty store, over four fixture vaults. The store is slice 9's staging-only capability (`9c0c2dc`), never the canonical Record Store: `readStagedRecord` and `createStagedRecord` are all it has.)*
- [x] Valid records may be converted into staging while blockers are reported. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the malformed fixture is the case: its fifteen reader problems are all warnings — the reader is tolerant, so those records entered state — and the run creates the records whose canonical payload it can build while four candidates are blocked with typed reasons in the same pass. Every candidate is accounted for as created, reused or blocked, so nothing is silently dropped, and the blockers carry machine-readable reasons rather than prose.)*
- [x] Staging is not canonical until activation. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(every materialization result reports `activation: 'not-performed'`; the store's authority is `legacy-import-staging-only`, and a store claiming canonical authority is refused by the materializers rather than written into; and after a full staging pass the application still reads the legacy vault, with none of the staged opaque ids present in that state.)*
- [x] Re-running the same import is idempotent with respect to already assigned import identities. — `d66622f` @ `2026-09-12T00:12:36+07:00` *(re-planning the same vault with a fresh allocator in a disjoint id range reuses every identity from the durable mapping, so a re-run cannot mint a second record for a source that already has one; the conversion ids and the manifest agree, and no identity is held by two records)*
- [x] An interrupted import resumes/replans without producing duplicate canonical records. — `d66622f` @ `2026-09-12T00:12:36+07:00` *(a run that stops is resumed from the stored manifest alone: the test persists the mapping, discards the plan, and re-plans with an allocator in a disjoint range — identities come back identical, a third pass is a fixed point rather than drifting, and a duplicated legacy alias still keeps both physical records distinct. The claim proven is identity reuse on replan; canonical materialization remains staged and not activated.)*
- [x] No hidden "some records now JSON, some still Markdown" live mode is allowed unless explicitly designed and tested. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(there is no mixed mode to allow: after a full staging pass the product's only source is still the legacy vault — `loadVaultState` over the same tree returns the legacy records and none of the staged ids — and no module outside the import planners reads a staging store. This box is a prohibition that currently holds by absence; if a mixed mode is ever designed, the box reopens and that mode must be tested rather than assumed.)*

> **Superseded at `d9d8c5e` @ `2026-09-12T02:35:31+07:00`.** Slice 9 proved these invariants for
> canonical-ready schema records in an isolated staging store (`9c0c2dc` @ `2026-09-11T19:01:24+07:00`).
> The broad physical task/project/event staging is no longer the open half:
> `tests/importStagingBytePreservation.test.ts` materializes every kind into one staging store over all
> four fixture vaults, with the byte-preservation proof run around the operation. **Activation** —
> choosing the staged records as canonical — is what remains, and that is HARD GATE C's.

## Duplicate legacy IDs

Do **not** silently choose one source file.

- [x] Every physical legacy record involved in an ID collision is identified separately. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(import planning consumes the compatibility reader's pre-dedup physical candidate inventory; the dedicated duplicate fixture exposes both `proj-twin` sources and both `task-shared` sources separately)*
- [x] Each decodable physical record can receive its own candidate opaque ID in staging. — `42a0361` @ `2026-09-11T19:14:55+07:00` *(staging persists the already-authored physical-source identity manifest; duplicate legacy aliases retain separate candidate IDs and complete collision evidence; no payload is guessed)*
- [x] The duplicate legacy alias is recorded as a collision. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(machine-readable collision groups retain the shared legacy alias plus every physical candidate's source provenance and separately allocated opaque identity)*
- [x] Any legacy relation/project reference that resolves through that duplicate alias remains explicitly unresolved/ambiguous. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(a project alias with multiple physical candidate mappings yields `resolution: ambiguous`, null selected project ID and the complete candidate-ID set; general non-project relation conversion remains open)*
- [x] No arbitrary filesystem/index order picks the target. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(all candidate identities may be deterministically listed, but a duplicate target alias never resolves by first/last/index order)*
- [x] Canonical activation cannot claim the migration is clean while ambiguous references remain unacknowledged. — `394179c` @ `2026-09-12T00:02:14+07:00` *(`import.status` reports the plan's outstanding `unresolvedProjectReferences`/`ambiguousProjectReferences` and the `appliedProjectSelection`, and `import.commit` refuses with those counts in machine-readable `error.outstandingProjectReferences` while either is nonzero, so the only machine path toward activation provably refuses rather than reading clean; canonical activation itself remains gated behind HARD GATE C)*
- [x] A machine-callable import-resolution operation exists if ambiguous identities require explicit mapping. — `bd64a34` @ `2026-09-11T23:57:13+07:00` *(`import.resolve` accepts the explicitly selected candidate project record id, resolves every ambiguous project reference whose candidate set contains it, and returns the resolved in-memory dry-run plan; an id that is a candidate of no ambiguous reference is refused as `invalid-action-input` rather than silently ignored, and `import.commit` stays typed-unavailable)*
- [x] Resolution decisions are included in the import evidence. — `bd64a34` @ `2026-09-11T23:57:13+07:00` *(the resolution returns the resolved schema-v1 plan as the action's evidence, so each affected reference, task workflow stage, workflow-order scope and event project association names the selected project and the reference counts are recomputed; the verification that described the pre-resolution plan is discarded and `import.inspect` re-verifies the resolved plan)*

## Malformed records

- [x] Parse/validation-blocking malformed record produces a structured import failure containing: — `3846805` @ `2026-09-11T19:22:40+07:00` *(staging-only problem manifest groups each physical source and preserves the structured evidence)*
  - [x] source path/reference; — `3846805` @ `2026-09-11T19:22:40+07:00`
  - [x] record kind if known; — `3846805` @ `2026-09-11T19:22:40+07:00`
  - [x] problem code; — `3846805` @ `2026-09-11T19:22:40+07:00`
  - [x] bounded diagnostic. — `3846805` @ `2026-09-11T19:22:40+07:00` *(uses `DIAGNOSTIC_LIMITS.problemDetail`)*

- [x] No JSON record is created from guessed fields. — `3846805` @ `2026-09-11T19:22:40+07:00` *(canonical payload materialization and canonical staging-record creation are both zero)*
- [x] Original malformed Markdown remains byte-identical. — `3846805` @ `2026-09-11T19:22:40+07:00` *(the accepted proof compares source bytes before and after)*
- [x] Other valid records may be prepared in staging. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the malformed fixture is the case: records with unreadable or invalid fields are reported by the plan, and the records that are valid are still prepared — created counts above zero while four candidates are blocked, in the same run, with the legacy bytes unchanged.)*
- [x] Canonical activation does not silently omit malformed records as though import were complete. — `c62a7dc` @ `2026-09-12T00:05:59+07:00` *(`import.status` reports the plan's `readerProblems` and `unsupportedFrontmatter`, and `import.commit` carries them in machine-readable `error.outstandingRecords` whenever any record could not be converted — including after the project references are acknowledged, so clearing ambiguity cannot make an incomplete import read as complete. Records the importer cannot convert are counted, not dropped; activation itself remains gated behind HARD GATE C.)*
- [x] A machine-readable unresolved-record count remains nonzero until deliberately resolved/skipped according to an explicit migration policy. — `3846805` @ `2026-09-11T19:22:40+07:00` *(manifest exposes `unresolvedRecordCount`; activation and resolution policy remain open)*

## Unsupported-frontmatter open question

The repository currently has a real unresolved semantic mismatch: repository loading can accept `unsupported-frontmatter` as a warning, while refresh treats that same code as blocking. The docs correctly preserve this as an open question. Do **not** invent an import rule for it.

- [ ] Before final migration activation, answer:

> Is an otherwise readable record containing `unsupported-frontmatter` importable using the interpreted fields with legacy source preserved as provenance, or must import block until the unsupported construct is resolved?

  *(Still the creator's decision, and `d9d8c5e` @ `2026-09-12T02:35:31+07:00` sharpens what it
  costs: the reader treats both `unsupported-frontmatter` and `frontmatter-parse-failure` in the
  malformed fixture as **warnings**, so those records enter state, and the staging pass then
  converts them with the interpreted fields. The answer therefore decides whether that
  conversion is correct by default or must be withheld — it is not a question about the
  machinery, which already handles both answers.)*

- [x] Until answered, importer reports it distinctly from an ordinary malformed record. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(`unsupported-frontmatter` is emitted as `unsupported-frontmatter-policy-pending`, while ordinary frontmatter parse failures remain separate reader problems; no importability policy is invented)*
- [ ] Tests encode the decided rule only after the decision exists. *(Waiting on the answer above, by the box's own wording. The current tests assert only what is decidable today: that the code is reported distinctly, that the record is otherwise readable, and that the legacy bytes are preserved either way.)*

## Byte-preservation proof

- [x] Hash every legacy Markdown record before import. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(`runLegacyImportBytePreservationProof` snapshots SHA-256 of every `.md` under the layout's record directories plus every file under each accepted external-artifact folder before the operation runs, and refuses to proceed when the artifact plan is absent rather than proving a subset.)*
- [x] Run import. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the operation is the real staging pass — projects, workflow stages, tasks, events, schema — over disposable copies of the fixture vaults, so the proof surrounds actual work: the staged sets are asserted non-empty, which a proof around a no-op could not claim.)*
- [x] Hash every legacy Markdown record afterward. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the same paths are hashed again after the operation, and the before/after entry lists are compared as sets, so a record that disappeared is as visible as one that changed.)*
- [x] Every hash matches. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(verdict `preserved`, zero changed paths, and — because a reader's account of itself is not proof — every digest the verifier reports is compared against a `node:crypto` hash of the file on disk. The instrument fails when it should: the same suite shows it reporting a change when a record is edited, when a source file is injected, and when one is removed.)*
- [x] Notes/drawings/attachments also remain untouched by the importer. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(three real artifact files are created inside the fixture project's own linked folders — a note, a canvas and a binary — and all three are byte-identical afterwards, on disk and in the verifier's digests. The artifact plan is reference-only by construction, and a machine-path reference is reported as unverifiable rather than claimed as proven.)*
- [x] No source "promotion" or ID injection is performed into legacy files. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the independent filesystem comparison covers additions as well as edits, so a promoted or injected file would appear as `added`; the verifier's own injection case proves that comparison reports one. Four fixture vaults are swept this way with zero changes.)*

## Import verification

Machine-check the legacy interpreted state against new-state semantics:

- [x] same count of valid physical task records accounted for; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(the task census reports `loadedRecords` equal to `counts.tasks`, with `unaccountedCandidates` zero and `loadedRecords + explicitlyRejected === recordCandidates`)*
- [x] same count of valid projects accounted for; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(the project census reports `loadedRecords` equal to `counts.projects`, with `unaccountedCandidates` zero and the candidate arithmetic closing)*
- [x] same count of valid events accounted for; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(the event census reports `loadedRecords` equal to `counts.events`, with `unaccountedCandidates` zero and the candidate arithmetic closing)*
- [x] every imported source has explicit import disposition; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`unaccountedCandidates` is zero for every kind, so each accepted candidate either became a record or was refused for a stated reason; every conversion also carries the `sourcePath` it came from, and each declared fixture path appears in the identity mapping or the problem list)*
- [x] names preserved; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`name` equals the declared frontmatter name on the project, task and event conversions)*
- [x] descriptions preserved; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`description` equals the declared single-line frontmatter description on every kind)*
- [x] dates preserved; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`createdAt`, `startDate` and `deadline` preserve the declared instants, compared as instants so a format normalisation cannot pass as data loss)*
- [x] task durations/weights preserved; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`weight: 3`, `isFixedDuration: true`, `fixedDuration: 90` and `maxDuration: 120` all survive exactly as declared)*
- [x] project associations mapped; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(both `project:` and `projectId:` resolve to the same canonical project record id, named in the task workflow stage, its workflow-order scope and the event project association; `unresolvedProjectReferences` is zero)*
- [x] custom property values mapped. — `a360fa9` @ `2026-09-11T16:08:36+07:00` *(ordinary task text, finite number, readable date, checkbox, select and multi-select values map through slice-4 opaque identities; event values remain captured-but-untyped; unresolved and derived families remain explicit)*
- [x] relations either resolved to new IDs or explicitly unresolved. — `400ccfc` @ `2026-09-11T16:24:16+07:00` *(exact physical/alias resolution uses existing opaque mappings; missing, ambiguous, malformed, disallowed-kind, duplicate-target and pending-schema outcomes are retained as machine-readable dispositions)*
- [x] recurrence mapped where representable; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`recurrence` is an explicit typed `null` on every task and event conversion — an own property, so "no recurrence" is a decision rather than an omitted key. Recurrence stays captured-but-untyped, so nothing is representable yet and no mapping is claimed.)*
- [x] archived/completed state preserved; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`status: archived` survives on the project conversion and `isCompleted: true` on the task, which remains planned with an execution state rather than being dropped as finished)*
- [x] no legacy `projectType` silo leaks into new capability filtering; — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`disposition` is `compatibility-import-metadata-only` and `canonicalCapabilityAuthority` is `associated-data-and-workspace`; projects, tasks and events are all planned, so the project's legacy type filters nothing out)*
- [x] no record filename is derived from record title. — `d7e6a6c` @ `2026-09-12T00:09:34+07:00` *(`recordId` is opaque on every conversion and carries no title text; the legacy filename survives only as `sourcePath` provenance; and two records declaring the same title still receive distinct identities)*

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

- [x] Canonical conversion-plan semantics tests. — `173b45e` @ `2026-09-11T15:04:55+07:00` *(physical-candidate status decomposition, completion override, unknown-status execution compatibility, project-scoped workflow-stage planning, independent scoped-order planning, ambiguous-project workflow refusal, and projectType compatibility-only treatment; zero staging/Record Store writes)*

- [x] Schema/settings conversion-plan contract tests. — `368b3bf` @ `2026-09-11T15:37:49+07:00` *(scoped identity reconciliation, canonical-ready primitive/select/multi-select/non-empty-formula records, presentation-only colors, relation/rollup/incomplete-formula pending states, collision refusal, parent-plan integration, mapping persistence and zero-write boundaries)*

- [x] Legacy custom-property value capture and conversion-plan contract tests. — `a360fa9` @ `2026-09-11T16:08:36+07:00` *(interpreted task/event evidence capture, scoped task-schema fallback, project-schema isolation, opaque schema/option mapping, explicit absent/unresolved/deferred outcomes, event untyped boundary, parent schema-version integration, and zero-write guarantees; focused 3 files / 22 tests; serialized full suite 155 files / 928 tests)*

- [x] Relation target resolution and wikilink→canonical-record-ID conversion contract tests. — `400ccfc` @ `2026-09-11T16:24:16+07:00` *(exact wikilink parsing, unambiguous opaque-ID conversion, duplicate-alias ambiguity, physical-path disambiguation, missing and disallowed-kind refusal, unknown-folder pending behavior, canonical-value boundary and zero-write guarantees; focused 4 files / 28 tests; serialized full suite 156 files / 934 tests)*

- [x] Rollup canonical-reference and derived rollup/formula conversion-plan contract tests. — `57e8c16` @ `2026-09-11T17:46:24+07:00` *(canonical relation-schema and target-property resolution with explicit missing/ambiguous/incompatible outcomes; derived values remain evidence-only; focused 5 files / 32 tests; serialized full suite 157 files / 938 tests; zero-write guarantees)*

- Full import against all four existing fixture vaults. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the planning pass and the full staging pass run over `vault-basic`, `vault-legacy`, `vault-duplicates` and `vault-malformed` on disposable copies, with every candidate in every kind accounted for as created, reused or blocked, and the byte proof around each one. The sweep asserts it was not four easy vaults: at least one fixture holds records the reader refused and at least one holds an identity collision.)*
- Dedicated duplicate-ID fixture assertions. — `be3efdf` @ `2026-09-11T14:52:38+07:00` *(pre-dedup candidate enumeration and collision groups)*; `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the sweep includes the colliding fixture and asserts the collision is reported rather than resolved silently — a duplicate legacy id is staged as its own candidate with its own id, because choosing one silently is the failure the section exists to prevent.)*
- Dedicated malformed-record fixture assertions. — `3846805` @ `2026-09-11T19:22:40+07:00` *(structured failure, no guessed fields, original bytes unchanged)*; `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the malformed fixture converts what it can and blocks four with typed reasons in the same run, with the tree unchanged.)*
- Legacy tree byte hashes before/after. — `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(SHA-256 before and after, independently re-derived from the files on disk, over four fixture vaults.)*
- Machine-readable import manifest/report. — `0fd5f51` @ `2026-09-11T14:28:25+07:00` *(the schema-v1 plan)*; `d9d8c5e` @ `2026-09-12T02:35:31+07:00` *(the byte-preservation proof is itself a machine-readable object — snapshot, per-path digests, changes, counts, `verifierWrites`, verdict — so a run's evidence can be diffed rather than read.)*
- Restart after staged import. *(Not yet: the staging store the proof uses is in memory, so "restart" has nothing durable to come back to. The identity half of restart is proven — `d66622f` resumes from the stored mapping — and the store half needs the durable staging backend wired to the import pass.)*
- Restart after committed import. *(Not yet: nothing commits, because activation is HARD GATE C's. This bullet closes with the cutover, not before it.)*
- Idempotent rerun. — `d66622f` @ `2026-09-12T00:12:36+07:00` *(a re-plan with a disjoint allocator range reuses every identity, and a third pass is a fixed point.)*
- No creator gesture. — `bd64a34` @ `2026-09-11T23:57:13+07:00` *(the administrative actions — `import.plan`, `import.inspect`, `import.resolve`, `import.commit`, `import.status` — are semantic and programmatic, and the staging materializers are plain functions; nothing in the import path requires a click.)*

---

# HARD GATE C — Canonical cutover

Do not enable any real record-editing UI until this gate closes.

## Work

- [x] Startup chooses the Proxima record store as canonical tasks/projects/events/schema source after successful migration activation. — `d6e2b30` @ `2026-09-12T03:02:30+07:00` *(both halves now exist and are tested. **Activation is an act with a marker**: `activateRecordStore` refuses an empty store, refuses to steal a store another import activated, refuses to overwrite a marker this build cannot read, and otherwise writes when it happened, which import it came from, and how many records of each kind — beside `records/` and `recovery/` in the store's own namespace, so "activated" is a fact rather than an inference. **The choice is one function with every answer named** (`chooseStartupSource`): no marker, an unreadable marker, a store emptied after activation, a store short of what it activated, and an unreadable store each keep the product on the legacy reader *and report why*, because an empty canonical store renders an empty application and that is worse than reading Markdown. Startup composes it: `startupSession` activates a `record-store` candidate when the decision says so, keeps a restored vault handle as that candidate's **artifact** reader rather than letting it become a competing source (a remembered folder would otherwise undo the cutover on every launch), and reports `sourceDecisionKind`/`Reason`/`Detail` in the startup inspection so a fallback is never invisible. The caveat worth stating: nothing in the shipped path *writes* the marker yet — that belongs to the import's commit step, so until an operator or the import activates a store, startup chooses legacy by design and says `no-activation-marker`.)*
- [ ] Legacy Markdown record directories remain present but become **legacy source only**. *(Present is proven — the byte-preservation proof at `d9d8c5e` leaves every file identical through a full staging pass, and nothing deletes a legacy record. "Legacy source only" is now reachable rather than hypothetical: an activated store makes the vault an artifact reader only, and `tests/recordStoreActivation.test.ts` shows a store-activated session reading the store's records while a legacy vault holding a different project sits unread beside it. What keeps the box open is that activation has no shipped trigger yet — with no marker, startup still reads Markdown for records, and that is the correct default until the import's commit path activates a store.)*
- [x] Legacy Markdown task/project/event changes after cutover do not silently overwrite JSON records. — `06c0702` @ `2026-09-12T02:53:45+07:00` *(the protection is unconditional today, which is stronger than the box asks: the only writer of canonical records is the record store's own boundary, and no legacy path can reach it — `importPlanner` refuses a record-store provenance with `legacyIdOriginOf`, and the reader has no writer at all. The isolation case asserts it rather than arguing it: after renaming the source Markdown **and** deleting it, `store.list()` returns the same records with the same observed revisions, while the vault's own note read returns what the vault now says.)*
- [x] Record-store mutations refresh every active Proxima surface. — `06c0702` @ `2026-09-12T02:53:45+07:00` *(proven for a mutation made through the store's own boundary: `createIfAbsent` a record and the next refresh classifies the load as `changed`, advances the source generation from 1 to 2, and the projection every surface renders gains the record — `session.projection().state.tasks` goes from one task to two. The refresh is the same one the interval policy triggers, so it is not a special path. What does not exist yet is a *UI* that performs such a mutation: adding a task by clicking is Stages 9–14's work, and this box's mechanism is what those stages will stand on.)*
- [x] Read-only projection/source abstractions are generalized so UI does not care whether state originated from legacy import fixtures or record store. — `738bb53` @ `2026-09-12T02:45:43+07:00` *(the missing piece was that nothing turned `CanonicalRecordV2` into `ProximaState`: the store held canonical records and every surface read the compatibility shape, so a record-store source could not even be represented. `src/app/recordStateProjection.ts` is that projection and `recordStoreStateLoad.ts` is the store-side load, in the same shape as the vault-side one (state plus the revisions a caller needs to notice change). `tests/recordStateProjection.test.ts` proves it end to end — records written through the canonical store boundary, read back through it, projected, and rendered by the real Task Board — and proves the claim that matters: the legacy reader and the record store draw **the same cards in the same three Elastic columns**, so the board asks the state what it holds rather than where it came from. Two things are deliberately not invented: a project's legacy `projectType` is reconstructed from what the project holds (A4 removed it from capability decisions), and a workflow stage is reported as having no slot in the readable world rather than being folded into a column (A2 keeps it independent). The wiring this box left open is done too: `06c0702` gives the session a third mode and a `StateSource` seam, so the two origins are switchable at runtime, not only in a test's imagination.)*
- [x] Current UI no longer labels the ordinary product as "Read-only workspace" once record mutations are enabled; at `608bcdc` that label is still hardcoded into the browser shell. — `9a04451` @ `2026-09-12T03:40:29+07:00` *(the literal is gone and the claim is now derived: `src/browser/workspaceIdentity.ts` returns "Editable workspace" only when records come from the record store **and** a record write path actually resolved, and "Read-only workspace" otherwise — so a record-store run whose writes are still refused keeps saying read-only, which is still true, and an activated store stops. Deriving it from the capability rather than the source mode is the whole point: a label tied to the mode would have claimed editability the moment a store existed, before any write path was resolved. The span carries `data-c1-key="workspace-identity"` and `data-workspace-writes` so the fact is readable rather than only the sentence, and `tests/workspaceIdentity.test.ts` holds the shell to consuming the derivation instead of restating it. The condition the box names is now met in the one configuration that can write: an activated store, which is what Stages 9+ deliver.)*
- [ ] Existing FSA creator-vault write boundary remains blocked for record files because record files are no longer creator-vault files at all. *(The guard is stronger than the box asks and now applies to the shell itself: `d6e2b30` resolves the browser's store source in the adapter layer and hands `main.ts` a `StateSource`, whose type has no mutation method, so the shell holds no RecordStore authority at all — `tests/recordMutationContainment.test.ts` asserts exactly that, and it fired on a first attempt that imported the store into `main.ts`, which is the guard doing its job. The FSA boundary remains closed and asserted (`evaluateFsaWriteBoundary()`, `tests/fsaWriteBoundary.test.ts`), and record files already live behind `RecordStoreFileBackend` with opaque names. What keeps the box open is its "because": it is a statement about the **shipped default**, and the shipped default is still the legacy reader until an activation trigger exists — item 2 above. Mutations existing is not the same as a product that reaches them by itself.)*
- [ ] H4 remains untouched. *(No instruction in this tree defines H4 beyond the creator's standing constraint; nothing in slices 39–46 went near it, and no path here writes to the creator's vault.)*

## Acceptance

- [x] Modify a legacy task Markdown file after cutover; canonical Proxima task does not change. — `06c0702` @ `2026-09-12T02:53:45+07:00` *(asserted in the configuration the cutover creates: with a record-store session active, renaming `Proxima/tasks/running.md` leaves the projection's tasks exactly as the store holds them (`['Store task']`, not the edited name), and the refresh reports `unchanged` rather than degrading — the legacy edit is not an event this source can see at all. The shipped default is still the legacy reader, so this is the mechanism the cutover will use rather than a statement about today's default; the checkbox is ticked because the assertion the box asks for now runs and passes.)*
- [x] Execute semantic JSON-backed task update; every surface changes. — `abf8204` @ `2026-09-12T03:20:05+07:00`, `cab1627` @ `2026-09-12T03:31:18+07:00` and `18c2e48` @ `2026-09-12T03:37:24+07:00` *(the operation the box was waiting for now exists and two UI callers execute it: an Elastic drop writes `execution-state` + `execution-order` as one accepted mutation, and the card editor's Save writes one typed mutation per changed field — both through `src/app/taskMutations.ts` over the real store and the real recovery gate, both carrying the revision the surface read. "Every surface changes" is asserted as the loop it is: the write is followed by the product's own refresh controller over the record store as a source, and the surfaces render that projection — the same projection `8dc3841` proved every surface draws, and the same refresh `06c0702` proved classifies a store change. Nothing is drawn as moved or saved before the store says so, and a refused write leaves every surface as it was.)*
- [x] Restart; JSON-backed state remains. — `d6e2b30` @ `2026-09-12T03:02:30+07:00` *(asserted at the level a restart actually is: the same durable pieces — the record files and the activation marker — are reopened as brand-new objects with nothing carried in memory, and the product comes back in `record-store` mode with the identical `StartupSourceDecision` and an identical projected state. The marker is what makes that answer stable rather than lucky: a rebuilt store with no marker would choose legacy, and the case starts from the marker, so the two halves of "it came back" are both checked. The browser's own storage layer is separately conformance-tested (`tests/opfsRecordStoreFileBackend.test.ts`); what this case covers is the composition.)*
- [x] Remove/rename legacy task source after cutover; canonical record remains. — `06c0702` @ `2026-09-12T02:53:45+07:00` *(the sharpest test of the cutover, and it passes in the configuration that matters: with a record-store session active, `delete`ing the legacy task file leaves the canonical task in every projection, the refresh still reports `unchanged`, and `store.list()` returns the same records with the same observed revisions — so the removal neither changed the state nor reached the store. Provenance is what would make a regression visible: a surface that still resolved through the legacy path would show a task whose `source.idOrigin` is not `record-store`.)*
- [x] Notes continue reading from vault. — `06c0702` @ `2026-09-12T02:53:45+07:00` *(asserted in the store-source configuration, which is the one that could break it: the record-store candidate still carries a `reader`, `session.reader()` still returns the vault, and after an edit the note read returns what the vault now says — while records come from the store. The candidate type requires a reader in every mode for exactly this reason, and `src/app/recordStoreStateLoad.ts` reads only the store, so the two halves cannot drift into each other.)*
- [x] Inspection identifies record-store source/revision rather than pretending JSON records are Markdown provenance. — `738bb53` @ `2026-09-12T02:45:43+07:00` *(provenance gained a `record-store` origin (`RecordOrigin`/`recordOriginOf` in `src/domain/records.ts`), so a projected record's `SourceRef` reports `idOrigin: 'record-store'`, the record id where a vault path would be, and the store's observed revision. `createInspectionProjection` carries that through unchanged: the case asserts the project, task and event provenance all say `record-store`, that the revision equals the one the store reported, and that the snapshot is still a valid inspection projection — so nothing downstream has to special-case a store origin. The widening also surfaced a real boundary: `importPlanner` copies a source's `idOrigin` into fields that can only mean a legacy Markdown answer, so those four sites now go through `legacyIdOriginOf`, which refuses a record-store record rather than letting one claim a vault origin.)*

## Evidence

- Cutover integration test. — `d6e2b30` @ `2026-09-12T03:02:30+07:00` *(`tests/recordStoreActivation.test.ts`: records placed through the store boundary, activated, decided, and read by a session whose surfaces render them — while a legacy vault holding a *different* project sits beside it, unread for records and still read for notes. The board is asserted from the store's state, including the three canonical execution columns.)*
- Cross-surface convergence test. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(one source change read back by eight surfaces plus all six Schedule views, with untouched records' revisions unchanged)*; `06c0702` @ `2026-09-12T02:53:45+07:00` *(the record-store variant: a record created through the store's boundary is classified `changed` on the next refresh and appears in the projection every surface renders.)*
- Legacy-source-isolation test. — `06c0702` @ `2026-09-12T02:53:45+07:00` *(`tests/recordStoreSourceSession.test.ts`: with records coming from the store, the source Markdown is renamed and then deleted; nothing the surfaces read changes, the refresh stays `unchanged`, and the store's records and observed revisions are untouched — while the vault's own note read returns the edited text. The vault is isolated to the half it still owns.)*
- Restart test. — `d6e2b30` @ `2026-09-12T03:02:30+07:00` *(the same durable pieces reopened as fresh objects: identical decision, identical state, still `record-store`. A store rebuilt without its marker chooses legacy, which is what makes the test about restart rather than about a lucky default.)*
- Machine-readable source-mode inspection. — `06c0702` @ `2026-09-12T02:53:45+07:00` and `d6e2b30` @ `2026-09-12T03:02:30+07:00` *(the third mode is a value the whole inspection path carries: `SourceMode` includes `record-store`, the session snapshot reports it, the startup inspection adds `sourceDecisionKind`/`Reason`/`Detail` so a fallback is never invisible, and the real-vault acceptance report carries `record-store` as its own mode instead of collapsing it into `fixture`. Provenance reports the store's revision per record (`738bb53`). What is still missing is a *shipped* run in that mode, because nothing writes an activation marker yet — startup says `no-activation-marker` and reads Markdown, correctly.)*

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

- [x] New Task Save calls `task.create`. — `c74003f` @ `2026-09-12T03:54:01+07:00` *(there was no New Task control anywhere in the tree — `renderElasticCockpit` drew cards, the session controls and the Task editor, and the Projects Hub's New Project modal was the only creation form — so the box needed a form rather than a wiring. `src/app/taskCreate.ts` is that form's model: a `FormDraft` defaulted from the reader's selection (a real project, or no project when the selection is only a filter), a projection over the same `TaskEditorField` vocabulary the card editor uses, and `planTaskCreate`, which turns the draft into one closed typed request — name, project, column, weight, dates, durations, and `executionOrder: 0`, because where a new card belongs among its peers is a drag and inventing an order here would claim a position nobody chose. Every refusal names its field, and the form offers only fields the request can carry: custom properties are absent rather than shown-and-refused, which is the same boundary the card editor's property refusal shows from the other side. `src/browser/newTaskModal.ts` draws it with hooks of its own (`data-new-task-field`), because the editor and the form can both be on the board and one binder answering the other's keystroke is the failure those hooks exist to prevent; Escape closes whichever modal is actually open. Save is a real control exactly when a write path resolved, is offered only once the form holds a name, and a refused create leaves the form open with what was typed. Fifteen cases: ten over the real store and the real recovery gate and five through the real renderer and binder.)*
- [x] Card edit Save calls typed task mutation. — `cab1627` @ `2026-09-12T03:31:18+07:00` and `18c2e48` @ `2026-09-12T03:37:24+07:00` *(`planTaskEditorSave` turns the draft into one typed mutation per field that actually changed — nothing else, so a field nobody touched cannot be rewritten over a concurrent editor's work — and refuses anything the record could not hold rather than half-writing the form; custom properties are refused by name because their values arrived through a compatibility projection and writing them back needs Stage 10's canonical mapping. `cab1627` is that plan and its sequence over the real store; `18c2e48` makes the modal's Save a real control, offered only when there is something to write, and reports the click through the real binder. A refused save keeps the edits so a reader retries from the authoritative revision; an accepted one clears them.)*
- [x] Delete calls `task.delete`. — `18c2e48` @ `2026-09-12T03:37:24+07:00` *(the modal's Delete is a real control whenever a write path resolved, it carries the revision the card was read at, and an accepted delete closes the editor while a refused one leaves it open — the bookkeeping is reported by the app layer rather than reached for, which is what makes it testable. The Timekeeping surface's copy of the same modal still passes the typed-unavailable constant on purpose: its binder has no form handlers at all, so its editor is read-only until Stage 14's write parity gives it some.)*
- [x] Drag Backlog → Running calls `task.execution.move`. — `abf8204` @ `2026-09-12T03:20:05+07:00` *(the drop
      is routed through the app-layer drop sequence (`src/app/elasticDropAction.ts`, extracted at `ed09e3d`) into
      `moveTaskByGesture`, which submits one `execution-state` + `execution-order` mutation through the
      semantic operation layer and then refreshes; the gesture names the operation from the column change, so a
      Backlog → Running drop reports `task.execution.move` and a within-column drop reports the reorder.)*
- [x] Drag Running → Finished calls same semantic family. — `abf8204` @ `2026-09-12T03:20:05+07:00` *(the same
      gesture with a different target column; completion follows it, because the write path derives `isCompleted`
      from the execution state, and the case asserts a Running card lands in Finished complete and unmodified
      elsewhere.)*
- [x] In-column card reorder calls `task.execution.reorder`. — `abf8204` @ `2026-09-12T03:20:05+07:00` *(a drop
      whose target column equals the card's own is the reorder operation and nothing else: the case asserts the
      action type, the new order and an unchanged execution state, so a reorder can never be reported as a move it
      did not make.)*
- [x] UI uses provisional card/placeholder feedback during drag. — `57860d3` @ `2026-09-10T09:14:42+07:00` *(built
      with the cockpit and already covered: `tests/elasticCockpit.test.ts` drives a real drag through the binder and
      asserts a correctly sized insertion placeholder appears at the drop target while no move has been emitted, that
      it moves to the slot under the pointer, and that exactly one semantic move leaves on drop.)*
- [x] UI does not update authoritative record until accepted. — `abf8204` @ `2026-09-12T03:20:05+07:00` *(the
      gesture writes first and the render reads the store afterwards — there is no optimistic card at any point, so
      there is nothing that can disagree with the record. The nine-case file asserts the store is the authority: the
      record's revision advances once, the projection is re-read through the product's own refresh controller, and a
      refused gesture leaves both the record and the store's revision untouched.)*
- [x] Stale refusal returns card to authoritative location and shows refusal feedback. — `abf8204` @
      `2026-09-12T03:20:05+07:00` *(a lost race is the one refusal where the board is showing a revision the store no
      longer holds, so the gesture re-reads before it returns, reports the revision that beat the caller, and the
      shell draws the typed reason in the refusal banner beside the authoritative card. Every other refusal leaves
      the world as it was and deliberately does not redraw.)*
- [x] Storage/recovery failure does not leave a card optimistically "saved." — `abf8204` @
      `2026-09-12T03:20:05+07:00` *(no write is attempted until the sanctioned path resolves, and that resolution
      refuses by name — `not-activated`, `recovery-blocked`, `store-unreadable` — so a store behind an unresolved
      recovery journal cannot be written at all. A failed write moves nothing; a failed refresh after an accepted
      write does not undo the write, and the card is never drawn from a guess.)*

## Agent parity

For every UI operation above:

*(The five boxes below compare two callers of one operation, so they need the UI caller to exist
before they can be compared — that is Stage 9's UI-wiring half. The agent side is now real rather
than promised: `e898a04`'s semantic write path **is** the programmatic entry point, it validates
before it writes, it refuses a stale caller with the revision that beat it, and it reports an
accepted write's resulting revision. Because a gesture will call that same path rather than a
second implementation, parity is structural once the wiring lands — but structural is not
asserted, so the boxes stay open until a case drives both.)*

- [x] same action accepted through agent entry point; — `1029a25` @ `2026-09-12T03:59:36+07:00` *(the programmatic entry point is the semantic write path — `createTask`/`updateTask`/`deleteTask` over the record store — and each UI operation is now driven twice, in two identical worlds, once through the sequence the UI executes and once through a directly submitted typed request, with record ids normalised away: create, update, move between columns, reorder inside a column and delete all leave the two affected records equal field for field.)*
- [x] same validation; — `1029a25` @ `2026-09-12T03:59:36+07:00` *(the same invalid request is refused in the same words by both callers, and neither moves the record. Writing the case found the gap it was meant to catch: the editor's plan refused an unfillable value as `invalid-value` while the write path said `validation-refused`, so the same refused keystroke read differently depending on which caller asked. The plan now speaks the taxonomy's word, and the case compares reason **and** detail rather than only success.)*
- [x] same stale behavior; — `1029a25` @ `2026-09-12T03:59:36+07:00` *(both callers lose the same race the same way: each holds the revision its own surface rendered, a winner writes first, and both are refused `stale-revision` with the revision that beat them — a second gap this case found, since the editor's refusals did not report `actualRevision` although the drop's did. The winner's value stands in both worlds and neither loser's value landed.)*
- [x] same resulting record revision; — `1029a25` @ `2026-09-12T03:59:36+07:00` *(both callers are told the revision the store observed, and the two revisions are equal once identity is normalised away: one accepted write, one revision, on both paths.)*
- [x] same resulting inspection state. — `1029a25` @ `2026-09-12T03:59:36+07:00` *(the inspection projection reports both records identically — same column, same duration, same record-store provenance and the same revision entry — which is the box's claim about what an agent inspecting afterwards sees after a human's write and after its own.)*

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

- [x] Human-style drag and direct semantic action produce identical durable task state. — `e62e8f4` @
      `2026-09-12T03:21:44+07:00` *(one task is moved by a drop and a second by the equivalent submitted operation,
      and the two stored records are compared field by field with only identity and the human-typed title removed:
      they are equal — execution state, order, completion and workflow order — and both callers are told the same
      resulting revision. The drag is not a second implementation of the move; it is a caller of the one operation.)*
- [x] Two agents/surfaces race same task revision: one wins, stale caller learns it lost. — `e898a04` @ `2026-09-12T03:10:20+07:00` *(asserted against the real store and the real coordinator: two callers hold the same revision and submit different names; the first is accepted, the second is refused as `stale-revision` **with the revision that beat it**, its own value never reaches the record, and retrying from that observed revision succeeds. Both halves of the box are checked — one wins, and the loser is told rather than left with a silent overwrite. A stale delete is refused the same way and the record survives it.)*
- [x] Elastic lock/progress remains local and does not increment task revision. — `e62e8f4` @
      `2026-09-12T03:21:44+07:00` *(asserted rather than assumed: a real dispatcher over the store's own projection
      takes the run target, locks the run, has an execution presentation derived from that session at a tick moment
      and unlocks, and afterwards every task's observed revision is byte-identical and the store holds exactly the
      records it held before. The tick predicate is the renderer's own — a live run asks for one and a deterministic
      run derives the same numbers on demand — so neither path can reach a record.)*
- [x] Completion semantics are consistent when moving into/out of Finished. — `e898a04` @ `2026-09-12T03:10:20+07:00` *(completion is **derived** from the execution state on every move rather than set beside it, so a task in Finished is complete and one that is not is not — the case moves a task in and back out and asserts both, and that the workflow stage and its position are untouched by either move. A standalone `completion` mutation exists for data edits, and it deliberately does not move the execution state: a caller that wants the board to change says so separately.)*
- [x] Reordering Elastic does not alter workflow-stage order. — `e898a04` @ `2026-09-12T03:10:20+07:00` *(execution order and workflow order are separate mutations, and the case asserts both directions: an execution reorder leaves `workflowOrder` and the canonical workflow-stage projection identical, and a workflow-order change leaves `executionOrder` where it was. Two rules the canonical codec enforces are also enforced here with sentences rather than store rejections — a task in a stage must carry its position in it, and a project change may not leave a stage behind from another project.)*

## Evidence

- Semantic action tests. — `e898a04` @ `2026-09-12T03:10:20+07:00` *(`tests/taskMutations.test.ts`: `task.create`, `task.update` and `task.delete` over the real store boundary and the real recovery coordinator — creation with a dozen typed refusals that leave every revision untouched, closed-field updates including property and duration clears, completion and both orderings, a contested write, and a delete that honours its revision. The required-action inventory is now real code: create/update/delete, property set and clear (relations ride the property value union), dates, weight and durations, both orderings, execution-state moves and recurrence set/clear. What is deliberately absent is the UI that calls it: no gesture dispatches these yet, and the containment guard still requires every registered record-mutation action to be refused through the dispatcher.)* **The UI now has a caller as of the drop wiring** — `abf8204` and `ed09e3d` route an Elastic drop into this path, and the containment guard was relaxed deliberately in that commit to the sharper rule it now asserts (the drop is routed to the operation layer and is deliberately *not* dispatched, no file under `src/browser/` composes a store, and the sanctioned composition names all three refusal reasons). What is still absent from the UI half is everything else the stage names: the card editor's Save and Delete, and the New Task modal.
- UI/agent equivalence tests. — `1029a25` @ `2026-09-12T03:59:36+07:00` *(the mutation half exists: `tests/uiAgentMutationParity.test.ts` runs the same operation twice, once through the UI's sequence and once through a submitted typed request, and compares acceptance, refusal vocabulary, stale behaviour, resulting revision and inspection state. What it compares are two callers of the **operation layer**, which is what the stage's own parity boxes define as the agent side; an agent-facing *submission* path over the action protocol is still missing, and Stage 0's two boxes below name that gap.)*
- Stale race tests. *(Two callers of one record: the two-writer race at `e898a04` over the real coordinator, and a *gesture* that lost a race at `abf8204` — the drop carries the revision the board was rendering, is refused, re-reads, and reports the revision that beat it.)*
- Automated drag tests. *(Three levels, all exercised rather than asserted as text: the binder's real drag through `tests/elasticCockpit.test.ts` at `57860d3`, the shell's drop sequence executed against a real store in the `Stage 9 shell glue` cases of `tests/taskMoveGesture.test.ts` at `ed09e3d`, and the gesture-to-record loop at `abf8204`.)*
- Restart/read-back tests. *(Open for task mutations specifically. The coordinator's own durability is covered — `recordMutationBeforeCommitProcessDeath.evidence.mjs` and `recordMutationAfterCommitProcessDeath.evidence.mjs` kill and restart a real process over a disposable root — and `tests/recordStoreActivation.test.ts` closes and reopens a store, but no case yet writes a task through the semantic path, reopens the backend and reads it back.)*
- Mutation journal request-ID attribution. *(Covered at the coordinator: `tests/recordMutationCoordinator.test.ts` asserts an outcome reports the caller's own `requestId` against the prepared/committed journal sequence, the durable record shape carries it (`RecoveryRecord.requestId`, persisted by the file-backed store), and `tests/recordMutationConcurrency.test.ts` asserts two callers keep distinct ids and that a loser retries under a new one. What the write path adds is that its refusals speak the same vocabulary the action result reports.)*

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

- [x] All editable custom property types round-trip through semantic operations. — `6dfad33` @ `2026-09-12T04:05:45+07:00` *(`src/app/propertyMutationPlan.ts` reverses the compatibility projection, and the case that matters does the whole loop through the real store and the real recovery gate: canonical values in, projection out (a select as its **label**, a number as a number, a relation as record ids), a form edit, the mapping back, and then both ends read again. All six editable types are written in one save — text, number, date, checkbox, select, multi-select and relation — and the record is asserted to hold canonical data (`{type:'select', optionId}`, `{type:'multi-select', optionIds}`, `{type:'relation', value:{relationSchemaId, targetRecordIds}}`) while the projection shows what was typed. Stage 9's blanket refusal of property edits is gone, which was the point of deferring it here.)*
- [x] Relations use IDs. — `6dfad33` @ `2026-09-12T04:05:45+07:00` *(A6 seen from the write side: a relation field holds record ids and is parsed as ids — comma- or space-separated because that is how it is shown — and a name typed into one is refused rather than resolved, because a relation that guessed would point at a record nobody chose. The canonical record also requires the value to name the schema it belongs to, so the mapping writes the property's own schema id as `relationSchemaId`; the codec refuses a relation whose `relationSchemaId` is not the property key, and the round-trip case asserts the stored value carries it.)*
- [x] Rollup/formula values are derived, not independently writable unless their schema says otherwise. — `6dfad33` @ `2026-09-12T04:05:45+07:00` *(refused by name with `unsupported-field` before anything is written, for both a rollup and a formula, and the round-trip case asserts a declared rollup is absent from the record after a save that wrote six other properties — a derived value is shown by the projection and is not the record's to set. No schema in this tree says otherwise, so "unless their schema says otherwise" is currently an empty permission rather than a silent one.)*
- [x] Schema validation occurs before record writer call. — `6dfad33` @ `2026-09-12T04:05:45+07:00` *(the plan validates against the schema — the type, the option a value names, whether the property is derived at all — and both refusal cases assert the record is still at its first revision afterwards, so nothing reached the coordinator. A property with no schema record is refused as `unknown-schema` rather than written as free text, and the canonical codec is still the second gate: the mapping produces values the encoder then validates, which is why the round trip can assert exact stored shapes.)*

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

- [x] click card opens editor; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(`tests/elasticCockpit.test.ts` routes task opening, target changes, lock and unlock through the real DOM, and the card now opens the same Task editor the board does.)*
- [x] drag pickup; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(a pickup marks the card `data-elastic-pickup` and dims it to 0.65, asserted before the pointer is released.)*
- [x] correctly sized placeholder; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(the insertion placeholder is 90px at the drop slot before release, and 0px once the drag ends.)*
- [x] column feedback; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(the destination column takes an outline while it is the drop target and loses it when the drag ends outside a slot.)*
- [x] invalid drop restoration; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(hover, pickup, placeholder and destination feedback all clear, no move is emitted, and the pre-storage refusal is rendered as text that says the task data was not changed.)*
- [x] successful drop persists; — `abf8204` @ `2026-09-12T03:20:05+07:00` and `e4e319b` @ `2026-09-12T03:44:25+07:00` *(the drop is no longer refused: it submits one accepted mutation and then re-reads, so the card that "persisted" is the record's own state rather than the DOM's. `tests/taskMoveGesture.test.ts` asserts the store's revision advanced exactly once and the projection agrees, and `tests/elasticChangeConvergence.test.ts` mounts the real renderers over the re-read projection and finds the card in Running on the Elastic column, the project Task Board's column and the Task editor's field.)*
- [x] Lock/Unlock; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(both are local-state actions routed through the real dispatcher from the rendered controls.)*
- [x] live run progression; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(per-task and overall progress advance deterministically while locked, and only the external Elastic surface ticks.)*

## Timekeeping

- [x] Calendar/Gantt/Countdown independent toggles; — `760e54d` @ `2026-09-10T11:18:58+07:00` *(`tests/timekeepingCockpit.test.ts` composes the panels non-exclusively through machine-key interactions.)*
- [x] simultaneous panels; — `37e722b` @ `2026-09-10T11:56:40+07:00` *(one task is observed in every Timekeeping panel its temporal data applies to at the same time.)*
- [x] live countdown buckets; — `2b8a145` @ `2026-09-10T11:51:56+07:00` *(all five buckets render, and items move between them as the injected clock advances.)*
- [x] Gantt bar follows pointer; — `c1f8c93` @ `2026-09-10T11:45:31+07:00` *(a phased pointer move previews whole days on the bar and resolves the occupied row continuously, with the proposal text naming both dates.)*
- [x] Shift resize; — `c1f8c93` @ `2026-09-10T11:45:31+07:00` *(Shift distinguishes start-edge from end-edge resize geometry and refuses an inverted preview.)*
- [ ] accepted drop remains; *(the Gantt move is refused with a typed result, so nothing is accepted to remain. Stage 14's Timekeeping write half owns this, under HARD GATE C.)*
- [x] refused drop visibly reverts; — `c1f8c93` @ `2026-09-10T11:45:31+07:00` *(after the refusal the bar is back on its original `gridColumn`, the row transform and the target marker are cleared, the pickup mark is gone, and the proposal text is the refusal itself.)*

## Schedule

- [x] six modes; — `215777a` @ `2026-09-12T02:11:10+07:00` *(one fixture set mounted through both renderers the application chooses between, each view compared against the same canonical occurrence projection clipped to what that view shows.)*
- [x] Today/Previous/Next; — `fc460f6` @ `2026-09-10T16:36:28+07:00` *(the shared contract is asserted for Day/4-Day/Week and for all six modes' date arithmetic.)*
- [x] empty-cell event creation; — `2e74059` @ `2026-09-10T15:29:20+07:00` *(an empty slot seeds a local one-hour proposal at its clicked civil time with no Save side effect.)*
- [x] event click; — `7357b4d` @ `2026-09-10T12:06:02+07:00` *(machine-key clicks open and close the local read-only event editor without changing event data.)*
- [x] 15-minute drag; — `7292075` @ `2026-09-10T14:54:37+07:00` *(moves follow the pointer and snap to Schedule-specific 15-minute slots in all three grid modes.)*
- [x] 15-minute resize; — `7292075` @ `2026-09-10T14:54:37+07:00` *(only the bottom edge resizes, with a live 15-minute snapped deadline preview.)*
- [x] cross-day move; — `7292075` @ `2026-09-10T14:54:37+07:00` *(a multi-day timed event moves across civil days with a segmented live preview and is restored after the typed refusal.)*
- [x] recurring occurrence scope; — `448c65f` @ `2026-09-10T16:53:37+07:00` and `fef3b8a` @ `2026-09-12T01:01:45+07:00` *(a recurring occurrence in Day reaches the scope-choice path on click, both scopes are offered, the choice can change, and Cancel discards it without touching a record.)*

## Projects Hub

- [x] cards expose pressure/summary; — `7f96a71` @ `2026-09-12T01:52:46+07:00` *(`tests/projectsHubCards.test.ts` asserts every field the checklist names, with the conditionals taken literally — a priority row only where a priority is represented, an unreadable created date as "Unknown", a swatch only for a usable colour.)*
- [x] clicking enters workspace; — `7f96a71` @ `2026-09-12T01:52:46+07:00` *(clicking a card opens that project's workspace, and the back control returns to the hub.)*
- [x] create/archive/restore/delete have visible feedback. — `68e11b6` @ `2026-09-10T17:19:10+07:00`, `7f96a71` @ `2026-09-12T01:52:46+07:00` and `08e505d` @ `2026-09-12T02:16:06+07:00` *(the lifecycle controls offer archive or restore plus delete, each disabled with its typed refusal and a visible note; Save keeps the provisional modal open and records its refusal on the modal; and an invalid form now answers with `invalid-action-input` rather than with the same unavailable refusal every valid form gets.)*

## Notes

- [x] file/folder click; — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(a file click reports its path and marks exactly that entry; a folder click toggles it.)*
- [x] expand; — `ead7927` @ `2026-09-12T02:02:58+07:00` *(a collapsed root emits no file buttons at all; the root and a nested folder are driven open and shut through the machine-key harness and all four states asserted.)*
- [x] context menu; — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(a context-menu event reports the path, the menu renders from view state under `data-project-note-context-path`, and Escape closes it.)*
- [x] hover actions; — `ead7927` @ `2026-09-12T02:02:58+07:00` *(the hover affordance is the stylesheet's `.project-note-entry:hover` on exactly the interactive entries, a hover reaches no handler, and a root the vault cannot read has nothing to hover.)*
- [x] drag destination; — `ead7927` @ `2026-09-12T02:02:58+07:00` *(only folder elements are destinations: a drag over a file previews nothing, the same drag over a folder previews `source -> target`, and the drop clears the preview.)*
- [x] move/rename/create/delete feedback as far as HARD GATE D permits. — `fa5bb33` @ `2026-09-10T19:43:38+07:00` *(`as far as HARD GATE D permits` is the operative clause and the feedback is the typed refusal: the context menu draws Rename, Move and Delete disabled with `action-not-available`, and a refused drop renders the refusal naming the source and the destination. The verbs themselves are Stage 15's, under that gate.)*

## Task Board

- [x] custom workflow columns; — `ead7927` @ `2026-09-12T02:02:58+07:00` *(one column per vault status definition in declaration order, and a column appended for any status a project task uses but the vault does not define.)*
- [x] card click; — `c8e35c3` @ `2026-09-10T19:54:34+07:00` *(the click opens the read-only inspector for that task, its text escaped, with Escape closing it.)*
- [x] card drag; — `ead7927` @ `2026-09-12T02:02:58+07:00` *(dragstart reports the picked-up card and the drop reports the move intent, with the record byte-identical across the whole sequence.)*
- [x] placeholder; — `c8e35c3` @ `2026-09-10T19:54:34+07:00` *(the hovered slot opens its insertion placeholder to 54px before the drop and is re-rendered away after it.)*
- [ ] workflow transition independent of Elastic execution state. *(The independence is proven in the domain — HARD GATE A2 at `07d4926`, on this branch: `src/domain/canonicalOrdering.ts` scopes workflow order by project and stage while execution order is scoped by execution state — but a card drop cannot perform a transition yet; it is refused like every other record mutation. Stage 10's Board write half owns the interaction, under HARD GATE C.)*

## Backlog

- [x] search; — `bdea4a1` @ `2026-09-12T00:34:29+07:00` *(typing searches as the field changes, the field shows the text that is searching, and an empty match says so.)*
- [x] filters; — `9b59d16` @ `2026-09-12T00:23:35+07:00` and `3fa16bc` @ `2026-09-12T01:41:25+07:00` *(field filters and property filters both chip, remove and refuse a value their type cannot compare while keeping the query they had.)*
- [x] sort; — `bdea4a1` @ `2026-09-12T00:34:29+07:00` *(a column sorts ascending, then descending, then clears.)*
- [x] resizable columns; — `8cadd24` @ `2026-09-12T01:31:08+07:00` *(a drag on the edge keeps the header and its cells together, and both clamps are asserted.)*
- [x] selection; — `9d6062c` @ `2026-09-12T01:11:58+07:00` *(a row checkbox marks it and the projection reports how many shown rows are marked.)*
- [x] select-all; — `9d6062c` @ `2026-09-12T01:11:58+07:00` *(select-all means the shown rows, and clears again; a marked task the query hides is counted rather than silently covered.)*
- [ ] bulk actions; *(the controls are present and refuse with a typed result, and the selection half is tested, but no bulk action can run: the per-entity result shape belongs with the first one that can. Stage 10's write parity owns this, under HARD GATE C.)*
- [x] relation/rollup/formula display. — `d7e6270` @ `2026-09-12T01:06:10+07:00` *(every custom property of a row is drawn and says which kind it is, including relation, rollup and formula cells.)*

## Modals

- [x] every meaningful field accessible; — `7ec8d17` @ `2026-09-12T00:39:14+07:00` and `b20cdca` @ `2026-09-12T00:56:55+07:00` *(the Task editor represents every field of the task and every schema property, whether the task has it or not, and the Event modal shows every field the record holds.)*
- [ ] Save; *(partly wired as of Stage 9: the Task editor's Save is a real control whenever a record write path resolved — `cab1627` plans one typed mutation per changed field and `18c2e48` lets the modal offer it — and it is refused with a typed reason otherwise. The box says **every** modal, so it stays open on the two that still cannot save: the Event modal (Stage 12's write half) and the New Project modal (Stage 11's).)*
- [x] Cancel; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(Cancel discards the provisional form state — a draft is `null` until something is edited — and the Elastic quick editor's Cancel is asserted too.)*
- [x] Escape; — `7825d20` @ `2026-09-12T00:44:55+07:00` *(Escape is the same discard, asserted for the Task editor, the Elastic quick editor, the New Project modal, the Notes context menu and both inspectors.)*
- [ ] Delete; *(partly wired as of Stage 9: the Task editor's Delete is a real control whenever a record write path resolved (`18c2e48`), it carries the revision the card was read at, and an accepted delete closes the editor while a refused one leaves it open. The Event modal's Delete still cannot run, so the box stays open on Stage 12's write half.)*
- [x] recurrence scope; — `fef3b8a` @ `2026-09-12T01:01:45+07:00` and `1ffdd55` @ `2026-09-12T01:19:47+07:00` *(both scopes are offered, the choice can change, Cancel discards it without touching a record, and the modal is reached from the occurrence selection.)*
- [x] invalid form refusal; — `08e505d` @ `2026-09-12T02:16:06+07:00` *(the New Project modal's Save with an empty or whitespace-only name is refused as `invalid-action-input` by the boundary it dispatches through, while a name that is a name still gets this stage's unavailable answer — so the modal does not answer every form with the same refusal. The boundary refuses an empty name directly in `tests/actionProtocol.test.ts`.)*
- [x] stale-save refusal; — `cab1627` @ `2026-09-12T03:31:18+07:00` and `18c2e48` @ `2026-09-12T03:37:24+07:00` *(the first real Save exists, so a stale save is now a thing that can happen and is asserted: the editor's write carries the revision the card was read at, a save built on a record someone else has since changed is refused as `stale-revision`, the loser's value never reaches the record, the card is re-read to the winner's state, and the form keeps its edits so a reader retries from the authoritative revision rather than retyping. The observed-revision contract underneath is Gate 13's, `052c3b4`.)*

## Feedback

- [x] provisional UI never masquerades as committed state; — `7ec8d17` @ `2026-09-12T00:39:14+07:00` and `57860d3` @ `2026-09-10T09:14:42+07:00` *(a fresh draft is not a change until something is edited; a drag preview is drawn by the surface and the record stays byte-identical; the pre-storage refusal says the task data was not changed rather than showing the move as done.)*
- [x] accepted action visibly settles; — `57860d3` @ `2026-09-10T09:14:42+07:00` *(the only actions that can be accepted today are presentation and local-state ones, and they settle visibly: target and lock presentation survive an ordinary rerender, a sort or filter redraws the rows it asked for, a selection reports its count. An accepted record mutation cannot exist yet — the Save/drop halves above are the gate.)*
- [x] stale/refused action visibly restores authoritative state; — `c1f8c93` @ `2026-09-10T11:45:31+07:00`, `7292075` @ `2026-09-10T14:54:37+07:00` and `ead7927` @ `2026-09-12T02:02:58+07:00` *(the Gantt bar returns to its original column and clears its markers, the Schedule grid restores a multi-day move after the typed refusal, and the Task Board's refused drop clears the placeholder while the record stays byte-identical.)*
- [x] operation failures are not swallowed; — `08e505d` @ `2026-09-12T02:16:06+07:00` *(a failed note preview is rendered with its failure code rather than as an empty pane, and idle/loading/ready are each distinct states; refusals elsewhere are rendered text naming the reason, and load problems reach the inspection projection rather than being discarded.)*
- [x] no gesture depends on opening raw JSON/Markdown to finish the operation. — `08e505d` @ `2026-09-12T02:16:06+07:00` *(every gesture above is driven through the machine-key harness against the rendered surface; no case in this pass reads a file to complete an operation. The one deliberately raw-text surface is the Template composer, whose format is this project's own and whose plan is data — slice 34's decision.)*

## Evidence

- Automated interaction recording/report covering every trace row. *(**Not claimed by this
  pass.** `proxima-interaction-parity-trace.md` is itself a reference document — "complete and
  stable", not a work item — and its interactions are prose, not rows a runner can enumerate.
  What this pass does is name, for each box, the case that asserts it. Making the trace itself
  executable as a conformance matrix is Stage 17's own line (see "Before calling UX parity
  complete" there), and that is where this bullet is satisfied or left open.)*
- Every expected DOM/state transition machine-asserted. *(Yes, and each of the fifty-one ticked
  boxes above names the file and case: happy-dom, the machine-key harness, the real binders and
  renderers, with state compared as JSON and records compared byte-for-byte where a write was
  refused.)*
- No "creator visually confirmed" evidence. *(Yes — nothing above depends on a human looking,
  and Stage 0's `## Acceptance` already made that binding for every suite since `5d5cebf`.)*
- Full action/inspection trace retained for the run. *(The dispatched actions a surface runs are
  retained in the dispatcher's own action sequence and exposed through the inspection
  projection, which the `actionProtocol` and `inspection` suites assert; the mutation leg is
  `null` because no mutation stream exists, as the projection says rather than fabricating one.)*

---

# Stage 19 — Cross-surface and agent convergence

The cockpit must behave as one system, not a collection of independently updated surfaces.

## Work

- [x] Task changed on Elastic updates: — `8dc3841` @ `2026-09-12T02:22:54+07:00` and `e4e319b` @ `2026-09-12T03:44:25+07:00` *(both halves now exist. The **origin** was the missing one: an Elastic edit was refused, so the surfaces below were converging on changes nobody could make from the UI. As of Stage 9's write half an Elastic drop and a card editor's Save are real writes — one accepted mutation each, carrying the revision the card was read at — and `tests/elasticChangeConvergence.test.ts` starts where a person does: a drop, then the product's own re-read, then the real renderers mounted over that projection. The five surfaces below are asserted for a *source-made* change at `8dc3841` and for an *Elastic-made* one at `e4e319b`, which is the pair the box was asking for.)*
  - [x] Backlog; — `8dc3841` *(the row shows the new deadline and the old value is gone from the table, not merely joined by the new one.)*
  - [x] project Task Board; — `8dc3841` *(the card shows the new deadline, and the status change moves it to the other column.)*
  - [x] Timekeeping; — `8dc3841` *(all three Timekeeping projections the panels draw from — Countdowns, the deadline Calendar and the Timeline/Gantt — report the new deadline for the same record.)*
  - [x] task modal; — `8dc3841` *(the Task editor's fields are the reloaded record's, including the deadline it answers with.)*
  - [x] project metrics. — `8dc3841` *(the Hub's next-deadline metric follows the earliest deadline across records: moving the earliest task past the other one makes the card report the other, so the metric is derived from state rather than copied from a task.)*

- [ ] Deadline changed in Gantt updates: *(Same split as the group above: the Gantt drag is refused, so the Gantt
  cannot originate a deadline change — Stage 14's write half owns that. A deadline change arriving from the source
  propagates to every surface here, `8dc3841` @ `2026-09-12T02:22:54+07:00`.)*
  - [x] Countdowns; — `8dc3841` *(the countdown entry for the record carries the new deadline.)*
  - [x] deadline Calendar; — `8dc3841` *(the calendar projection's entry carries the new deadline.)*
  - [x] task modal; — `8dc3841` *(the editor shows the new value.)*
  - [x] project Hub next-deadline metric. — `8dc3841` *(read above.)*

- [ ] Event changed in Week updates: *(The Week origin is a Schedule write and is refused, so Stage 12 owns it; the
  propagation is proven at `8dc3841` @ `2026-09-12T02:22:54+07:00` for a change made at the source.)*
  - [x] Day; — `8dc3841` *(the card names the new instant and the new name, and the old instant appears nowhere in the view.)*
  - [x] 4-Day; — `8dc3841` *(as Day.)*
  - [x] Month; — `8dc3841` *(the occurrence button draws the new name; the old one is gone.)*
  - [x] Year; — `215777a` @ `2026-09-12T02:11:10+07:00` *(Year draws a per-date occurrence count and no per-event element, so it is asserted through those counts by the six-view convergence case rather than through the event's own values.)*
  - [x] Agenda. — `8dc3841` *(the date group and the row carry the new name and start.)*

- [ ] Project archive updates navigator/Hub/workspace everywhere. *(Half of it is demonstrable and half is not
  built to be tested: the Hub and the workspace read the project record on every render, so a status change
  arriving from the source moves the project between the Active and Archived filters and changes the workspace
  eyebrow. The **navigator** list is rendered inline by `src/browser/main.ts`, which has no exported surface for a
  test to mount, so this box stays open until that rendering is extracted or covered — and the archive *action*
  itself is a record mutation, which Stage 11 owns under HARD GATE C.)*
- [ ] Relation/schema changes reproject Backlog without restart. *(The Backlog already draws a column per declared
  property on every render, so reprojection is structural — but the schema it reads is canonical record data: the
  legacy reader returns `taskSchema: []` and property definitions arrive with the record store (HARD GATE A5,
  accepted, plus the cutover). Closes when a schema record can change at runtime.)*
- [ ] Agent write appears on human cockpit without a manual Refresh click. *(There is no agent write path: the
  loopback bridge is a read-only vault reader that serves list/read/walk and refuses writes. The source-refresh
  mechanism this would build on exists and is what `8dc3841` exercises from the human side.)*
- [ ] Human cockpit write becomes visible to agent inspection without manual refresh. *(The human side cannot write
  a record yet either, so there is nothing for inspection to notice; the inspection projection and its revision
  reporting exist and are asserted.)*
- [x] Multiple independent Proxima surfaces converge to the same record revision. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(the record's revision changes in the loader's map while the other records' revisions do not, and every surface listed above renders from that one reloaded state; in the record-store age the record revision takes the source revision's place and the convergence contract does not change.)*
- [x] Each surface may keep independent local view state. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(a Backlog query and a selection survive the data changing underneath them: the same view state renders the renamed task under the new query and still reports the marked-but-hidden row, so view state and record state are independent in both directions.)*

Current action dispatch already has state revisions and source-replacement semantics; preserve that concept while moving canonical state to the record store.

## Acceptance

- [ ] Agent modifies task while Board and Backlog are open; both converge. *(The Board-and-Backlog half is
  proven — `8dc3841` changes a task at the source and asserts both surfaces move together — and the "agent
  modifies" half waits on an agent write path, which does not exist: the bridge is read-only. Closes with the
  first agent-capable mutation (Stage 17's agent parity, under HARD GATE C).)*
- [ ] UI and agent race one record; stale loser explicit. *(The contract this needs is already built and
  conformance-tested at the store level: observed revision in, `stale-revision` out, no silent merge (Gate 13,
  `052c3b4`, `10dc3c3`, `eb0f3fe`). One of the two writers now exists — the UI writes records as of Stage 9
  (`abf8204`, `18c2e48`), and both of its paths are asserted to lose a race explicitly, reporting the revision
  that beat them — so the box is down to its other half: no agent can write a record yet, because the dispatcher
  refuses every record mutation and the loopback bridge is read-only. It closes with the agent-facing caller,
  which Stage 17's agent parity and HARD GATE C's remaining activation item own.)*
- [x] Separate records update independently. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(one task's file changes and its revision, its surfaces and its deadline move; the other task's and the event's revisions are unchanged, and every view of them still shows what it showed.)*
- [x] Local surface selections do not bleed into canonical storage. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(after a marked selection, a reader query and a reload, every file in the vault is byte-for-byte what it was — the peer's edit and nothing else. A selection is how this reader is looking at the table.)*
- [x] No manual source-refresh control is required for normal record-store coherence. — `abf8204` @ `2026-09-12T03:20:05+07:00` and `18c2e48` @ `2026-09-12T03:37:24+07:00` *(a write converges the cockpit by itself: both the drop and the editor's Save re-read the source as part of the write sequence, and nothing in the UI has to be clicked for the surfaces to agree with the store. What the header's Refresh source button remains is an option, not the mechanism — and changes made elsewhere arrive without it too, through the session's refresh policy (`createRefreshPolicy` in `src/app/refreshPolicy.ts`), which triggers an `interval` refresh while the page is visible at `intervalMs: 60_000` from `main.ts`'s boot. The box's own condition — "becomes true with the first mutation that reprojects every surface by itself" — is what Stage 9 delivered.)*

## Evidence

- Multi-surface integration tests. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(`tests/surfaceConvergence.test.ts` edits a vault behind an open cockpit, reloads it the way the application does, and asks eight surfaces what they show: the project Task Board, the Backlog, the project Deadlines list, the Elastic cockpit's column, the Task editor, the Countdowns, the deadline Calendar and the Timeline/Gantt — plus the six Schedule views and the event editor for an event change.)*
- UI+agent concurrent-operation tests. *(Not available: there is no agent write path and no UI write path, so no two writers can race. The store-level concurrency conformance suite stands in for the contract and is cited on the acceptance box above; this bullet closes with the first writer pair.)*
- Revision convergence report. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(the report is the per-surface table the test asserts: every named surface reports the changed value, the changed record's revision moves in the loader's map, and the untouched records' revisions do not.)*
- Local-state isolation report. — `8dc3841` @ `2026-09-12T02:22:54+07:00` *(the third case: a query and a selection survive the data changing under them, a marked-but-hidden row is reported rather than covered, and the vault holds exactly the peer's edit.)*

---

# Stage 20 — Remove transitional read-only scaffolding from the product surface

Only after parity writes are genuinely working.

At `608bcdc`, the visible page still contains fixture/FSA acceptance controls, build evidence panels and a `"Read-only workspace"` identity. These are useful engineering surfaces but are not the final old-Proxima cockpit.

## Work

- [ ] Ordinary user surface no longer leads with acceptance-probe chrome.
- [ ] Engineering diagnostics remain programmatically available.
- [ ] FSA disposable-probe controls are not confused with ordinary record ownership.
- [x] "Read-only workspace" disappears from normal record-backed operation. — `9a04451` @ `2026-09-12T03:40:29+07:00` *(the string is now a derived value rather than a literal, and it disappears exactly when a record write path resolved — which is what "normal record-backed operation" means: an activated store. A record-backed run that cannot write still says read-only, deliberately, because that is true of it. The rest of this stage's transitional chrome — the fixture/FSA acceptance controls, the build-evidence panels — is untouched by this box and remains named by the three boxes above it.)*
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
