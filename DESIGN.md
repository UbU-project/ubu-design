# UbU Design

Status: Draft  
Repository: `ubu-design`  
Purpose: Canonical public design document for the UbU project

---

## 1. Overview

**UbU** is a privacy-first planning, coordination, and self-governance system.

UbU takes messy real-world inputs—tasks, calendar events, messages, external events, user preferences, physical/emotional state, and integration data—and turns them into explicit, inspectable, recalculable Plans.

UbU is not merely a task list or calendar application. It is intended to become a personal and organizational planning kernel: a system that models desired outcomes, constraints, risks, dependencies, available time, and human limitations, then helps determine what should happen next.

The first MVP is designed around **dogfooding**: using UbU to coordinate the design, development, release, and maintenance of UbU itself.

---

## 2. Core Principles

### 2.1 User sovereignty

The user is the final authority over what the user wants and what occurred.

UbU may recommend, infer, estimate, warn, and automate, but it must not override user sovereignty.

User overrides are authoritative, but not necessarily consistent. Two forms of consistency matter:

- **Logistical consistency**: hard consistency required by the data model and planner.
- **Philosophical consistency**: broader consistency between the user’s stated goals and actual behavior.

UbU may reject or require repair of logistical contradictions. Philosophical contradictions are allowed and may be surfaced later through reporting.

Example:

- A user cannot maintain an active preference cycle such as `A > B`, `B > C`, `C > A`.
- A user may state an Objective like “communicate more with X” and later ignore a message from X. That is philosophically meaningful, but not a data-model violation.

### 2.2 Explicit value

Value must be explicit in the UbU data model.

Value is attached to **Objectives** through user-defined **Preferences**. Numeric “utils” may be derived for plan scoring, but these are transient computational artifacts, not canonical facts about the user.

LLMs may estimate or suggest value-related structures, but AI-generated value is non-canonical unless accepted through UbU’s explicit model.

### 2.3 Explicit planning

Planning must remain explicit and constraint-based.

UbU should model:

- Tasks
- dependencies
- preconditions
- effects
- Objectives
- Preferences
- UniverseState
- Plans
- Calendars
- external events
- decision/recalculation triggers

LLMs may assist, but the canonical planning and decision logic must remain explicit and recalculable outside the LLM.

### 2.4 Privacy-first architecture

UbU is designed around privacy, local-first operation, compartmentalized data, multiple Identities, and user-controlled sharing.

Sensitive data must not leak merely because structural planning metadata is useful.

### 2.5 Affect-aware planning

Human beings are not machines.

In `user_mode`, affective state is part of the planning problem. Energy, stress, tiredness, mood, and related human limitations are constraints that planning must respect.

UbU should not assume that users can simply execute arbitrary work because a schedule says they should.

### 2.6 Dogfooding

UbU should be useful for managing its own development.

The Phase 1 MVP should coordinate UbU’s GitHub issues, pull requests, reviews, CI events, release milestones, design questions, and contributor interactions.

### 2.7 LLM boundary

LLMs are useful but bounded.

LLMs may serve as:

- planning oracles,
- advisory systems,
- screenshot/UI interpreters,
- external workflow assistants,
- value-reflection assistants,
- document summarizers,
- automation helpers.

LLMs must not be the canonical real-time decision engine.

Short-turnaround execution decisions should be computed by UbU’s explicit decision logic.

---

## 3. Model-committee dogfooding

UbU may use model-committee automation to help maintain its own design process.

The model committee is not the canonical decision engine. It is an advisory Automation Worker pattern that can:

- read the canonical design repo,
- identify unresolved questions,
- propose answers,
- critique alternatives,
- generate candidate patches,
- run consistency checks,
- estimate MVP readiness,
- rank remaining open questions,
- identify follow-up questions.

Accepted design state exists only when committed to the canonical design repo.

Model-committee automation has three expected lifecycle modes:

1. **Pre-MVP:** design-freeze assistant.
2. **MVP dogfooding:** repo-maintenance and planning worker.
3. **Post-MVP:** continuous design-governance assistant.

The goal is to accelerate implementation, not to create unlimited pre-implementation design work.

Model-committee automation must be bounded by a stop rule. It should recommend further design work only when that work has greater expected value than beginning or continuing implementation.

---

## 4. MVP Release Phases

### 4.1 Phase 1: Single-user GitHub dogfooding

A single user uses UbU to coordinate development of UbU itself.

Primary goals:

- import or observe GitHub issues, PRs, reviews, CI events, and milestones;
- represent them in UbU’s Objective/Task/Calendar model;
- generate useful Plans;
- update GitHub as a low-dimensional projection of UbU state;
- expose limitations and open questions through dogfooding.

### 4.2 Phase 2: Single-user multi-device synchronization

A single user runs UbU across multiple Devices / execution enclaves.

Phase 2 validates:

- local-first sync;
- partial replication;
- Zone and Compartment boundaries;
- device roles;
- conflict handling.

Design rubric:

> Phase 2 should feel like multi-agent coordination, but all agents happen to agree.

### 4.3 Phase 3: Minimal multi-user / Identity coordination

Multiple humans coordinate through explicit Identities, capabilities, limited disclosure, and commitments.

Phase 3 should enable coordination without surveillance or shared global truth.

---

## 5. Operating Modes

Each UbU instance runs in exactly one mode. Modes are mutually exclusive and cannot change after initialization.

### 5.1 `user_mode`

A personal UbU instance operated for an autonomous human user.

Properties:

- includes user affect modeling;
- represents personal Objectives and Preferences;
- may integrate with personal calendars, tasks, messages, sensors, and devices;
- supports personal Zones and Compartments.

### 5.2 `organization_mode`

An organizational UbU instance operated on behalf of a project or organization.

Important philosophical note:

An organization is not an autonomous human. Organization mode is shorthand for a human-operated planning system where the organization appears as a structure in UniverseState, directives, Identities, and Preferences.

Properties:

- does not model intrinsic affect;
- may use Preferences as organizational directives;
- may be run on a thin web/database host;
- may delegate work to Automation Workers;
- may expose a web UI;
- may eventually support classic user accounts and access control.

For MVP, all organization-mode users may be treated as admin-equivalent to avoid premature RBAC complexity.

### 5.3 `worker_mode`

A worker-mode instance performs delegated work assigned by another UbU instance.

A worker-mode instance is usually:

- one-device / one-enclave;
- daemon/service-oriented;
- administered through a web page and/or CLI;
- capable of running heavy compute or GPU workloads;
- externally represented as an Identity;
- assigned Tasks by a user-mode or organization-mode instance.

Worker mode may run on a local machine, a server, or a thin controller that starts/stops cloud compute resources.

---

## 6. Core Entity Summary

The core model includes:

- Objective
- Technique
- Preference
- WorkItem
- Task
- Container
- UniverseState
- Snapshot
- Plan
- Calendar
- Log
- Identity
- Relationship
- Zone
- Compartment
- Automation Worker
- External Event
- External Association

Some entities are implemented in MVP. Others are documented now to avoid future contradiction.

---

## 7. Objectives

An **Objective** is a desired or maintained state of the universe.

Examples:

- “Release UbU MVP”
- “Review open pull requests”
- “Maintain relationship with contributor X”
- “Collect affect information relevant to important usage”
- “Finish documentation draft”

Objectives are the canonical anchor for value.

### 7.1 Objective modes

An Objective has one of two modes:

- `one_time`
- `evergreen`

#### One-time Objective

A one-time Objective is completed once and does not reactivate.

#### Evergreen Objective

An evergreen Objective may become satisfied and later become active again.

Example:

- “Maintain clean kitchen”
- “Keep relationship with X warm”
- “Collect affect information”
- “Manage GitHub issue queue”

### 7.2 MVP Objective fields

Required:

- `objective_id`
- `title_or_description`
- `mode`
- `status`

Optional:

- `notes`
- `tags`
- `linked_container_refs`

Derived / transient:

- `derived_util_cache`
- predicted satisfaction
- observed satisfaction

Not present in MVP:

- linked Techniques
- explicit satisfaction field
- required provenance

### 7.3 Objective statuses

Candidate MVP statuses:

- `active`
- `satisfied`
- `completed`
- `abandoned`
- `invalid`
- `superseded`

Rules:

- `completed` applies to one-time Objectives.
- `satisfied` applies to evergreen Objectives.
- Evergreen Objectives may transition from `satisfied` back to `active`.
- One-time Objectives do not reactivate after completion.

### 7.4 Evergreen recurrence

Evergreen Objectives may include recurrence/reactivation behavior.

For MVP:

- default recurrence type: `maintenance_time_decay`
- recurrence may be represented as a static timespan or simple PDF-like field
- user declarations or authorized observations may modify satisfaction state

---

## 8. Preferences and Value

A **Preference** is a relation between Objectives.

Value is derived from Preferences, not directly authored as an absolute scalar.

### 8.1 Preference object

MVP fields:

- `objective_a`
- `objective_b`
- `order`
- `acquired_method`
- `acquired_date`
- `enabled`

`order` may be:

- `a_preferred_to_b`
- `a_indifferent_to_b`

`acquired_method` may include:

- `user_defined`
- `llm_estimated`

More detailed method metadata may be added later.

### 8.2 Ordinal rankings

Ordinal UI input compiles immediately into pairwise Preference objects.

The original ordinal ranking may be retained in the log, but Preferences remain pairwise in the canonical model.

### 8.3 Indifference

Indifference is explicit.

Indifferent Objectives are assigned equal derived util values.

### 8.4 Preference contradictions

Preference cycles are logistical consistency errors.

Example:

- `A > B`
- `B > C`
- `C > A`

UbU must query the user for resolution with high priority.

### 8.5 Derived utils

Derived util values are transient and may be cached on Objectives.

They must be treated as volatile and recalculated when needed.

Default MVP direction:

- active Preferences form a DAG of Objectives;
- indifference creates equal-util levels;
- least-preferred level receives util `1.0`;
- each higher level is multiplied by `√2`.

Util derivation is typically local to the Objective subset being compared in a single planning process.

---

## 9. WorkItems, Tasks, and Containers

### 9.1 WorkItem

A **WorkItem** is the abstraction over concrete work-like entities.

A WorkItem may be:

- Task
- Container
- possible future subtype

### 9.2 Task

A **Task** is a schedulable WorkItem.

Tasks may be:

- Static Task
- Dynamic Task

#### Static Task

A Static Task has fixed start and end times.

Examples:

- meeting
- class
- appointment

Static Tasks are included directly in Plans.

#### Dynamic Task

A Dynamic Task has flexible scheduling.

Dynamic Tasks may have:

- duration or duration PDF
- dependencies
- preconditions
- effects
- Objective link
- success probability
- affect delta
- expected cost

### 9.3 MVP Task schedulability invariant

A Task is schedulable in MVP if it has:

- stable ID
- Objective link
- duration or duration PDF
- active status
- title

Permitted:

- dependencies may be empty
- earliest-start may be absent
- due may be absent
- cost may be absent
- effect may be absent in exceptional cases

Tasks with no known modeled effect may be reportable as low-utility or “meaningless” for plan scoring.

### 9.4 Container

A **Container** groups WorkItems.

Containers are not directly scheduled in Plans. Plans contain Tasks.

A Container may represent:

- decomposed work
- preempted work
- Technique instantiation
- grouped child Tasks
- Super Automation workflow structure

Container completion is derived from child states.

A Container is complete when all child Tasks are either:

- completed
- moot

### 9.5 Moot

`moot` is a first-class terminal Task status.

It is functionally equivalent to completion for planning, but distinct for logs and reporting.

Candidate MVP moot reason codes:

- `externally_satisfied`
- `superseded`
- `delegated`
- `no_longer_relevant`
- `invalidated_by_world_change`
- `replaced_by_new_plan_structure`
- `user_declared_moot`
- `automation_obsolete`
- `duplicate`

---

## 10. Task Preconditions and Effects

### 10.1 Preconditions

Preconditions are deterministic constraints over UniverseState.

If preconditions are unknown or partially modeled, they are treated as absent in MVP.

MVP preconditions support:

- equality checks
- membership checks
- absence checks
- simple AND/OR logic

Numeric comparisons are not in MVP.

Failed preconditions should generally make a Task blocked, not invalid.

### 10.2 Effects

A Task effect describes predicted mutation of UniverseState if the Task succeeds.

MVP effect object:

- scalar success probability
- mutation list

If success probability is `1` or `null`, the effect is assumed to occur when the Task completes.

If a Task fails, UniverseState is unchanged in MVP.

### 10.3 Duration and success probability

Duration uncertainty and success probability are distinct.

A Task may have:

- fixed duration
- duration PDF
- scalar success probability on the effect object

Task duration PDFs likely use seconds as the canonical time unit in MVP.

---

## 11. UniverseState

**UniverseState** is a first-class object representing the modeled state of the world relevant to UbU planning.

For MVP, UniverseState is a lightweight shell with loosely typed facts and events.

### 11.1 MVP UniverseState fields

Core shell:

- `universe_state_id`
- `timestamp` or valid-at instant
- `facts`
- `numeric_values`
- `set_memberships`
- `event_markers`
- `source_summary`
- `confidence_summary` optional

### 11.2 UniverseState values

MVP value discipline:

- fact keys are free-form strings;
- default keys should use a lightweight namespace convention;
- values are text / JSON-like payloads.

A stricter ontology can be added later.

### 11.3 Mutation vocabulary

MVP mutations support:

- `set_fact`
- `clear_fact`
- `increment_numeric`
- `decrement_numeric`
- `add_membership`
- `remove_membership`
- `append_event_marker`

Exact mutation item schema remains open.

Recommended direction:

- target key: dotted string
- operation enum
- payload: JSON-compatible value
- optional note/source

---

## 12. Snapshots

A **Snapshot** is an observed state update.

User-declared and sensor-derived observations use the same object type.

MVP snapshot fields:

- `snapshot_id`
- `timestamp`
- `source`
- per-dimension or per-field values
- confidence

### 12.1 Snapshot precedence rule

- Latest observed snapshot overrides simulation on conflicting fields.
- User-declared snapshots are top-priority observations.
- Confidence is stored, but does not override explicit user declaration in MVP.

Snapshot application semantics remain partially open:

- patch vs full assertion
- immutable log behavior
- confidence per snapshot vs per field

---

## 13. Affect

Affect is core in `user_mode`.

Affect belongs to UniverseState.

Affect is not intrinsic to organizations or machines.

### 13.1 MVP affect dimensions

MVP uses simplified user-reportable dimensions:

- energy / tiredness
- stress level
- mood

Values are reported in the range `0.0` to `1.0`.

### 13.2 Mood

Mood is represented as:

- categorical trinary state:
  - `happy`
  - `sad`
  - `angry`
- intensity scalar from `0.0` to `1.0`

`interested/bored` is an independent derived dimension.

### 13.3 Affect snapshots

Affect snapshots are ordinary UniverseState data produced by user query.

They include:

- timestamp
- source: `user`
- per-dimension values

### 13.4 Affect confidence

In MVP, affect confidence decays with age.

Low confidence is determined by algorithm configuration.

Confidence is global across affect dimensions in MVP and may become per-dimension later.

### 13.5 Affect collection Objective

UbU may include an evergreen high-value Objective such as:

> Collect affect information relevant to important usage.

When affect data is missing or stale, the planning algorithm may create direct UI survey Tasks.

### 13.6 Affect constraints

Affect is a constraint-satisfaction concern.

Burnout / affect exhaustion is modeled as a constraint violation rather than a first-class Risk object in MVP.

---

## 14. External Events

An **External Event** is an instantaneous change in the universe.

External Events have no duration and can overlap Tasks.

External Events are not part of feasibility evaluation for an individual Plan in MVP.

Examples:

- GitHub issue comment
- PR opened
- CI failed
- user receives message
- train delay
- another user completes dependent work

External Events may trigger:

- logs
- Objective updates
- Tasks
- recalculation
- worker assignment

---

## 15. Plans and Calendars

### 15.1 Plan

A **Plan** is a finite ordered set of Tasks from a start time to an end time, satisfying Calendar Logic.

A Plan includes:

- Static Tasks
- Dynamic Tasks
- external events

A Plan does not directly contain:

- Containers
- Objectives
- Techniques
- Recipes

Those are logical/model relations outside the calendar-view layer.

### 15.2 Calendar

A **Calendar** is a group of possible Plans.

A Calendar has a default Plan.

The default Plan is the current best recommendation, not a commitment.

The user controls what actually becomes historical log.

### 15.3 Calendar Logic

Calendar Logic includes constraints such as:

- no overlapping Tasks;
- dependencies respected;
- temporal constraints respected;
- preconditions evaluated;
- affect constraints respected in user mode.

### 15.4 Gaps

Plans may contain gaps.

Gap time is discretionary.

For MVP, gap suggestions are UI suggestions outside the Plan. Future versions may instantiate Gap Tasks.

---

## 16. Compact Calendar

A compact Calendar is a transport/storage representation of a Calendar.

It is intended to efficiently represent a large set of possible Plans.

Compact Calendar support is considered important for MVP because it enables recursive self-analysis and transport between devices/workers.

### 16.1 Compact Calendar concept

A compact Calendar may include:

- Task set
- Static Tasks
- duration distributions
- Task success probabilities
- external-event trigger distributions
- stochastic grammar
- expansion threshold(s)
- coverage value

### 16.2 Coverage

Coverage belongs to the compact serialization, not the abstract Calendar.

Coverage represents the probability mass of possible futures covered by the compact representation.

### 16.3 Deterministic DFS direction

A compact Calendar may not need PRNG seeds.

Instead, a deterministic DFS expansion may explore likely branches using a probability threshold `p`.

Open questions remain:

- What is a DFS node?
- What does expansion add?
- What exactly does `p` mean?
- Is DFS sorted by probability, value, deadline urgency, or composite heuristic?

---

## 17. Logs

A **Log** is the canonical record of what actually happened in the universe.

A Log consists of timestamped entries recording:

- Task completion or failure
- External Events that occurred
- Observed Snapshots (user-declared or sensor-derived state)
- Objective status transitions
- Plan realizations
- Decisions made and by whom
- System recalculations

Logs are immutable once written, but may be annotated or corrected through new entries.

### 17.1 Log vs Plan

- **Plan**: a possible ordered sequence of future Tasks, representing prediction
- **Log**: a timestamped record of what actually occurred, representing reality

Plans are inherently multiple. Logs are singular and authoritative for the specific timeline that occurred.

### 17.2 Log and Feedback

Logs enable feedback loops. A Log records the gap between prediction and reality, enabling better future planning.

The comparison of Logs against Plans is essential for:

- detecting estimation errors
- updating probability models
- surfacing unmodeled constraints
- improving forecasting algorithms

---

## 18. Identities

An **Identity** is the external-facing communication and authorization surface.

Humans may have multiple Identities.

Organizations and workers are also represented through Identities externally.

UbU interacts with outside agents through Identities, not directly through metaphysical assumptions about humans.

Examples:

- personal identity
- family identity
- GitHub identity
- pseudonymous identity
- worker identity
- organization identity

---

## 19. Relationships

A **Relationship** is structured UniverseState data representing the relationship between two Identities.

MVP Relationship data includes:

- two identity refs;
- one identity controlled by the user;
- user-stated affect state toward the other identity;
- inferred/speculated affect state of the other identity toward the user.

Communication and maintenance metadata are not stored directly on Relationship in MVP. They may be accessed through Compartments or external storage.

Objectives attach to Relationships indirectly through UniverseState.

---

## 20. Zones, Devices, and Compartments

### 20.1 Device

A **Device** is an execution enclave, not necessarily physical hardware.

Examples:

- OS user profile
- container
- VM
- secure enclave

One physical machine may host multiple Devices.

### 20.2 Zone

A **Zone** is a workspace-like UbU instance context.

A Device belongs to one Zone.

A Zone may have many Devices.

Zones maintain explicit allowlists/denylists of Compartments, defaulting to deny.

### 20.3 Compartment

A **Compartment** is a first-class data containment object.

Compartments enforce hard invariants that the user cannot casually override.

Hard invariants may include:

- storage backend constraints
- device eligibility constraints
- identity disclosure constraints
- export/integration constraints
- retention constraints
- audit constraints

### 20.4 Sensitive content

WorkItems must remain structurally usable without dereferencing sensitive content.

Sensitive Compartment data should be referenced by link/reference, not embedded in WorkItem structure.

Un-compartmented content is treated as low-security and may require per-integration prompts.

---

## 21. Automation Workers and Super Automation

### 21.1 Automation Worker

An **Automation Worker** is a worker-mode UbU instance or compatible execution unit that performs delegated work.

Automation Workers may:

- run LLM queries;
- process photos or screenshots;
- label GitHub events;
- perform external API actions;
- run document analysis;
- submit authorized mutations to a canonical UbU instance.

A worker-mode instance is externally represented as an Identity. A model-committee worker is an Automation Worker that reads the canonical design state, runs local and cloud LLMs against a selected open question, synthesizes candidate answers, and proposes reviewable patches.

### 21.2 Worker mode

Worker mode:

- is one of the three mutually exclusive UbU modes;
- is usually daemon/service-oriented;
- may expose an admin web UI;
- may use CLI settings;
- often runs on GPU-capable hardware;
- may control cloud compute resources.

### 21.3 Super Automation

**Super Automation** is a product/UX pattern, not the technical name of the device.

Super Automation uses Automation Workers, local services, or external APIs to abstract away difficult external interactions from the user.

It may include:

- screenshot interpretation;
- user-mediated UI actions;
- GitHub processing;
- document parsing;
- API work;
- LLM-assisted workflow execution.

---

## 22. Organization Mode

Organization mode is an instance-wide option.

It is isolated from personal user-mode installations.

Organization mode:

- does not model intrinsic affect;
- may disable affect dimensions on Relationship objects;
- may use organizational Preferences as directives;
- may use authority-source metadata/logging;
- may delegate work to Automation Workers;
- may expose a web interface.

For MVP, roles/RBAC may be omitted and all users treated as admin-equivalent.

---

## 23. GitHub Dogfooding and Projection

GitHub is a projection of UbU state, not the source of truth.

UbU should be able to use GitHub as an interface for FOSS contributors while maintaining canonical state internally.

### 23.1 GitHub object mapping

Provisional mapping:

- GitHub Issue → one or more Objectives
- Objective → one or more GitHub Issues
- GitHub PR → External Event and/or analysis Objective
- Review request → Task
- CI failure → External Event and/or analysis Objective
- Milestone/release → Objective with Calendar detail
- Contributor comment → External Event and/or analysis Objective

### 23.2 Pipeline state

`pipeline_state` is distinct from `Objective.status`.

Candidate pipeline states:

- `unlabeled`
- `invalid`
- `under_specified`
- `valid_unprioritized`
- `unassigned`
- `in_process_awaiting_pr`
- `awaiting_review`
- `awaiting_ci`
- `complete`

### 23.3 GitHub projection

UbU may project data to GitHub through:

- labels
- issue body blocks
- comments
- milestones
- assignees

Recommended MVP rule:

> UbU should only write clearly marked UbU-managed labels, comments, or blocks, and treat all other GitHub edits as external events.

### 23.4 GitHub reconciliation

Missed GitHub updates are expected in MVP.

A reconciliation report should compare GitHub state against UbU state.

Possible comparisons:

- GitHub issues vs UbU Objectives
- GitHub labels vs `pipeline_state`
- GitHub comments vs event log
- PRs / CI vs external events

---

## 24. Risk Reporting

Risk is not a first-class object in MVP.

Risk is reportable from Calendar/Plan analysis.

Possible MVP reports:

- P90 completion time
- critical path
- deadline miss probability
- affect constraint violation probability
- low compact-calendar coverage warning
- dependency fragility
- worker failure / automation bottleneck

Plan scoring does not include explicit risk penalty in MVP.

Burnout / affect exhaustion is modeled as a constraint violation.

---

## 25. Recalculation Triggers

Candidate MVP recalculation triggers:

- `task_completed`
- `task_failed`
- `task_moot`
- `observed_snapshot`
- `affect_confidence_decay`
- `external_event`
- `github_update`
- `user_override`
- `elapsed_time`
- `low_compact_calendar_coverage`
- `worker_request`

Final trigger list remains open.

---

## 26. Current Major Open Questions

The major remaining questions are tracked in `OPEN_QUESTIONS.md`.

Key unresolved areas include:

- Phase 1 MVP scope **not yet frozen**
- Log structure and fields
- Worker identity/capability model
- Worker mutation request schema
- GitHub projection/reconciliation rules
- GitHub event triage
- UniverseState mutation schema
- Precondition schema
- Compact Calendar DFS grammar
- Risk reporting primitives
- Recalculation trigger taxonomy
- Container mutation semantics
- Moot reason-code taxonomy

---

## 27. Design Process

The GitHub repository is the canonical public design process for UbU.

Chat discussions and private notes may generate proposals, but accepted decisions become official only when reflected in this repository.

Design changes should be recorded as:

- updates to `DESIGN.md`,
- accepted decisions in `DECISIONS.md`,
- unresolved issues in `OPEN_QUESTIONS.md`,
- or GitHub Issues linked from `OPEN_QUESTIONS.md`.

The project should prefer explicit decisions over hidden assumptions.

### Canonical and derived project documents

For UbU design governance:

- `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md` are canonical design inputs.
- `README.md` and `OUTREACH.md` are derived public-facing projections.

Question-answering uses canonical files. Consistency checking includes derived files and patches them when they fall out of sync.
