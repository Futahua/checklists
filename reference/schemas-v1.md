# Schemas

Required fields. A missing field makes the artifact malformed — that is the enforcement, and
it is why none of this is repeated as prose in the constitution.

Validators: `packet-validate`, `deviation-record`, `gate-record`, `handoff-build`.

## AUTHOR packet

```
packet_version
role = AUTHOR
repo
base_sha
branch
read_set[]                 files actually read at base_sha
intent
invariants[]
non_goals[]
artifact[]
allowed_changed_files[]
verification[]
acceptance_criteria[]
authority_required[]       destructive or authority-bearing operations, named
stop_conditions[]
```

Each entry in `artifact[]` declares its form:

```
new_file             { path, contents }
replace_file         { path, contents }
guarded_replacement  { path, preimage, replacement, occurrences = 1 }
delete_file          { path }
```

`guarded_replacement` is the default for modifying an existing file. A unified diff is an
optional form only where the channel is known to preserve it byte-for-byte; it is not the
default, because rendered transport mangles hunk metadata.

An artifact without placement semantics fails validation. No prose rule is needed telling
the AUTHOR not to make the executor work out where a fragment goes.

## Execution evidence

```
packet_id
baseline_sha
baseline_clean
artifact_application       per artifact: applied | refused, with reason
commands[]
changed_files[]
unexpected_files[]
logs[]                     path, lines, bytes, hash
deviations[]
status                     EXECUTED | EVIDENCE_READY | FAILED
```

Each entry in `commands[]`:

```
authored_command
actual_command
authored_command_executed  true | false
exit_code
log_path
```

`authored_command_executed` is the field that makes a substituted verification command
impossible to mistake for completion. It is false until the authored command itself has run.

## Deviation record

```
authored_operation         the exact instruction that could not be executed
trigger                    the objective failure: exit code, error text, mismatch
deviation                  exactly what mechanism changed
equivalence_basis          the mechanical fact showing semantics and evidence survived
equivalence_status         PROVEN | UNPROVEN
scope                      files and commands the deviation touched
postcondition              what was actually produced or run
non_deviations             authored portions deliberately left alone
evidence                   bounded diffstat, hash, or command output
```

There is no `ASSUMED`. An `UNPROVEN` deviation is not invalid — it is something the gate
must see as unresolved.

A good `equivalence_basis` is a fact: *`git rev-parse da7881f` resolved uniquely to
`da7881f712…`, and HEAD was that object.* A bad one is judgement in a fact's clothing: *the
rest looked unchanged.*

Deviations appear in the evidence packet **even when execution succeeded**.

## Gate record

```
slice
commit_or_tree
claims[]
evidence_packet
deviations[]
unproven_deviations[]
creator_decision           ACCEPTED | REJECTED
decision_timestamp
```

A gate cannot be recorded as accepted without `creator_decision`.

## Handoff

```
goal
repo
branch
sha
accepted_state
open_work
governing_invariants
evidence_locations
open_questions
next_operation
```

No transcripts. Point at reports on disk; never embed them.

## Checklist stage

```
purpose
work
acceptance
evidence
hard_dependencies
violation_consequence      what breaks if the order is ignored
open_questions
```

`violation_consequence` is what makes a hard gate a gate rather than a preference.
