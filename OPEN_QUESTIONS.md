# UbU Open Questions

Status: Draft  
Purpose: Public list of unresolved design questions for the UbU project.

This file tracks issues that are not yet settled. Some are MVP blockers. Others are post-MVP or architectural questions that should be preserved without blocking implementation.

The goal is not to answer everything before development begins. The goal is to identify which questions must be resolved for Phase 1 MVP and which can safely become later design issues.

---


## Priority Legend

- **MVP blocker**: Must be resolved before or during Phase 1 implementation.
- **MVP important**: Should be resolved early, but does not necessarily block initial coding.
- **Post-MVP**: Important later, but should not delay Phase 1.
- **Research**: Needs experimentation, external feedback, or theoretical refinement.

---


## Question block schema

Each open question block uses the following format:

```text
## UBU-Q0001: Question title

Status: Open | Solved | Deferred | Superseded | Archived
Priority: MVP blocker | MVP important | Post-MVP | Research
Phase: Phase 1 | Phase 2 | Phase 3 | Post-MVP
Decision type: Scope | Data model | Process | Governance | Product | Security | Architecture
Auto-choice eligibility: Auto eligible | Human approval required | Human only
Importance score: TBD | 0-100
Automation-likelihood score: TBD | 0-100
Risk score: TBD | 0-100
Depends on: None | UBU-Qxxxx
Blocks: None | Phase 1 implementation | Phase 1 scope freeze | etc.
Resolved by: Unresolved | UBU-Dxxxx
Last scored: Never | YYYY-MM-DD
Scored from commit: None | commit SHA
```

---


## UBU-Q0001: Phase 1 MVP Scope Freeze

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Scope
Auto-choice eligibility: Human only
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

1. What is the exact Phase 1 MVP feature set?
2. What is explicitly deferred to Phase 2?
3. What is explicitly deferred to Phase 3?
4. Which abstractions should be documented but not implemented?
5. What rule prevents new abstractions from delaying Phase 1 indefinitely?
6. What is the minimum dogfooding loop that proves UbU’s core model?

### Candidate MVP rule

Phase 1 may include abstractions needed for future compatibility, but only implements the subset required for single-user GitHub dogfooding.

### Resolution

Unresolved.

---


## UBU-Q0002: GitHub Projection and Reconciliation

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0003
Blocks: Phase 1 GitHub dogfooding
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

1. Which GitHub fields does UbU write?
   - labels
   - issue body blocks
   - comments
   - milestones
   - assignees
   - PR statuses
2. Should UbU write only clearly marked `ubu:` labels and managed blocks?
3. Which GitHub edits are treated as external events?
4. Can any GitHub edit override UbU state?
5. How does UbU detect missed GitHub updates?
   - polling
   - webhooks
   - manual sync
   - worker-driven reconciliation
6. What does the reconciliation report compare?
   - GitHub Issues vs UbU Objectives
   - GitHub labels vs `pipeline_state`
   - GitHub comments vs event log
   - PRs / CI runs vs External Events
7. Does drift create a report only, or also Tasks to repair drift?
8. Does GitHub reconciliation run in the main UbU instance or an Automation Worker?

### Current direction

UbU should write only clearly marked UbU-managed labels, comments, or blocks, and treat other GitHub edits as External Events.

### Resolution

Unresolved.

---


## UBU-Q0003: GitHub ↔ UbU Association Model

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 GitHub dogfooding
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

GitHub objects and UbU objects have many-to-many relationships.

Examples:

- one GitHub Issue may map to many Objectives;
- one Objective may map to many GitHub Issues;
- PRs, comments, reviews, and CI runs may associate with Objectives or Tasks.

### Question

1. Should association be represented with generic `external_refs[]`?
2. Or should there be a dedicated `ExternalAssociation` object?
3. If using `ExternalAssociation`, what fields are required?
   - external system
   - external object type
   - external object ID
   - UbU object type
   - UbU object ID
   - relation type
   - confidence
   - created by
   - last verified time
   - sync policy
   - projection policy
4. Can associations target both Objectives and Tasks?
5. Can associations target External Events?
6. How are duplicate associations detected?
7. Can an Automation Worker create or modify associations?

### Current leaning

A dedicated `ExternalAssociation` object is likely cleaner than embedding all external refs directly on core objects.

### Resolution

Unresolved.

---


## UBU-Q0004: Pipeline State

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0003
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

`Objective.status` is the canonical UbU lifecycle status. `pipeline_state` is workflow/project-management state.

### Question

1. Is `pipeline_state` generic or GitHub-specific?
2. Can one Objective have multiple pipeline states for multiple projections?
3. Is `pipeline_state` stored on Objective directly or in projection metadata?
4. What is the MVP pipeline enum?
5. Can Automation Workers mutate `pipeline_state`?
6. Does every pipeline state transition create an event/log entry?

### Candidate MVP enum

```text
unlabeled
invalid
under_specified
valid_unprioritized
unassigned
in_process_awaiting_pr
awaiting_review
awaiting_ci
complete
```

### Resolution

Unresolved.

---


## UBU-Q0005: GitHub Event Triage Rules

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0002
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

GitHub events must be interpreted into UbU events, Tasks, Objectives, or recalculation triggers.

### Question

1. Which GitHub events are logged only?
2. Which GitHub events create External Events?
3. Which GitHub events create Objectives?
4. Which GitHub events create Tasks?
5. Which GitHub events trigger recalculation?
6. Which GitHub events trigger Automation Worker assignment?
7. Which GitHub events trigger GitHub projection updates?
8. How are duplicate GitHub events detected?
9. How are missed events reconstructed during reconciliation?

### Candidate MVP event classes

```text
issue_opened
issue_commented
issue_labeled
issue_closed
pr_opened
pr_updated
review_requested
review_submitted
ci_failed
ci_passed
milestone_changed
```

### Resolution

Unresolved.

---


## UBU-Q0006: Objective and Task Explosion Control

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0005
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

GitHub events may create analysis Objectives or Tasks. This could generate excessive noise.

### Question

1. When does a GitHub event deserve a new Objective?
2. When is it appended to an existing Objective?
3. When is it merely logged?
4. When does it create a Task?
5. How are duplicate analysis Objectives detected?
6. Do analysis Objectives inherit value from parent Objectives?
7. Do analysis Objectives automatically become moot or completed after resolution?
8. How does UbU prevent its own management process from becoming too noisy?

### Resolution

Unresolved.

---


## UBU-Q0007: Automation Worker Identity and Capabilities

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Security
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

A worker-mode UbU instance is externally represented as an Identity. Workers need bounded authority.

### Question

1. What capabilities can a worker Identity receive?

   * read Task
   * read Objective
   * read UniverseState subset
   * create Task
   * create Objective
   * mutate Task
   * mutate Objective
   * mutate `pipeline_state`
   * append External Event
   * submit Snapshot
   * request recalculation
   * update GitHub projection
2. Are capabilities scoped by:

   * object ID
   * Objective subtree
   * Task set
   * Compartment
   * external integration
   * time window
3. Can a worker be revoked?
4. Can a worker operate across multiple organization-mode instances?
5. Can a worker operate for user-mode instances?
6. How are worker credentials rotated?
7. Does worker capability state live on Identity, a capability object, or both?

### Current direction

Automation Worker = worker-mode UbU instance externally represented as an Identity.

### Resolution

Unresolved.

---


## UBU-Q0008: Worker Assignment Model

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0007
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Workers need a way to discover or receive work.

### Question

1. Does an organization-mode instance explicitly assign Tasks to workers?
2. Or do workers poll for Tasks matching their capabilities?
3. Can multiple workers observe the same Task?
4. Can multiple workers compete for the same Task?
5. What happens if a worker disappears mid-Task?
6. Is assignment itself logged?
7. Can workers reject assignments?
8. Can workers request clarification Tasks?
9. Can workers spawn child Tasks?

### Current MVP leaning

Explicit assignment is likely simplest.

### Resolution

Unresolved.

---


## UBU-Q0009: Worker Mutation Request Schema

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0007
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Automation Workers need a bounded way to submit changes back to canonical UbU state.

### Question

1. Does a worker submit:

   * event records,
   * mutation requests,
   * proposed patches,
   * or all three?
2. What fields are required?

   * worker Identity
   * authority source
   * target object
   * operation
   * expected prior version
   * new value
   * reason
   * evidence reference
   * timestamp
   * idempotency key
3. Are valid mutations applied immediately?
4. Are invalid mutation attempts logged?
5. Can mutation requests be batched atomically?
6. Can workers request creation of new Objectives or Tasks?
7. Are worker mutations reversible?
8. How does UbU prevent stale worker mutations from overwriting newer canonical state?

### Resolution

Unresolved.

---


## UBU-Q0010: GitHub Token Custody

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Security
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0007
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Automation Workers may interact with GitHub using access tokens.

### Question

1. Are GitHub tokens stored:

   * on the central UbU instance,
   * only on worker-mode instances,
   * or both?
2. Are tokens tied to:

   * bot accounts,
   * maintainer accounts,
   * individual contributor accounts?
3. Can tokens be scoped per repository?
4. Can tokens be scoped per Task?
5. Does the central UbU instance ever see the token?
6. Does UbU verify GitHub writes by re-reading GitHub?
7. What is the MVP security assumption?

### Current leaning

For MVP, workers may own their GitHub tokens. The canonical UbU instance stores external refs/results, not necessarily the token.

### Resolution

Unresolved.

---


## UBU-Q0011: Inter-Instance Protocol

Status: Open
Priority: Post-MVP
Phase: Phase 3
Decision type: Architecture
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 3 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Automation Worker communication may overlap with future user-to-user or instance-to-instance communication.

### Question

1. Is there one generic UbU inter-instance protocol?
2. Or is worker communication a separate MVP API?
3. Should the protocol support:

   * messages
   * assignments
   * status updates
   * mutation requests
   * capability grants
   * External Event submission
   * recalculation requests
4. Can this protocol later support Phase 3 multi-user Identity coordination?
5. Does the MVP worker API intentionally approximate the future inter-instance protocol?

### Resolution

Unresolved.

---


## UBU-Q0012: Organization Mode Object Rules

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Organization mode does not model intrinsic affect but otherwise shares much of the same data model.

### Question

1. Are all core objects available in organization mode?

   * Objective
   * Preference
   * Task
   * Container
   * UniverseState
   * Plan
   * Calendar
   * Identity
   * Relationship
   * Compartment
2. Are affect fields omitted, disabled, or merely unused?
3. Can Relationship objects exist without affect dimensions?
4. Can organization-mode instances receive limited signals from personal user-mode instances later?
5. Is `authority_source` required on organization-created Preferences, Objectives, and Tasks?
6. How are organization users represented before RBAC exists?

### Current direction

All users in organization mode may be treated as admin-equivalent in MVP.

### Resolution

Unresolved.

---


## UBU-Q0013: Authority Source Vocabulary

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0012
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Organizational directives and worker updates need authority/source metadata.

### Question

1. Which objects carry `authority_source`?

   * Preference
   * Objective
   * Task
   * pipeline state
   * worker assignment
   * external projection
   * mutation request
2. Is `authority_source` required only in organization mode?
3. What are MVP authority-source values?

### Candidate values

```text
human_admin
automation_worker
github_event
project_policy
imported_config
llm_advisory
user_override
```

### Resolution

Unresolved.

---


## UBU-Q0014: UniverseState Mutation Schema

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

UniverseState mutation vocabulary is accepted, but the concrete schema remains open.

### Accepted MVP mutation operations

```text
set_fact
clear_fact
increment_numeric
decrement_numeric
add_membership
remove_membership
append_event_marker
```

### Question

1. What target key format should MVP use?

   * dotted string
   * JSON pointer
   * tuple path
2. What fields exist on each mutation item?

   * target
   * operation
   * payload
   * note
   * source
3. What payload types are allowed?

   * string
   * number
   * boolean
   * JSON object
   * set member
   * event marker
4. Are mutation items always unconditional once Task effect succeeds?
5. Can mutation items target affect fields?
6. Can mutation items target Relationship payloads?
7. Should mutation items contain confidence?
8. Should mutation items contain provenance in MVP?

### Current leaning

Use dotted string targets and JSON-compatible payloads.

### Resolution

Unresolved.

---


## UBU-Q0015: Task Precondition Schema

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Preconditions are deterministic constraints over UniverseState.

### Accepted MVP precondition types

* equality
* membership
* absence
* simple AND/OR logic

Numeric comparisons are not in MVP.

### Question

1. Should preconditions use:

   * `all_of[]` / `any_of[]`,
   * or flat list with connectors?
2. What are the predicate fields?

   * target
   * predicate type
   * expected value
3. Can preconditions reference event markers?
4. Does failed precondition mean:

   * blocked
   * unschedulable
   * invalid
5. Can preconditions reference affect fields?
6. Can preconditions reference Relationship payloads?

### Current leaning

Failed precondition should mean blocked, not invalid.

### Resolution

Unresolved.

---


## UBU-Q0016: Compact Calendar DFS Grammar

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Architecture
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Compact Calendar support is important for recursive self-analysis and future sync/transport. The current direction is deterministic DFS rather than PRNG seed sampling.

### Question

1. What is a DFS node?

   * partial ordered Task sequence
   * partial timed Plan
   * partial UniverseState trajectory
   * probability-mass state
   * some combination of the above
2. What does expansion add?

   * next Task
   * duration branch
   * success/failure branch
   * external event branch
   * Objective recurrence branch
3. What does threshold `p` mean?

   * branch pruning threshold
   * cumulative coverage target
   * minimum child probability
   * or multiple parameters
4. Is DFS sorted by:

   * probability
   * Objective value
   * deadline urgency
   * critical path
   * composite heuristic
5. Does Compact Calendar encode:

   * ordering constraints
   * duration PDFs
   * success probabilities
   * external-event distributions
   * affect constraints
6. Are concrete Plans stored at all?
7. Or are Plans always reconstructed on demand?
8. How is coverage recalculated after time advances?
9. What is the minimum MVP implementation?

### Resolution

Unresolved.

---


## UBU-Q0017: Compact Calendar Coverage and Regeneration

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0016
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Coverage belongs to compact Calendar serialization.

### Question

1. Is coverage exact or estimated in MVP?
2. Does coverage include:

   * duration uncertainty
   * Task success/failure uncertainty
   * external-event uncertainty
   * Objective recurrence uncertainty
3. Does a compact Calendar store coverage value only, or also uncovered mass?
4. What is the default regeneration threshold?
5. Is the threshold global, device-specific, Calendar-specific, or all three?
6. Does low coverage create:

   * report only,
   * recalculation trigger,
   * Task,
   * worker assignment?

### Current direction

Default threshold may be `0.5`, but this is not final.

### Resolution

Unresolved.

---


## UBU-Q0018: Risk Reporting Primitives

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Risk is not a first-class object in MVP. Risk is reportable from Calendar/Plan analysis.

### Question

1. Which reports are MVP?

   * P90 completion time
   * critical path
   * deadline miss probability
   * affect constraint violation probability
   * low coverage warning
   * dependency fragility
   * worker failure / automation bottleneck
2. Are risk reports computed:

   * on demand,
   * cached,
   * generated by Automation Workers,
   * stored as artifacts?
3. Are risk reports part of release ceremonies?
4. Which risk reports demonstrate that UbU supersedes PERT?
5. Can risk reports create Tasks?

### Resolution

Unresolved.

---


## UBU-Q0019: Recalculation Trigger Taxonomy

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Architecture
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

The decision layer is a pure function over Plans + current state, so recalculation triggers must be explicit.

### Candidate MVP triggers

```text
task_completed
task_failed
task_moot
observed_snapshot
affect_confidence_decay
external_event
github_update
user_override
elapsed_time
low_compact_calendar_coverage
worker_request
```

### Question

1. Which triggers are Phase 1?
2. Which triggers are Phase 2?
3. Which triggers are post-MVP?
4. Are triggers logged as events?
5. Can Automation Workers create triggers?
6. Can triggers be batched?
7. Which triggers force immediate recalculation?
8. Which triggers merely mark the Calendar stale?

### Resolution

Unresolved.

---


## UBU-Q0020: Automation Worker Retry Semantics

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0008
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Automation Workers may fail or produce failed child Tasks.

### Question

1. If a worker-created child Task fails, does UbU:

   * mutate the same Task,
   * create retry sibling,
   * mark failed then create replacement,
   * mark moot?
2. Is retry policy defined by:

   * Task
   * Objective
   * Worker
   * integration type
3. How are retry attempts logged?
4. How are repeated failures prevented from creating infinite loops?
5. Does a worker failure affect risk reports?

### Current leaning

Failed attempt + retry sibling is likely best for auditability.

### Resolution

Unresolved.

---


## UBU-Q0021: Automation Worker Parent / Child Structure

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0008
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Automation Workers may create canonical child Tasks.

### Question

1. Is the outer Automation/Super Automation Task also the Container?
2. Or is a separate Container created under it?
3. Are child Tasks ordinary Dynamic Tasks?
4. Or are child Tasks a dedicated automation-step subtype?
5. If child Tasks are ordinary Dynamic Tasks, how is automation-specific metadata stored?
6. How are retries connected to the original child Task?

### Resolution

Unresolved.

---


## UBU-Q0022: Moot Reason-Code Taxonomy

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

`moot` is a terminal Task status and requires a reason code.

### Candidate MVP reason codes

```text
externally_satisfied
superseded
delegated
no_longer_relevant
invalidated_by_world_change
replaced_by_new_plan_structure
user_declared_moot
automation_obsolete
duplicate
```

### Question

1. Is this list sufficient for MVP?
2. Should `duplicate` be included?
3. Should `delegated` be separate from `externally_satisfied`?
4. Are reason codes free-form extensible or enum-only in MVP?

### Resolution

Unresolved.

---


## UBU-Q0023: Container Mutation Semantics

Status: Open
Priority: MVP important
Phase: Phase 2
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 2 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Tasks may mutate into Containers, especially during preemption or decomposition.

### Question

1. When a Task mutates into a Container, does the original Task handle become the Container handle?
2. Do all child Tasks always get new handles?
3. Which fields stay on the Container?
4. Which fields copy to child Tasks?
5. How are external IDs preserved?
6. How does this interact with GitHub-linked Tasks?
7. How does this interact with Automation Worker child Tasks?

### Resolution

Unresolved.

---


## UBU-Q0024: Objective Status Transition Table

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Objective statuses are accepted, but the precise transition table remains open.

### Accepted Objective statuses

```text
active
satisfied
completed
abandoned
invalid
superseded
```

### Question

1. What are legal transitions for one-time Objectives?
2. What are legal transitions for evergreen Objectives?
3. Can `invalid` occur from any state?
4. Can `superseded` occur from any state?
5. Can `abandoned` occur from any state?
6. Can evergreen Objectives transition `satisfied → active` only by observation, or also by simulation?
7. Does transition always create a log event?

### Resolution

Unresolved.

---


## UBU-Q0025: Snapshot Application Semantics

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Snapshots override simulated state when conflicting, but application details remain open.

### Question

1. Are snapshots patches or full assertions?
2. Are snapshots immutable once logged?
3. Is confidence stored:

   * per snapshot,
   * per field,
   * or both?
4. If two user snapshots conflict, does latest always win?
5. Can a Snapshot be revoked or corrected?
6. Does correction create a new Snapshot?

### Resolution

Unresolved.

---


## UBU-Q0026: Relationship Maintenance Modeling

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Relationship is modeled as structured UniverseState payload between two Identities.

### Question

1. Where does communication cadence live?

   * Objective recurrence
   * Task history
   * external storage
   * Relationship payload
2. Where does neglect risk live?

   * risk report
   * Objective recurrence
   * Relationship payload
3. How does UbU model “maintain relationship with contributor X”?
4. Can GitHub contributor interactions update relationship state?
5. Is relationship maintenance in MVP, or only documented for future use?

### Resolution

Unresolved.

---


## UBU-Q0027: Organization Mode and Worker Mode Public UX

Status: Open
Priority: Post-MVP
Phase: Post-MVP
Decision type: Product
Auto-choice eligibility: Human only
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Post-MVP product
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

Organization mode and worker mode may use web admin UIs.

### Question

1. What does the organization-mode UI show first?
2. What does the worker-mode UI show first?
3. Does worker mode expose logs, assignment queue, capability grants, GPU/cloud status?
4. Does organization mode expose pipeline state, risk reports, worker assignments, GitHub projection status?
5. Which UI is required for Phase 1?

### Resolution

Unresolved.

---


## UBU-Q0028: Minimum Privacy / Compartment Promise for MVP

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Security
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

UbU is privacy-first, but MVP implementation must avoid overclaiming.

### Question

1. Are Compartments implemented in Phase 1?
2. If yes, what hard invariants exist?

   * no cloud LLM routing
   * export blocking
   * retention
   * audit logging
   * device eligibility
3. If not fully implemented, how is this disclosed?
4. How is un-compartmented content labeled low-security?
5. What can UbU honestly claim about local-first operation in Phase 1?
6. What can UbU honestly claim about cloud LLM usage in Phase 1?

### Resolution

Unresolved.

---


## UBU-Q0029: Open-Core / FOSS Contribution Boundary

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Governance
Auto-choice eligibility: Human only
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

UbU is intended to recruit FOSS contributors.

### Question

1. Which components are definitely open source?

   * data model
   * planner
   * GitHub projection
   * worker mode
   * compact Calendar serialization
   * local-first sync
   * Super Automation API
2. Which components may remain experimental or private?
3. How does UbU avoid giving contributors the impression that the open core is bait?
4. What licensing strategy should implementation repos use?
5. What is the commercial/premium boundary, if any?

### Resolution

Unresolved.

---


## UBU-Q0030: Phase 1 Public Demo Criteria

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Product
Auto-choice eligibility: Human only
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 release
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

The MVP should demonstrate that UbU is real and worth contributing to.

### Question

1. What demo proves Phase 1 works?
2. Does the demo use real GitHub issues from UbU?
3. Does it generate a Calendar?
4. Does it show a Plan?
5. Does it update GitHub projection labels/comments?
6. Does it show risk reports?
7. Does it show affect constraints?
8. Does it show worker assignment?
9. What is the smallest demo that is still persuasive?

### Resolution

Unresolved.

---


## UBU-Q0031: Log Structure and Fields

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Data model
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Phase 1 implementation
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

A Log is the canonical record of what actually happened. Its structure and fields need specification.

### Question

1. What are MVP required Log entry fields?
   - timestamp
   - event type
   - actor/Identity
   - target object
   - old value / new value
   - result (success/failure)
   - notes / reason
2. How are different event types represented?
   - Task completion
   - Task failure
   - External Event
   - Snapshot observation
   - Objective transition
   - Plan realization
   - Recalculation trigger
3. Are Log entries immutable once written?
4. Can Log entries be annotated or corrected?
5. Does correction create a new entry or modify the original?
6. What is the retention/archive policy for Logs?
7. Are Logs stored per instance or per device?
8. How does Log query/search work for large histories?
9. Should Logs include confidence/provenance metadata?
10. How do Automation Workers contribute to Logs?

### Resolution

Unresolved.

---


## UBU-Q0032: Model Committee Process and Authority

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: None
Blocks: Model-committee v0.1 correctness
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

What authority should the model-committee process have when proposing answers, patches, consistency checks, readiness scores, and new open questions?

### Subquestions

1. Which actions may be automated?
2. Which actions require human review?
3. Which actions are forbidden in v0.1?
4. How are model outputs weighted?
5. How are failed provider calls logged?
6. What quorum is required for a valid committee result?

### Resolution

Unresolved.

---


## UBU-Q0033: Phase 1 MVP Readiness Scoring Rubric

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0001
Blocks: README readiness signal
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

How should UbU estimate how close the project is to Phase 1 scope freeze and MVP readiness?

### Resolution

Unresolved.

---


## UBU-Q0034: Design Automation Stop Rule

Status: Open
Priority: MVP blocker
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0001
Blocks: Phase 1 scope freeze
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

When should UbU stop answering additional pre-MVP design questions and begin coding the MVP?

### Subquestions

1. What categories of questions may block Phase 1?
2. What categories must be deferred even if unresolved?
3. What MVP readiness score is sufficient to begin implementation?
4. What maximum rate of new MVP-blocker creation is acceptable?
5. How should the value of answering another question be compared against coding?
6. Can the model committee recommend that no further pre-MVP design work is justified?

### Resolution

Unresolved.

---


## UBU-Q0035: Automation Coverage Taxonomy

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Auto eligible
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0032
Blocks: Question-ranking accuracy
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

How should remaining design work be classified by automation eligibility?

### Resolution

Unresolved.

---


## UBU-Q0036: Committee Log and Provenance Format

Status: Open
Priority: MVP important
Phase: Phase 1
Decision type: Process
Auto-choice eligibility: Auto eligible
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0032
Blocks: model-committee v0.1 logging
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

What minimum files and fields must a model-committee run log preserve?

### Resolution

Unresolved.

---


## UBU-Q0037: Post-MVP Question Lifecycle

Status: Open
Priority: Post-MVP
Phase: Post-MVP
Decision type: Process
Auto-choice eligibility: Human approval required
Importance score: TBD
Automation-likelihood score: TBD
Risk score: TBD
Depends on: UBU-Q0032
Blocks: None
Resolved by: Unresolved
Last scored: Never
Scored from commit: None

### Question

How should post-MVP design questions be preserved, re-ranked, reopened, or retired after the first MVP release?

### Resolution

Unresolved.

---


## Suggested Initial GitHub Issues

Create these first:

1. `UBU-Q0001`: Define Phase 1 MVP Scope Freeze
2. `UBU-Q0002`: Define GitHub Projection and Reconciliation Model
3. `UBU-Q0003`: Define GitHub ↔ UbU Association Model
4. `UBU-Q0007`: Define Automation Worker Identity and Capability Model
5. `UBU-Q0009`: Define Worker Mutation Request Schema
6. `UBU-Q0014` + `UBU-Q0015`: Define UniverseState Mutation and Precondition Schemas
7. `UBU-Q0016`: Define Compact Calendar DFS Grammar
8. `UBU-Q0018`: Define Risk Reporting Primitives
9. `UBU-Q0019`: Define Recalculation Trigger Taxonomy
10. `UBU-Q0030`: Define Phase 1 Public Demo Criteria

