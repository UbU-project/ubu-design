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

Each open question block uses the following format.

The metadata line may be stored as a single physical line. `model-committee` v0.1 must parse this single-line metadata format.

```text
## UBU-X0001: Question title

Status: Open | Solved | Deferred | Superseded | Archived | Decomposed Priority: MVP blocker | MVP important | Post-MVP | Research Phase: Phase 1 | Phase 2 | Phase 3 | Post-MVP Decision type: Scope | Data model | Process | Governance | Product | Security | Architecture Auto-choice eligibility: Auto eligible | Human approval required | Human only Importance score: TBD | 0-100 Automation-likelihood score: TBD | 0-100 Risk score: TBD | 0-100 Answerability score: TBD | 0-100 Depends on: None | UBU-Qxxxx Blocks: None | Phase 1 implementation | Phase 1 scope freeze | etc. Resolved by: Unresolved | UBU-Dxxxx Last scored: Never | YYYY-MM-DD Scored from commit: None | commit SHA
```

Optional metadata fields may appear after `Scored from commit:`:

```text
Supersedes: None | UBU-Qxxxx Superseded by: None | UBU-Qxxxx Decomposes: None | UBU-Qxxxx Decomposed into: None | UBU-Qxxxx, UBU-Qyyyy
```

Required metadata labels are exact and case-sensitive.

Allowed sentinel values include:

- `TBD`
- `Never`
- `None`
- `Unresolved`

---

## Question selection policy

`model-committee` uses answerability as the first gate.

A question is eligible for ordinary work only if:

- it has no dependencies;
- all dependencies are solved;
- or all dependencies are being answered in the same work item.

Blocked questions may still be selected for decomposition work if decomposition is expected to produce replacement questions with fewer, simpler, or no dependencies.

After answerability is established, questions are ranked by:

1. automation-likelihood score,
2. importance score,
3. risk score ascending.

---

## UBU-Q0001: Phase 1 MVP Scope Freeze

Status: Solved Priority: MVP blocker Phase: Phase 1 Decision type: Scope Auto-choice eligibility: Human only Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0097 Last scored: Never Scored from commit: None

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

Solved by `UBU-D0097`.

Phase 1 is frozen around the single-user GitHub dogfooding loop. The MVP implements only the subset of UbU needed for one local `user_mode` operator to bootstrap context, import or load UbU GitHub project data, generate an inspectable Plan, act on one recommended next Task, record feedback, recalculate, and preview or perform bounded GitHub projection.

The Phase 1 feature set includes:

- local single-user `user_mode` instance for UbU-runs-UbU;
- bootstrap interview, current or stale affect Snapshot handling, and initial Objective/Task seed creation;
- live or fixture-backed GitHub issue, PR, review, CI, milestone, and comment import;
- ExternalReference-style links from GitHub objects to UbU Objectives, Tasks, External Events, and Logs;
- MVP Objective, Preference, Task, Container, UniverseState, Snapshot, Plan, Calendar, Log, Identity, Relationship, Compartment, Automation Worker, External Event, and External Reference schemas only to the depth required for dogfooding;
- schedulable Static and Dynamic Tasks with Objective links, duration, dependency/precondition/effect fields, lifecycle status, and moot handling;
- lightweight UniverseState mutation, affect, and precondition evaluation;
- append-only per-instance Logs with provenance, corrections, annotations, worker submissions, and recalculation-trigger entries;
- Plan and Calendar generation for the next work window with a default Plan and inspectable explanation;
- next-action focus mode with start, done, snooze, reject, decompose, explain-more, and feedback controls;
- derived risk and human-complete plan-quality reports;
- minimal Compartment guardrails, low-security labeling, and logged boundary decisions;
- Automation Worker Identity, scoped capability grants, explicit assignment/status, and mutation or projection request submission;
- bounded GitHub projection previews or human-approved writes for clearly marked UbU-managed labels, comments, or blocks;
- manually structured Release Outreach Pipeline work items and artifact records.

Phase 2 defers:

- multi-device local-first sync;
- partial replication across Devices, Zones, or Compartments;
- secure cross-device Compartment propagation;
- sync conflict handling;
- cross-device worker or enclave coordination beyond the single local instance boundary.

Phase 3 defers:

- multi-human coordination;
- shared or partially shared truth between user instances;
- user-to-user Identity commitments, capabilities, and limited disclosure;
- multi-party governance, invitation, revocation, or trust protocols.

Documented but not implemented in Phase 1:

- Technique as a first-class planning object;
- full Compact Calendar planner grammar and high-coverage transport format;
- complete Zone and Device system beyond the current local execution enclave;
- organization-mode and worker-mode web admin consoles;
- richer relationship-management, personal CRM, and longitudinal affect/growth models;
- full Release Outreach Pipeline video generation, rendering, and publication workflow;
- broad email, text-message, file, invoice, note, or personal-data ingestion;
- adaptive model-committee weighting, automatic patch application, GitHub mutation, and direct cloud-provider APIs.

Stop rule:

> A new abstraction may be added to Phase 1 only when it is required to complete the single-user GitHub dogfooding loop, enforce an accepted hard invariant, or avoid a known irreversible schema contradiction. Otherwise it must be documented as a Phase 2, Phase 3, or post-MVP concern and must not block Phase 1 implementation.

Minimum dogfooding loop:

1. bootstrap the operator, project context, available work window, constraints, and current or stale affect Snapshot;
2. import or load a curated UbU GitHub fixture with issues, PR/review/CI signals, milestone context, and source links;
3. map those inputs into Objectives, Tasks, External Events, Logs, UniverseState facts, and External References;
4. generate a Calendar with a default Plan for the next work window;
5. present one recommended next Task with an explanation of Objective value, dependencies, deadlines, affect constraints, worker status, and risk findings;
6. record completion, failure, snooze, rejection, decomposition, or override as Log evidence and trigger recalculation when appropriate;
7. preview or perform a human-approved UbU-managed GitHub projection update;
8. show a reconciliation or risk summary that makes the changed model inspectable.

---

## UBU-Q0002: GitHub Projection and Reconciliation

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0003 Blocks: Phase 1 GitHub dogfooding Resolved by: Unresolved Last scored: Never Scored from commit: None

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

## UBU-Q0003: GitHub ↔ UbU External Reference Model

Status: Solved Priority: MVP blocker Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 GitHub dogfooding Resolved by: UBU-D0098 Last scored: Never Scored from commit: None

GitHub objects and UbU objects have many-to-many relationships.

Examples:

- one GitHub Issue may map to many Objectives;
- one Objective may map to many GitHub Issues;
- PRs, comments, reviews, and CI runs may link to Objectives or Tasks.

### Question

1. Should external links be represented with generic `external_refs[]`?
2. Or should there be a dedicated `ExternalReference` object?
3. If using `ExternalReference`, what fields are required?
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
4. Can External References target both Objectives and Tasks?
5. Can External References target External Events?
6. How are duplicate External References detected?
7. Can an Automation Worker create or modify External References?

### Current leaning

A dedicated `ExternalReference` object is likely cleaner than embedding all external refs directly on core objects.

### Resolution

Solved by `UBU-D0098`. GitHub-to-UbU links are represented by first-class `ExternalReference` objects. Generic `external_refs[]` may still be used as lightweight references on Logs, provenance, or import artifacts, but they are not the authoritative many-to-many external-link model.

MVP `ExternalReference` fields are `external_reference_id`, `external_system`, `external_object_type`, `external_object_id`, `ubu_object_type`, `ubu_object_id`, `relation_type`, `confidence`, `created_by_identity_ref`, `created_at`, `last_verified_at`, `sync_policy`, `projection_policy`, and `provenance`.

External References may target Objectives, Tasks, External Events, and Log entries in Phase 1. This lets GitHub Issues, PRs, comments, reviews, CI runs, and milestones remain traceable without forcing them into one-to-one mappings. MVP relation types are schema-controlled enums: `represents`, `supports`, `evidence_for`, `source_event_for`, `projection_of`, `duplicate_of`, and `supersedes`.

Duplicate detection uses a normalized uniqueness key over `external_system`, `external_object_type`, `external_object_id`, `ubu_object_type`, `ubu_object_id`, and `relation_type`. Reobserving the same external reference updates verification metadata or logs an idempotent no-op rather than creating a duplicate. Distinct relation types between the same objects are allowed.

Automation Workers cannot directly create or mutate canonical External References in Phase 1. They may submit external-reference mutation requests through authorized `mutation_request.submit` capability grants; the canonical instance validates and logs applied or rejected outcomes.

---

## UBU-Q0004: Pipeline State

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0003 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0002 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0005 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Solved Priority: MVP blocker Phase: Phase 1 Decision type: Security Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0095 Last scored: Never Scored from commit: None

A worker-mode UbU instance is externally represented as an Identity. Workers need bounded authority.

### Question

1. What capabilities can a worker Identity receive?
   - read Task
   - read Objective
   - read UniverseState subset
   - create Task
   - create Objective
   - mutate Task
   - mutate Objective
   - mutate `pipeline_state`
   - append External Event
   - submit Snapshot
   - request recalculation
   - update GitHub projection
2. Are capabilities scoped by:
   - object ID
   - Objective subtree
   - Task set
   - Compartment
   - external integration
   - time window
3. Can a worker be revoked?
4. Can a worker operate across multiple organization-mode instances?
5. Can a worker operate for user-mode instances?
6. How are worker credentials rotated?
7. Does worker capability state live on Identity, a capability object, or both?

### Current direction

Automation Worker = worker-mode UbU instance externally represented as an Identity.

### Resolution

Solved by `UBU-D0095`. Worker authority is represented by explicit capability grants attached to a worker Identity. The Identity is the external actor and credential subject; capability grants are separate authority objects issued by a specific parent UbU instance.

Phase 1 worker capabilities are `task.read`, `objective.read`, `universe_state.read_subset`, `external_event.append`, `snapshot.submit`, `mutation_request.submit`, `recalculation.request`, and `projection.github.request_update`. Workers do not directly create or mutate canonical Tasks, Objectives, UniverseState, `pipeline_state`, or GitHub projection state in Phase 1. Those changes are submitted as mutation or projection requests for validation by the canonical instance.

Capabilities may be scoped by object ID, Objective subtree, Task set, Compartment, external integration, operation kind, and time window. Compartment policy is a hard upper bound on worker access and export authority. A grant cannot authorize a worker to receive, route, or export data that the relevant Compartment forbids.

Workers can be revoked by disabling or deleting grants and rotating or invalidating credentials. Credential rotation keeps audit continuity by versioning credentials under the worker Identity unless the grant itself changes. Prior Logs are not rewritten.

A worker may operate for multiple organization-mode or user-mode instances only through separate parent-specific grants, credentials, and audit trails. Cross-parent data sharing is forbidden unless explicitly granted by each parent and allowed by all relevant Compartment policies. User-mode worker operation is allowed, but affect and other personal data require narrow read-subset grants and must obey Compartment and low-security disclosure rules.

---

## UBU-Q0008: Worker Assignment Model

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0007 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0007 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

Automation Workers need a bounded way to submit changes back to canonical UbU state.

### Question

1. Does a worker submit:
   - event records,
   - mutation requests,
   - proposed patches,
   - or all three?
2. What fields are required?
   - worker Identity
   - authority source
   - target object
   - operation
   - expected prior version
   - new value
   - reason
   - evidence reference
   - timestamp
   - idempotency key
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

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Security Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0007 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

Automation Workers may interact with GitHub using access tokens.

### Question

1. Are GitHub tokens stored:
   - on the central UbU instance,
   - only on worker-mode instances,
   - or both?
2. Are tokens tied to:
   - bot accounts,
   - maintainer accounts,
   - individual contributor accounts?
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

Status: Solved Priority: Post-MVP Phase: Phase 3 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 3 implementation Resolved by: UBU-D0144 Last scored: Never Scored from commit: None

Automation Worker communication may overlap with future user-to-user or instance-to-instance communication.

### Question

1. Is there one generic UbU inter-instance protocol?
2. Or is worker communication a separate MVP API?
3. Should the protocol support:
   - messages
   - assignments
   - status updates
   - mutation requests
   - capability grants
   - External Event submission
   - recalculation requests
4. Can this protocol later support Phase 3 multi-user Identity coordination?
5. Does the MVP worker API intentionally approximate the future inter-instance protocol?

### Resolution

Solved by `UBU-D0144`. UbU should have one generic inter-instance protocol family for communication between UbU instances, worker-mode instances, and future compatible peers. The protocol is a family of typed envelopes with shared Identity, capability, Compartment, provenance, idempotency, versioning, and review semantics.

Phase 1 worker communication remains a separate MVP API surface in implementation terms, but it is intentionally a narrow worker profile of the future protocol. It should support assignment, status, mutation-request, projection-request, External Event, Snapshot or Log candidate, and recalculation-request payloads only as needed for Phase 1 dogfooding. It should not implement native user-to-user messaging, peer discovery, Association reconciliation, or generic multi-user transport.

The future protocol should support contextual messages, assignments, status updates, mutation requests, capability grants, External Event submission, authorized Snapshot or Log candidate submission, recalculation requests, and clarification request/response flows. Payload families may have different review defaults, but they share envelope semantics and never bypass canonical admission rules.

Phase 3 multi-user Identity coordination should extend this same protocol family. User-to-user requests, status updates, questions, commitments, blockers, and Message Context Envelopes are peer payloads under the same Identity, Compartment, disclosure, provenance, and user-sovereignty boundaries.

Concrete schemas remain in narrower open questions, including worker assignment, worker mutation requests, Message Context Envelopes, legacy adapter upgrade paths, capability-grant exchange details, and Association-related coordination.

---

## UBU-Q0012: Organization Mode Object Rules

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0101 Last scored: Never Scored from commit: None

Organization mode does not model intrinsic affect but otherwise shares much of the same data model.

### Question

1. Are all core objects available in organization mode?
   - Objective
   - Preference
   - Task
   - Container
   - UniverseState
   - Plan
   - Calendar
   - Identity
   - Relationship
   - Compartment
2. Are affect fields omitted, disabled, or merely unused?
3. Can Relationship objects exist without affect dimensions?
4. Can organization-mode instances receive limited signals from personal user-mode instances later?
5. Is `authority_source` required on organization-created Preferences, Objectives, and Tasks?
6. How are organization users represented before RBAC exists?

### Current direction

All users in organization mode may be treated as admin-equivalent in MVP.

### Resolution

Solved by `UBU-D0101`. Organization mode uses the shared UbU core object model except where fields or behavior are intrinsically personal-affect-specific. Objective, Preference, Task, Container, UniverseState, Snapshot, Plan, Calendar, Log, Identity, Relationship, Compartment, Automation Worker, External Event, External Reference, and deferred Association-related objects are available in organization mode to the depth required by the organization or project-planning workflow.

Intrinsic affect fields are absent from mode-specific organization schemas. If a shared implementation schema contains affect-capable fields for storage or migration convenience, those fields are disabled in organization mode and validation must reject organization-created intrinsic-affect values rather than merely ignoring them.

Relationship objects may exist in organization mode without affect dimensions. They represent structured UniverseState between Identities such as contributors, maintainers, workers, projects, vendors, integrations, or external organizations. Non-affect relationship-relevant project information belongs in ordinary UniverseState facts, External Events, Logs, External References, candidate AssociationAttestations, Objectives, Tasks, or risk reports; organization mode must not claim private organizational emotional state.

Organization-created Objectives, Preferences, and Tasks require `authority_source` metadata. MVP authority metadata may be coarse, but it must identify the authority path, such as an admin-equivalent operator Identity, imported project policy, imported external event, Automation Worker submission, or human-approved import/projection action. The detailed authority-source vocabulary and other authority-bearing objects remain open in `UBU-Q0013`.

Before RBAC exists, organization-mode human users are represented as operator Identities with admin-equivalent authority over the instance. Their actions still write Logs with actor Identity and provenance so future RBAC can be introduced without rewriting history.

Organization-mode instances may later receive limited signals from personal user-mode instances only through explicit user-controlled sharing, Identity-mediated authorization, Compartment/export checks, and clear provenance. Phase 1 does not implement personal-to-organization cross-instance sharing. Future designs should prefer structural signals such as availability, commitment status, task completion, or user-approved projection summaries rather than raw affect, private relationship state, or broad personal context.

---

## UBU-Q0013: Authority Source Vocabulary

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0012 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

Organizational directives and worker updates need authority/source metadata.

### Question

1. Which objects carry `authority_source`?
   - Preference
   - Objective
   - Task
   - pipeline state
   - worker assignment
   - external projection
   - mutation request
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

Status: Solved Priority: MVP blocker Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0130 Last scored: Never Scored from commit: None

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
   - dotted string
   - JSON pointer
   - tuple path
2. What fields exist on each mutation item?
   - target
   - operation
   - payload
   - note
   - source
3. What payload types are allowed?
   - string
   - number
   - boolean
   - JSON object
   - set member
   - event marker
4. Are mutation items always unconditional once Task effect succeeds?
5. Can mutation items target affect fields?
6. Can mutation items target Relationship payloads?
7. Should mutation items contain confidence?
8. Should mutation items contain provenance in MVP?

### Current leaning

Use dotted string targets and JSON-compatible payloads.

### Resolution

Solved by `UBU-D0130`. MVP UniverseState mutation items use dotted string targets. The first segment names the target UniverseState collection: `facts`, `numeric_values`, `set_memberships`, or `event_markers`. The remaining segments form the namespaced key inside that collection.

Required fields are `operation` and `target`. `payload` is required except for `clear_fact`. `note` is optional. Item-level `source`, `provenance`, and `confidence` are not part of the MVP mutation item because those belong on the containing Task effect, Snapshot, Log entry, worker mutation request, External Reference, or import/projection envelope.

Payloads are operation-specific: `set_fact` accepts any JSON-compatible value; `clear_fact` has no payload; numeric increments/decrements require numeric deltas; membership operations use JSON scalar members, usually strings; and event markers use JSON object payloads. Mutation lists are unconditional once the containing Task effect succeeds, with conditional behavior handled through preconditions, effect success probability, planner branching, or request validation.

Mutation targets may include affect keys in `user_mode`, subject to Snapshot precedence and user sovereignty. Organization and worker modes reject intrinsic-affect mutations. Mutation targets may include Relationship-relevant UniverseState keys, but private or inferred relationship facts remain subject to Compartment policy, mode rules, provenance/logging envelopes, and user acceptance where required. Task effects and worker/import/LLM flows must not silently overwrite user-declared private affect or Relationship truths.

---

## UBU-Q0015: Task Precondition Schema

Status: Solved Priority: MVP blocker Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0131 Last scored: Never Scored from commit: None

Preconditions are deterministic constraints over UniverseState.

### Accepted MVP precondition types

- equality
- membership
- absence
- simple AND/OR logic

Numeric comparisons are not in MVP.

### Question

1. Should preconditions use:
   - `all_of[]` / `any_of[]`,
   - or flat list with connectors?
2. What are the predicate fields?
   - target
   - predicate type
   - expected value
3. Can preconditions reference event markers?
4. Does failed precondition mean:
   - blocked
   - unschedulable
   - invalid
5. Can preconditions reference affect fields?
6. Can preconditions reference Relationship payloads?

### Current leaning

Failed precondition should mean blocked, not invalid.

### Resolution

Solved by `UBU-D0131`. MVP Task preconditions use a recursive boolean object with `all_of` and `any_of` arrays for simple AND/OR logic. A group node contains one of those arrays. A leaf predicate contains `target`, `predicate`, and optional `expected`.

Targets use the same dotted UniverseState target convention as mutation items: the first segment is `facts`, `numeric_values`, `set_memberships`, or `event_markers`, and the remaining segments form the namespaced key.

MVP predicates are `equals`, `member_of`, and `absent`. `equals` compares the target value with a JSON-compatible expected value. `member_of` checks that a JSON scalar expected value is present in a `set_memberships` target. `absent` checks that the target is missing or cleared and does not use `expected`. Numeric comparisons, ranges, thresholds, and arithmetic expressions are not in MVP.

Preconditions may reference event markers. They may reference affect keys in `user_mode`, but organization-mode and worker-mode validators reject intrinsic-affect preconditions. They may reference Relationship-relevant UniverseState keys, including interaction markers and maintenance facts, subject to Compartment policy, mode rules, provenance/logging envelopes, and user acceptance for private or inferred claims.

A failed precondition means the Task is blocked for planning and execution, not invalid. `unschedulable` is a derived planner result when an otherwise valid Task cannot be placed in the current Calendar scope while satisfying preconditions and Calendar Logic. `invalid` is reserved for malformed Tasks, malformed precondition schema, forbidden targets, or canonical-state contradictions. Unknown or partially modeled preconditions are treated as absent in MVP unless explicitly represented as deterministic predicates.

---

## UBU-Q0016: Compact Calendar planner grammar and execution profile

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0014, UBU-Q0015 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

Compact Calendar support is important for recursive self-analysis, future sync/transport, and fast recalculation. The current direction is no longer a bare DFS grammar. The planner architecture begins with skeleton Plan generation, then legitimization, then candidate Plan expansion and validation, with reactive mobile stewardship around the selected Plan.

### Question

1. What is the minimum skeleton Plan representation?
   - Static Task placement
   - dependency DAG frontier
   - prerequisite roots
   - ordered prerequisite chains
   - initial UniverseState assumptions
   - unsatisfied dependency diagnostics
2. What does legitimization add?
   - affect constraints
   - recovery Tasks
   - transition buffers
   - sleep/food/rest requirements
   - setup/teardown time
   - context-switch limits
   - slack and fragility thresholds
3. What is the minimum candidate Plan representation after legitimization?
   - materialized Tasks
   - decision envelopes
   - Plan probability provenance
   - value score
   - legitimacy score or threshold result
   - explanation lineage
4. Which search methods are allowed in each execution profile?
   - greedy baseline
   - DFS-like candidate construction
   - BFS-like near-term branch construction
   - solver-backed exact validation
   - GPU-friendly candidate scoring/simulation
   - local repair recipes
5. How is Plan probability represented?
   - scalar probability
   - log probability
   - probability interval
   - provenance expression over probabilistic inputs
6. How does the implementation avoid naïve independence assumptions when probabilities are correlated?
7. Does Compact Calendar encode:
   - skeleton Plan metadata
   - legitimized skeleton baseline
   - ordering constraints
   - duration PDFs
   - success probabilities
   - external-event distributions
   - interruption distributions
   - affect constraints
   - decision envelopes
   - protected/flexible/disposable Task metadata
   - cached explanations
   - execution-mode metadata such as time delta, branch horizon, GPU/CPU resource limits, and privacy-routing limits
8. Which concrete Plans are stored?
   - the legitimized skeleton baseline
   - the default Plan
   - user-previewed Plans
   - risk-report Plans
   - debug/reproducibility Plans
   - high-probability near-term Plans within a horizon
9. Which Plans or repairs are reconstructed on demand?
10. How is coverage recalculated after time advances?
11. What is the minimum MVP implementation?

### Current direction

The planner should first create a skeleton Plan from Static Tasks and dependency DAGs, then legitimize that skeleton Plan into a minimally human-viable baseline. Candidate Plans are then generated, semi-legitimized or fully legitimized, validated, and compared. DFS-like search may be one candidate-construction strategy, but it is no longer the full conceptual foundation. BFS-like branch caching remains useful for near-term divergence, but mobile UX should also use decision envelopes, cached explanations, criticality metadata, last-legitimate-Plan repair, and conflict severity.

The ideal search may be NP-hard or otherwise combinatorially expensive, but finite Task instances, bounded time scope, configurable deltas, pruning, greedy baselines, GPU-friendly scoring/simulation, cached subplans, and adaptive execution modes should make practical approximations tractable.

### Resolution

Unresolved. Must be refined into an MVP planner grammar and execution profile before Phase 1 implementation can be considered stable.

---

## UBU-Q0017: Compact Calendar Coverage and Regeneration

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

Coverage belongs to compact Calendar serialization.

### Question

1. Is coverage exact or estimated in MVP?
2. Does coverage include:
   - duration uncertainty
   - Task success/failure uncertainty
   - external-event uncertainty
   - Objective recurrence uncertainty
3. Does a compact Calendar store coverage value only, or also uncovered mass?
4. What is the default regeneration threshold?
5. Is the threshold global, device-specific, Calendar-specific, or all three?
6. Does low coverage create:
   - report only,
   - recalculation trigger,
   - Task,
   - worker assignment?

### Current direction

The provisional short-horizon branch coverage target is `0.99` probability mass. Coverage and regeneration thresholds may be device-specific, Calendar-specific, or execution-mode-specific. This is not final.

### Resolution

Unresolved.

---

## UBU-Q0018: Risk Reporting Primitives

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0145 Last scored: Never Scored from commit: None

Risk is not a first-class object in MVP. Risk is reportable from Calendar/Plan analysis.

### Question

1. Which reports are MVP?
   - P90 completion time
   - critical path
   - deadline miss probability
   - affect constraint violation probability
   - low coverage warning
   - dependency fragility
   - worker failure / automation bottleneck
2. Are risk reports computed:
   - on demand,
   - cached,
   - generated by Automation Workers,
   - stored as artifacts?
3. Are risk reports part of release ceremonies?
4. Which risk reports demonstrate that UbU supersedes PERT?
5. Can risk reports create Tasks?

### Resolution

Solved by `UBU-D0145`.

Risk reports remain derived analysis rather than first-class Risk objects. They are computed from Calendars, Plans, Tasks, Logs, Snapshots, External Events, worker status, External References, and compact Calendar metadata.

The Phase 1 MVP report set is `p90_completion_time`, `critical_path`, `deadline_miss_probability`, `affect_constraint_violation_probability`, `low_compact_calendar_coverage_warning`, `dependency_fragility`, `worker_or_automation_bottleneck`, `stale_affect_warning`, `destructive_pressure_warning`, and `post_plan_depletion_warning`.

Relationship neglect, preference uncertainty, repeated override/deviation, motivation mismatch, stale discovery-mode reconciliation, and overdue Calendar preview or Log review findings may be computed opportunistically when inputs exist, but they are not required Phase 1 reports.

Risk reports are computed on demand from the current Calendar or Plan. They may be cached as derived artifacts on Calendars, Plans, run artifacts, or release packages, but caches are invalidated or marked stale after relevant Task, Log, Snapshot, External Event, worker-status, coverage, or recalculation-trigger changes.

Automation Workers may compute or refresh risk-report artifacts under explicit read capabilities. Worker results are advisory until admitted by the canonical instance and cannot create canonical Risk objects or directly mutate Tasks.

Risk reports may recommend Tasks or submit task-creation/mutation requests through the normal admission path. In MVP they do not silently create canonical Tasks. Typical follow-ups are clarification, affect collection, dependency repair, worker retry or escalation, Calendar regeneration, Log review, Calendar preview, and GitHub projection or reconciliation work.

Risk reports are part of UbU-runs-UbU release ceremonies. Release readiness and Release Outreach Pipeline packages should include deadline risk, critical path, dependency fragility, worker/automation bottleneck, and low coverage warnings when the relevant inputs exist, while respecting Compartment and public-projection boundaries.

The PERT-superiority demo should show that UbU handles more than duration networks: explicit dependencies and preconditions, affect constraints, worker/automation status, compact Calendar coverage, recalculation from Logs and Snapshots, and actionable Plan repair or next-Task recommendations.

---

## UBU-Q0019: Recalculation Trigger Taxonomy

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0008 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

Automation Workers may fail or produce failed child Tasks.

### Question

1. If a worker-created child Task fails, does UbU:
   - mutate the same Task,
   - create retry sibling,
   - mark failed then create replacement,
   - mark moot?
2. Is retry policy defined by:
   - Task
   - Objective
   - Worker
   - integration type
3. How are retry attempts logged?
4. How are repeated failures prevented from creating infinite loops?
5. Does a worker failure affect risk reports?

### Current leaning

Failed attempt + retry sibling is likely best for auditability.

### Resolution

Unresolved.

---

## UBU-Q0021: Automation Worker Parent / Child Structure

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0008 Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP important Phase: Phase 2 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 2 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0100 Last scored: Never Scored from commit: None

Snapshots override simulated state when conflicting, but application details remain open.

### Question

1. Are snapshots patches or full assertions?
2. Are snapshots immutable once logged?
3. Is confidence stored:
   - per snapshot,
   - per field,
   - or both?
4. If two user snapshots conflict, does latest always win?
5. Can a Snapshot be revoked or corrected?
6. Does correction create a new Snapshot?

### Resolution

Solved by `UBU-D0100`. Snapshots are partial observed assertions over specific UniverseState fields, not full assertions of all UniverseState. Applying a Snapshot updates only included fields and says nothing about omitted fields.

Snapshots are immutable once accepted into the append-only Log. The original observation is preserved as historical evidence. Annotation, correction, and revocation are represented by later Log entries that point to the original Snapshot observation or Log entry.

MVP confidence is stored both per Snapshot and, when needed, per field. Snapshot-level confidence is required as the default; optional per-field confidence overrides allow different dimensions to carry different reliability. Affect Snapshots may continue using global confidence across affect dimensions unless per-field confidence is explicitly provided.

Conflict resolution is field-local. Latest observed Snapshot data overrides simulated state. User-declared Snapshots have top priority in MVP. If two user-declared Snapshots conflict on the same field, the latest `effective_at` or Snapshot timestamp wins unless a later correction supersedes it. Non-user observations may use source priority, timestamp, and confidence, but confidence does not defeat explicit user declaration in MVP.

A Snapshot can be corrected or revoked only through a new Log entry. Correction that replaces observed state creates a new Snapshot linked to the corrected Snapshot or Log entry. Revocation without replacement creates a correction/revocation Log entry that removes the original Snapshot from corrected query views while preserving the historical claim.

---

## UBU-Q0026: Relationship Maintenance Modeling

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0076 Last scored: Never Scored from commit: None

Relationship is modeled as structured UniverseState payload between two Identities.

### Question

1. Where does communication cadence live?
   - Objective recurrence
   - Task history
   - external storage
   - Relationship payload
2. Where does neglect risk live?
   - risk report
   - Objective recurrence
   - Relationship payload
3. How does UbU model “maintain relationship with contributor X”?
4. Can GitHub contributor interactions update relationship state?
5. Is relationship maintenance in MVP, or only documented for future use?

### Resolution

Solved by `UBU-D0076`. Communication cadence lives on the evergreen Objective's recurrence/reactivation rule. Interaction evidence lives in Logs, External Events, Task history, or Compartment/external references; it is not stored directly on the Relationship payload.

Neglect risk is a risk-report finding derived from the maintenance Objective recurrence, observed interaction history, and current Plan/Calendar state. It is not stored on Relationship and does not make risk first-class in MVP.

"Maintain relationship with contributor X" is modeled as an evergreen Objective linked indirectly to the contributor Relationship or relationship-relevant UniverseState key. The Objective may create ordinary Dynamic Tasks such as reply, review, check in, or follow up, whose effects update UniverseState or append event markers.

GitHub contributor interactions may update relationship-relevant modeled state when imported as External Events associated with the user's GitHub Identity and the contributor Identity. They may satisfy or reactivate the maintenance Objective, but they do not overwrite user-stated affect or canonicalize sensitive inferred relationship facts without user acceptance.

Phase 1 supports relationship maintenance only through existing Objective, Task, Log, External Event, UniverseState, Identity, Relationship, and risk-report mechanisms. Dedicated relationship-management UI, cadence fields on Relationship, and full personal CRM behavior are deferred.

---

## UBU-Q0027: Organization Mode and Worker Mode Public UX

Status: Solved Priority: Post-MVP Phase: Post-MVP Decision type: Product Auto-choice eligibility: Human only Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Post-MVP product Resolved by: UBU-D0075 Last scored: Never Scored from commit: None

Organization mode and worker mode may use web admin UIs.

### Question

1. What does the organization-mode UI show first?
2. What does the worker-mode UI show first?
3. Does worker mode expose logs, assignment queue, capability grants, GPU/cloud status?
4. Does organization mode expose pipeline state, risk reports, worker assignments, GitHub projection status?
5. Which UI is required for Phase 1?

### Resolution

Solved by `UBU-D0075`. Organization-mode public UX is a project operations dashboard. Its first screen shows pipeline state, Plan/risk summaries, worker assignments and health, pending worker mutation requests, GitHub projection/reconciliation status, and recent decision/projection/worker Log entries requiring operator attention.

Worker-mode public UX is an operator console. Its first screen shows connection and Identity status, service health and last check-in, active assignment and assignment queue, granted capability scopes, recent Log or mutation submissions, rejection/error state, and local resource status such as GPU availability or cloud compute state when applicable.

Both modes may expose operational logs and status appropriate to that mode, but they must default to summarized/redacted views and must not leak Compartment-protected payloads, broader planning state, or personal affect data.

No organization-mode or worker-mode web admin UI is required for Phase 1. Phase 1 requires only the single-user GitHub dogfooding surface and enough visible worker assignment/status information for the public demo, which may be shown in that UI, CLI output, or run artifacts.

---

## UBU-Q0028: Minimum Privacy / Compartment Promise for MVP

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Security Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0074 Last scored: Never Scored from commit: None

UbU is privacy-first, but MVP implementation must avoid overclaiming.

### Question

1. Are Compartments implemented in Phase 1?
2. If yes, what hard invariants exist?
   - no cloud LLM routing
   - export blocking
   - retention
   - audit logging
   - device eligibility
3. If not fully implemented, how is this disclosed?
4. How is un-compartmented content labeled low-security?
5. What can UbU honestly claim about local-first operation in Phase 1?
6. What can UbU honestly claim about cloud LLM usage in Phase 1?

### Resolution

Solved by `UBU-D0074`. Phase 1 implements a minimal Compartment guardrail layer, not the full Phase 2 multi-device containment system. Compartments may classify content with policies such as `local_only`, `no_cloud_llm`, `no_external_export`, allowed integrations, and allowed Devices within the single local Device model.

The hard MVP invariants are narrow: `no_cloud_llm` content is not routed to cloud LLMs; `no_external_export` content is not exported, projected, or handed to workers except as redacted structural references; Compartment-marked content crosses boundaries only through allowed routes and user-visible actions; and boundary-crossing attempts that reach UbU are logged as allowed or denied. Sensitive Compartment content is referenced rather than embedded in ordinary WorkItem structure.

Phase 1 does not claim complete privacy isolation, cryptographic isolation, hardware attestation, secure multi-device partial replication, protection from a malicious local administrator, or automated retention deletion/redaction. Retention policies may be recorded, but enforcement beyond append-only Log retention is post-MVP unless separately implemented and disclosed.

Un-compartmented content is labeled `security_level: low`. Phase 1 may claim local-first operation only in the limited sense that canonical planning state, Logs, and source-linked project model data live in the local single-user UbU instance by default. Cloud LLM use may be optional, explicit, integration-scoped, and advisory, but cloud LLMs are not the canonical planner and must not receive `no_cloud_llm` Compartment content.

---

## UBU-Q0029: Open-Core / FOSS Contribution Boundary

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Governance Auto-choice eligibility: Human only Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0073 Last scored: Never Scored from commit: None

UbU is intended to recruit FOSS contributors.

### Question

1. Which components are definitely open source?
   - data model
   - planner
   - GitHub projection
   - worker mode
   - compact Calendar serialization
   - local-first sync
   - Super Automation API
2. Which components may remain experimental or private?
3. How does UbU avoid giving contributors the impression that the open core is bait?
4. What licensing strategy should implementation repos use?
5. What is the commercial/premium boundary, if any?

### Resolution

Solved by `UBU-D0073`. UbU uses an open-core strategy, but the open core includes the planning kernel and contributor-facing integration surface: data model schemas and migrations, explicit planner and Calendar-generation logic needed for Phase 1 dogfooding, GitHub import/projection/reconciliation tooling, worker-mode runtime surfaces, compact Calendar serialization needed for transport or analysis, local-first storage and sync protocols when implemented, and the Super Automation extension/API boundary.

Private or commercial code may exist only outside that boundary, such as hosted-service operations, managed cloud infrastructure, paid support/packaging, premium hosted worker capacity, enterprise administration or compliance layers, proprietary connectors to closed third-party systems, and short-lived experiments that are not required for the public dogfooding loop. If a private experiment becomes required for the advertised open-source workflow, it must be opened before public reliance or the public promise must be narrowed.

Core implementation repos should default to MPL-2.0, with stronger copyleft considered for network-hosted service code and permissive licenses allowed for examples, SDK stubs, or interoperability fixtures. Repositories and packages should be labeled clearly as open core, private experiment, premium hosted service, or external connector so contributors are not misled about the commercial boundary.

---

## UBU-Q0030: Phase 1 Public Demo Criteria

Status: Solved Priority: MVP blocker Phase: Phase 1 Decision type: Product Auto-choice eligibility: Human only Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 release Resolved by: UBU-D0072 Last scored: Never Scored from commit: None

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

Solved by `UBU-D0072`. The Phase 1 public demo must be a real or fixture-backed GitHub dogfooding loop using UbU's own issues. It must import or observe the issue set, map it into Objectives and schedulable Tasks, generate a Calendar with a default Plan, and show the Plan rationale.

The demo also shows one or more risk reports, user-mode affect constraints or the affect-collection Task created by stale data, Automation Worker assignment/status, and the exact UbU-managed GitHub labels/comments/blocks to be written or previewed.

Live GitHub mutation is optional for the public recording when safety requires dry-run mode, but the projection payload must be generated by the same path used for a human-approved write. Phase 2 sync, Phase 3 multi-user coordination, full RBAC, and autonomous GitHub mutation are not required.

---

## UBU-Q0031: Log Structure and Fields

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 implementation Resolved by: UBU-D0071 Last scored: Never Scored from commit: None

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

Solved by `UBU-D0071`. MVP Logs are append-only per-instance event records using a shared entry envelope and event-specific payloads. Required fields are `log_entry_id`, `schema_version`, `instance_id`, `recorded_at`, `effective_at`, `event_type`, `actor_identity_ref`, `recorded_by_device_ref`, `target_ref`, `result`, `event_payload`, and `provenance`. Optional fields cover old/new values, reason, notes, confidence, related Plan references, external references, correction/annotation links, and idempotency keys.

MVP event types cover Task completion/failure/moot, External Event observation, Snapshot observation, Objective transition, Plan realization, decision recording, recalculation trigger, worker mutation submission/application/rejection, and Log annotation/correction. Log entries are immutable; annotation or correction creates a new entry pointing to the original rather than modifying it. Canonical Logs are stored per instance, with device references recorded on entries. MVP retention is indefinite, with archival allowed only if queryability and integrity are preserved. Large-history search uses rebuildable indexes and cursor-paginated time-window queries. Automation Workers contribute through worker Identities by submitting events or mutation requests that the canonical instance validates and records as applied or rejected.

---

## UBU-Q0032: Model Committee Process and Authority

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Model-committee v0.1 correctness Resolved by: UBU-D0057, UBU-D0058, UBU-D0059, UBU-D0060, UBU-D0065, UBU-D0069, UBU-D0070 Last scored: Never Scored from commit: None

### Question

What authority should the model-committee process have when proposing answers, patches, consistency checks, readiness scores, and new open questions?

### Subquestions

1. Which actions may be automated?
2. Which actions require human review?
3. Which actions are forbidden in v0.1?
4. How are model outputs weighted?
5. How are failed provider calls logged?
6. What quorum is required for a valid committee result?
7. How does Codex CLI provider authority differ from direct API authority?
8. What must remain outside model-committee authority in v0.1?

### Current direction

`model-committee` is advisory and repo-driven. It may propose and score changesets, but accepted design state exists only when committed to the canonical repo. v0.1 uses Codex CLI as the primary proposal/scoring provider and Ollama as secondary proposal providers. v0.1 must not call OpenAI APIs directly, mutate GitHub, auto-apply patches, or allow Codex to directly modify canonical repo files.

### Resolution

Solved for v0.1 by accepted decisions covering advisory authority, v0.1 restrictions, model weighting, question ranking, provisional quorum/provider-failure behavior, Codex CLI provider behavior, and the explicit v0.1 authority boundary.

`model-committee` may automate derived analysis and review artifact generation, including consistency checks, question rankings, readiness estimates, candidate questions, candidate changesets, patch validation, Codex scoring, and selected-patch artifact writing. It may not create accepted design state without a human-reviewed committed repo change.

Direct API calls, GitHub mutation, automatic patch application, auto-merge, auto-push, automatic PR creation, internal manual override of failed selection, readiness-score writes to derived public files, and direct model edits to canonical files remain outside v0.1 authority.

Detailed mechanics remain open in the narrower follow-up questions for log/provenance format, changeset validation/scoring, recursive-loop blocking semantics, and decomposition/design-burden scoring.

---

## UBU-Q0033: Phase 1 MVP Readiness Scoring Rubric

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0001 Blocks: README readiness signal Resolved by: Unresolved Last scored: Never Scored from commit: None

### Question

How should UbU estimate how close the project is to Phase 1 scope freeze and MVP readiness?

### Resolution

Unresolved.

---

## UBU-Q0034: Design Automation Stop Rule

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0001 Blocks: Phase 1 scope freeze Resolved by: Unresolved Last scored: Never Scored from commit: None

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

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0032 Blocks: Question-ranking accuracy Resolved by: Unresolved Last scored: Never Scored from commit: None

### Question

How should remaining design work be classified by automation eligibility?

### Resolution

Unresolved.

---

## UBU-Q0036: Committee Log and Provenance Format

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Process Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0032 Blocks: model-committee v0.1 logging Resolved by: UBU-D0064 Last scored: Never Scored from commit: None

### Question

What minimum files and fields must a model-committee run log preserve?

### Current direction

v0.1 should use the provisional filesystem log format defined in `UBU-D0064`. The provisional format includes canonical file snapshots, schema files, Codex prompts, Ollama prompts, Codex JSON outputs, Codex JSONL event logs, provider stderr, parsed proposals, patch files, selected patch, review artifact, and commit message. The final log/provenance format remains open and may be refined after the first working implementation exists.

### Resolution

Partially resolved by `UBU-D0064`; final log/provenance requirements remain open.

---

## UBU-Q0037: Post-MVP Question Lifecycle

Status: Open Priority: Post-MVP Phase: Post-MVP Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0032 Blocks: None Resolved by: Unresolved Last scored: Never Scored from commit: None

### Question

How should post-MVP design questions be preserved, re-ranked, reopened, or retired after the first MVP release?

### Resolution

Unresolved.

---

## UBU-Q0038: Changeset-Based Work Phase

Status: Open Priority: MVP blocker Phase: Phase 1 Decision type: Process Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0032 Blocks: model-committee v0.1 work execution Resolved by: UBU-D0063, UBU-D0069 Last scored: Never Scored from commit: None

### Question

How should the model-committee work phase represent, score, select, apply, and commit concrete changesets?

### Subquestions

1. What format should work proposals use?
2. What validation is required before work scoring?
3. May models score their own work?
4. What criteria should work scoring use?
5. When may a selected changeset be committed locally?
6. What files may be modified in v0.1?
7. How does the work phase generalize from design questions to code changes and bug fixes?
8. How should Codex CLI schema-constrained proposals fit into the work phase?
9. How should Ollama secondary proposals be included in Codex scoring?
10. What should happen when Codex scoring selects a mechanically invalid proposal?

### Current direction

The work phase should produce explicit patch-style changesets, score those changesets, select the best one, and create reviewable artifacts in v0.1. v0.1 uses Codex CLI as the primary schema-constrained work and scoring provider, with Ollama as secondary proposal providers. Codex produces proposals and scores only; it does not directly edit canonical repo files. v0.1 writes `selected.patch`, `commit_message.txt`, `review.md`, and logs. Remote GitHub mutation, automatic patch application, and automatic PR creation remain out of scope for v0.1.

### Resolution

Partially resolved by `UBU-D0063` and `UBU-D0069`; detailed scoring and validation rules may be refined after implementation.

---

## UBU-Q0039: Prioritized Recursive Loop Semantics

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0032 Blocks: model-committee v0.1 loop semantics Resolved by: UBU-D0066 Last scored: Never Scored from commit: None

### Question

How should model-committee represent and enforce the prioritized recursive loop of consistency, prioritization, and work?

### Subquestions

1. What exact events trigger a system-wide consistency check?
2. What consistency failures should block ordinary work?
3. How are consistency failures converted into questions or work items?
4. When may prioritization run if consistency has warnings but no hard failures?
5. When may work proceed against a known inconsistency?
6. How should this loop map into future UbU Automation Worker behavior?
7. How should LLM model updates trigger re-checks or re-scoring?
8. How should Codex CLI provider updates trigger re-checks or re-scoring?

### Current direction

System-wide consistency has highest priority, question/problem prioritization has second priority, and work has third priority. Work should not proceed against a known-inconsistent state unless the selected work item repairs that inconsistency.

### Resolution

Partially resolved by `UBU-D0066`; detailed trigger and blocking semantics remain open.

---

## UBU-Q0040: Question Decomposition and Design Burden Scoring

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0039 Blocks: model-committee prioritization accuracy Resolved by: UBU-D0068 Last scored: Never Scored from commit: None

### Question

How should model-committee distinguish harmful question proliferation from valuable decomposition of hard questions into simpler, more automatable questions?

### Subquestions

1. How is unresolved design burden measured?
2. How is automation difficulty compared between an original question and its replacements?
3. When may a question be marked decomposed rather than solved?
4. What metadata should link replacement questions to the original question?
5. How should work scoring reward valid decomposition?
6. How should the stop rule account for decomposition that increases question count but lowers total difficulty?
7. When is dependency-reducing decomposition preferable to waiting for all dependencies to be answered?
8. How should the system score decompositions that produce at least one immediately answerable replacement question?
9. How should dependency simplification affect question ranking?
10. How should answerability be computed from dependency metadata?
11. When should a blocked question be selected for decomposition rather than skipped?
12. Should answerability be a hard gate or a weighted score?

### Current direction

Increasing the number of open questions is acceptable when a hard or blocked question is split into simpler, clearer, lower-risk, or more automatable questions. This is especially valuable when at least one replacement question has fewer dependencies, simpler dependencies, or no dependencies, allowing the system to make progress without waiting for the full original dependency chain.

Question selection should use answerability as the first gate. Ordinary work should only run on questions whose dependencies are resolved, absent, or handled in the same work item. Blocked questions may still be selected for decomposition if the decomposition is expected to produce replacement questions with fewer, simpler, or no dependencies.

### Resolution

Partially resolved by `UBU-D0068`; detailed scoring mechanics remain open.

---


## UBU-Q0041: Public recruitment language for a small core cohort

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Contributor recruitment Resolved by: UBU-D0078, UBU-D0085, UBU-D0093 Last scored: Never Scored from commit: None

### Question

What public language best recruits a small core cohort of serious, self-directed contributors without implying scarcity, exclusion, or competition for a single privileged role?

### Subquestions

1. How should UbU distinguish serious contributors from passive interest without sounding unwelcome?
2. How should public materials invite multiple committed contributors while preserving bounded contribution paths?
3. Which contributor roles should be named publicly?
4. What language should be avoided because it implies a single co-builder slot?
5. How should ETHConf follow-up route interested people into concrete next actions?

### Current direction

Use language such as “small core cohort of serious, self-directed contributors” rather than “the highest-priority contact is a co-builder.” Several serious contributors are welcome if they work on the trunk of UbU and can own bounded subsystems.

### Resolution

Solved by `UBU-D0093`, building on `UBU-D0078` and `UBU-D0085`. Public recruitment should invite a small core cohort of serious, self-directed contributors, not a single co-builder or privileged slot. Seriousness is distinguished by concrete public follow-up: workflow examples, design review, synthetic or redacted fixtures, parser or validation tests, model-committee artifact review, narrow implementation-ready issues, or repeated reviewed work on bounded subsystems.

Baseline public copy:

> UbU is looking for a small core cohort of serious, self-directed contributors. Good first contributions include workflow examples, design review, synthetic or redacted fixtures, parser or validation tests, model-committee artifact review, and narrow implementation-ready issues. If the work keeps the planning kernel inspectable, privacy-first, and useful for dogfooding, there is room for multiple contributors to earn bounded ownership over subsystems.

Public materials may name workflow informant, design reviewer, fixture/test contributor, implementation contributor, and bounded module owner as staged contributor roles. Prototype-funder or design-partner conversations may be routed through outreach, but they are not privileged contributor ranks.

Avoid phrases such as `the co-builder`, `highest-priority contact`, `one founding slot`, `only serious builder`, `competing for a role`, `exclusive inner circle`, `prove you belong`, and `hand-picked elite`. Casual interest should not be dismissed; it should be routed into workflow examples, design feedback, useful introductions, prototype-funder leads, public issue comments, or future contributor paths.

ETHConf and similar follow-up should classify interested people by one concrete next action: send a workflow example, review a model-committee artifact, comment on a public design question, contribute a fixture or test, take a narrow implementation-ready issue, introduce a serious contributor, or discuss a trunk-compatible prototype sponsorship. Enthusiasm alone is not validation until it becomes concrete follow-up.

---

## UBU-Q0042: Feedback, dignity, emotional limits, and growth pressure

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Affect-aware planning quality Resolved by: UBU-D0081, UBU-D0082, UBU-D0092 Last scored: Never Scored from commit: None

### Question

How should UbU model fast feedback, dignity, emotional limits, and growth pressure as part of plan quality?

### Subquestions

1. What observable signals show that a plan is succeeding or failing quickly enough?
2. How should UbU distinguish informative failure from humiliating or demoralizing failure?
3. How should UbU suggest improvement after failure without user-blaming?
4. How should UbU represent sustainable stretch versus destructive pressure?
5. How should affect-related plan fragility appear in risk reports?
6. How should plan quality account for whether a plan leaves the user better or worse off?
7. Which parts belong in Phase 1 and which are post-MVP?

### Current direction

A plan is not high-quality merely because it is internally consistent or time-feasible. High-quality plans should produce fast feedback, respect dignity and emotional limits, distinguish sustainable stretch from destructive pressure, and remain recalculable when reality contradicts the model.

### Resolution

Solved by `UBU-D0092`, building on `UBU-D0081` and `UBU-D0082`.

Phase 1 models human-complete plan quality as a derived, recalculable assessment over existing objects rather than a new first-class canonical object. Signals include feedback latency, checkpoint coverage, affect margin, failure pattern, stretch pressure, and expected post-plan state.

Informative failure is failure that improves future planning by exposing bad estimates, missing constraints, stale affect data, interruptions, dependency problems, or changed Objectives. Humiliating or demoralizing failure is indicated by repeated overload, late discovery, avoidable public exposure, dignity-risking presentation, or repeated disregard of observed limits.

After failure, UbU should suggest model repairs rather than user blame: smaller Tasks, added checkpoints, revised estimates, recovery, clarification, delegation, changed constraints, or Objective reconsideration. Failure should normally be presented as a failed plan assumption or changed world state unless the user records another interpretation.

Sustainable stretch is allowed when the Plan exceeds the user's baseline while preserving near-term feedback, recovery margin, and a plausible improvement path. Destructive pressure is a warning condition when the Plan depends on overriding observed limits, hides failure until too late, lacks recovery, or is expected to leave the user worse off.

Affect-related fragility appears in Phase 1 risk reports as derived findings such as stale affect data, affect constraint violation probability, repeated late-failure pattern, destructive-pressure warning, dignity/demoralization warning, and post-plan depletion warning. Richer growth models, personalized baseline learning, and UI-specific coaching language are post-MVP.

---

## UBU-Q0043: First technical essay claim, avoidances, and request

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Public outreach Resolved by: UBU-D0083, UBU-D0091 Last scored: Never Scored from commit: None

### Question

What should the first public technical essay claim, avoid, and request?

### Subquestions

1. Should the working title be “The Planning Kernel: Why Your Task Manager Is Lying to You”?
2. How should the essay explain affect-blind planning without using negative metaphors?
3. How should the essay distinguish UbU from task managers, calendars, project boards, and opaque AI assistants?
4. How should the essay explain LLMs as advisory rather than canonical planners?
5. How should the essay point to `model-committee` as visible dogfooding?
6. What single concrete next action should the essay request?

### Current direction

The essay should be problem-first, not a product brochure. It should argue that real planning requires explicit objectives, state transitions, dependencies, constraints, logs, uncertainty, affect, and recalculation.

### Resolution

Solved by `UBU-D0091`, building on `UBU-D0083`.

Use `The Planning Kernel: What Task Managers Leave Out` as the working title. Do not use `The Planning Kernel: Why Your Task Manager Is Lying to You` as the working public title because it is accusatory and weakens the humane, problem-first tone.

The essay should make the planning-kernel claim: task managers, calendars, project boards, and opaque AI assistants are useful projections, but they are not enough for real planning unless objectives, state transitions, dependencies, constraints, logs, uncertainty, affect, and recalculation are explicit.

The outline is:

1. Start with a concrete planning failure that a list, calendar, board, or opaque assistant cannot represent cleanly.
2. Explain affect-blind planning as human-incomplete planning, using terms such as affect-blind, emotionally incomplete, human-incomplete, mechanistic planning, or affect-insensitive planning.
3. Contrast adjacent tools: task managers record intended work, calendars allocate time, boards track status, and opaque AI assistants suggest plausible next steps, while UbU aims to model the planning kernel explicitly.
4. Explain LLMs as advisory systems that interpret, summarize, propose, critique, and generate fixtures, not as canonical planners.
5. Show `model-committee` as visible dogfooding: a constrained loop that reads canonical design state, proposes reviewable changesets, scores them, and preserves human-reviewed canonical authority.
6. End with one reader request for a concrete planning-kernel workflow example.

The essay should avoid product-brochure structure, negative metaphors for affect-blind systems, grandiose inevitability claims, privacy overclaims, scarcity-implying contributor language, and language implying that LLMs own the plan.

The concrete reader request is: send one real or carefully anonymized planning workflow that current tools cannot represent cleanly, including the objective, current state, dependencies, constraints, uncertainty, affect or energy limits, and the decision that needs recalculation.

Publication should happen outside the canonical design files, with links to the canonical design repo, one visible `model-committee` artifact or summary, and a public path for workflow-example submissions.

---

## UBU-Q0044: Long-arc project narrative without grandiosity

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Public narrative Resolved by: UBU-D0084, UBU-D0090 Last scored: Never Scored from commit: None

### Question

How should UbU present its long intellectual development history and recent LLM-enabled viability without sounding grandiose, unrealistic, or inevitable?

### Subquestions

1. How much of the long personal-development history should be public-facing?
2. How should UbU explain that LLM capabilities changed the feasibility frontier?
3. How should outreach communicate durable significance without overpromising world-historical impact?
4. Where should this narrative appear: essay, outreach, README, talks, or interviews?
5. What language should be avoided?

### Current direction

UbU may describe itself as a long-running personal and technical project whose time may now be arriving. Public language should remain grounded and prefer “could matter for a long time” over “will change the world.”

### Resolution

Solved by `UBU-D0090`, building on `UBU-D0084`.

Public materials may use the long arc, but only as compact context: UbU grew out of a long personal and technical effort, which explains commitment and design maturity. Detailed personal history belongs in essays, talks, and interviews when relevant; README and outreach copy should keep it brief and return quickly to current dogfooding and concrete next actions.

LLM-enabled viability should be explained as a practical change in the feasibility frontier. Modern LLMs make interpretation, summarization, proposal generation, review, fixture creation, and advisory automation cheap enough to help build and test an explicit planning kernel. They do not make UbU inevitable, and they do not replace the canonical planner, user sovereignty, or inspectable model.

Durable significance should be framed as a possibility to validate, not a promised outcome. Preferred language is `could matter for a long time`, `worth building carefully`, `the tools may finally be good enough for a narrow public version`, and `a serious attempt at privacy-first self-governance software`.

Avoid destiny, superiority, inevitability, totalizing, and world-historical claims, including `will change the world`, `inevitable`, `once-in-a-generation`, `the future of work`, `solves coordination`, `the only real solution`, `decades ahead`, `everyone will need this`, and `LLMs make this inevitable`.

This provides enough canonical guidance for final public copy in derived files without adding another narrative-blocking question.

---

## UBU-Q0045: Smallest prototype-funder workflow for independent technical consultants

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Prototype-funder discovery Resolved by: UBU-D0079, UBU-D0089 Last scored: Never Scored from commit: None

### Question

What is the smallest prototype-funder workflow for privacy-sensitive independent technical consultants and similar independent knowledge workers?

### Subquestions

1. What exact pain should the first funded prototype address?
2. Which inputs are required: calendar, GitHub, tasks, email, notes, invoices, or manual declarations?
3. What can be implemented without violating privacy-first architecture?
4. What output would be valuable enough to fund: daily plan, commitment-risk report, client-compartment view, or weekly review?
5. How should paid prototype work remain on the trunk of the personal self-governance product?
6. What price, prepayment, or sponsorship structure is plausible?

### Current direction

Independent technical consultants, freelance developers, security researchers, solo founders, independent academics, technical writers, and similar users are a leading commercial beachhead hypothesis because they combine privacy, multi-client complexity, deadlines, dependency management, and personal self-governance pressure.

### Resolution

Solved by `UBU-D0089`, building on `UBU-D0079`.

The smallest fundable workflow is a local client commitment-risk review plus next-day Plan for independent consultants. It addresses the pain of realizing too late that commitments across clients, deadlines, dependencies, availability, and energy no longer fit.

Required inputs are manual client/project declarations, commitments/deadlines, tasks, current availability, compartment labels, and a current or stale affect Snapshot. Calendar busy/free blocks and GitHub issue/PR refs are optional explicit imports. Full email, notes, invoices, and private documents are deferred unless represented as structural references or later privacy-preserving connectors.

The output is a compartment-aware weekly risk report paired with a next-day default Plan. It reports overcommitment, deadline risk, blocked/stale commitments, cross-client dependency pressure, and affect/energy risk without exposing client payloads across compartments.

Funded work remains on trunk by implementing reusable open-core structures: Objectives, Tasks, Compartments, Logs, Calendar/Plan generation, risk reports, and optional calendar/GitHub ingestion. Customer-specific templates, private imports, credentials, hosting, and support may remain commercial configuration.

Prototype-funder discovery should test prepaid design-partner offers: roughly USD 250-750 for a focused workflow review, USD 2,000-10,000 for a prototype sponsorship, or USD 1,000-3,000/month for a limited design-partner retainer. These ranges are discovery hypotheses rather than permanent pricing policy.

---

## UBU-Q0046: Public dogfooding artifacts for contributor credibility

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0036, UBU-Q0038 Blocks: Contributor recruitment Resolved by: UBU-D0077, UBU-D0086 Last scored: Never Scored from commit: None

### Question

What public dogfooding artifacts should `model-committee` expose to make UbU credible and actionable to potential contributors?

### Subquestions

1. Which run artifacts should be committed, linked, summarized, or ignored?
2. How should selected patches, review notes, and commit messages be presented?
3. How should public artifacts avoid leaking private reasoning or unsafe provider outputs?
4. What would convince a developer that the loop is real and reviewable?
5. How should artifacts connect to GitHub Issues or PRs?
6. How should failed or partially successful runs be shown without damaging credibility?

### Current direction

The project should show the dogfooding loop, not merely describe it. Artifacts should demonstrate that open questions become model-assisted proposals, reviewable patches, decisions, and updated canonical state.

### Resolution

Partially resolved by `UBU-D0077` and `UBU-D0086`; exact artifact publication policy remains open.

---

## UBU-Q0047: Minimum committed-contributor onboarding path

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Auto eligible Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Contributor recruitment Resolved by: UBU-D0078, UBU-D0086, UBU-D0088 Last scored: Never Scored from commit: None

### Question

What is the minimum onboarding path for serious, self-directed contributors who may join the small core cohort?

### Subquestions

1. What should a contributor read first?
2. What command should a contributor run first?
3. What first issue or fixture should a contributor touch first?
4. What architectural boundaries must be understood before implementation work?
5. How should contributors move from workflow informant to design reviewer to implementation contributor to module owner?
6. How can onboarding avoid requiring direct access to the project owner’s private context?

### Current direction

A contributor should be routed into bounded contribution paths: design review, workflow examples, test fixtures, implementation-ready issues, review of `model-committee` artifacts, and narrow implementation tasks.

### Resolution

Solved by `UBU-D0088`, building on `UBU-D0078` and `UBU-D0086`.

The minimum onboarding path is public, bounded, and fixture-first. A serious contributor should read the project overview/core principles, model-committee dogfooding material, Phase 1 demo criteria, GitHub dogfooding/projection rules, open-core boundary, Phase 1 Compartment baseline, design-process rules, and the accepted recruitment/outreach decisions relevant to their first task.

The first command should be a no-private-access local smoke check. For `model-committee`, the expected first command is `uv run model-committee doctor`, followed by a fake-provider or fixture-backed run/test when available. First tasks should touch synthetic or redacted workflow examples, fixtures, parser or validation tests, `model-committee` artifact review, public design review, or narrow implementation-ready issues with explicit acceptance criteria.

Before implementation work, contributors must understand the canonical/derived document boundary, advisory `model-committee` authority, v0.1 provider/network limits, no-auto-apply rule, GitHub-as-projection, LLM advisory boundary, Compartment and low-security-content promises, user sovereignty, mode boundaries, and open-core contributor surface.

Contributor progression runs from workflow informant to design reviewer to fixture/test contributor to implementation contributor to bounded module owner. Work that requires private project-owner context is not onboarding-ready; missing context should become a public issue, fixture, design note, or open question with sensitive details redacted or replaced by synthetic examples.

---

## UBU-Q0048: Funding offers incompatible with self-governance mission

Status: Solved Priority: MVP important Phase: Phase 1 Decision type: Governance Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Prototype-funder discovery Resolved by: UBU-D0079, UBU-D0080, UBU-D0087 Last scored: Never Scored from commit: None

### Question

What funding offers, consulting opportunities, or commercial prototypes would be incompatible with UbU’s self-governance mission?

### Subquestions

1. Which requested features would push UbU toward surveillance project management?
2. Which enterprise-dashboard features are incompatible with contributor sovereignty?
3. What funding terms would create unacceptable control or IP risk?
4. What crypto/tokenization requests should be rejected or deferred?
5. How should UbU distinguish acceptable prototype funding from distracting custom work?
6. What rules ensure paid work funds trunk features rather than distracting branches?

### Current direction

Funding is compatible only when it funds trunk features needed by the full personal self-governance product. Funding that requires surveillance, generic enterprise dashboards, centralized productivity telemetry, manager-first reporting, token-first coordination, or a pivot away from personal self-governance should be rejected or deferred.

### Resolution

Solved by `UBU-D0087`, building on `UBU-D0079` and `UBU-D0080`.

UbU may accept funding, consulting, sponsorship, prepayment, or prototype work only when it accelerates reusable trunk capabilities needed by the personal self-governance product and preserves user sovereignty, contributor sovereignty, privacy, and the open-core boundary.

Offers requiring surveillance project management, activity scoring, keystroke or screen monitoring, manager-first ranking dashboards, centralized productivity telemetry, exposure of affect or Compartment-protected data to managers or funders, generic enterprise reporting, token-first coordination, speculation-first crypto positioning, or bespoke private branches are incompatible.

Funding terms are incompatible when they require funder control over the roadmap or canonical design process, exclusive ownership or proprietary relicensing of open-core work, private replacement components for public dogfooding capabilities, confidentiality that prevents honest public explanation of constraints, or a pivot away from privacy-first personal self-governance.

Crypto, tokenization, and DAO-specific requests should be rejected when token-first or speculation-first, and deferred when merely integration-specific rather than needed for the personal self-governance trunk.

Paid work should be trunk-first by default. Customer-specific configuration, hosting, support, packaging, compliance, or proprietary connectors may remain commercial only when they stay outside the open-core boundary and do not become required for public dogfooding.

---

## UBU-Q0049: Release Outreach Pipeline artifact model and implementation boundary

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0030, UBU-Q0036, UBU-Q0038 Blocks: Release Outreach Pipeline implementation, release communication, contributor recruitment Resolved by: UBU-D0094 Last scored: Never Scored from commit: None

### Question

What is the minimum useful artifact model and implementation boundary for the Release Outreach Pipeline?

### Subquestions

1. What files and metadata should a release outreach package contain?
2. How should screenshots, UI-test exports, fixture captures, and demo recordings record provenance?
3. What schema should distinguish implemented behavior, mock behavior, future plans, and speculative goals?
4. What human approval gates are required before video rendering, platform upload, public posting, or external channel mutation?
5. How should Compartment, Identity, public-projection, and export rules prevent private data leakage?
6. Which parts of the pipeline belong in Phase 1 dogfooding and which should remain post-MVP?
7. How should project configurations define audience-specific communication Objectives?
8. Which video-generation tools or local renderers should be treated as Automation Workers versus external publication systems?

### Current direction

`UBU-D0094` accepts the feature bundle and tagline: "UbU should make every release explain itself." The minimum path should start with manually reviewed release outreach packages generated from repo state, release notes, accepted decisions, closed issues, and approved screenshots. Full automated video generation and publication should be deferred until the artifact schema, provenance model, privacy gates, and review workflow are explicit.

### Resolution

Partially established by `UBU-D0094`; detailed artifact schema, implementation boundaries, provenance requirements, and review gates remain open.

---

## UBU-Q0050: Minimum Phase 1 bootstrap interview and next-action focus UX

Status: Solved Priority: MVP blocker Phase: Phase 1 Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: None Blocks: Phase 1 public demo, nontechnical onboarding, mock app prototype, Release Outreach Pipeline demo scripts Resolved by: UBU-D0129 Last scored: Never Scored from commit: None

### Question

What is the smallest useful Phase 1 bootstrap interview and next-action focus mode that demonstrates UbU’s user-facing value without overclaiming personal-data ingestion, therapeutic authority, or complete planning automation?

### Subquestions

1. What exact questions should the Phase 1 bootstrap interview ask?
2. Which answers become Objectives, Preferences, Snapshots, Tasks, Logs, or UniverseState facts?
3. What minimum data is required to recommend one next Task?
4. What must the “why this matters now” explanation include?
5. What controls must the next-action screen expose: start, done, snooze, reject, decompose, explain more, or override?
6. How should the UI preserve full-Plan inspectability while defaulting to one-task focus?
7. What feedback should UbU collect after completion, failure, rejection, or override?
8. How should the Phase 1 mock app distinguish hardcoded/fixture behavior from implemented planning behavior?
9. How should this loop appear in Release Outreach Pipeline videos and public demos?
10. What claims must public materials avoid until broader integrations exist?

### Current direction

The Phase 1 UX should be narrow, explicit, and dogfooding-centered. It should ask a few bootstrapping questions, collect or refresh a simple affect Snapshot, create an initial Objective/Task seed set, generate a candidate Plan, and show one recommended next Task with an explanation. The mock app may be fixture-backed, but the canonical Phase 1 implementation should ground the recommendation in explicit UbU objects and Logs.

The UI should not imply that UbU already understands all of the user’s emails, texts, files, and personal life. Broad personal-data ingestion is future work unless separately implemented and disclosed. The first version should prove the experience: “UbU can recommend one meaningful next action and explain why.”

### Resolution

Solved by `UBU-D0129`, refining `UBU-D0096` and `UBU-D0102`. The Phase 1 bootstrap interview asks eight narrow questions: what the user is trying to move forward, which project context to use, available work-window time, relevant deadline or external event, work to consider first, current blockers or exclusions, current energy/stress/mood, and the tradeoff UbU should favor today.

Answers map only into existing Phase 1 objects. Project context, availability, deadlines, constraints, fixtures/imports, and blockers become UniverseState facts, External Events, Tasks, External References, or Logs. Affect answers become a user-declared Snapshot or an affect-collection Task when skipped/stale. Initial work answers seed Objectives and Tasks. Tradeoff answers become Preferences only after explicit user acceptance; otherwise they remain Log notes, Objective annotations, or noncanonical review evidence.

The minimum recommendation data is a user/operator Identity, at least one active Objective, at least one active schedulable Task linked to that Objective, a current work window, current or explicitly stale affect state, and known blockers/deadlines/dependencies/source references when available. If this is missing, UbU recommends clarification, import, Calendar preview, Log review, or affect collection rather than pretending to optimize.

The next-action screen shows one Task by default with title, Objective link, estimated duration or work window, status, provenance/source label, why it matters now, and what UbU considered. The explanation includes served Objective, timing reason, dependency/blocker status, affect or stale-affect status, and the most relevant risk or opportunity. Full Plan inspection remains one action away through an inspector showing ordered Tasks, assumptions, source links, and explanation fragments.

Required controls are `start`, `done`, `snooze`, `reject`, `decompose`, `override`, and `explain more`. Completion, failure, snooze, rejection, and override each collect lightweight reason/effect/estimate/affect feedback, write Logs, and trigger recalculation when modeled state changes. Failure, rejection, and override are treated as model evidence, not user blame.

Fixture-backed and mock-app behavior must be labeled at the point of use. Public demos and Release Outreach Pipeline scripts should show bootstrap, one recommended next Task, explanation, feedback, recalculation, and full-Plan inspection while distinguishing implemented planner behavior from fixture or hardcoded behavior. Public materials must avoid claiming broad personal-data ingestion, complete email/text/file understanding, therapeutic care, autonomous life coaching, complete planning automation, complete privacy isolation, Phase 2 sync, or Phase 3 multi-user coordination.

---

## UBU-Q0051: Minimum preference-calibration examples for Phase 1 onboarding and review

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0050 Blocks: Phase 1 onboarding quality, Preference calibration, Calendar preview, Log review Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum useful set of preference-calibration examples for Phase 1 onboarding, Calendar preview, and Log review?

### Subquestions

1. Which common situations should UbU use to emotionally ground early Preference judgments?
2. How many examples are enough for Phase 1 without making onboarding burdensome?
3. Which answers become Preferences, Snapshots, Logs, Objective annotations, or noncanonical review notes?
4. How should examples avoid leading the user toward an assumed value model?
5. How should calibration examples distinguish urgent value, emotional cost, social pressure, recovery value, and long-term importance?
6. How should UbU revise or retire examples that repeatedly fail to help the user make accurate judgments?

### Current direction

Preference calibration is MVP important but not an MVP blocker. UbU should use examples of common emotional costs, rewards, and tradeoffs to help users make better Preference statements. Examples are grounding aids, not canonical Preferences, unless the user accepts or edits them into canonical entries.

### Resolution

Open.

---

## UBU-Q0052: Discovery-mode action inference and override semantics

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0050 Blocks: Discovery mode, mobile sensor workflow, behavior reconciliation, habit-pattern inference Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum Phase 1 model for discovery mode, actual-action inference, and user override semantics?

### Subquestions

1. How does the user select discovery mode, pause it, exit it, and inspect what it collected?
2. Which mobile sensor, integration, quick-note, or app-state signals are acceptable Phase 1 discovery inputs?
3. How should UbU represent actual user action when it differs from the Calendar?
4. When does an override become a Log entry, Snapshot, Preference update, Task status change, Objective reconsideration, or unresolved review item?
5. What clarification prompt is required before treating repeated behavior as a habit pattern?
6. How should UbU reconcile undetailed or under-specified time periods without overclaiming certainty?
7. How should Discovery mode preserve user sovereignty and avoid covert surveillance semantics?

### Current direction

Discovery mode is a user-selectable workflow state available at any time, especially from the mobile app. It may gather evidence useful for later Log review and UbU-directed reconciliation, but inferred observations are not final truth until accepted, corrected, or otherwise handled according to user-visible rules.

### Resolution

Open.

---

## UBU-Q0053: Calendar preview and Log review psychological annotations

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0050 Blocks: Regular review Tasks, preview UX, Log review UX, psychological annotation boundary Resolved by: None Last scored: Never Scored from commit: None

### Question

What psychological annotations should Phase 1 Calendar preview and Log review collect, store, or report?

### Subquestions

1. What is the minimum recurring Calendar preview Task?
2. What is the minimum recurring Log review Task?
3. How often should these Tasks run by default, and how should the user adjust cadence?
4. Which annotations belong in canonical Logs, Preferences, Snapshots, Objectives, Tasks, or Reports?
5. Which annotations should remain noncanonical review notes?
6. Should autonomy, competence, relatedness, social pressure, attitude, subjective norms, perceived control, and expected execution be modeled directly or only through preview/review comments?
7. How should UbU ask useful consistency questions without becoming therapeutic, accusatory, or paternalistic?

### Current direction

Calendar preview and Log review are notable Tasks that should run regularly to ensure that UbU is correctly modeling the user's intended behavior, actual behavior, affective constraints, and Preference judgments. Self-determination theory and theory of planned behavior mostly inform these interface and reporting layers rather than Phase 1 core ontology.

### Resolution

Open.

---

## UBU-Q0054: Social identity theory impact on Identity, role, group membership, and mode switching

Status: Open Priority: Post-MVP Phase: Post-MVP Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0025 Blocks: Post-MVP multi-user Identity modeling, group-membership modeling, mode-switching policy Resolved by: None Last scored: Never Scored from commit: None

### Question

How should social identity theory affect UbU's Identity model, role model, group-membership model, and mode-switching semantics?

### Subquestions

1. How should UbU distinguish Identity as external presentation, permission boundary, social role, self-concept, group membership, and mode-switching context?
2. How should group membership affect Objectives, Preferences, disclosure, trust, and coordination behavior?
3. How should UbU represent in-group and out-group effects without hard-coding stereotypes or paternalistic judgments?
4. How should social identity interact with Compartments, Relationships, and organization-mode planning?
5. Which parts are needed for Phase 3 multi-user coordination and which remain later research?

### Current direction

Identity is already central to UbU. Social identity theory may require richer group-membership, salience, and role-switching semantics, but its impact is post-MVP and must not block Phase 1 implementation.

### Resolution

Open.

---

## UBU-Q0055: Social choice theory and collective decision legitimacy

Status: Open Priority: Post-MVP Phase: Post-MVP Decision type: Governance Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0025 Blocks: Post-MVP organizational governance, multi-user decision procedures, collective legitimacy Resolved by: None Last scored: Never Scored from commit: None

### Question

How should social choice theory affect UbU's model of collective decisions, organizational legitimacy, dissent, and exit?

### Subquestions

1. What collective decision procedures should UbU be able to represent?
2. How should UbU distinguish authority, consent, voting, delegation, consensus, veto, and exit rights?
3. How should collective Preferences or directives be aggregated without pretending they are one person's Preferences?
4. How should UbU preserve dissent, minority reports, or unresolved disagreement?
5. What minimum governance semantics are required for Phase 3 multi-user / Identity coordination?
6. Which social-choice impossibility or legitimacy problems should UbU surface rather than hide?

### Current direction

Social choice theory is post-MVP. UbU should eventually model collective decision legitimacy explicitly for organizations and multi-user coordination, but Phase 1 should remain single-user dogfooding.

### Resolution

Open.

---

## UBU-Q0056: Game theory, strategic interaction, and counterparty modeling

Status: Open Priority: Post-MVP Phase: Post-MVP Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0025 Blocks: Strategic interaction modeling, counterparty incentives, post-MVP coordination protocols Resolved by: None Last scored: Never Scored from commit: None

### Question

How should game theory affect UbU's model of strategic interaction, counterparty incentives, commitments, and adversarial or cooperative behavior?

### Subquestions

1. Which strategic patterns can be represented through External Events and Techniques?
2. Which patterns require explicit strategic-interaction objects or counterparty models?
3. How should UbU represent credible commitments, signaling, free-riding, principal-agent problems, bargaining, and trust-but-verify workflows?
4. How should strategic reasoning interact with Identity, capability grants, Compartments, and external projections?
5. How should UbU avoid overconfident game-theoretic recommendations when the counterparty model is speculative?
6. Which strategic-interaction features are useful for FOSS coordination, skilled contributors, grants, issue triage, bug bounties, and future Skill Barter systems?

### Current direction

Many strategic patterns can be represented through External Events and reusable Techniques. Deeper counterparty modeling and strategic-interaction primitives are post-MVP research areas and should not block Phase 1.

### Resolution

Open.

---

## UBU-Q0057: Evergreen Dynamic Task and gap-filling semantics

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016 Blocks: Gap filling before Static Tasks, mobile next-action UX, Calendar preview quality Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU represent evergreen Dynamic Tasks or evergreen Objective-maintenance Tasks that can fill spare time when all predetermined Tasks before the next Static Task are complete, blocked, moot, or unsuitable?

### Subquestions

1. Are evergreen gap-fillers a Task subtype, a Task property, an Objective-maintenance pattern, a Technique-instantiation rule, or planner behavior?
2. What fields are required?
   - flexible start time
   - flexible duration
   - minimum useful duration
   - maximum useful duration
   - location invariance or broad location category
   - required materials or device state
   - affect suitability
   - cooldown/frequency limit
   - Objective link
   - recurrence/reactivation rule
3. How should UbU choose among evergreen candidates such as meditation, Calendar preview, Log review, lightweight cleanup, reflection, review queues, or relationship-maintenance prompts?
4. How should evergreen Tasks avoid becoming filler that crowds out recovery, transition time, or user autonomy?
5. How should the reactive branch layer consider evergreen Tasks when early completion creates a gap before the next Static Task?
6. Which evergreen semantics are necessary for Phase 1 and which can wait?

### Current direction

The planner should not leave the user with unexplained idle gaps merely because all predetermined Dynamic Tasks before a Static Task are complete. UbU should be able to suggest or schedule useful evergreen Dynamic Tasks when constraints allow, but the exact representation remains open.

### Resolution

Open.

---

## UBU-Q0058: Adaptive planning granularity and offline precomputation policy

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016 Blocks: Mobile-only planning, offline mode, low-power mode, Compact Calendar runtime policy Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU choose, switch, and explain Compact Calendar time delta, branch horizon, and branch coverage settings across full-detail, mobile, low-power, and offline execution modes?

### Subquestions

1. Should default deltas be exactly one minute, five minutes, and fifteen minutes, or configurable presets?
2. What user-visible explanation is required when UbU switches to a coarser delta?
3. Which triggers cause dynamic execution-mode switching?
   - low battery
   - thermal throttling
   - offline state
   - expected offline window
   - heavy workload
   - user setting
   - missing external worker
4. How much precomputation should UbU run before a known offline window?
5. How should cached plans expire after the user's actual behavior diverges from the precomputed branch?
6. What is the minimum mobile-only guarantee for preserving the core UbU experience?

### Current direction

Provisional defaults are one-minute full-detail delta, five-minute moderate mobile delta, fifteen-minute low-power/offline delta, one-hour reactive horizon, and `0.99` short-horizon branch coverage target. Mobile-only UbU must preserve the core experience, but may use coarser granularity, shallower branch coverage, reduced analysis depth, and fewer LLM-assisted features.

### Resolution

Open.

---

## UBU-Q0059: Execution-provider trust, worker backends, and privacy-preserving compute roadmap

Status: Open Priority: Post-MVP Phase: Phase 2 Decision type: Security Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016 Blocks: Phase 2 personal worker devices, hosted compute policy, third-party provider compatibility Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU define the trust, privacy, capability, API, and disclosure boundary for execution backends beyond the current local instance?

### Subquestions

1. What is the minimum Phase 2 personal worker protocol for a user-owned laptop, desktop, or server?
2. How should the planner route work among mobile, local desktop/laptop, personal worker, corporate cloud, and third-party provider backends?
3. What Compartment rules, PII stripping, encryption, redaction, and provenance are required before any external backend receives work?
4. What must be open-core so FOSS contributors can inspect, run, modify, and self-host the planning loop without a hidden service?
5. How should third-party UbU-compatible providers interoperate without being privileged over local execution?
6. Should dedicated personal worker appliances be treated as commercial packaging, reference hardware, or future product work?
7. How should future practical FHE-backed or comparable encrypted compute be prioritized if it becomes viable?
8. Should idle compute monetization be an external API-enabled user choice rather than an UbU corporate marketplace?

### Current direction

Cloud or external compute may improve performance, granularity, and analysis depth, but must not be a hidden mandatory dependency for the open-core planning loop. User-owned worker devices are Phase 2. Dedicated appliances, corporate cloud, third-party providers, compute monetization, and FHE/private encrypted compute are future commercial or strategic-research directions.

### Resolution

Open.


---

## UBU-Q0060: External/cloud LLM provider abstraction and routing policy

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0028 Blocks: LLM provider routing, cloud LLM disclosure, UbUCorp inference boundary, BYOK configuration Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum provider-neutral LLM routing model that supports local Ollama, user-configured BYOK cloud APIs, optional UbUCorp managed inference, user-owned remote workers, and future compatible providers while preserving Compartment policy and user sovereignty?

### Subquestions

1. What interface should normalize local and cloud model providers?
2. What provider metadata is required for location, cost, context window, capability, retention/disclosure profile, and safety behavior?
3. How should Compartment policy prevent `no_cloud_llm` or `no_external_export` payloads from crossing a provider boundary?
4. What context-minimization, redaction, and provenance fields are required before cloud routing?
5. How should BYOK mode store and scope provider credentials?
6. How should UbUCorp managed inference be represented without becoming a mandatory dependency of the open core?
7. What user-visible disclosure is required before a workflow uses a cloud LLM?

### Current direction

Cloud LLMs are optional execution providers, not the canonical planner. The FOSS core should remain local-capable, provider-neutral, BYOK-capable, and self-hostable. Cloud routing must be policy-governed, explicit, and advisory.

### Resolution

Open.

---

## UBU-Q0061: Association object model and lifecycle

Status: Open Priority: Post-MVP Phase: Phase 3 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0054, UBU-Q0055, UBU-Q0056 Blocks: Phase 3 multi-user coordination, Association reconciliation, future skill-barter systems Resolved by: None Last scored: Never Scored from commit: None

### Question

Should UbU introduce a first-class Association object, and if so what minimum fields describe an Identity-scoped perceived coordination structure without pretending that membership, authority, or boundaries are globally objective?

### Subquestions

1. What distinguishes an Association from an Organization Identity, Relationship, or External Reference?
2. Can an Association exist entirely inside one user's `user_mode` model?
3. What minimum fields describe perceived members, roles, shared Objectives, commitments, lifecycle, norms, confidence, and disclosure policy?
4. How should UbU represent informal groups such as friend groups, parties, amateur leagues, FOSS projects, conference cohorts, and skill networks?
5. How does an Association become formal enough to justify `organization_mode`?
6. How are invitations, exits, revocations, dormancy, and dissolution represented?
7. Which parts are required for Phase 3, and which remain later research?

### Current direction

An Association is an Identity-scoped, perspective-bound model of emergent coordination. Legal entities and institutional records are External References or evidence, not the whole Association.

### Resolution

Open.

---

## UBU-Q0062: AssociationAttestation provenance, trust, and dispute semantics

Status: Open Priority: Post-MVP Phase: Phase 3 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0061 Blocks: Association reconciliation, organizational introspection, pseudonymous reputation, multi-user trust Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU represent claims about Associations as attestations with provenance, confidence, disclosure policy, review status, and dispute or supersession semantics?

### Subquestions

1. What claim types are required: membership, non-membership, role, authority, commitment, objective, norm, governance rule, capability, reputation, relationship, priority, and dissolution?
2. What is the difference between a user-authored attestation, imported attestation, worker-generated candidate, and LLM-generated candidate?
3. What provenance is required for generated attestations: source locator, excerpt hash, timestamp range, model/prompt metadata, parser version, and Compartment?
4. How should an affected Identity or Association dispute, annotate, accept, reject, or supersede an attestation?
5. How should trust weights or confidence differ between public records, legal filings, signed descriptors, chat logs, meeting notes, and LLM interpretations?
6. How should private or permissioned attestations avoid leaking membership, role, or relationship facts?

### Current direction

LLM-generated AssociationAttestations are candidate claims. They must be reviewable, evidence-backed, confidence-scored, and never treated as authoritative social truth merely because they came from a large corpus.

### Resolution

Open.

---

## UBU-Q0063: Organizational introspection MVP/dogfooding workflow

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0046, UBU-Q0049, UBU-Q0050 Blocks: ETHConf follow-up, public dogfooding artifacts, organizational introspection demo Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum useful Phase 1 workflow for dogfooding organizational introspection on the UbU project itself without implementing full Association automation?

### Subquestions

1. Which UbU artifacts should be used as evidence: design files, open questions, decisions, issue fixtures, outreach notes, follow-up Tasks, and public retrospectives?
2. What structured output should be generated: candidate AssociationAttestations, mission-alignment questions, priority-drift observations, follow-up Tasks, and redacted retrospective notes?
3. How should UbU ask whether its actual outreach behavior proves commitment to its stated goals?
4. Which parts can be manual or fixture-backed in Phase 1?
5. How should public artifacts avoid exposing private notes or contact details?
6. What acceptance criteria show that UbU successfully applied organizational introspection to itself?

### Current direction

Phase 1 should use EthConf outreach and UbU project records as a manually structured dogfooding case. The result should be an evidence-backed retrospective and follow-up plan, not an automated surveillance system.

### Resolution

Open.

---

## UBU-Q0064: SharedAssociationDescriptor model and reconciliation boundary

Status: Open Priority: Post-MVP Phase: Phase 3 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0061, UBU-Q0062 Blocks: Multi-party Association coordination, formal project descriptors, public organizational introspection Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU represent a SharedAssociationDescriptor as a signed or reviewable shared artifact without turning it into a false global truth object?

### Subquestions

1. What fields belong in a descriptor: label, purpose, declared mission, public references, governance rules, participation criteria, disclosure policy, contribution paths, and signatures?
2. How should descriptors be versioned, superseded, forked, or disputed?
3. How should multiple Identities indicate acceptance, partial acceptance, rejection, or interpretation of a descriptor?
4. How should organizational introspection compare actual behavior to declared descriptors?
5. How should legal entity records and public registry references be linked as External References?
6. How should descriptors avoid implying that all affected members consented or that membership is objectively settled?

### Current direction

A SharedAssociationDescriptor is a coordination artifact. Multiple Identities may reference or sign it, but each UbU instance still maintains perspective-bound Association models and attestations.

### Resolution

Open.

---

## UBU-Q0065: Skill Barter marketplace and lawful private settlement boundary

Status: Open Priority: Post-MVP Phase: Post-MVP Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0054, UBU-Q0055, UBU-Q0056, UBU-Q0061, UBU-Q0062 Blocks: Future Skill Barter marketplace and delegated skilled-work features Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU model the Skill Barter marketplace as a future specialization of Association coordination and the Delegation Substrate without becoming token-first, speculation-first, platform-custodial, exploitative, or illicit-market infrastructure?

### Subquestions

1. What primitives are required: pseudonymous Identity, capability claims, reputation attestations, scoped work agreements, bonds, escrow-like commitments, dispute workflows, and settlement references?
2. Which payment rails can be represented as External References without UbU becoming a custodian or money transmitter?
3. How should privacy-preserving settlement options be described without implying sanctions evasion, tax evasion, illicit services, or unlawful use?
4. How should UbU distinguish skill barter, paid work, grants, bug bounties, volunteer passion-project work, human executors, agentic executors, and General Contractor coordination?
5. What public language must outreach avoid?
6. What lawful-use and safety boundaries are required before implementation?

### Current direction

The Skill Barter marketplace is a future cypherpunk/privacy-builder recruiting hook and product direction. It is a specialization of Association modeling and the Delegation Substrate, not the root concept and not a Phase 1 marketplace commitment. MVP-relevant work should focus on Delegation Substrate primitives that can later support Skill Barter.

### Resolution

Open.

---

## UBU-Q0066: Minimal Phase 3 Message Context Envelope schema

Status: Open Priority: MVP important Phase: Phase 3 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0061, UBU-Q0062 Blocks: Phase 3 cross-user communication, message priority triage, UbU-to-UbU interoperability Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum Message Context Envelope schema required for Phase 3 cross-user communication to support useful priority, interrupt, Task, Objective, and response triage without leaking excessive private context?

### Subquestions

1. Which fields are required for Phase 3: sender Identity, receiver Identity, source system, raw body, message kind, topic, priority, interrupt recommendation, response expectation, deadline, assumptions, ambiguities, provenance, confidence, disclosure policy, and Compartment?
2. Which fields may reference local-only objects without disclosing hidden identifiers or private Objective/Task details?
3. How should the sender specify whether the receiver may treat the message as a Task, status update, blocker, commitment, or FYI?
4. How should a receiver's UbU convert envelope metadata into Calendar interruption, communication review, or Task-creation suggestions?
5. What provenance and confidence markings are required when metadata is inferred rather than explicitly provided?
6. What minimum user controls prevent accidental disclosure of Relationship, Association, Objective, or Compartment state?

### Current direction

Phase 3 should include a small context-rich messaging envelope as a premier feature. The first useful version should prioritize message kind, topic, priority, interrupt recommendation, response expectation, assumptions, ambiguities, and provenance over deep relationship reconstruction.

### Resolution

Open.

---

## UBU-Q0067: Legacy communication adapter and UbU-to-UbU upgrade protocol

Status: Open Priority: Post-MVP Phase: Phase 3 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0066 Blocks: WhatsApp/SMS/Discord/IRC/Slack/email integration, viral interoperability, native contextual messaging Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU integrate with legacy messaging systems so a flat external message can be locally interpreted by one UbU instance, and upgraded into UbU-native contextual messaging when both sender and receiver use UbU?

### Subquestions

1. Which legacy systems should be represented first as examples: WhatsApp, SMS, email, Discord, IRC, Slack, Matrix, or other systems?
2. What transport patterns are acceptable: side channel, attachment, linkable External Reference, embedded metadata, shared relay, or explicit native UbU transport?
3. How should two UbU instances discover that both sides support richer contextual messaging without creating spam, surveillance, or platform-policy violations?
4. How should raw legacy messages remain human-readable while contextual envelopes remain machine-readable?
5. How should UbU handle one-sided use, where only the local user has UbU?
6. What consent, disclosure, and Compartment checks are mandatory before sending structured context to another user?
7. How should invitation flows encourage adoption without coercive or spammy viral loops?

### Current direction

UbU should define a stable internal message envelope first, then bind it to legacy transports through adapters. Legacy integration can become a value-led adoption path, but must preserve user consent, recipient respect, and privacy boundaries.

### Resolution

Open.

---

## UBU-Q0068: Structured message extraction schema, validation, and model strategy

Status: Open Priority: Post-MVP Phase: Phase 3 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0066 Blocks: direct-message ingestion, group-chat ingestion, communication-to-Task conversion, Association evidence extraction Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU implement the Message Context Extractor that converts unstructured direct-message and group-chat text plus available metadata into strict UbU JSON candidate structures?

### Subquestions

1. What input bundle should the extractor receive: raw message, source system, channel type, channel purpose, sender, receiver, Identity mapping, Association mapping, timestamp, thread context, Relationship history, and Compartment policy?
2. What output schemas are required: message classification, candidate Task, Objective link, priority, interrupt recommendation, actionability, assumptions, ambiguities, response expectation, confidence, and provenance?
3. How should validators and repair loops handle malformed JSON, invalid enum values, missing required fields, and overconfident inferences?
4. How should UbU distinguish explicit facts, channel metadata, thread inference, Relationship inference, Association inference, model guesses, and user-confirmed corrections?
5. Which extractor outputs can be accepted automatically, and which require user review?
6. When should UbU consider fine-tuned, distilled, or adapter-trained extractor models instead of general LLMs with strict schemas?
7. What training data and correction logs are needed before custom extractor models become justified?

### Current direction

Start with schema-constrained general LLMs or local models plus validation, repair, confidence, and provenance. Specialized extractor models are attractive later for privacy, latency, cost, and reliability, but should follow schema stabilization and labeled examples.

### Resolution

Open.

---

## UBU-Q0069: Personalized TTS, voice-profile descriptors, and anti-impersonation controls

Status: Open Priority: Post-MVP Phase: Post-MVP Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0066 Blocks: expressive asynchronous messaging, accessibility, voice-compressed communication Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU represent optional voice or pronunciation metadata so text messages can be rendered as sender-like speech without creating unacceptable biometric, deception, or impersonation risk?

### Subquestions

1. What is the difference between a pronunciation descriptor, a style descriptor, a local voice profile, and a transferable voice model?
2. Which forms should UbU allow to cross Identity, Device, Zone, Compartment, or user boundaries?
3. How should users opt in, revoke, rotate, or restrict voice descriptors?
4. What disclosure, watermarking, provenance, or UI indicators are required when speech is synthesized rather than actually recorded?
5. How should UbU prevent voice synthesis from being treated as authentication or proof that the sender literally spoke the words?
6. Are there narrow accessibility-first versions that could be implemented earlier without creating broad impersonation risk?

### Current direction

Voice descriptors are a promising post-MVP communication and accessibility feature. They should be consent-gated, compartmentalized, separated from authentication, and designed with anti-impersonation controls from the start.

### Resolution

Open.

---


## UBU-Q0070: Skeleton Plan failure diagnostics and user clarification flow

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0014, UBU-Q0015, UBU-Q0016 Blocks: robust planning failure handling Resolved by: None Last scored: Never Scored from commit: None

### Question

When skeleton Plan generation fails, what exact diagnostic payload and user clarification flow should UbU produce?

### Subquestions

1. Which failure classes are required for MVP: missing starting state, impossible dependency, cyclic dependency, Static Task collision, insufficient Calendar window, unavailable resource, blocked External Event, or unknown precondition?
2. How should UbU explain the failed causal chain without overwhelming the user?
3. Which alternatives can UbU safely suggest: relax deadline, remove Task, add prerequisite, mark state already satisfied, choose alternate Technique, extend planning horizon, or ask for manual decision?
4. When should this become an immediate blocking prompt instead of a normal planning warning?

### Current direction

Skeleton Plan failure is a critical model-consistency failure. UbU should not proceed as if the Plan merely needs optimization. It should explain the cause and request clarification or a user choice.

### Resolution

Open.

---

## UBU-Q0071: Legitimization and semi-legitimization cost model

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016, UBU-Q0053 Blocks: realistic candidate Plan search Resolved by: None Last scored: Never Scored from commit: None

### Question

How expensive is full legitimization, and what semi-legitimization heuristics are needed before full candidate validation?

### Subquestions

1. Which constraints belong to full legitimization versus cheap semi-legitimization?
2. Are affect budget, slack preservation, dependency fragility, user-mode compatibility, local repair, and legitimacy-delta estimates sufficient for MVP?
3. Is legitimacy binary, graded, or both?
4. How does the planner compare a high-value but brittle Plan against a lower-value but more humane Plan?
5. How are recuperative Tasks represented when they are required for Plan legitimacy rather than optional gap-filling?

### Current direction

The legitimized skeleton Plan is the baseline feasible Plan. If full legitimization is cheap, it can be used as a frequent validity oracle. If expensive, UbU needs approximate semi-legitimization before full validation of finalists.

### Resolution

Open.

---

## UBU-Q0072: GPU-aware planner kernels and solver selection

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016 Blocks: practical planner implementation, mobile/desktop/cloud execution profile Resolved by: None Last scored: Never Scored from commit: None

### Question

Which parts of UbU planning should use CPU-exact logic, and which parts should use GPU-friendly search, simulation, scoring, or learned-model inference?

### Subquestions

1. Which solver/library candidates should be evaluated for skeleton validation, finalist validation, contradiction diagnosis, and candidate optimization?
2. Which candidate expansion, stochastic simulation, affect scoring, and robustness scoring operations can be batched for GPU execution?
3. What are the mobile GPU targets for Android and iOS, and what CPU fallback is required?
4. What desktop/laptop GPU path is appropriate for power users?
5. What cloud GPU path is appropriate for premium wide-horizon planning?
6. How does UbU enforce the rule that GPU search may propose but exact/conservative validation must certify?

### Current direction

GPU suitability is a first-class solver-selection criterion. CPU logic should certify hard constraints and explanations. GPU-capable approaches should handle expensive candidate evaluation, stochastic robustness, affect scoring, and premium cloud planning where practical.

### Resolution

Open.

---

## UBU-Q0073: Mobile stewardship metadata and MVP repair rules

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016, UBU-Q0058 Blocks: mobile/local planning UX Resolved by: None Last scored: Never Scored from commit: None

### Question

What compact Calendar metadata and local repair rules are required so mobile UbU can preserve legitimacy and next-action clarity without full global optimization?

### Subquestions

1. What is the exact schema for protected, flexible, and disposable Task criticality?
2. What is the MVP schema for decision envelopes?
3. What conflict severity levels are required?
4. What explanation fragments should be cached with each Task or Plan segment?
5. What simple repair recipes are required for late Task, skipped Task, fatigue report, approaching Static Task, and missing prerequisite?
6. How is the last legitimate Plan stored and compared with current reality?
7. When should mobile ask the user, silently repair, or wait for desktop/cloud refinement?

### Current direction

Mobile should be a real-time steward of Plan legitimacy, user agency, and next-action clarity. MVP should include Task criticality, last legitimate Plan storage, simple repair rules, conflict severity, cached explanations, next-best-action mode, and basic decision envelopes.

### Resolution

Open.

---

## UBU-Q0074: Stochastic personality and affect-disruption model

Status: Open Priority: Research Phase: Post-MVP Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0053 Blocks: advanced affect-aware planning, personalized legitimization Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU model user personality, current affect, and likely desired planning style as stochastic parameters without claiming false precision or reducing user sovereignty?

### Subquestions

1. What are the minimal user-mode categories: deep work, rest, socialization, autonomy, structure, switching, recovery?
2. How should current affect shift candidate Plan probabilities or legitimacy scores?
3. When should mood/affect changes be treated like External Event-like disruptions?
4. How should ex post Log review update these distributions?
5. How can the user explicitly choose to become more like a different preferred planning/personality pattern?
6. How does UbU avoid manipulative nudging or pseudo-therapeutic overreach?

### Current direction

Stochastic personality modeling is plausible, but not required for MVP. The MVP can use explicit user inputs, conservative defaults, and Log review prompts before learning deeper distributions.

### Resolution

Open.

---

## UBU-Q0075: Optional VoxPopuli EthConf demo boundary

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0050, UBU-Q0068 Blocks: optional EthConf public demo Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the smallest safe optional VoxPopuli demo that lets a user describe an unstructured planning problem in natural language and review the LLM-produced structured UbU candidate output?

### Subquestions

1. What input prompt should invite open-ended user speech without implying therapeutic authority or full life modeling?
2. Which candidate outputs are safe to show: Objectives, Tasks, constraints, Preferences, assumptions, ambiguities, and suggested follow-up questions?
3. How does the UI show that LLM output is candidate structure, not canonical state?
4. What should be excluded from the demo to avoid overclaiming Phase 1 capability?
5. When should this be skipped so it does not displace higher-priority EthConf deliverables?

### Current direction

VoxPopuli is an optional EthConf/public demonstration and populist hook. It is not a replacement for the narrow Phase 1 bootstrap interview and should only be implemented if cheap relative to higher-priority dogfooding, contributor, and funder work.

### Resolution

Open.

---

## UBU-Q0076: Planning horizon, early-preparation bias, and short-horizon time discounting

Status: Open Priority: Research Phase: Phase 1 Decision type: Process Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0016, UBU-Q0051 Blocks: detailed planning horizon policy, premium planning horizon design Resolved by: None Last scored: Never Scored from commit: None

### Question

How far beyond the visible Calendar window should UbU look, when should prerequisite work be front-loaded, and when does time discounting become relevant to detailed planning?

### Subquestions

1. What is the default internal look-ahead for a one-day visible Calendar?
2. When should a dependency chain be scheduled early rather than just in time?
3. What makes a prerequisite chain fragile enough to justify early preparation?
4. Should one week be the default upper bound for detailed local planning?
5. Which longer-horizon plans belong to premium cloud, user-owned worker, or research modes?
6. When should explicit temporal-discounting Preferences override the short-horizon zero-discount assumption?

### Current direction

The internal planning horizon may exceed the visible Calendar window. Fragile prerequisites should be completed as early as reasonably viable within short detailed horizons to avoid forced stressful choices later. For operational windows of one day to roughly one week, time discounting may usually be treated as negligible unless user Preferences say otherwise.

### Resolution

Open.

---

## Suggested Initial GitHub Issues

Create these first:

1. `UBU-Q0001`: Define Phase 1 MVP Scope Freeze
2. `UBU-Q0002`: Define GitHub Projection and Reconciliation Model
3. `UBU-Q0003`: Define GitHub ↔ UbU External Reference Model
4. `UBU-Q0007`: Define Automation Worker Identity and Capability Model
5. `UBU-Q0009`: Define Worker Mutation Request Schema
6. `UBU-Q0014` + `UBU-Q0015`: Define UniverseState Mutation and Precondition Schemas
7. `UBU-Q0016`: Define Compact Calendar planner grammar and execution profile
8. `UBU-Q0018`: Define Risk Reporting Primitives
9. `UBU-Q0019`: Define Recalculation Trigger Taxonomy
10. `UBU-Q0030`: Define Phase 1 Public Demo Criteria
11. `UBU-Q0036`: Define Committee Log and Provenance Format
12. `UBU-Q0038`: Define Changeset-Based Work Phase
13. `UBU-Q0039`: Define Prioritized Recursive Loop Semantics
14. `UBU-Q0040`: Define Question Decomposition and Design Burden Scoring
15. `UBU-Q0041`: Define public recruitment language for a small core cohort
16. `UBU-Q0042`: Define feedback, dignity, limits, and growth-pressure planning quality
17. `UBU-Q0043`: Define the first technical essay claim and concrete request
18. `UBU-Q0045`: Define the smallest prototype-funder workflow
19. `UBU-Q0046`: Define public dogfooding artifacts for contributor credibility
20. `UBU-Q0047`: Define minimum committed-contributor onboarding path
21. `UBU-Q0048`: Define commercial funding red lines
22. `UBU-Q0049`: Define the Release Outreach Pipeline artifact model and implementation boundary
23. `UBU-Q0050`: Define the minimum Phase 1 bootstrap interview and next-action focus UX
24. `UBU-Q0051`: Define minimum preference-calibration examples for Phase 1 onboarding and review
25. `UBU-Q0052`: Define discovery-mode action inference and override semantics
26. `UBU-Q0053`: Define Calendar preview and Log review psychological annotations
27. `UBU-Q0054`: Analyze social identity theory impact on Identity, role, group membership, and mode switching
28. `UBU-Q0055`: Analyze social choice theory and collective decision legitimacy
29. `UBU-Q0056`: Analyze game theory, strategic interaction, and counterparty modeling
30. `UBU-Q0057`: Define Evergreen Dynamic Task and gap-filling semantics
31. `UBU-Q0058`: Define adaptive planning granularity and offline precomputation policy
32. `UBU-Q0059`: Define execution-provider trust, worker backends, and privacy-preserving compute roadmap
33. `UBU-Q0066`: Define minimal Phase 3 Message Context Envelope schema
34. `UBU-Q0067`: Define legacy communication adapter and UbU-to-UbU upgrade protocol
35. `UBU-Q0068`: Define structured message extraction schema, validation, and model strategy
36. `UBU-Q0069`: Define personalized TTS, voice-profile descriptors, and anti-impersonation controls
37. `UBU-Q0070`: Define skeleton Plan failure diagnostics and user clarification flow
38. `UBU-Q0071`: Define legitimization and semi-legitimization cost model
39. `UBU-Q0072`: Evaluate GPU-aware planner kernels and solver selection
40. `UBU-Q0073`: Define mobile stewardship metadata and MVP repair rules
41. `UBU-Q0075`: Bound the optional VoxPopuli EthConf demo
42. `UBU-Q0076`: Define planning horizon, early-preparation bias, and short-horizon time discounting

---

## UBU-Q0077: Realtime interaction session and candidate update schema

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0025, UBU-Q0031, UBU-Q0068 Blocks: realtime model adapters, discovery mode, meeting capture, interruption handling Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum schema for realtime interaction sessions and realtime-derived candidate updates?

### Subquestions

1. Should realtime sessions be represented as Tasks, Events, Logs, sensor streams, `InteractionSession` objects, or a hybrid?
2. What candidate update types are required: interruption, task progress, affect signal, external condition change, clarification question, Plan deviation, Log candidate, Task candidate, or AssociationAttestation candidate?
3. How should UbU distinguish elapsed time noticed by a model from planner-valid Task, Calendar, or Log semantics?
4. What provenance and confidence metadata is mandatory for audio/video/text-derived observations?
5. Which realtime features are local-only, cloud-optional, or prohibited under sensitive Compartments?

### Current direction

Realtime models are optional interaction backends. They emit candidate updates. The planner, Logs, Compartment policy, and user-review rules decide what becomes canonical.

### Resolution

Open.

---

## UBU-Q0078: Interruption, escalation, and discovery-mode consent policy

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0052, UBU-Q0077 Blocks: realtime UX, discovery mode, short-horizon reactive repair Resolved by: None Last scored: Never Scored from commit: None

### Question

When may UbU interrupt, pause, escalate, or ask for clarification based on realtime or inferred conditions?

### Subquestions

1. What user-visible modes are required: off, text-only, voice session, discovery mode, meeting/logging mode, local-only mode, cloud-assisted mode?
2. What conditions justify interruption: imminent deadline failure, blocked Task, safety issue, unexpected external event, significant affect shift, or user-requested monitoring?
3. How should interruption policy avoid becoming surveillance, nagging, or emotional paternalism?
4. How should UbU record user overrides of interruptions and use them for future calibration?
5. What UI indicators must show active capture, routing, retention, and review status?

### Current direction

Realtime and discovery modes must be explicit and bounded. Interruption should preserve user sovereignty and Plan legitimacy rather than maximizing engagement or compliance.

### Resolution

Open.

---

## UBU-Q0079: MCP client/server capability and Compartment policy

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0028, UBU-Q0032, UBU-Q0060 Blocks: MCP-style integrations, external agents, Delegation Substrate APIs Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum MCP-style client/server integration boundary that lets UbU use external tools and expose narrow UbU capabilities without giving outside agents broad authority over the user's life model?

### Subquestions

1. Which UbU operations may be exposed as tools in Phase 1 or fixtures?
2. What capability fields are required: object scope, Objective subtree, Task set, operation kind, Compartment, Identity, time window, rate/cost limits, and review requirement?
3. How should external agents submit candidate updates rather than canonical writes?
4. How should tool calls be logged, audited, denied, retried, or rolled back?
5. What is the minimum developer-facing MCP fixture or adapter needed for dogfooding?

### Current direction

UbU should be both an MCP-style client and server, but every tool surface is bounded by user-owned policy, Compartment rules, capability grants, and review semantics.

### Resolution

Open.

---

## UBU-Q0080: Delegation Substrate MVP schema and self-reminder use

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0032, UBU-Q0060, UBU-Q0079 Blocks: Task delegation, Automation Worker assignment, solo Task formalization, future Skill Barter marketplace Resolved by: None Last scored: Never Scored from commit: None

### Question

What is the minimum Delegation Substrate schema that prepares Tasks for delegation while also helping the user perform solo Tasks more clearly?

### Subquestions

1. Which fields belong directly on Task versus a separate `DelegationPacket`?
2. What executor types are needed: self, local agent, remote/cloud agent, tool, human Identity, Association, General Contractor, or external provider?
3. What authority, evidence, privacy, expected-output, review, deadline, and escalation fields are required?
4. How should a solo Task use the same structure as a self-reminder without implying actual handoff?
5. Which subset is required for Phase 1 GitHub dogfooding and Automation Worker assignments?

### Current direction

The MVP should implement Delegation Substrate primitives where they support dogfooding, self-reminder clarity, and worker assignment. The full Skill Barter marketplace is not Phase 1.

### Resolution

Open.

---

## UBU-Q0081: General Contractor role and subdelegation semantics

Status: Open Priority: Post-MVP Phase: Phase 2 Decision type: Data model Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0080, UBU-Q0061 Blocks: multi-executor coordination, Skill Barter marketplace, larger Association workflows Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU model a General Contractor who coordinates multiple human, agentic, tool, or Association executors toward an Objective?

### Subquestions

1. What authority can a General Contractor receive and subdelegate?
2. How are subordinate Tasks, executors, evidence, and status reports linked?
3. What review rights does the user or originating Association retain?
4. How are budget, privacy, Compartment, tool, and settlement constraints propagated?
5. How does UbU prevent a General Contractor from becoming an unbounded agentic authority?

### Current direction

General Contractor is a first-class delegated coordination role. It is not an ordinary executor field. Subdelegation requires explicit authority, provenance, evidence, and review semantics.

### Resolution

Open.

---

## UBU-Q0082: Skill Barter marketplace outreach, privacy tech, and MVP boundary

Status: Open Priority: MVP important Phase: Phase 2 Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0065, UBU-Q0080, UBU-Q0081 Blocks: EthConf cypherpunk outreach, Skill Barter future roadmap, privacy-tech positioning Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU present the Skill Barter marketplace as an EthConf/cypherpunk outreach hook and future marketplace direction without over-scoping the MVP or implying token-first speculation?

### Subquestions

1. What is the cleanest language for voluntary coordination, sovereign identity, privacy, open markets, FOSS contribution, and pseudonymous capability?
2. How can Skill Barter attract younger developers with drive and time for FOSS contribution?
3. How should the marketplace direction connect to FHE, ZK, private reputation, private commitments, secure compute, and Ethereum-compatible privacy infrastructure?
4. What claims must be avoided in public outreach?
5. What is the smallest credible demo or diagram that shows the future direction while leaving Phase 1 focused on Delegation Substrate primitives?

### Current direction

Skill Barter is a future marketplace direction and “cool factor” outreach lane. It should not become a Phase 1 public marketplace commitment.

### Resolution

Open.

---

## UBU-Q0083: ContextBundle governance and long-context model routing

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Security Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0028, UBU-Q0060 Blocks: long-context LLM use, organizational introspection, repository/chat archive review Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU represent and govern context assembly for LLMs and agents, especially when long-context models can ingest large archives or repositories?

### Subquestions

1. What fields should a `ContextBundle` contain?
2. How should Compartments, Identities, Associations, retention policy, provider destination, and minimization rules be recorded?
3. When must the user approve a ContextBundle before routing it to a model?
4. How should UbU summarize context exposure after a run?
5. How should ContextBundles link to downstream candidate updates and Logs?

### Current direction

Context assembly is a privacy-relevant act. More context is not automatically better context.

### Resolution

Open.

---

## UBU-Q0084: Computer-use AgentAction and BackgroundProcess model

Status: Open Priority: MVP important Phase: Phase 1 Decision type: Architecture Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0031, UBU-Q0032, UBU-Q0060, UBU-Q0079 Blocks: background agents, scheduled agents, computer-use automation, prompt-injection controls Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU model computer-use agents and background processes that consume compute, credentials, money, privacy budget, or external authority without necessarily occupying user Calendar time?

### Subquestions

1. What fields belong in `AgentAction` versus `BackgroundProcess`?
2. How should triggers, recurrence, schedules, cost budgets, notification policy, and escalation be represented?
3. How should prompt-injection exposure be scored when agents consume webpages, messages, documents, or tool outputs?
4. What rollback or mitigation metadata is required for irreversible side effects?
5. Which background processes belong in the Calendar, and which should remain separate from user time blocking?

### Current direction

Computer-use and background agents are high-risk external actors. They require authority scopes, audit trails, rollback or mitigation paths, prompt-injection handling, and candidate-update semantics.

### Resolution

Open.

---

## UBU-Q0085: State-transition cockpit UX model

Status: Open Priority: Post-MVP Phase: Phase 2 Decision type: Product Auto-choice eligibility: Human approval required Importance score: TBD Automation-likelihood score: TBD Risk score: TBD Answerability score: TBD Depends on: UBU-Q0050, UBU-Q0077, UBU-Q0080 Blocks: post-MVP UX, generative UI, review workflows, candidate/canonical distinction Resolved by: None Last scored: Never Scored from commit: None

### Question

How should UbU evolve from Phase 1 one-next-Task focus into a state-transition cockpit without losing first-person legibility?

### Subquestions

1. What are the core state-transition screens: next Task, message reply, Log review, Plan repair, Delegation Substrate packet, agent action approval, AssociationAttestation review, organizational introspection, and projection publication?
2. How should candidate state differ visually from canonical state?
3. Where can generative UI be useful without becoming opaque or inconsistent?
4. What minimum cockpit elements should appear in Phase 1 explanations?
5. How should users inspect evidence, constraints, expected effects, authority, and rollback paths?

### Current direction

UbU should become a state-transition cockpit over time. Phase 1 remains the narrow one-next-Task proof.

### Resolution

Open.

