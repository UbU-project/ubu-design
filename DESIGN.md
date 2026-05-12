# UbU Design

Status: Draft / active pre-MVP dogfooding  
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

### 2.5.1 Human-complete planning quality

UbU treats affect as a core part of planning, not a decorative wellness feature.

A plan that ignores fatigue, stress, boredom, motivation, emotional load, recovery, and dignity is not merely incomplete. It may become actively misleading.

A high-quality plan should:

- produce fast feedback about success or failure;
- make failure informative rather than humiliating;
- suggest revision after failure;
- respect the user’s dignity;
- respect emotional and physical limits;
- distinguish sustainable stretch from destructive pressure;
- help the user grow beyond current limitations when appropriate;
- remain recalculable when reality contradicts the model.

The goal is neither comfort-maximization nor coercive productivity. The goal is humane self-governance: disciplined action that respects the user’s emotional and physical reality.

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
- generate candidate changesets,
- run consistency checks,
- estimate MVP readiness,
- rank remaining open questions,
- identify follow-up questions.

Accepted design state exists only when committed to the canonical design repo.

Question rankings are derived planning metadata. They may guide the next committee run, but they are not canonical design truth.

Model-committee automation has three expected lifecycle modes:

1. **Pre-MVP:** design-freeze assistant.
2. **MVP dogfooding:** repo-maintenance and planning worker.
3. **Post-MVP:** continuous design-governance assistant.

The goal is to accelerate implementation, not to create unlimited pre-implementation design work.

Model-committee automation must be bounded by a stop rule. It should recommend further design work only when that work has greater expected value than beginning or continuing implementation.

The first implementation of this process is intentionally constrained by the v0.1 restrictions recorded in `DECISIONS.md`.

### 3.0 Current dogfooding status

`model-committee v0.1` is the first runnable bootstrap artifact for UbU’s dogfooding process.

It is not the full UbU planner, but it exercises the recursive project-governance loop: parse canonical state, check consistency, select answerable work, generate candidate changesets, score them, validate patches, and produce reviewable artifacts.

This establishes active pre-MVP dogfooding while preserving the rule that accepted design state exists only when committed to the canonical design repository.

The current strategic emphasis is to use visible dogfooding, contributor recruitment, and prototype-funder discovery to accelerate the trunk of UbU rather than to expand design philosophy indefinitely.

### 3.1 Codex-first provider model

`model-committee` v0.1 uses Codex CLI as the primary model provider.

The runtime calls `codex exec` for:

- primary work proposal generation;
- work scoring.

Codex outputs are schema-constrained. Prompts are passed through stdin. Final responses are written to JSON files. JSONL event streams and stderr output are preserved in run logs.

Codex is used only as a proposal and scoring provider in v0.1. It must not directly mutate canonical repo files. It produces JSON work proposals and score results. Patches are validated and selected by `model-committee`, then written as review artifacts.

Every runtime Codex call must pass `--skip-git-repo-check`.

`model-committee` does not pass deprecated `--disable web_search` flags. If Codex web search must be disabled, that is handled through Codex configuration or profile state outside `model-committee`.

Local Ollama models remain secondary work proposal providers. They provide local diversity, dissent, fallback, and offline review, but Codex is the required scoring provider for automatic patch selection in v0.1.

### 3.2 Changeset-based work phase

Model-committee automation should make implementation explicit.

After a selected question or problem is chosen, models may be asked to produce concrete changesets. A changeset may be a documentation patch, code patch, schema patch, or other explicit repo-state transition artifact.

Other models, or a designated scoring model, then score those changesets. The best changeset is selected and written as reviewable artifacts such as:

- `selected.patch`
- `commit_message.txt`
- `review.md`
- run logs

This prevents implementation from being hidden inside an external editor agent and makes the committee loop applicable to documentation changes, code changes, bug fixes, and future UbU implementation work.

VS Code or another editor may still be used for human review, but it is not part of the canonical committee loop.

### 3.3 Prioritized recursive loop

Model-committee automation is expected to evolve into a prioritized recursive loop:

1. **System-wide consistency check** verifies that the current project state is coherent.
2. **Question/problem prioritization selection** chooses the next work item only after consistency is known.
3. **Work** produces and scores concrete changesets.

Consistency has the highest priority because an inconsistent project state invalidates future planning.

Prioritization is second because it selects the next intended state transition.

Work is third because it should implement only a selected and justified transition.

This structure is intended to make `model-committee` an early dogfooding example of UbU coordinating its own development.

### 3.4 Consistency requirements

System-wide consistency checks should include both document consistency and logical consistency.

For `model-committee`, consistency checking should verify at least:

- canonical files exist and are parseable;
- question IDs are unique;
- decision IDs are unique;
- question dependencies point to existing questions;
- question dependencies do not contain cycles;
- `Resolved by` fields point to existing decisions or are explicitly unresolved;
- solved, decomposed, deferred, or superseded questions are marked consistently;
- question metadata satisfies the declared schema;
- derived documents do not contradict canonical files when derived-document checks are enabled.

A question should not be selected for ordinary answer/work execution if it has unresolved dependencies, unless those dependencies are answered in the same work item.

Blocked questions may still be selected for decomposition work when decomposition can produce replacement questions with fewer, simpler, or no dependencies.

### 3.5 Direct project directives

The UbU project may receive direct project-owner directives that are appended to `DECISIONS.md` as accepted decisions.

These directive decisions are treated as canonical once committed.

Directive decisions are a “word of God” mechanism for project governance, but they are still represented as explicit repo state rather than hidden chat context.

If a directive decision creates inconsistency, the next system-wide consistency check should detect it and convert the inconsistency into a problem report, question update, or work item.

### 3.6 Decomposition and design-burden reduction

Model-committee should not treat every increase in open-question count as failure.

A hard, ambiguous, or blocked question may be validly split into multiple simpler questions when the replacement questions are clearer, narrower, lower-risk, or easier to automatically answer.

This is especially valuable when a blocked question can be decomposed into replacement questions where at least one replacement question has fewer dependencies, simpler dependencies, or no dependencies.

The relevant metric is unresolved design burden, not merely raw open-question count.

A decomposition is bad when it creates more, harder, vaguer, or more coupled questions.

A decomposition is good when it exposes smaller answerable units and improves future automation.

### 3.7 Answerability-first prioritization

Question selection should use answerability as the first gate.

A question is eligible for ordinary work only if:

- it has no dependencies;
- all dependencies are solved;
- or all dependencies are being answered in the same work item.

After answerability is established, questions are ranked by:

1. automation-likelihood,
2. importance,
3. risk ascending.

Questions blocked by unresolved dependencies may be selected for decomposition rather than ordinary answering.

### 3.8 v0.1 provider and network boundaries

`model-committee` v0.1 is a narrow local Python CLI.

It may communicate only with:

- local Ollama `base_url`;
- Codex CLI subprocesses.

It must not call:

- GitHub;
- OpenAI APIs directly;
- Anthropic APIs;
- Gemini APIs;
- arbitrary HTTP URLs.

`httpx` may be used only for the configured Ollama `base_url`.

Codex must be invoked only through subprocess.

This no-network policy preserves the bootstrap architecture and prevents accidental API creep.

### 3.9 v0.1 testing and diagnostics

`model-committee` v0.1 should include fake provider mode for deterministic tests.

Fake provider mode should not call Codex or Ollama. It should load canned fixture responses, then run normal JSON validation, patch validation, scoring, selection, and artifact-writing logic.

`model-committee` v0.1 should also include a `doctor` command that checks the local environment:

- Python version;
- `git` availability;
- `codex` availability;
- required `codex exec` flags;
- Ollama reachability;
- configured Ollama model availability;
- required target repo files;
- runs directory writability.

A `version` command should print the installed `model-committee` version.

### 3.10 v0.1 authority boundary

`model-committee` v0.1 has advisory authority only. It may produce derived analysis and review artifacts, but it must not directly create accepted design state. Accepted design state exists only after an ordinary human-reviewed repo change is committed to the canonical repo.

The following actions may be automated in v0.1:

- read `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`;
- parse open questions and their metadata;
- run consistency checks over canonical files;
- rank answerable questions using answerability, automation-likelihood, importance, and risk;
- generate schema-constrained Codex work proposals and score results;
- collect Ollama work proposals as secondary proposal inputs;
- validate proposal JSON and candidate patches mechanically;
- select a patch only from mechanically valid proposals using a valid Codex score result;
- write run logs, review artifacts, selected patches, and commit-message suggestions.

The following actions require human repository review in v0.1:

- accepting a proposed answer as design state;
- applying, editing, or committing any candidate patch to canonical files;
- changing question status, priority, dependencies, or resolved-by metadata in the canonical repo;
- treating readiness estimates as release, scope-freeze, or go/no-go decisions;
- converting a proposed open question into canonical `OPEN_QUESTIONS.md` state;
- changing provider weights, quorum rules, or network/provider boundaries.

The following actions are outside v0.1 authority:

- direct OpenAI, Anthropic, Gemini, GitHub, or arbitrary HTTP API calls;
- auto-merge, auto-push, automatic PR creation, or GitHub mutation;
- automatic patch application to canonical repo files;
- allowing Codex CLI or Ollama providers to directly edit canonical repo files;
- internal manual override of Codex scoring or patch-selection failures;
- readiness-score writes to derived public files such as `README.md`;
- deriving canonical user value, project directives, or release commitments from model output alone.

Provider outputs are weighted by configured trust weights and observed reliability metadata, not by one-provider-one-vote counting. Static configured weights are sufficient for v0.1; adaptive weighting remains deferred.

Provider failures are logged as run events. A failure should record the provider, model, run phase, failure class, timeout or exit status when available, stderr/response artifact path when available, and whether quorum remained satisfied.

A valid v0.1 committee result requires at least one mechanically valid work proposal and a valid Codex score result. Two or more valid proposals are preferred but not required. Failed secondary providers do not invalidate a run when quorum is met.

Codex CLI authority differs from direct API authority because Codex is invoked only through `codex exec` as a subprocess provider. Codex outputs are proposal and scoring artifacts only. Direct OpenAI API authority is zero in v0.1 because direct OpenAI API calls are forbidden.

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

### 4.1.1 Phase 1 public demo criteria

The Phase 1 public demo should use real UbU GitHub issues or a frozen fixture captured from real UbU GitHub data when live access is unsafe, unavailable, or non-reproducible.

The smallest persuasive demo is an end-to-end single-user dogfooding loop:

1. import a curated set of UbU issues, PR/review/CI signals, and milestone context;
2. map those inputs into Objectives, schedulable Tasks, External Events, and traceable source links;
3. generate a Calendar with a default Plan for the next work window;
4. show why the Plan was chosen, including dependencies and worker assignment or worker status;
5. show user-mode affect constraints by applying a current affect Snapshot or by creating an affect-collection Task when affect data is stale or missing;
6. write or preview clearly marked UbU-managed GitHub projection labels, comments, or managed blocks;
7. show a risk summary covering at least deadline risk, dependency fragility, and worker or automation bottlenecks.

The demo must not require Phase 2 sync, Phase 3 multi-user coordination, full RBAC, a complete Compact Calendar UI, or autonomous remote GitHub mutation. If live GitHub writes are unsafe for the public recording, a dry-run projection is acceptable only when it shows the exact payload that would be written after human approval.

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

### 17.1 MVP Log entry fields

MVP Log entries use a shared event envelope. Required fields:

- `log_entry_id`
- `schema_version`
- `instance_id`
- `recorded_at`
- `effective_at`
- `event_type`
- `actor_identity_ref`
- `recorded_by_device_ref`
- `target_ref`
- `result`
- `event_payload`
- `provenance`

`recorded_at` is when UbU accepted the entry. `effective_at` is when the modeled event occurred and may be earlier for imported or reconstructed events. `target_ref` identifies the primary canonical object or imported External Event. `result` is one of `success`, `failure`, `partial`, or `not_applicable`. `event_payload` is JSON-compatible event-specific data.

Optional fields:

- `old_value`
- `new_value`
- `reason`
- `notes`
- `confidence`
- `related_plan_ref`
- `external_refs`
- `annotation_of`
- `correction_of`
- `idempotency_key`

`old_value` and `new_value` are used for mutation-like events and may be absent for observational, external-only, or compartment-sensitive records. `provenance` records the source kind and source reference; `confidence` is stored when the entry is inferred, sensor-derived, imported, or worker-submitted.

### 17.2 MVP Log event types

MVP event types are:

- `task_completed`
- `task_failed`
- `task_moot`
- `external_event_observed`
- `snapshot_observed`
- `objective_transitioned`
- `plan_realized`
- `decision_recorded`
- `recalculation_triggered`
- `worker_mutation_submitted`
- `worker_mutation_applied`
- `worker_mutation_rejected`
- `log_annotation_added`
- `log_correction_added`

All event types share the required envelope. Event-specific details live in `event_payload` and may be validated by event-specific schemas.

### 17.3 Immutability, annotation, and correction

Log entries are append-only. Annotation and correction never modify the original entry. They create a new Log entry with `event_type` set to `log_annotation_added` or `log_correction_added`, and with `annotation_of` or `correction_of` pointing to the original `log_entry_id`.

Corrections supersede interpretation of the original entry but do not erase the original historical claim. Later queries should resolve corrected views by following correction links.

### 17.4 Storage, retention, and query

Canonical Logs are stored per UbU instance. Device-local Logs or queues may exist as transport and audit buffers, but canonical history belongs to the instance; each entry records `recorded_by_device_ref` when known.

MVP retention is indefinite for canonical Logs. Archival may move old entries to colder local storage, but must preserve queryability and integrity. Deletion or redaction policies are governed by Compartment retention rules and remain post-MVP except where required by a hard Compartment invariant.

MVP query/search is index-backed over `recorded_at`, `effective_at`, `event_type`, `actor_identity_ref`, `target_ref`, `external_refs`, and correction/annotation links. Large histories should be queried by time-windowed, cursor-paginated APIs. Derived search indexes may be rebuilt from the append-only Log.

### 17.5 Automation Worker contributions

Automation Workers contribute to Logs through their worker Identity. A worker may submit events or mutation requests, but the canonical instance validates authority and writes the canonical Log entry. Accepted worker mutations create applied entries; invalid or unauthorized attempts create rejected entries.

Worker-supplied `idempotency_key`, provenance, evidence references, and confidence metadata are retained when available so duplicate submissions and stale worker results can be detected.

### 17.6 Log vs Plan

- **Plan**: a possible ordered sequence of future Tasks, representing prediction
- **Log**: a timestamped record of what actually occurred, representing reality

Plans are inherently multiple. Logs are singular and authoritative for the specific timeline that occurred.

### 17.7 Log and Feedback

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

Communication and maintenance metadata are not stored directly on Relationship in MVP. Cadence policy for "keep this relationship warm" lives on an evergreen Objective's recurrence/reactivation rule. Observed interactions live in Logs, External Events, Task history, or Compartment/external references, depending on source and sensitivity.

Objectives attach to Relationships indirectly through UniverseState. A relationship-maintenance Objective points at the Relationship or relationship-relevant UniverseState key, and its Tasks mutate ordinary UniverseState or append events; they do not add a special Relationship-maintenance schema in MVP.

Neglect risk is not stored on Relationship in MVP. It is a risk-report finding derived from the maintenance Objective's recurrence rule plus observed interaction history and current Plan state.

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

#### Phase 1 Compartment baseline

Phase 1 implements Compartments as explicit classification and routing guardrails, not as the complete Phase 2 multi-device containment system. The minimum Phase 1 promise is:

- Compartment-marked content stores a `compartment_ref` and is handled through references rather than embedded in ordinary WorkItem structure.
- A Compartment may declare `local_only`, `no_cloud_llm`, `no_external_export`, `allowed_integration_refs`, and `allowed_device_refs` policies.
- Content in a `no_cloud_llm` Compartment must not be sent to cloud LLM routes. Content in a `no_external_export` Compartment must not be exported, projected, or handed to workers except as redacted structural references.
- Other Compartment-marked content may cross a boundary only through an allowed route and a user-visible action. Boundary-crossing attempts that reach UbU are recorded in Logs as allowed or denied.
- In Phase 1, device eligibility is limited to the current single local Device / execution enclave and configured allowlists. Hardware attestation, cross-device partial replication enforcement, and cryptographic isolation are not MVP claims.
- Phase 1 does not promise automated retention deletion or redaction for Compartment content. Retention policies may be recorded, but enforcement beyond append-only Log retention is post-MVP unless separately implemented and disclosed.

Phase 1 public messaging must describe this as a minimal Compartment guardrail layer. It must not claim complete privacy isolation, complete retention enforcement, secure multi-device Compartments, or protection from a malicious local administrator.

### 20.4 Sensitive content

WorkItems must remain structurally usable without dereferencing sensitive content.

Sensitive Compartment data should be referenced by link/reference, not embedded in WorkItem structure.

Un-compartmented content is treated as low-security and may require per-integration prompts.

In Phase 1, un-compartmented content is explicitly labeled `security_level: low`. Low-security content may be used by configured integrations or cloud LLM-backed Automation Workers after a user-visible integration or worker action, but UbU must not market that content as compartment-protected.

### 20.5 Phase 1 local-first and cloud LLM disclosure

Phase 1 can honestly claim that canonical planning state, Logs, and source-linked project model data live in the local single-user UbU instance by default. It cannot claim Phase 2 local-first sync, conflict handling, partial replication, or secure multi-device Compartment propagation.

Phase 1 can honestly claim that cloud LLM usage is optional, explicit, and advisory. Cloud LLMs may be used by configured Automation Workers, Super Automation flows, or bootstrap tools such as model-committee, but they are not the canonical planner and must not receive `no_cloud_llm` Compartment content. When a workflow uses cloud LLMs on un-compartmented low-security content, the UI or run artifact must disclose that routing before or at execution time.

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

A worker-mode instance is externally represented as an Identity.

A model-committee worker is an Automation Worker pattern that reads canonical project state, runs Codex CLI and local Ollama proposal workflows against a selected open question or problem, produces candidate changesets, scores candidate changesets, and writes reviewable artifacts.

In v0.1, model-committee is still an external bootstrap tool rather than a fully integrated UbU worker-mode runtime component.

### 21.2 Worker mode

Worker mode:

- is one of the three mutually exclusive UbU modes;
- is usually daemon/service-oriented;
- may expose an admin web UI;
- may use CLI settings;
- often runs on GPU-capable hardware;
- may control cloud compute resources.

### 21.2.1 Worker-mode public UX

Worker-mode public UX is an administrative console for the worker operator, not the primary planning UI.

The first worker-mode screen should show:

- connection and identity status for the parent UbU instance;
- current service health and last check-in;
- active assignment, assignment queue, and retry/error state;
- granted capabilities and their scopes;
- recent Log submissions, mutation requests, and rejection reasons;
- local resource status, including GPU availability and cloud compute state when applicable.

The worker UI may expose detailed logs and operational controls, but it should default to summarized, redacted views. It must not expose Compartment-protected payloads, broader organization planning state, or personal affect data merely because the worker executed related work.

No worker-mode web admin UI is required for Phase 1. Phase 1 only needs enough visible worker assignment/status information for the GitHub dogfooding demo, which may be shown in the user-mode dogfooding UI, CLI output, or run artifacts.

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

### 22.1 Organization-mode public UX

Organization-mode public UX is a project operations dashboard for human operators of an organization or project instance.

The first organization-mode screen should show:

- pipeline state for imported/project WorkItems and Objectives;
- risk summary for current Plans, including deadline, dependency, and worker bottleneck risk;
- worker assignments, worker health, and pending mutation requests;
- GitHub projection and reconciliation status;
- recent decision, projection, and worker Log entries that need operator attention.

Organization mode may expose pipeline state, risk reports, worker assignments, and GitHub projection status as first-class public UI concepts. It should not expose personal user-mode affect surfaces, and admin-equivalent MVP assumptions must be labeled when no full RBAC is implemented.

No organization-mode web admin UI is required for Phase 1. The Phase 1 public demo may show organization-like project coordination data, but the required UI is the single-user dogfooding surface defined by the Phase 1 demo criteria, not a general organization console.

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

Contributor interactions may also be associated with a GitHub Identity and relationship-maintenance Objective when the user has explicitly modeled that contributor relationship. These imported events may update relationship-relevant UniverseState or satisfy/reactivate the maintenance Objective, but they do not directly rewrite private Relationship affect fields without user acceptance.

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
- relationship-maintenance neglect warning
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
- Model-committee work phase
- Model-committee prioritized recursive loop
- Model-committee question decomposition and answerability semantics
- Model-committee Codex provider behavior
- Contributor recruitment language
- Independent knowledge-worker prototype-funder workflow
- Public technical essay claim and request
- Public dogfooding artifact publication policy

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


### Current strategic posture

UbU has moved from pure design preparation into active pre-MVP dogfooding.

The project should now prioritize:

- visible `model-committee` dogfooding output;
- recruitment of a small core cohort of serious, self-directed contributors;
- prototype-funder discovery among privacy-sensitive independent knowledge workers;
- conversion of outreach into concrete next actions;
- implementation of trunk features needed by the personal self-governance product.

Further broad philosophical elaboration should generally be subordinated to implementation, recruitment, dogfooding, or market discovery.

Public-facing materials should avoid implying that there is only one meaningful contributor role. They should welcome several serious contributors while still distinguishing committed work from passive interest.

Public materials should also avoid negative metaphors when criticizing planning systems that fail to model affect. Preferred terms include affect-blind, emotionally incomplete, human-incomplete, mechanistic planning, or affect-insensitive planning.

### Contributor onboarding baseline

Committed-contributor onboarding should be public, bounded, and fixture-first. The minimum path is: read the project overview/core principles, model-committee dogfooding, Phase 1 demo, GitHub dogfooding, open-core, Compartment, and design-process sections; run the no-private-access local smoke command for the relevant repo; make a small public contribution; then earn broader ownership through reviewed work.

For `model-committee`, the first command should be `uv run model-committee doctor`, followed by a fake-provider or fixture-backed run/test when available. The first task should touch a synthetic or redacted fixture, parser or validation test, model-committee artifact review, public workflow example, or narrow implementation-ready issue with explicit acceptance criteria.

Contributors should understand the core boundaries before implementation: canonical state lives only in committed canonical files; model-committee is advisory; v0.1 provider/network and no-auto-apply boundaries are hard; GitHub is a projection; LLMs are advisory; Compartment and low-security rules constrain data routing; and the open-core planning kernel must remain inspectable and self-hostable.

Contributor progression runs from workflow informant to design reviewer to fixture/test contributor to implementation contributor to bounded module owner. Work that requires private project-owner context is not onboarding-ready; it should be converted into a public issue, fixture, design note, or open question with sensitive details redacted or synthesized.

### Commercial funding red lines

Funding is acceptable only when it accelerates trunk capabilities needed by the personal self-governance product and preserves the user's authority over objectives, logs, plans, affect data, compartments, and external projections.

Acceptable prototype funding may pay for planning-kernel, local-first, privacy, Compartment, affect-aware planning, GitHub/calendar/task ingestion, Log, risk-report, worker, or projection features that generalize to the open core.

Incompatible funding includes requests for:

- surveillance-style project management, activity scoring, keystroke or screen monitoring, or always-on productivity telemetry;
- manager-first dashboards that rank, pressure, or compare contributors instead of helping a person or project operator govern commitments explicitly;
- centralized productivity telemetry across users, teams, clients, or contributors without explicit user-controlled sharing;
- generic enterprise dashboards that make UbU a conventional reporting layer rather than a self-governance planner;
- features that expose affect, private relationship data, Compartment payloads, or low-security personal context to managers, funders, or customers as a condition of use;
- token-first, speculation-first, governance-token, DAO-dashboard, or financialized coordination work that would reposition UbU as a crypto product;
- custom branches whose value depends on one funder's private workflow and would not become trunk capability.

Funding terms are incompatible when they require:

- funder control over the product roadmap, canonical design process, licensing boundary, or accepted decisions;
- exclusive ownership, assignment, or proprietary relicensing of open-core planning-kernel work;
- a closed-source replacement for functionality that public contributors need for ordinary dogfooding;
- confidentiality terms that prevent honest public explanation of architectural constraints, privacy limits, or contributor-facing behavior;
- urgency, deliverables, or support obligations that materially displace Phase 1 implementation, recruitment, or public dogfooding.

Crypto, tokenization, or DAO-specific requests should be rejected when they are token-first or speculation-first, and deferred when they are merely integration-specific rather than needed for the personal self-governance trunk.

Paid work should fund trunk features by default. When a funded prototype needs customer-specific configuration, that configuration should remain outside the core boundary unless it exposes a reusable open-core abstraction.

### Open-core and FOSS boundary

UbU treats the planning kernel and contributor-facing integration surface as the open core. A public contributor must be able to inspect, run, modify, and self-host the core system needed for ordinary single-user and project dogfooding without depending on private replacement components.

The definitely open-source surface includes:

- canonical data model schemas and migrations for Objectives, Preferences, WorkItems, Tasks, Containers, UniverseState, Snapshots, Plans, Calendars, Logs, Identities, Relationships, Zones, Compartments, External Events, External Associations, worker assignments, mutation requests, and projection state;
- explicit planner and Calendar-generation logic required for Phase 1 dogfooding, including constraint evaluation, recalculation triggers, compact Calendar serialization needed for transport or analysis, and MVP risk-report generation;
- GitHub import, triage, projection, reconciliation, fixture/demo tooling, and the managed-label/comment/block formats used for FOSS collaboration;
- worker-mode runtime surfaces required for delegated work, including Identity/capability checks, assignment, status, mutation request, and audit/log contribution APIs;
- local-first storage and sync protocols when implemented;
- the Super Automation extension/API boundary needed for third-party workers, connectors, or local services.

Private or commercial code may exist only outside that core boundary. Acceptable private areas include hosted-service operations, managed cloud infrastructure, paid support/packaging, premium hosted worker capacity, enterprise administration/compliance layers, proprietary connectors to closed third-party systems, and short-lived experimental prototypes that are not required for the public dogfooding loop.

Private experiments must not become hidden mandatory dependencies for public contributors. If an experimental component becomes necessary for the advertised open-source workflow, UbU must either open it before relying on it publicly or explicitly narrow the public promise.

Implementation repositories should use OSI-approved licenses. The default license for core implementation repos is MPL-2.0 so modifications to core files remain shareable while integrations can be built without relicensing unrelated code. Stronger copyleft may be considered for network-hosted service code, and permissive licensing may be used for small examples, SDK stubs, or interoperability fixtures when that better serves adoption.

Contributor trust requires clear labeling of each repository or package as open core, private experiment, premium hosted service, or external connector. UbU should not recruit FOSS contributors around a capability that depends on an undisclosed private substitute for the open implementation.

### Canonical and derived project documents

For UbU design governance:

- `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md` are canonical design inputs.
- `README.md` and `OUTREACH.md` are derived public-facing projections.

Question-answering uses canonical files. Consistency checking includes derived files and patches them when they fall out of sync.

### Directive decisions

Direct project-owner directives may be appended to `DECISIONS.md` as accepted decisions.

Directive decisions are canonical once committed.

They may override provisional decisions, create new questions, close questions, split questions, or require consistency repairs.

The model-committee process must treat directive decisions as authoritative input during the next system-wide consistency check.
