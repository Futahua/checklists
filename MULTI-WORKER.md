# Multi-Worker Execution Workflow

This is the coordination contract for running multiple EXECUTOR workflows against one Long
Horizon plan. It reduces elapsed time through safe parallelism; it does not split the product
into competing roadmaps or weaken AUTHOR review and creator acceptance.

## 1. Core model

There is one Long Horizon interpretation and one accepted frontier. The AUTHOR assigns bounded
packets to temporary EXECUTOR slots, reviews their evidence, advances the frontier explicitly,
and assigns the next dependency-safe packet as a slot becomes available.

```text
LONG HORIZON -> AUTHOR -> EXECUTOR A / EXECUTOR B / EXECUTOR C
                         \________ AUTHOR REVIEW ________/
                                      |
                              ACCEPTED FRONTIER
```

Workers are not permanent subsystem owners and do not become separate teams.

## 2. Authority

The AUTHOR owns requirement interpretation, dependency analysis, slice selection, acceptance
conditions, technical review, correction decisions, coordination, and frontier advancement. It
must not claim to have run commands performed only by an EXECUTOR.

An EXECUTOR owns only its assigned packet. It may inspect the stated baseline, edit permitted
files, run the stated checks, report evidence, apply AUTHOR corrections, and commit/push when
permitted. It must not change scope, redesign, consume another packet, merge worker branches,
or rewrite shared history.

The creator retains final product acceptance and any authority reserved by the existing workflow.

## 3. One accepted frontier

Every packet states its repository, branch, and exact baseline SHA. Workers never infer a
baseline from another worker's branch. When the frontier advances, the AUTHOR decides whether
older packets continue, are rebased/restarted, or are finished and explicitly transplanted.

## 4. Scheduling and parallelism

Workers are a pool of execution slots, not fixed portions of Long Horizon. Concurrent packets
are allowed only when correctness is independent of unresolved work in another packet. The
dependency graph controls scheduling, not checklist numbering. Dependent UI, storage, activation,
or contract work waits for the accepted prerequisite; genuinely independent work elsewhere may
run concurrently.

## 5. Assignment packet

Each packet is self-contained and includes:

```text
WORKER
BASELINE (repository, branch, SHA)
TARGET (exact checklist row/gate/slice)
PURPOSE
IN SCOPE
OUT OF SCOPE
CONTRACT
ACCEPTANCE (commands, evidence, invariants)
DEPENDENCIES
CONCURRENCY (known independent packets)
STOP CONDITIONS
```

Packets are bounded enough to review as one technical decision.

## 6. Worker states

Each worker is exactly one of: `IDLE`, `ASSIGNED`, `IMPLEMENTING`, `AWAITING_AUTHOR_REVIEW`,
`CORRECTION_REQUIRED`, `TECHNICALLY_CLOSED`, `COMMITTED`, `PUSHED`, `VERIFIED`, `BLOCKED`, or
`CANCELLED`.

Normal flow is `IDLE -> ASSIGNED -> IMPLEMENTING -> AWAITING_AUTHOR_REVIEW -> TECHNICALLY_CLOSED
-> COMMITTED -> PUSHED -> VERIFIED -> IDLE`. A failed review follows
`AWAITING_AUTHOR_REVIEW -> CORRECTION_REQUIRED -> IMPLEMENTING`.

## 7. Review and completion

When any worker finishes, the AUTHOR reviews it immediately, sends a correction or technical
closure, verifies the exact resulting SHA, advances the frontier only if the required review and
creator-acceptance path is complete, and gives that slot the next ready packet. The AUTHOR does
not wait for unrelated workers to finish as a batch.

Before advancing a frontier, verify baseline, exact diff, acceptance evidence, scope, compatibility,
pushed SHA, and any required creator acceptance. A latest commit is not automatically accepted.

## 8. Concurrent baselines and overlap

A worker remains attached to its packet baseline until the AUTHOR changes it. File overlap is a
warning, not proof of dependency; semantic independence is the deciding criterion. If results
overlap materially, the AUTHOR chooses integration order. Workers never merge each other's branches.

Corrections return to the worker that produced the finding unless the AUTHOR deliberately reassigns
them. A correction packet states the same reviewed baseline, exact finding, minimal required change,
must-not-change behavior, and acceptance proof.

## 9. Priority and critical paths

Review completed workers first, then corrections, then critical-path packets, then ready independent
work, then speculative analysis. Sequential chains such as contract -> storage -> mutation ->
recovery -> activation must remain sequential. Spare workers stay idle or take independent work;
parallelism must not fabricate dependencies or integration debt.

## 10. Cross-repository and branch isolation

Every packet names its repository. Accepted frontiers are tracked independently per repository,
while the Long Horizon dependency graph remains singular. A host capability is unavailable to
another repository until its required technical and creator acceptance path closes.

Each active worker normally uses its own branch and worktree. Workers never share a writable
worktree or treat an in-progress branch as authority. Branches are disposable containers; the
accepted SHA is authoritative.

## 11. Reporting format

Completion reports contain:

```text
BASELINE (exact SHA)
RESULT
FILES
SEMANTICS
TESTS (exact commands and exit status)
DEVIATIONS
UNRESOLVED
WORKTREE (clean/dirty)
COMMIT (none or exact SHA)
```

The AUTHOR reviews evidence rather than relying on a “done” claim.

## 12. No speculative authority

No worker gains authority because another worker is busy. Workers must not invent architecture,
reinterpret an ambiguous row, merge results, declare creator acceptance, modify a shared baseline,
or begin dependent work against an unaccepted implementation. Material uncertainty is reported.

## 13. Invariants and success condition

The AUTHOR preserves one interpretation, one accepted frontier per repository, explicit baselines,
bounded packets, resolved dependencies, prompt review, explicit integration, distinct technical
closure/creator acceptance, and unchanged product semantics. The workflow succeeds only when extra
workers deliver accepted capability sooner without divergence, duplication, weakened acceptance,
hidden integration debt, or authority expansion.

