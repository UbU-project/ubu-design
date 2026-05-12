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

v0.1 must implement:

- parse `OPEN_QUESTIONS.md`
- run consistency checks
- rank answerable questions
- generate Codex work prompt
- launch Codex CLI work provider
- run configured Ollama work models sequentially by priority
- import and validate candidate work proposals
- mechanically validate patches
- generate Codex scoring prompt
- launch Codex CLI scoring provider
- select winning patch
- write `selected.patch`, `commit_message.txt`, `review.md`, and logs
- support fake provider mode for tests
- include a `doctor` command for environment checks
- include a `version` command

v0.1 must not implement:

- direct OpenAI/Anthropic/Gemini API calls
- GitHub API
- auto-merge
- auto-push
- automatic PR creation
- adaptive model scoring
- readiness score updates to `README.md`
- derived `README.md`/`OUTREACH.md` consistency
- automatic patch application
- arbitrary network calls outside approved providers

v0.1 tooling and architecture:

- Python 3.12+
- `uv`
- `argparse`
- `pydantic`
- `httpx`
- `pytest`
- `ruff`
- custom Markdown parser for `OPEN_QUESTIONS.md`
- `git apply --check` for patch validation
- filesystem logs

v0.1 provider/network policy:

- `model-committee` itself may communicate only with:
  - local Ollama `base_url`;
  - Codex CLI subprocesses.
- It must not call:
  - GitHub;
  - OpenAI APIs directly;
  - Anthropic APIs;
  - Gemini APIs;
  - arbitrary HTTP URLs.
- `httpx` may be used only for the configured Ollama `base_url`.
- Codex must be invoked only through subprocess.

**Consequences:**


- v0.1 remains narrow enough to implement quickly.
- Codex CLI is represented as the primary work and scoring provider.
- Local Ollama execution remains in the earliest implementation as a secondary proposal source.
- Direct cloud APIs, GitHub integration, derived-file consistency, and adaptive scoring are deferred.
- v0.1 may create review artifacts but must not mutate remote GitHub state.
- v0.1 must not allow Codex to directly modify canonical repo files.
- Fake provider mode allows deterministic tests without calling Codex or Ollama.
- The `doctor` command improves reproducibility by checking local runtime prerequisites.
- The no-network rule preserves the intended bootstrap architecture and avoids accidental API creep.

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


## UBU-D0060: Open questions are selected by answerability, automation-likelihood, importance, and risk

**Status:** Accepted


After consistency checks, the model-committee process should score every open question for:

- answerability,
- automation-likelihood,
- importance,
- risk.

Question selection uses answerability as the first gate.

A question should not be selected for ordinary answer/work execution if it has unresolved dependencies, unless those dependencies are answered in the same work item.

Blocked questions may be selected for decomposition work when decomposition can produce replacement questions with fewer, simpler, or no dependencies.

After answerability is established, questions are ranked by automation-likelihood, then importance, then risk ascending.

**Consequences:**


- The process should not attempt to answer questions that are logically blocked by unresolved dependencies.
- Dependency-free or dependency-resolved questions are preferred for ordinary work.
- Blocked but important questions may still be selected for decomposition.
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

---


## UBU-D0063: Model-committee work is changeset-based

**Status:** Accepted


The model-committee process should not rely on a hidden external editor, VS Code agent, or other opaque implementation actor to apply accepted answers.

After the conceptual answer phase, the committee should run an explicit work phase in which models produce concrete changesets.

The work phase is followed by work scoring, work selection, local patch application in later versions, and review artifact generation before consistency checks run.

**Consequences:**


- The implementation step becomes auditable.
- VS Code may be used for human review, but is not part of the canonical committee loop.
- Work proposals should be represented as patches or equivalent changesets.
- Work scoring evaluates whether proposed changesets implement the selected answer cleanly.
- v0.1 writes `selected.patch`, `commit_message.txt`, `review.md`, and logs.
- Later versions may create local review-branch commits after work selection.
- v0.1 must not push, merge, create pull requests, or mutate remote GitHub state.
- This abstraction allows the same loop to later handle code changes, bug fixes, tests, and implementation tasks.

---


## UBU-D0064: Model-committee v0.1 uses a provisional filesystem log format

**Status:** Accepted


For v0.1, the model-committee implementation should define a provisional filesystem log format in code.

The final log and provenance format may be refined later by the model-committee process itself.

**Consequences:**


- `UBU-Q0036` remains open for final log/provenance design.
- v0.1 development is not blocked on fully resolving `UBU-Q0036`.
- The provisional log format should be simple, inspectable, and filesystem-based.
- Logs should preserve enough information to audit prompts, provider results, selected work proposals, selected changesets, consistency reports, question-ranking reports, generated review artifacts, Codex JSONL event logs, and provider stderr.

Provisional v0.1 log layout:

```text
runs/
  <timestamp>-<question-id>/
    manifest.json
    snapshot/
      DESIGN.md
      DECISIONS.md
      OPEN_QUESTIONS.md
    schemas/
      work_proposal.schema.json
      score_result.schema.json
    prompts/
      codex_work_prompt.md
      ollama_work_prompt.md
      codex_score_prompt.md
    responses/
      codex_work_response.json
      codex_work_events.jsonl
      codex_work_stderr.txt
      ollama_<safe_model_name>_response.txt
      codex_score_response.json
      codex_score_events.jsonl
      codex_score_stderr.txt
    parsed/
      codex_work_proposal.json
      ollama_<safe_model_name>_proposal.json
      score_result.json
    patches/
      codex.patch
      ollama_<safe_model_name>.patch
      selected.patch
    review.md
    commit_message.txt
```

---


## UBU-D0065: Model-committee v0.1 uses provisional quorum and provider-failure rules

**Status:** Accepted


For v0.1, model-committee runs should use simple provisional quorum and provider-failure rules.

These rules are sufficient to begin implementation and may be refined later.

Provisional quorum rules:

- Minimum valid work proposals: 1.
- Preferred valid work proposals: 2 or more.
- A Codex work proposal should be attempted before selecting a patch.
- Ollama work proposals should be attempted sequentially by configured priority.
- If Ollama responses finish within timeout and validate, they are included in Codex scoring.
- If an Ollama provider fails, the failure is logged and the run may continue if Codex produces at least one valid work proposal.
- If no valid work proposal exists, the run writes logs and exits nonzero.
- Provider failures are logged but do not invalidate the run if quorum is met.
- The Codex scoring response is required for automatic patch selection.
- If Codex scoring does not produce a valid score result, the run writes logs and exits nonzero.
- Manual override is not allowed in v0.1.
- If `selected_proposal_id` refers to a proposal that failed mechanical validation, `work-select` fails with exit code `7`, does not write `selected.patch`, and writes `review.md` explaining the failure if possible.

**Consequences:**


- v0.1 does not need a perfect provider scheduler before development begins.
- Failed, unavailable, invalid-output, timed-out, or interrupted providers are recorded as run events.
- The committee can continue when enough valid structured results exist.
- Codex is the required scoring provider in v0.1.
- More sophisticated quorum, retry, weighting, cooldown, and provider-health rules are deferred.

---


## UBU-D0066: Model-committee follows a prioritized recursive loop

**Status:** Accepted


The model-committee project should be developed as a bootstrap version of UbU’s future self-automation and dogfooding loop.

The loop has three prioritized modes:

1. system-wide consistency check,
2. question/problem prioritization selection,
3. work.

System-wide consistency checks have highest priority and should run after every merge, UbU directive change, LLM model update, or other state-changing event that could invalidate the project model.

Question/problem prioritization runs after consistency checks and selects the next work item by scoring answerability, automation-likelihood, importance, and risk.

Work is lowest priority and should normally run only after the current project state is coherent and the next work item has been selected.

**Consequences:**


- `model-committee` is not merely a question-answering tool.
- Consistency failures should usually become higher-priority work than unrelated future questions.
- Work should not proceed against a known-inconsistent repo unless the work item is specifically to repair that inconsistency.
- Early releases should preserve this structure even if the first implementation is simple.
- This loop should later map naturally into UbU’s own self-governance and Automation Worker model.

---


## UBU-D0067: Directive decisions may be appended directly

**Status:** Accepted


The UbU project may receive direct project-owner directives that are appended to `DECISIONS.md` as accepted decisions without first passing through the ordinary model-committee question-answering loop.

These directive decisions are treated as canonical once committed to `DECISIONS.md`.

**Consequences:**


- The model committee must treat directive decisions as authoritative.
- Directive decisions may override prior provisional decisions.
- If a directive decision creates inconsistencies, the next system-wide consistency check must detect them.
- Directive decisions may create, close, split, or reclassify open questions.
- Directive decisions should still use normal `UBU-Dxxxx` numbering.
- Directive decisions should identify affected `UBU-Qxxxx` questions where practical.

---


## UBU-D0068: Model-committee may decompose hard questions into easier questions

**Status:** Accepted


The model-committee process should not treat every increase in open-question count as a failure.

A work proposal may validly split, narrow, or restate a hard question into multiple simpler questions.

**Consequences:**


- The committee should track unresolved design burden, not merely question count.
- A decomposition is valid only if the resulting questions are clearer, narrower, lower-risk, or easier to automatically answer than the original.
- Replacement questions should not be harder to automatically answer than the question they replace unless the exception is explicitly justified.
- The original question should be marked as narrowed, partially resolved, superseded, or decomposed.
- Work scoring should reward useful decomposition and penalize scope-expanding decomposition.
- Decomposition is especially valuable when it reduces dependency blocking.
- A blocked question may be decomposed into replacement questions when at least one replacement question has fewer dependencies, simpler dependencies, or no dependencies.
- Replacement questions should explicitly declare their dependencies so the consistency checker can determine which questions are answerable next.

---


## UBU-D0069: Model-committee v0.1 uses Codex CLI as the primary model provider

**Status:** Accepted


`model-committee` v0.1 uses Codex CLI as the primary model provider for work proposal generation and work scoring.

The runtime calls `codex exec` with schema-constrained output. Prompts are passed through stdin. Final responses are written to JSON files. JSONL event streams and stderr are preserved in run logs.

Every runtime Codex call must pass `--skip-git-repo-check`.

`model-committee` does not pass deprecated `--disable web_search` flags. If web search must be disabled, that is handled through Codex configuration or profile state outside `model-committee`.

Codex must not directly modify repository files in v0.1. It produces JSON work proposals and score results. Patches are validated and selected by `model-committee`, then written as review artifacts.

**Consequences:**


- Browser-mediated ChatGPT copy/paste is removed from v0.1.
- Codex is the primary proposal and scoring provider.
- Ollama remains a secondary local proposal provider.
- v0.1 does not call OpenAI APIs directly.
- v0.1 does not allow Codex to mutate canonical repo state directly.
- All Codex outputs must be schema-constrained and logged.
- Runtime Codex calls use stdin prompt mode.
- Runtime Codex calls preserve JSONL event output and stderr output.
- Codex web-search configuration is treated as external Codex profile/config state, not managed by `model-committee` v0.1.

---

## UBU-D0070: Model-committee v0.1 authority boundary is explicit

**Status:** Accepted

`model-committee` v0.1 has authority to produce derived analysis, candidate answers, candidate questions, readiness estimates, consistency reports, provider scores, candidate changesets, and review artifacts. It has no authority to create accepted design state without an ordinary committed change to the canonical repo.

Automated actions allowed in v0.1:

- reading canonical design files;
- parsing and scoring open questions;
- running consistency checks;
- generating Codex and Ollama work proposals;
- mechanically validating structured outputs and patches;
- invoking Codex CLI for required scoring;
- selecting a mechanically valid patch from valid proposals when Codex scoring succeeds;
- writing filesystem run logs and review artifacts.

Human review is required for:

- accepting answers, patches, or new questions into canonical design state;
- applying or committing patches to `DESIGN.md`, `DECISIONS.md`, or `OPEN_QUESTIONS.md`;
- closing, decomposing, superseding, archiving, or reprioritizing questions in the canonical repo;
- treating readiness scores as scope-freeze, release, or implementation go/no-go decisions;
- changing provider weights, quorum rules, or provider/network boundaries.

Forbidden actions in v0.1:

- direct OpenAI, Anthropic, Gemini, GitHub, or arbitrary HTTP API calls;
- auto-merge, auto-push, automatic PR creation, or remote GitHub mutation;
- automatic patch application to canonical repo files;
- direct canonical-file edits by Codex CLI, Ollama, or any model provider;
- internal manual override that bypasses failed Codex scoring or patch validation;
- updating derived readiness signals in `README.md` or `OUTREACH.md`;
- treating model output as project-owner directives, canonical user value, or release commitment.

Provider outputs are weighted by configured trust weights and observed reliability metadata rather than raw vote count. Static configured weights are sufficient in v0.1. Adaptive reliability weighting is deferred.

Provider failures are logged as run events. Each failure should preserve the provider ID, model name when known, run phase, failure class, timeout or exit status when available, stderr or raw response artifact path when available, and whether the run still met quorum.

A valid v0.1 committee result requires at least one mechanically valid work proposal and a valid Codex score result. A Codex work proposal should be attempted before patch selection. Two or more valid work proposals are preferred but not required. Failed secondary providers do not invalidate the run when quorum is met.

Codex CLI has subprocess-provider authority only. It may produce schema-constrained proposal and scoring artifacts through `codex exec`, but those artifacts are non-canonical until validated, selected, reviewed by a human, and committed. Direct OpenAI API authority is zero in v0.1 because direct OpenAI API calls are forbidden.

**Consequences:**

- `UBU-Q0032` is resolved for v0.1 authority.
- Future refinements to logs, scoring, changeset validation, recursive-loop blocking, and decomposition metrics remain in their dedicated follow-up questions.
- The committee remains an advisory Automation Worker pattern until a later accepted decision expands its authority.

---


## UBU-D0071: MVP Logs are append-only per-instance event records

**Status:** Accepted

Resolved question: `UBU-Q0031`.

MVP Logs use a shared append-only entry envelope with event-specific payloads. Required fields are `log_entry_id`, `schema_version`, `instance_id`, `recorded_at`, `effective_at`, `event_type`, `actor_identity_ref`, `recorded_by_device_ref`, `target_ref`, `result`, `event_payload`, and `provenance`. Optional fields include old/new values, reason, notes, confidence, related Plan references, external references, annotation/correction links, and idempotency keys.

MVP event types are `task_completed`, `task_failed`, `task_moot`, `external_event_observed`, `snapshot_observed`, `objective_transitioned`, `plan_realized`, `decision_recorded`, `recalculation_triggered`, worker mutation submission/application/rejection events, and Log annotation/correction events.

Log entries are immutable once written. An annotation or correction creates a new Log entry that points to the original entry; it does not modify or delete the original. Corrections supersede interpretation of the original entry for query views while preserving the historical record.

Canonical Logs are stored per UbU instance, with device references recorded on entries. Device-local queues may exist for transport and audit, especially in later multi-device sync. MVP retention is indefinite for canonical Logs; archival may move old entries to colder local storage while preserving queryability and integrity. Deletion or redaction is deferred except where required by Compartment retention invariants.

Automation Workers contribute to Logs through worker Identities by submitting events or mutation requests. The canonical instance validates authority and records applied or rejected worker contributions with provenance, confidence when available, evidence references when available, and idempotency keys.

**Consequences:**

- `UBU-Q0031` is resolved for Phase 1 MVP.
- Logs can support audit, reconciliation, worker accountability, plan-vs-reality feedback, and correction without losing historical claims.
- Detailed event-specific payload schemas may be refined alongside Task, Snapshot, Objective transition, worker mutation, and recalculation-trigger schemas.
- Large-history search can rely on rebuildable indexes over the append-only Log rather than treating indexes as canonical state.

---


## UBU-D0072: Phase 1 public demo is an end-to-end GitHub dogfooding loop

**Status:** Accepted

Resolved question: `UBU-Q0030`.

The Phase 1 public demo must prove that UbU can coordinate UbU's own development in a single-user dogfooding loop. It should use real UbU GitHub issues, PR/review/CI events, and milestone context when possible; if live access is unsafe, unavailable, or non-reproducible, a frozen fixture captured from real UbU GitHub data may be used with fixture provenance shown.

The smallest persuasive demo imports a curated issue set, maps it to Objectives and schedulable Tasks, generates a Calendar with a default Plan, explains the chosen Plan, displays at least one risk report, respects a user-mode affect Snapshot or stale-affect collection Task, shows Automation Worker assignment/status for delegated analysis or GitHub projection work, and writes or previews clearly marked UbU-managed GitHub projection labels/comments/blocks.

Live GitHub mutation is not required in a public recording. A dry-run projection is acceptable if it uses the same projection payloads and validation path that would be written after human approval. The demo must not depend on Phase 2 multi-device sync, Phase 3 multi-user coordination, full RBAC, fully settled Compact Calendar DFS grammar, or autonomous remote GitHub mutation.

**Consequences:**

- `UBU-Q0030` is resolved for Phase 1 release criteria.
- The demo bar is end-to-end behavior, not complete implementation of every unresolved Phase 1 design question.
- Remaining GitHub projection, worker authority, risk-reporting, affect, and Compact Calendar details may still be refined in their dedicated open questions.
- Public messaging should describe any fixture, dry-run, or human-approval boundary explicitly.

---


## UBU-D0073: Core UbU planning and contributor surfaces are open source

**Status:** Accepted

Resolved question: `UBU-Q0029`.

UbU uses an open-core strategy, but the open core must include the planning kernel and the contributor-facing integration surface. A public contributor must be able to inspect, run, modify, and self-host the core system needed for ordinary single-user and project dogfooding without depending on private replacement components.

The definitely open-source surface includes data model schemas and migrations; the explicit planner and Calendar-generation logic required for Phase 1 dogfooding; GitHub import, triage, projection, reconciliation, fixture/demo tooling, and managed-label/comment/block formats; worker-mode runtime surfaces required for delegated work; compact Calendar serialization needed for transport or analysis; local-first storage and sync protocols when implemented; and the Super Automation extension/API boundary needed for third-party workers, connectors, or local services.

Private or commercial code may exist outside that boundary. Acceptable private areas include hosted-service operations, managed cloud infrastructure, paid support and packaging, premium hosted worker capacity, enterprise administration or compliance layers, proprietary connectors to closed third-party systems, and short-lived experimental prototypes that are not required for the public dogfooding loop.

Private experiments must not become hidden mandatory dependencies for public contributors. If an experimental component becomes necessary for the advertised open-source workflow, UbU must either open it before relying on it publicly or explicitly narrow the public promise. Repositories and packages should be labeled as open core, private experiment, premium hosted service, or external connector so contributors can tell where their work fits.

Implementation repositories should use OSI-approved licenses. The default license for core implementation repos is MPL-2.0 so modifications to core files remain shareable while integrations can be built without relicensing unrelated code. Stronger copyleft may be considered for network-hosted service code, and permissive licensing may be used for small examples, SDK stubs, or interoperability fixtures when that better serves adoption. No contributor agreement should grant unilateral proprietary relicensing of core contributions unless a later accepted decision explicitly changes that rule.

**Consequences:**

- `UBU-Q0029` is resolved for Phase 1 governance.
- The commercial boundary is service, operations, premium capacity, enterprise layers, proprietary closed-system connectors, and private experiments, not a hidden replacement for the planning kernel.
- Public contributor messaging should avoid claims that require private components.
- Future implementation repos need license files and package labels consistent with this boundary.

---


## UBU-D0074: Phase 1 privacy promise is a minimal Compartment guardrail layer

**Status:** Accepted

Resolved question: `UBU-Q0028`.

Phase 1 implements Compartments as metadata-backed classification and routing guardrails, not as the full multi-device containment system intended for later phases. A Phase 1 Compartment can mark content as local-only, disallow cloud LLM routing, disallow external export, declare allowed integrations, and declare allowed Devices within the limits of the single local Device model.

The hard Phase 1 invariants are narrow: `no_cloud_llm` Compartment content must not be sent to cloud LLM routes; `no_external_export` Compartment content must not be exported, projected, or handed to workers except as redacted structural references; Compartment-marked content crosses boundaries only through an allowed route and user-visible action; and boundary-crossing attempts that reach UbU are recorded in Logs as allowed or denied. Sensitive Compartment content is referenced rather than embedded in ordinary WorkItem structure.

Phase 1 does not promise complete privacy isolation, cryptographic isolation, hardware attestation, secure multi-device partial replication, protection from a malicious local administrator, or automated retention deletion/redaction. Retention policies may be recorded, but enforcement beyond append-only Log retention is post-MVP unless a specific implementation later adds and discloses it.

Un-compartmented content is explicitly labeled `security_level: low`. Low-security content is not compartment-protected and may be routed to configured integrations or cloud LLM-backed Automation Workers only through a user-visible integration or worker action.

Phase 1 may claim local-first operation only in the limited sense that canonical planning state, Logs, and source-linked project model data live in the local single-user UbU instance by default. It must not claim local-only operation, Phase 2 sync, conflict handling, partial replication, or secure multi-device Compartment propagation. Phase 1 may claim cloud LLM usage is optional, explicit, integration-scoped, and advisory; cloud LLMs are not the canonical planner and must not receive `no_cloud_llm` Compartment content.

**Consequences:**

- `UBU-Q0028` is resolved for Phase 1 MVP messaging and minimum implementation promises.
- Public messaging must distinguish privacy-first architecture from the narrower implemented Phase 1 privacy baseline.
- Full Compartment enforcement across sync, retention, device eligibility, and cryptographic isolation remains future work unless separately accepted and implemented.
- Implementations must label un-compartmented content as low-security rather than implying default protection.

---


## UBU-D0075: Organization and worker web admin UIs are post-MVP public surfaces

**Status:** Accepted

Resolved question: `UBU-Q0027`.

Organization-mode public UX is a project operations dashboard. The first screen should emphasize pipeline state, Plan/risk summaries, worker assignments and health, pending worker mutation requests, GitHub projection/reconciliation status, and recent decision/projection/worker Log entries requiring attention. It should avoid personal affect UX and should label admin-equivalent operation when full RBAC is absent.

Worker-mode public UX is an operator console for a worker instance. The first screen should emphasize connection and Identity status, service health and last check-in, active assignment and assignment queue, granted capability scopes, recent Log or mutation submissions, rejection/error state, and local resource status such as GPU availability or cloud compute state where applicable.

Both UIs may expose logs, queues, capability grants, resource status, pipeline state, risk reports, worker assignments, and GitHub projection status when the data is relevant to that mode. These views must default to summarized and redacted operational information and must not leak Compartment-protected payloads, broader planning state, or personal affect data through worker/admin convenience views.

No organization-mode or worker-mode web admin UI is required for Phase 1. Phase 1 requires only the single-user GitHub dogfooding surface and enough visible worker assignment/status information to satisfy the public demo criteria; that information may appear in the user-mode dogfooding UI, CLI output, or run artifacts.

**Consequences:**

- `UBU-Q0027` is resolved as a Post-MVP product direction rather than a Phase 1 implementation requirement.
- Phase 1 public UX scope remains focused on the single-user dogfooding loop.
- Future organization and worker admin UIs have a stable default first-screen direction without forcing RBAC or full admin products into MVP.
- Admin views must respect Compartment boundaries and mode boundaries.


---


## UBU-D0076: Relationship maintenance uses Objectives, history, and risk reports

**Status:** Accepted

Resolved question: `UBU-Q0026`.

In MVP, Relationship remains a structured UniverseState payload between two Identities and stores only the minimal relationship state already accepted: identity refs, the user-controlled Identity, user-stated affect toward the other Identity, and inferred/speculated affect of the other Identity where applicable.

Communication cadence belongs to an evergreen Objective recurrence/reactivation rule, not to the Relationship payload. Interaction evidence belongs in Logs, External Events, Task history, or Compartment/external references depending on source and sensitivity. Message bodies, private notes, or integration-specific history should remain behind Compartment or external-storage references when sensitive.

"Maintain relationship with contributor X" is modeled as an evergreen Objective linked indirectly to the contributor Relationship or relationship-relevant UniverseState key. That Objective can generate Dynamic Tasks such as reply, review, check in, or follow up. Task effects and imported External Events update ordinary UniverseState facts or event markers used to evaluate the Objective; they do not require a special Relationship-maintenance object in Phase 1.

Neglect risk is a risk-report finding derived from the Objective recurrence, observed interaction history, and current Plan/Calendar state. It is not stored on Relationship and does not make risk a first-class MVP object.

GitHub contributor interactions may update relationship-relevant modeled state when they are imported as External Events and associated with the user's GitHub Identity and the contributor Identity. They may satisfy or reactivate a relationship-maintenance Objective, but they must not overwrite user-stated private affect fields or infer sensitive relationship facts as canonical without user acceptance.

For Phase 1, relationship maintenance is supported only through existing Objective, Task, Log, External Event, UniverseState, Identity, Relationship, and risk-report mechanisms. A dedicated relationship-management UI, special cadence schema on Relationship, and full personal CRM behavior are deferred.

**Consequences:**

- `UBU-Q0026` is resolved for Phase 1 modeling.
- Relationship payload stays small and privacy-sensitive.
- Communication cadence remains schedulable and recalculable through Objective recurrence.
- GitHub dogfooding can model contributor follow-up without adding a new relationship subsystem to MVP.
- Future richer relationship-management features can refine cadence evidence and private notes without changing the MVP anchor model.

---

## UBU-D0077: Model-committee v0.1 marks active pre-MVP dogfooding

**Status:** Accepted

`model-committee v0.1` marks a transition from pure design preparation into active pre-MVP dogfooding.

The project now has a runnable bootstrap artifact that can help process UbU design questions, generate reviewable changesets, and make the dogfooding loop visible.

This does not make `model-committee` the full UbU planner. It is a constrained bootstrap workload and advisory Automation Worker pattern.

**Consequences:**

- Public messaging should no longer imply that UbU is only an ideal design without runnable project machinery.
- The next strategic bottleneck is no longer the absence of a runnable skeleton.
- The next strategic bottlenecks are contributor conversion, visible dogfooding output, first-use workflow selection, and prototype-funder discovery.
- Further design writing should generally be subordinated to implementation, recruitment, dogfooding, or market discovery.
- `README.md` and `OUTREACH.md` should describe active pre-MVP dogfooding while preserving the canonical authority of `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`.

---

## UBU-D0078: Recruitment targets a small core cohort, not a single co-builder

**Status:** Accepted

UbU’s near-term recruitment goal is to attract a small core cohort of serious, self-directed contributors.

The project should avoid public language implying that there is only one meaningful contributor role or that interested developers are competing for a single privileged position.

Popularity is not the goal, but multiple committed builders could materially accelerate UbU toward sustained full-time development.

**Consequences:**

- Public outreach should welcome several serious contributors.
- Contributor language should emphasize self-direction, seriousness, alignment, and concrete work rather than scarcity.
- The project should prefer committed contributors who can own bounded subsystems over broad passive interest.
- Casual interest remains useful when it produces workflow examples, design feedback, contributor leads, or prototype-funder leads.
- Recruitment success should be measured by concrete follow-up, contributions, design review, prototype funding, or subsystem ownership rather than raw attention.

---

## UBU-D0079: Independent knowledge workers are the first commercial beachhead hypothesis

**Status:** Accepted

UbU will treat privacy-sensitive independent knowledge workers as a leading commercial beachhead hypothesis.

This includes independent technical consultants, freelance developers, security researchers, solo founders, independent academics, technical writers, and similar workers who manage complex multi-client work privately.

This market is compatible with UbU’s north-star vision because these users experience personal self-governance, confidentiality, dependency, deadline, attention, and affect constraints directly.

Prototype funding from this market is acceptable only when it funds trunk features needed by the full personal self-governance product.

**Consequences:**

- Commercial discovery should include interviews with independent knowledge workers, not only FOSS maintainers or Ethereum teams.
- Prototype-funder outreach should test whether these users would fund or prepay for concrete core functionality.
- Acceptable funded work includes the planning kernel, local-first data model, privacy/Compartment model, affect-aware planning, GitHub/calendar/task ingestion, Logs, and recalculable Plans.
- Funding that requires surveillance, generic enterprise dashboards, centralized productivity telemetry, or manager-first reporting is incompatible unless a later accepted decision changes the project boundary.
- This decision is a market hypothesis, not a commitment to abandon FOSS or personal self-governance.

---

## UBU-D0080: Ethereum and FOSS outreach are recruitment and validation channels

**Status:** Accepted

Ethereum, FOSS, protocol, and autonomous developer communities are valuable early outreach channels because they expose UbU to high-autonomy contributors, complex coordination failures, anti-surveillance norms, and developer-tooling expectations.

These communities are not necessarily the first commercial buyer market.

Their primary near-term role is recruitment, workflow discovery, dogfooding validation, contributor-sustainability research, and project-management pain discovery.

**Consequences:**

- ETHConf and similar events should be treated as discovery and recruitment opportunities, not as proof that UbU is primarily a crypto project.
- FOSS outreach should seek concrete workflow examples, contributor candidates, design partners, and maintainers willing to discuss real coordination failures.
- Ethereum/protocol outreach should avoid token-first positioning.
- Project-management positioning should remain subordinate to personal self-governance and contributor sovereignty.
- UbU should not chase generic crypto speculation communities.

---

## UBU-D0081: Affect-aware planning is a core humane-planning requirement

**Status:** Accepted

UbU treats affect-aware planning as a core requirement, not a secondary wellness feature.

Planning systems that ignore fatigue, stress, boredom, motivation, emotional load, recovery, and dignity can produce plans that are technically organized but humanly unrealistic or harmful.

UbU should provide fast feedback about plan success or failure, suggest improvement after failure, respect emotional and physical limits, and still help users grow beyond current limitations.

The goal is neither comfort-maximization nor coercive productivity. The goal is humane self-governance: disciplined action that respects the user’s emotional and physical reality.

**Consequences:**

- Affect belongs to the core planning model in `user_mode`.
- Plans should be evaluated not only for logistical feasibility but also for human realism.
- A plan that repeatedly fails due to affect, fatigue, stress, boredom, or overload should cause model revision rather than user-blaming.
- Risk reports should eventually identify affect-related plan fragility.
- Public messaging may describe conventional planning tools as affect-blind, emotionally incomplete, human-incomplete, or mechanistic.

---

## UBU-D0082: High-quality plans need feedback, dignity, limits, and growth pressure

**Status:** Accepted

A UbU plan is not high-quality merely because it is internally consistent or time-feasible.

A high-quality plan should:

- produce fast feedback about success or failure;
- make failure informative rather than humiliating;
- suggest revision after failure;
- respect the user’s dignity;
- respect emotional and physical limits;
- distinguish sustainable stretch from destructive pressure;
- help the user grow beyond current limitations when appropriate;
- remain recalculable when reality contradicts the model.

This invariant is especially important in `user_mode`, where affect belongs to UniverseState.

**Consequences:**

- Plan evaluation should eventually consider whether a plan supports learning, adaptation, and sustainable self-improvement.
- Failure should generally produce improved modeling, revised constraints, or new suggested actions rather than moralized blame.
- UbU should push users toward growth only within a humane and feedback-sensitive planning loop.
- A plan that leaves the user worse off despite achieving nominal task completion should be considered suspect.
- This decision should inform `DESIGN.md` planning-quality language and future UI/UX choices.

---

## UBU-D0083: Technical essay should present a problem-first planning-kernel thesis

**Status:** Accepted

UbU should publish a problem-first technical essay that explains the planning-kernel thesis without reducing UbU to a product brochure.

The essay should argue that ordinary task managers, calendars, project boards, and opaque AI assistants fail to model real work because they do not represent objectives, state transitions, dependencies, constraints, logs, uncertainty, affect, and human limitations explicitly.

The essay should emphasize that most existing planning tools are affect-blind. They model tasks, deadlines, statuses, and calendar blocks, but not the emotional and physical reality of the person who must execute the plan.

The essay should explain why LLMs are useful but advisory: they can interpret, summarize, propose, and critique, but canonical planning must remain explicit, inspectable, and recalculable.

The essay should point to `model-committee` as UbU’s first visible dogfooding loop and end with a concrete contribution, interview, or prototype-funder request.

**Consequences:**

- The essay should lead with the problem, not with a feature list.
- The essay should avoid generic startup marketing language.
- The essay should invite concrete next actions from developers, maintainers, autonomous-team leads, and prototype funders.
- `OUTREACH.md` may summarize the essay project, but the essay itself may live outside the canonical design files.

---

## UBU-D0084: Public narrative may use moderated long-arc framing

**Status:** Accepted

UbU may publicly describe its long intellectual development history and the fact that modern LLMs have made the project newly viable.

This narrative may be used to attract contributors who want to work on software with durable significance.

Public framing should remain grounded, humble, and specific. It should avoid unrealistic claims, inevitability claims, or overstated promises about changing the world.

**Consequences:**

- Outreach may describe UbU as a long-running personal and technical project whose time may now be arriving.
- The narrative may help explain why the project has a mature design before it has a mature product.
- The narrative should be used to communicate commitment and depth, not destiny or superiority.
- Contributor recruitment should connect the long arc to concrete present work.

---

## UBU-D0085: Avoid exclusionary and scarcity-implying public framing

**Status:** Accepted

UbU public materials should avoid language that unintentionally makes interested contributors feel unwelcome, replaceable, or in competition for a single meaningful role.

UbU should also avoid accusatory language when describing planning systems that fail to model affect.

Preferred terms include:

- affect-blind;
- emotionally incomplete;
- human-incomplete;
- mechanistic planning;
- machine-like planning;
- non-humane planning;
- affect-insensitive planning.

**Consequences:**

- Public recruitment language should refer to a small core cohort or several serious contributors rather than a single highest-priority co-builder slot.
- Public language may still distinguish between serious contributors and passive interest.
- The project may strongly criticize mechanistic planning systems without using negative metaphors.
- Derived public-facing files should be updated when they imply scarcity or exclusion.
- Canonical design files should remain precise and humane in how they discuss affect, dignity, limits, and growth.

---

## UBU-D0086: Public outreach should convert interest into concrete next actions

**Status:** Accepted

UbU should not treat popularity as achievement.

Public outreach is successful when it produces concrete next actions that accelerate the project toward a working self-governance product.

Concrete next actions include:

- code contributions;
- test fixtures;
- design review;
- workflow examples;
- maintainer interviews;
- prototype-funder conversations;
- implementation-ready issues;
- review of `model-committee` run artifacts;
- sustained subsystem ownership;
- credible paths toward full-time development of core features.

**Consequences:**

- Outreach artifacts should contain clear next steps.
- ETHConf follow-up should classify contacts by likely concrete action, not by enthusiasm alone.
- Broad interest is welcome if it can be routed into bounded contribution paths.
- Vague praise without follow-up should not be treated as validation.
- The project should preserve its north-star self-governance mission when evaluating funding, contributors, and market opportunities.

---

## UBU-D0087: Commercial funding must preserve self-governance

**Status:** Accepted

Resolved question: `UBU-Q0048`.

UbU may accept funding, consulting, sponsorship, prepayment, or commercial prototype work only when the work accelerates trunk capabilities needed by the personal self-governance product and preserves user sovereignty, contributor sovereignty, privacy, and the open-core boundary.

A funding offer is compatible when it pays for reusable core work such as the planning kernel, local-first data model, privacy and Compartment guardrails, affect-aware planning, GitHub/calendar/task ingestion, Logs, recalculable Plans, risk reports, worker assignment/status, projection/reconciliation, or other features that become ordinary trunk capability.

Incompatible requested features include:

- surveillance-style project management, activity scoring, keystroke or screen monitoring, or always-on productivity telemetry;
- manager-first dashboards that rank, pressure, compare, or discipline contributors instead of supporting explicit self-governance and project coordination;
- centralized productivity telemetry across users, teams, clients, or contributors without explicit user-controlled sharing;
- generic enterprise reporting dashboards that pull UbU away from the planning kernel and toward conventional management software;
- features that expose affect, relationship state, Compartment payloads, or low-security personal context to managers, funders, or customers as a condition of use;
- token-first, speculation-first, governance-token, DAO-dashboard, or financialized coordination work that would reposition UbU as a crypto product;
- bespoke custom branches whose value depends on one funder's private workflow and does not produce reusable trunk capability.

Incompatible funding terms include:

- funder veto or control over the roadmap, canonical design process, accepted decisions, licensing boundary, or contributor access;
- exclusive ownership, assignment, or unilateral proprietary relicensing of open-core work;
- private replacement components for functionality that public contributors need for ordinary dogfooding;
- confidentiality terms that prevent honest public explanation of architecture, privacy limits, funded influence, or contributor-facing behavior;
- required pivot away from personal self-governance, privacy-first architecture, or the open-core planning kernel.

Acceptable prototype funding must default to trunk-first implementation. Customer-specific configuration, connectors, hosting, packaging, support, or compliance work may remain commercial when it stays outside the open-core boundary and does not become required for public dogfooding.

Crypto, tokenization, and DAO-specific requests should be rejected when they are token-first or speculation-first. They should be deferred when they are merely integration-specific and not required for the personal self-governance trunk. Ethereum and FOSS communities remain useful for recruitment, validation, and workflow discovery, not as a reason to reposition UbU as a crypto product.

Paid work should be evaluated with a simple rule: if the funded deliverable would make the open personal self-governance trunk better for independent knowledge workers and future public dogfooding, it may be considered; if it creates a private branch, surveillance surface, or funder-controlled roadmap, it should be rejected or renegotiated.

**Consequences:**

- `UBU-Q0048` is resolved for Phase 1 commercial red-line policy.
- Prototype-funder discovery can proceed with a clear accept/reject screen.
- Commercial discovery should prioritize independent knowledge-worker workflows that fund core planning, privacy, affect, worker, and projection capabilities.
- Enterprise opportunities are acceptable only when they preserve contributor sovereignty and remain subordinate to the planning-kernel trunk.
- Ethereum or DAO-related opportunities must not drive token-first positioning.
- Governance review remains required for ambiguous funding terms, especially exclusivity, IP assignment, confidentiality, roadmap control, and custom-branch obligations.

---

## UBU-D0088: Committed-contributor onboarding is public, bounded, and fixture-first

**Status:** Accepted

Resolved question: `UBU-Q0047`.

The minimum onboarding path for serious, self-directed contributors is a public, bounded path from context to a small verified contribution. It must not depend on private project-owner chats, unstated roadmap knowledge, private calendars, private GitHub data, or credentials.

A contributor should first read:

- the project overview and core principles in `DESIGN.md`;
- the model-committee dogfooding, Phase 1 public demo, GitHub dogfooding, design-process, open-core, and Phase 1 Compartment sections of `DESIGN.md`;
- the accepted decisions for open-core boundary, minimal Compartment promise, small core cohort recruitment, concrete outreach actions, and commercial self-governance red lines;
- the specific public issue, fixture, or model-committee artifact they intend to touch.

The first command should be a no-private-access local smoke check. For `model-committee`, the expected first command is `uv run model-committee doctor`, followed by a fake-provider or fixture-backed test/run when the implementation repo supports it. Equivalent first commands for later modules must avoid private tokens and should make missing optional providers or credentials visible as diagnostics rather than hidden prerequisites.

The first contribution should be one of: a synthetic or redacted workflow example, a fixture, a parser/validation test, review of a `model-committee` run artifact, documentation tied to a specific open question, or a narrow implementation-ready issue with explicit acceptance criteria. New contributors should not begin with hidden-roadmap work, direct GitHub mutation, Compartment-sensitive payloads, private-context reconstruction, broad planner rewrites, or module ownership.

Before implementation work, contributors must understand these boundaries: canonical design state lives only in committed canonical files; `model-committee` is advisory; v0.1 provider/network and no-auto-apply limits are hard; GitHub is a projection, not the source of truth; LLMs are advisory, not canonical planners; Compartment and low-security-content promises constrain data routing; the planning kernel and contributor-facing integration surface are open core; user sovereignty and mode boundaries are non-negotiable.

Contributor progression is staged:

1. Workflow informant: provides a concrete workflow, pain point, or fixture candidate.
2. Design reviewer: reviews a canonical question, decision, or model-committee artifact against public acceptance criteria.
3. Fixture/test contributor: adds or repairs a public fixture, fake-provider response, parser case, or validation test.
4. Implementation contributor: takes a narrow implementation-ready issue with tests and no hidden context dependency.
5. Module owner: earns bounded ownership after repeated reviewed contributions, demonstrated boundary understanding, and willingness to keep public docs, fixtures, tests, and interfaces coherent.

If a task requires private explanation to do correctly, it is not ready for contributor onboarding. The project should convert that missing context into a public issue, fixture, design note, or open question, with sensitive details redacted or replaced by synthetic examples.

**Consequences:**

- `UBU-Q0047` is resolved for Phase 1 onboarding.
- Contributor recruitment can point to bounded contribution paths without promising a single privileged role.
- First contributions should prove public reproducibility and boundary understanding before broad implementation authority.
- Implementation-ready issues should include enough context and acceptance criteria that direct access to the project owner's private context is unnecessary.
- Contributor progression is based on reviewed public work, not enthusiasm or private alignment claims.
