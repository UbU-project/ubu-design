# UbU Decisions

Status: Draft  
Purpose: Lightweight architectural and data-model decision log for the UbU project.

This file records accepted design decisions so they do not need to be rediscovered from chat history. It is not a full specification. Details belong in `DESIGN.md`; unresolved matters belong in `OPEN_QUESTIONS.md`.

---


## UBU-D0001: GitHub repository is canonical for public design

**Status:** Accepted


The public GitHub repository is the canonical public design process for UbU.

Private chats, notes, and external documents may generate proposals, but accepted decisions become official only when reflected in the repository.

**Consequences:**


- `DESIGN.md` holds the current canonical design summary.
- `DECISIONS.md` records accepted decisions.
- `OPEN_QUESTIONS.md` records unresolved questions.
- Future chat interactions should generate proposed patches to these files rather than remain hidden sources of truth.

---


## UBU-D0002: Start public design documentation with four Markdown files

**Status:** Accepted


The initial public design repo should remain simple and LLM-friendly.

Initial files:

- `README.md`
- `DESIGN.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`

**Consequences:**


- Avoid premature documentation architecture.
- Avoid splitting the model into many files before public contributors can understand it.
- Keep the design easy to copy into LLMs for review.

This decision describes the initial repo structure. Later derived public-facing files such as `OUTREACH.md` may exist, but are not canonical design inputs.

---


## UBU-D0003: UbU is a privacy-first planning and coordination system

**Status:** Accepted


UbU is not merely a task list, calendar, or project-management dashboard.

UbU is a system for converting messy real-world inputs into explicit, inspectable, recalculable plans.

Inputs may include:

- Tasks
- calendar events
- messages
- external events
- user preferences
- physical state
- affective state
- GitHub/project data
- integration data

**Consequences:**


- Planning must be explicit.
- Value must be explicit.
- Constraints must be explicit.
- LLM behavior must not silently replace canonical planning logic.

---


## UBU-D0004: User sovereignty is foundational

**Status:** Accepted


The user is the final authority over what the user wants and what occurred.

UbU may recommend, infer, estimate, warn, and automate, but it must not override user sovereignty.

**Consequences:**


- User overrides are authoritative.
- LLM recommendations are advisory.
- AI-generated values are non-canonical unless accepted into UbU’s explicit model.
- User-declared state snapshots have top priority in MVP.

---


## UBU-D0005: Distinguish logistical consistency from philosophical consistency

**Status:** Accepted


UbU distinguishes:

- **Logistical consistency:** hard consistency required by the data model and planner.
- **Philosophical consistency:** broader consistency between stated user goals and actual behavior.

Logistical contradictions must be rejected, repaired, or resolved. Philosophical inconsistencies may be logged and reported later.

**Example:**

A cyclic active preference relation is a logistical contradiction. Ignoring a message despite an Objective to communicate more with someone is a philosophical inconsistency.

**Consequences:**


- The user may behave inconsistently.
- The data model may not remain logistically inconsistent.
- Reports may later reveal philosophical inconsistency.

---


## UBU-D0006: LLMs are bounded assistants, not the canonical decision engine

**Status:** Accepted


LLMs may assist UbU, but they are not the canonical real-time planner or decision engine.

LLMs may serve as:

- planning oracles,
- advisory systems,
- UI/screenshot interpreters,
- external workflow helpers,
- document interpreters,
- value-reflection assistants.

**Consequences:**


- Canonical Plans are owned by UbU, not the LLM.
- LLM-generated structures are advisory unless transformed into canonical objects through UbU logic.
- Short-turnaround decision loops must not depend on live LLM calls.

---


## UBU-D0007: Value is attached to Objectives

**Status:** Accepted


From a data-model perspective, value is anchored to Objectives.

Tasks may derive value from the Objectives they serve, but Tasks are not the canonical source of value.

**Consequences:**


- Every schedulable Task must link to an Objective.
- Ad hoc Tasks should still have an Objective.
- Temporary or one-task Objectives may exist if needed.
- LLM-suggested “valuable Tasks” should be modeled through Objective/Task pairs.

---


## UBU-D0008: Preference is a first-class relation object

**Status:** Accepted


Objective value is derived from Preference objects.

MVP Preference fields:

- `objective_a`
- `objective_b`
- `order`
- `acquired_method`
- `acquired_date`
- `enabled`

`order` may represent:

- Objective A preferred to Objective B
- Objective A and Objective B are equally preferred / indifferent

**Consequences:**


- Preferences may be pairwise or compiled from ordinal ranking input.
- Indifference is explicit.
- Disabled Preferences need no richer MVP structure beyond logging.
- Overridden Preferences are tracked through logs.

---


## UBU-D0009: Ordinal rankings compile into pairwise Preferences

**Status:** Accepted


If the user provides an ordinal ranking, UbU compiles it immediately into pairwise Preference objects.

The original ordinal input may be retained in the log, but the canonical value model uses pairwise Preferences.

**Consequences:**


- The canonical Preference graph remains simple.
- UI may choose pairwise or ordinal questioning.
- Value derivation algorithms operate on pairwise relations.

---


## UBU-D0010: Preference cycles are logistical consistency errors

**Status:** Accepted


Active cyclic Preferences are not allowed.

Example:

- A preferred to B
- B preferred to C
- C preferred to A

This is a logistical contradiction.

**Consequences:**


- UbU must query the user for resolution with high priority.
- LLMs may assist in identifying the problem but cannot decide the canonical correction.
- Cycles are not treated as indifference.

---


## UBU-D0011: Derived utils are transient computational artifacts

**Status:** Accepted


Numeric utility values may be derived from Preferences, but they are transient and volatile.

They may be cached on Objectives, but must be recalculated when needed.

**Consequences:**


- Derived utils are not canonical user values.
- Different algorithms may assign different util spacing.
- Util derivation may be local to the Objective subset under consideration.

---


## UBU-D0012: Default util spacing uses √2 per preference level

**Status:** Accepted as MVP default, subject to future revision


The default MVP util derivation assigns:

- `1.0` to the lowest preference level,
- each higher level multiplied by `√2`.

Indifferent Objectives are placed at the same level and receive equal util values.

**Consequences:**


- The topology of the Preference DAG determines ordering and equality.
- The exact spacing is algorithm-dependent and may change later.
- Plan scores can be sensitive to util-spacing choices.

---


## UBU-D0013: UbU has three mutually exclusive operating modes

**Status:** Accepted


Each UbU instance runs in exactly one mode:

- `user_mode`
- `organization_mode`
- `worker_mode`

The mode is chosen at initialization and cannot change afterward.

**Consequences:**


- Mode selection is instance-wide.
- Mode migration, if ever needed, is a separate process.
- Mode-specific behavior can be reasoned about cleanly.

---


## UBU-D0014: User mode models intrinsic human affect

**Status:** Accepted


`user_mode` is the mode for an autonomous human user.

Only user mode models intrinsic human affect.

**Consequences:**


- Affect belongs to the human user, not to Identities, organizations, or machines.
- User mode may include sensors, affect snapshots, personal Objectives, personal Preferences, and relationship data.
- Affect-related data requires strong privacy consideration.

---


## UBU-D0015: Organization mode does not model intrinsic affect

**Status:** Accepted


`organization_mode` represents an organization/project planning instance, but an organization is not a human.

Organization mode does not model intrinsic affect.

**Consequences:**


- Affect fields are absent or disabled.
- Organization Preferences represent directives rather than personal emotional value.
- Organization mode may still model human-related risks or external constraints through reports or imported data.
- MVP may treat all organization users as admin-equivalent.

---


## UBU-D0016: Worker mode is a special UbU mode for delegated work

**Status:** Accepted


`worker_mode` is a one-device or one-enclave UbU mode used by Automation Workers.

Worker mode may run as:

- a daemon/service,
- a local workstation process,
- a GPU-capable device,
- a thin cloud-control server,
- or another specialized execution environment.

**Consequences:**


- Worker mode is distinct from user mode and organization mode.
- Worker mode receives assigned work from other UbU instances.
- Worker mode is externally represented as an Identity.
- Worker mode may perform LLM calls, external API work, document processing, GitHub processing, or other delegated tasks.

---


## UBU-D0017: Automation Worker is the technical term; Super Automation is a UX/product pattern

**Status:** Accepted


An **Automation Worker** is the technical execution entity.

**Super Automation** is a product/UX pattern in which UbU abstracts away difficult external interaction by using local services, Automation Workers, APIs, screenshots, photos, or LLM processing.

**Consequences:**


- Super Automation is not limited to screenshot workflows.
- Automation Workers may support Super Automation but are not synonymous with it.
- The data model should use Automation Worker / worker mode terminology for technical structure.

---


## UBU-D0018: GitHub is a projection of UbU, not the source of truth

**Status:** Accepted


For dogfooding, GitHub is treated as a low-dimensional projection of canonical UbU state.

UbU is the source of truth.

**Consequences:**


- GitHub Issues, PRs, comments, labels, reviews, CI, and milestones must be interpreted into UbU objects/events.
- UbU may project selected state back into GitHub.
- External GitHub edits are external events, not authoritative canonical state by default.
- Missed GitHub updates require reconciliation.

---


## UBU-D0019: GitHub projection requires reconciliation

**Status:** Accepted


Missed GitHub updates are expected in MVP.

UbU should support a reconciliation report comparing GitHub state to UbU state.

**Consequences:**


- Resynchronization is an expected MVP concern.
- The reconciliation report may compare GitHub Issues, labels, comments, PRs, CI state, and milestones against UbU objects/events.
- Drift may create reports and/or Tasks for repair.

---


## UBU-D0020: Objective status and pipeline state are separate

**Status:** Accepted


`Objective.status` is the canonical UbU lifecycle status.

`pipeline_state` is a workflow/project-management status, such as a GitHub issue pipeline state.

**Consequences:**


- GitHub workflow states do not overload Objective lifecycle status.
- One Objective may eventually support multiple workflow states for multiple projections.
- Pipeline state is projection/workflow metadata.

---


## UBU-D0021: One GitHub object may map to many UbU objects and vice versa

**Status:** Accepted


GitHub ↔ UbU association is many-to-many.

Examples:

- One GitHub Issue may map to many Objectives.
- One Objective may map to many GitHub Issues.
- PRs, comments, reviews, and CI runs may associate with Objectives or Tasks.

**Consequences:**


- A simple one-to-one external reference field may be insufficient.
- A dedicated association model may be needed.
- Association/reconciliation remains an open design question.

---


## UBU-D0022: Objective has minimal MVP fields

**Status:** Accepted


MVP Objective required fields:

- `objective_id`
- `title_or_description`
- `mode`
- `status`

MVP Objective optional fields:

- `notes`
- `tags`
- `linked_container_refs`

Derived/transient Objective data:

- `derived_util_cache`
- predicted satisfaction
- observed satisfaction

Not in MVP:

- linked Techniques
- explicit satisfaction field
- required provenance

---


## UBU-D0023: Objective modes are one-time or evergreen

**Status:** Accepted


Objectives have mode:

- `one_time`
- `evergreen`

One-time Objectives complete once and do not reactivate.

Evergreen Objectives can become satisfied and later active again.

**Consequences:**


- Relationship maintenance, affect collection, GitHub issue management, and recurring maintenance can be modeled as evergreen Objectives.
- Evergreen recurrence/reactivation may be modeled through elapsed-time rules and UniverseState changes.

---


## UBU-D0024: Objective satisfaction is derived in MVP

**Status:** Accepted


Objective satisfaction is not stored directly on Objective in MVP.

It is inferred from:

- Task effects on UniverseState,
- observed Snapshots,
- user declarations,
- other modeled state.

**Consequences:**


- Objective satisfaction must be recalculated.
- Observed state can override simulated state.
- User-declared state has top priority in MVP.

---


## UBU-D0025: WorkItems include Tasks and Containers

**Status:** Accepted


A WorkItem is the abstraction over work-like entities.

A WorkItem may be:

- Task
- Container
- future subtype

**Consequences:**


- Tasks are schedulable.
- Containers group WorkItems but do not directly appear in Plans.
- Future WorkItem subtypes remain possible.

---


## UBU-D0026: Plans contain Tasks, not Containers

**Status:** Accepted


Plans contain an ordered array of Tasks.

Plans do not directly contain:

- Containers
- Objectives
- Techniques
- Recipes

**Consequences:**


- Containers remain logical/grouping structures.
- Plans are calendar-view objects.
- Preempted work can appear as multiple Tasks whose lineage is tracked outside the Plan.

---


## UBU-D0027: Static Tasks appear in Plans

**Status:** Accepted


Static Tasks are included directly in Plans.

**Consequences:**


- A Plan is a complete time-ordered view.
- Fixed meetings/appointments/classes appear alongside Dynamic Tasks.
- Static Tasks are not merely invisible constraints.

---


## UBU-D0028: MVP Task schedulability invariant

**Status:** Accepted


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

---


## UBU-D0029: Task preconditions are deterministic UniverseState constraints in MVP

**Status:** Accepted


Task preconditions are deterministic constraints over UniverseState.

MVP preconditions support:

- equality checks
- membership checks
- absence checks
- simple AND/OR logic

Numeric comparisons are not in MVP.

**Consequences:**


- Unknown or partially modeled preconditions are treated as absent.
- Failed preconditions should generally make a Task blocked, not invalid.

---


## UBU-D0030: Task effects mutate UniverseState

**Status:** Accepted


A Task effect describes predicted mutation of UniverseState if the Task succeeds.

MVP effect object contains:

- scalar success probability
- mutation list

If success probability is `1` or `null`, the effect is assumed to occur when the Task completes.

If a Task fails, UniverseState is unchanged in MVP.

---


## UBU-D0031: Duration uncertainty and effect success probability are distinct

**Status:** Accepted


A Task may have:

- fixed duration or duration PDF,
- scalar success probability on the effect object.

These are separate.

**Consequences:**


- Task duration uncertainty affects scheduling.
- Task success probability affects UniverseState simulation.
- A Task may complete yet fail to produce its modeled effect in MVP.

---


## UBU-D0032: UniverseState is first-class

**Status:** Accepted


UniverseState is a first-class data object.

MVP UniverseState is a lightweight shell with loosely typed facts and events.

Core fields:

- `universe_state_id`
- `timestamp` or valid-at instant
- `facts`
- `numeric_values`
- `set_memberships`
- `event_markers`
- `source_summary`
- optional `confidence_summary`

**Consequences:**


- Plans can simulate UniverseState changes.
- Objectives can be evaluated against UniverseState.
- Affect and Relationship data may live in UniverseState.

---


## UBU-D0033: UniverseState uses lightweight free-form keys in MVP

**Status:** Accepted


MVP UniverseState keys are free-form strings.

Default keys should use a lightweight namespace convention, but enforcement is post-MVP.

Values may be text / JSON-like payloads.

**Consequences:**


- MVP remains flexible.
- A stricter ontology can be added later.
- Namespacing should be encouraged but not enforced.

---


## UBU-D0034: UniverseState mutation vocabulary

**Status:** Accepted


MVP mutations support:

- `set_fact`
- `clear_fact`
- `increment_numeric`
- `decrement_numeric`
- `add_membership`
- `remove_membership`
- `append_event_marker`

Exact mutation-item schema remains open.

---


## UBU-D0035: Snapshots are observed state updates

**Status:** Accepted


A Snapshot is an observed update to UniverseState.

User-declared and sensor-derived observations use the same object type.

MVP snapshot fields include:

- `snapshot_id`
- `timestamp`
- `source`
- values
- confidence

**Consequences:**


- User and sensor observations can share infrastructure.
- Confidence can be stored even if not deeply used in MVP.

---


## UBU-D0036: Latest observed snapshot overrides simulation on conflict

**Status:** Accepted


MVP precedence rule:

- latest observed snapshot overrides simulation on conflicting fields;
- user-declared snapshots are treated as top-priority observations;
- confidence is stored but does not defeat explicit user declaration.

**Consequences:**


- Simulated Plan state cannot override observed reality.
- User declaration has “word of god” authority in MVP.

---


## UBU-D0037: Affect belongs to UniverseState in user mode

**Status:** Accepted


Affect is part of UniverseState in `user_mode`.

Affect is not intrinsic to organizations or machines.

**Consequences:**


- Affect data is disabled/absent in organization mode and worker mode.
- Human affect is a core planning constraint.
- Affect data should be treated as sensitive.

---


## UBU-D0038: MVP affect dimensions

**Status:** Accepted


MVP affect dimensions:

- energy / tiredness
- stress level
- mood

Values are user-queryable.

Energy/tiredness and stress may be scored from `0.0` to `1.0`.

Mood is represented as:

- categorical trinary: `happy`, `sad`, `angry`
- intensity scalar from `0.0` to `1.0`

Interested/bored is independent and derived.

---


## UBU-D0039: Affect confidence decays by age in MVP

**Status:** Accepted


In MVP, affect confidence decreases over time due to staleness.

The threshold/frequency is an algorithm configuration setting.

**Consequences:**


- Missing/stale affect data may activate an affect-collection Objective.
- Per-dimension confidence is post-MVP.

---


## UBU-D0040: Affect collection is modeled through an evergreen Objective

**Status:** Accepted


UbU may include an evergreen Objective:

> Collect affect information relevant to important usage.

When affect data is missing or stale, the planning algorithm may create UI survey Tasks.

**Consequences:**


- Affect feedback is not automatically requested after every Task.
- Affect collection is itself planned work.
- UI feedback Tasks can be scheduled and prioritized.

---


## UBU-D0041: External Events are instantaneous

**Status:** Accepted


An External Event is an instantaneous change in the universe.

External Events have no duration and may overlap Tasks.

They are not part of feasibility evaluation for an individual Plan in MVP.

**Consequences:**


- External Events can appear in Plans/Logs.
- External Events may trigger recalculation, new Tasks, or Objective updates.
- Other agents’ actions can later be modeled as External Events.

---


## UBU-D0042: Calendar is a set of possible Plans

**Status:** Accepted


A Calendar is a set of possible Plans.

A Calendar has a default Plan.

The default Plan is a current best recommendation, not a user commitment.

**Consequences:**


- Plans model modal futures.
- Logs/history are distinct from unrealized Plans.
- The user remains final authority over what occurred.

---


## UBU-D0043: Compact Calendar coverage belongs to compact serialization

**Status:** Accepted


Coverage is a property of a compact Calendar representation, not of the abstract Calendar itself.

Coverage represents the probability mass of possible futures covered by the compact representation.

**Consequences:**


- Coverage is useful for transport, pruning, and regeneration.
- The abstract Calendar does not store a single intrinsic coverage value.
- Compact Calendar grammar remains an open design question.

---


## UBU-D0044: Compact Calendar may use deterministic DFS instead of PRNG seeds

**Status:** Provisional


A compact Calendar may not require PRNG seeds.

Instead, deterministic DFS expansion may explore likely branches using a probability threshold `p`.

**Consequences:**


- Seed-based Plan identity may not be needed.
- DFS grammar and `p` semantics remain open.
- Compact Calendar is an important MVP design issue.

---


## UBU-D0045: Identity is the external-facing interaction surface

**Status:** Accepted


UbU interacts with outside agents through Identities.

A human may have multiple Identities.

Organizations and worker-mode instances are externally represented as Identities.

**Consequences:**


- External communication is Identity-mediated.
- Pseudonymous and compartmentalized operation are possible.
- Worker authorization can be expressed through Identity capabilities.

---


## UBU-D0046: Relationship is structured UniverseState data

**Status:** Accepted


A Relationship is structured UniverseState payload data representing the relationship between two Identities.

MVP Relationship data includes:

- two identity refs;
- one identity controlled by the user;
- user-stated affect state toward the other identity;
- inferred/speculated affect state of the other identity toward the user.

**Consequences:**


- Relationship Objectives attach indirectly through UniverseState.
- Communication/maintenance metadata is not stored directly on Relationship in MVP.
- Affect dimensions of Relationships are disabled/absent in organization mode.

---


## UBU-D0047: Device means execution enclave

**Status:** Accepted


A Device is an execution enclave, not physical hardware.

Examples:

- OS profile
- container
- VM
- secure enclave

**Consequences:**


- One physical machine may host multiple Devices.
- A Device belongs to one Zone.
- This supports compartmentalization and multi-zone use on one machine.

---


## UBU-D0048: Zone is a workspace-like instance context

**Status:** Accepted


A Zone is a workspace-like UbU context.

A Device belongs to exactly one Zone.

A Zone may have multiple Devices.

Zones maintain explicit allowlists/denylists of Compartments, defaulting to deny.

---


## UBU-D0049: Compartment is first-class

**Status:** Accepted


A Compartment is a first-class data containment object.

Compartments enforce hard invariants, such as:

- storage backend constraints
- device eligibility constraints
- identity disclosure constraints
- export/integration constraints
- retention constraints
- audit constraints

**Consequences:**


- WorkItems can remain structurally usable while sensitive content stays compartment-contained.
- UbU cannot casually override Compartment invariants.
- Un-compartmented content is treated as low-security.

---


## UBU-D0050: Sensitive content is referenced, not embedded

**Status:** Accepted


If content is specific to a Compartment, a WorkItem should refer to it through a Compartment-scoped reference.

WorkItems must remain structurally usable without dereferencing sensitive content.

**Consequences:**


- Plans can be structure-only.
- Sensitive content can remain contained.
- Planning can proceed even when content is inaccessible.

---


## UBU-D0051: Risk is reportable, not first-class in MVP

**Status:** Accepted


Risk is not a first-class object in MVP.

Risk is handled through reports derived from Calendar/Plan analysis.

Examples:

- P90 completion time
- critical path
- deadline miss probability
- affect constraint violation probability
- low coverage warning
- dependency fragility
- worker failure / bottleneck

**Consequences:**


- Plan scoring does not include explicit risk penalty in MVP.
- Tasks are not marked as mitigation Tasks in MVP.
- Burnout/affect exhaustion is modeled as constraint violation.

---


## UBU-D0052: Moot is first-class terminal Task status

**Status:** Accepted


`moot` is a terminal Task status.

It is functionally equivalent to completion for planning, but distinct for logging/reporting.

Moot requires a reason code.

Candidate reason codes remain open.

---


## UBU-D0053: GitHub managed state should be clearly marked

**Status:** Accepted as MVP direction


UbU should avoid fighting manual GitHub edits.

MVP direction:

> UbU writes only clearly marked UbU-managed labels, comments, or blocks, and treats other GitHub edits as external events.

**Consequences:**


- GitHub users can still interact normally.
- UbU-managed projection is visible and bounded.
- Reconciliation is still required.

---


## UBU-D0054: The Phase 1 MVP target is dogfooding

**Status:** Accepted


The first MVP should help coordinate the UbU project itself.

Phase 1 focuses on single-user GitHub dogfooding before multi-device sync or multi-user coordination.

**Consequences:**


- GitHub integration/projection is central.
- Design questions should be tested against whether they help UbU run UbU.
- Scope must be frozen aggressively to begin implementation.

---


## UBU-D0055: Scope freeze is now a priority

**Status:** Accepted


The data-model discussion has reached the point of diminishing private returns.

Further unresolved questions should become public GitHub Issues when possible.

**Consequences:**


- Do not wait for the entire model to be complete before coding.
- Freeze a Phase 1 MVP subset.
- Move unresolved questions into `OPEN_QUESTIONS.md`.
- Use public feedback to refine scope.

---


## UBU-D0056: File authority model for model-committee runs

**Status:** Accepted


The canonical source files for model-committee question-answering are:

- `DESIGN.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`

`README.md` and `OUTREACH.md` are derived public-facing projections of the canonical design state.

**Consequences:**


- Question-answering runs must not use `README.md` or `OUTREACH.md` as design authority.
- Consistency checks should include all Markdown files.
- If `README.md` or `OUTREACH.md` conflicts with canonical files, the derived file should normally be patched.
- If a derived-file inconsistency reveals a genuine source-level design issue, the issue should be added to `OPEN_QUESTIONS.md`.

---


## UBU-D0057: Model-committee automation is advisory and repo-driven

**Status:** Accepted


The model-committee process may read the canonical design repo, identify unresolved questions, generate proposed answers, run consistency checks, estimate MVP readiness, score open questions, and propose patches.

The model committee does not maintain its own durable question registry. `OPEN_QUESTIONS.md` remains the canonical unresolved-question queue.

**Consequences:**


- Committee runs are derived from the current repo state.
- Accepted changes become official only when committed to `ubu-design`.
- The model committee may generate patches but must not become the canonical decision engine.
- Full run logs should live outside `ubu-design`.

---


## UBU-D0058: Model-committee v0.1 is intentionally constrained

**Status:** Accepted


The first model-committee implementation should be a narrow local Python CLI, not a general model-governance platform.

**v0.1 restrictions:**

1. Supports only the `ubu-design` repo shape.
2. Requires structured `OPEN_QUESTIONS.md` question blocks.
3. Runs one selected question per committee run.
4. Does not auto-merge.
5. Embeds Markdown file contents directly; no file-upload APIs.
6. Requires strict JSON-schema model outputs.
7. Uses static model weights.
8. Supports only `ollama`, `openai_compatible`, and `manual` providers.
9. Uses a simple priority-order scheduler.
10. Writes filesystem logs only.
11. Does not implement semantic diffing.
12. Does not use the GitHub API in v0.1.

---


## UBU-D0059: Model committee outputs are weighted by capability and observed reliability

**Status:** Accepted


Model-committee synthesis should not use equal one-model-one-vote aggregation. Models may differ in reasoning quality, context length, instruction-following, access tier, cost, and observed reliability.

Premium or deeper cloud models may receive higher default trust weights than free-tier or smaller local models.

**Consequences:**


- Committee synthesis should use weighted support, not raw vote count.
- Local models remain useful for diversity, dissent, fallback, and offline review.
- Static configured weights are sufficient for v0.1.
- Adaptive reliability weighting is deferred.

---


## UBU-D0060: Open questions are ranked by automation-likelihood before importance

**Status:** Accepted


After consistency checks, the model-committee process should score every open question for:

- automation-likelihood,
- importance,
- risk.

The next question should normally be selected by automation-likelihood first, then importance, subject to a minimum importance threshold.

**Consequences:**


- The process should create visible progress before attempting the hardest human-governance questions.
- Question scores are derived metadata and may be updated after every consistency phase.
- The committee must track whether it is reducing or increasing unresolved design burden.

---


## UBU-D0061: DECISIONS.md is a bounded decision-memory index

**Status:** Accepted


`DECISIONS.md` is not an unbounded historical transcript. It is a bounded decision-memory index used to preserve accepted constraints and prevent settled questions from being rediscovered.

Full decision history is preserved by git history and model-committee logs.

**Consequences:**


- Stable design details should migrate into `DESIGN.md`.
- `DECISIONS.md` should retain compact active rules, resolved-question links, and anti-regression notes.
- Superseded or absorbed decisions should leave compact tombstones.
- The consistency process should warn when `DECISIONS.md` exceeds the configured prompt budget.

Initial prompt-budget warning threshold: approximately 12,000 estimated tokens.
Initial hard warning threshold: approximately 20,000 estimated tokens.

---


## UBU-D0062: Model-committee is a bootstrap UbU dogfooding workload

**Status:** Accepted


The model-committee project should begin as a constrained external bootstrap tool, but should move toward the mainline UbU implementation as soon as the mainline codebase can host it cleanly.

**Consequences:**


- The model-committee loop is an early example of UbU coordinating its own design and implementation.
- Its logs, question rankings, consistency reports, and patch proposals should inform the first real UbU dogfooding workflows.
- The tool should remain constrained enough to produce useful results before becoming a general UbU runtime component.
