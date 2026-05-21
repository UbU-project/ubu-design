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


## UBU-D0044: Compact Calendar should prefer deterministic planner grammar over opaque PRNG seeds

**Status:** Provisional, refined by `UBU-D0108`, `UBU-D0123`, `UBU-D0124`, and `UBU-D0125`


A compact Calendar may not require PRNG seeds. Earlier design notes used deterministic DFS expansion as the candidate example. The current direction is broader: compact Calendar reconstruction should be based on deterministic, inspectable planner grammar and stored planning metadata, including skeleton Plan structure, legitimization state, candidate lineage, coverage, and repair metadata where appropriate.

DFS-like expansion may still be one implementation technique, but it is not the full architecture.

**Consequences:**


- Seed-based Plan identity may not be needed.
- Compact Calendar planner grammar and threshold semantics remain open.
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

Derived public-facing projections of the canonical design state currently include:

- `README.md`
- `OUTREACH.md`
- `PM_BRIEF.md`
- `FUNDER_BRIEF.md`
- `SOVEREIGN_COORDINATION.md`
- `ORG_INTROSPECTION_BRIEF.md`

**Consequences:**


- Question-answering runs must not use derived public-facing files as design authority.
- Consistency checks should include all Markdown files.
- If a derived public-facing file conflicts with canonical files, the derived file should normally be patched.
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

Live GitHub mutation is not required in a public recording. A dry-run projection is acceptable if it uses the same projection payloads and validation path that would be written after human approval. The demo must not depend on Phase 2 multi-device sync, Phase 3 multi-user coordination, full RBAC, fully settled Compact Calendar planner grammar, or autonomous remote GitHub mutation.

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

---

## UBU-D0089: First prototype-funder workflow is commitment-risk review plus next-day plan

**Status:** Accepted

Resolved question: `UBU-Q0045`.

The smallest fundable workflow for privacy-sensitive independent technical consultants is a local client commitment-risk review plus next-day Plan. It addresses the pain of discovering too late that multi-client commitments, deadlines, dependencies, energy, and unavailable time no longer fit.

The first prototype should not require full inbox, notes, invoice, or message-body ingestion. Required inputs are manual client/project declarations, current commitments/deadlines, tasks or work items, current availability, compartment labels, and a current or stale affect Snapshot. Optional inputs are calendar busy/free blocks and GitHub issue/PR references when the consultant explicitly connects them. Email, notes, invoices, and private client documents may be represented only as user-approved structural references or later explicit connectors that obey Compartment rules.

The primary output is a compartment-aware weekly commitment-risk report with a next-day default Plan. The report should show each client/project compartment at a structural level, identify overcommitment, deadline risk, stale or blocked work, cross-client dependency pressure, and affect/energy constraint risk, then propose the next concrete work window. The output must be inspectable and recalculable from explicit data; it must not rank client value secretly or expose one client's sensitive payload in another client view.

A daily plan alone is too generic for the first funded prototype. A client-compartment view alone is too static. A weekly review alone may be too passive. The smallest valuable bundle is the weekly risk review plus the next-day Plan because it converts private commitments into immediate action without requiring broad surveillance-style ingestion.

Paid prototype work remains on the trunk only if the implementation uses reusable open-core structures: Objectives for client/project outcomes, Tasks for commitments, Compartments for client separation, Logs for declarations and actuals, Calendar/Plan generation for schedule recommendations, risk reports for commitment and dependency pressure, and optional GitHub/calendar ingestion through user-visible routes. Customer-specific templates, data imports, hosting, credentials, and support may remain commercial configuration.

Prototype-funder discovery should test prepaid design-partner structures, not open-ended bespoke consulting. Plausible offers to test are: a paid discovery/review session, a prepaid prototype sponsorship that funds an implementation slice, or a monthly design-partner retainer. As a working hypothesis, discovery can test roughly USD 250-750 for a focused review, USD 2,000-10,000 for a prototype sponsorship, and USD 1,000-3,000/month for a limited design-partner retainer. These are discovery hypotheses, not permanent pricing policy.

**Consequences:**

- `UBU-Q0045` is resolved for prototype-funder workflow selection.
- Prototype-funder outreach should ask whether consultants will prepay for commitment-risk clarity, not a generic productivity assistant.
- Initial implementation should prioritize manual declarations, Compartments, Logs, risk reports, Calendar/Plan generation, affect Snapshot handling, and optional calendar/GitHub structural imports.
- Full email, notes, invoices, and private document ingestion are deferred until explicit privacy-preserving connector routes are designed.
- Funding that only produces a customer-private workflow branch should be rejected or renegotiated into trunk capability.

---

## UBU-D0090: Long-arc public narrative stays modest and testable

**Status:** Accepted

Resolved question: `UBU-Q0044`.

UbU may say that it grew out of a long personal and technical effort to understand planning, self-governance, privacy, and humane coordination. Public materials should include only enough of that history to explain commitment, design maturity, and why the project has more structure than a fresh prototype.

Modern LLMs should be described as changing the feasibility frontier for UbU, not as making success automatic. The grounded claim is that LLMs now make interpretation, summarization, proposal generation, fixture creation, review, and advisory automation cheap enough to support an explicit planning kernel. LLMs remain bounded assistants; they do not replace UbU's canonical planner, user sovereignty, or inspectable data model.

The long-arc narrative should communicate seriousness and durable possibility. Preferred public phrasing includes `long-running personal and technical project`, `the tools may finally be good enough to build the first narrow version`, `could matter for a long time if the dogfooding and contributor work prove it`, and `worth building carefully in public`.

The detailed version belongs in the first technical essay, selected outreach, talks, and interviews. README-level use should stay short and connect immediately to active dogfooding, concrete contribution paths, and prototype-funder discovery.

Avoid language that implies destiny, superiority, inevitability, or guaranteed world-historical impact. Avoid claims such as `will change the world`, `inevitable`, `once-in-a-generation`, `the future of work`, `solves coordination`, `the only real solution`, `decades ahead`, `everyone will need this`, and `LLMs make this inevitable`.

**Consequences:**

- `UBU-Q0044` is resolved for Phase 1 public narrative guidance.
- Public copy may use the long personal arc, but only as evidence of commitment and depth.
- LLM-enabled viability should be explained through concrete capability changes and bounded advisory use.
- Durable significance should be framed as a possibility to test through dogfooding, contributors, and prototype-funder discovery.
- Derived public-facing files may now be patched against this guidance without adding more canonical narrative questions.

---


## UBU-D0091: First technical essay makes a precise planning-kernel request

**Status:** Accepted

Resolved question: `UBU-Q0043`.

The first public technical essay should make one central claim: ordinary task managers, calendars, project boards, and opaque AI assistants are useful projections, but they are not enough for real planning because they usually do not model objectives, state transitions, dependencies, constraints, logs, uncertainty, affect, and recalculation as explicit objects.

The working title should be:

> The Planning Kernel: What Task Managers Leave Out

The previously proposed title, `The Planning Kernel: Why Your Task Manager Is Lying to You`, should not be used as the working public title. It is memorable, but it implies accusation and undermines the humane, problem-first tone.

The essay should explain affect-blind planning as human-incomplete planning. Fatigue, stress, boredom, motivation, emotional load, recovery, and dignity are planning constraints. They are not excuses, decorative wellness features, or moral failures. A plan that ignores them can be internally organized while still being unrealistic for the human who must execute it.

The essay should distinguish UbU from adjacent tools as follows:

- task managers record intended work;
- calendars allocate time;
- project boards track workflow status;
- opaque AI assistants can generate plausible suggestions;
- UbU is intended to be an explicit planning kernel that relates Objectives, Tasks, UniverseState, Plans, Calendars, Logs, constraints, uncertainty, affect, and recalculation.

The essay should explain LLMs as advisory systems. They may interpret messy input, summarize state, propose structures, critique plans, generate fixtures, and assist `model-committee`, but they are not the canonical planner. Accepted planning state must remain inspectable, explicit, and recalculable outside the LLM.

The essay should use `model-committee` as the first visible dogfooding example: UbU is already using a constrained automation loop to read canonical project state, propose reviewable changesets, score them, and preserve human-reviewed canonical authority. The essay must not imply that `model-committee` is the full UbU planner.

The essay should end with one concrete request:

> Send one real or carefully anonymized planning workflow that current tools cannot represent cleanly, including the objective, current state, dependencies, constraints, uncertainty, affect or energy limits, and what decision needs recalculation.

That request may route readers into a public issue, fixture contribution, design review, interview, or prototype-funder conversation, but the requested action remains one concrete workflow example.

Publication plan: draft the essay outside the canonical design files, then publish it with links to the canonical design repo, one visible `model-committee` artifact or summary, and a public path for submitting workflow examples. The essay should be updated only when canonical decisions change enough to alter the claim, avoidances, or request.

**Consequences:**

- `UBU-Q0043` is resolved for Phase 1 public outreach.
- The first essay has a stable thesis, title direction, outline, avoidances, dogfooding reference, and reader request.
- Derived outreach copy can summarize this essay without reopening the core claim.
- Publication work can move to execution rather than another canonical design question.

---


## UBU-D0092: Plan quality includes fast feedback, dignity, limits, and humane stretch

**Status:** Accepted

Resolved question: `UBU-Q0042`.

Phase 1 models human-complete plan quality as derived analysis over Plans, Tasks, Logs, Snapshots, affect constraints, and risk reports. It does not add a first-class canonical PlanQuality object in MVP. Any cached assessment is advisory and recalculable.

A candidate Plan should be checked for:

- fast feedback: important work has an observable checkpoint soon enough to revise before large loss;
- checkpoint coverage: success, failure, blocked preconditions, user overrides, affect Snapshots, or External Events can reveal whether the Plan is still accurate;
- affect margin: scheduled work does not consume energy, stress, mood, or recovery capacity beyond configured user-mode limits;
- dignity preservation: failure presentation does not moralize the user, expose avoidable embarrassment, or reuse wording that frames observed limits as character flaws;
- non-blaming revision: failed execution should suggest model repair, smaller Tasks, added checkpoints, updated estimates, recovery, clarification, delegation, or Objective reconsideration;
- humane stretch: the Plan may exceed the current baseline when feedback is close, recovery margin remains, and the expected post-plan state is not worse;
- destructive pressure: the Plan depends on overriding observed limits, lacks recovery, hides failure until too late, or repeatedly requires performance above observed capacity.

Task failure remains an ordinary Log result, but the interpretation of that failure should be plan-centered. UbU should treat failure as evidence about estimates, constraints, dependencies, affect state, interruptions, or Objective fit unless the user explicitly records another interpretation.

Affect-related plan fragility appears in Phase 1 risk reports as derived findings, not first-class Risk objects. Candidate findings include stale affect data, affect constraint violation probability, repeated late-failure pattern, destructive-pressure warning, dignity or demoralization warning, and post-plan depletion warning.

Plan quality should account for the expected state after the Plan, not only nominal completion. A Plan that completes tasks while predictably leaving the user depleted, ashamed, overloaded, or unable to continue should be treated as suspect and should trigger a revised Plan or risk report.

Post-MVP work may add longitudinal baseline learning, richer growth-pressure models, UI-specific coaching language, morale/dignity trend analysis, and more personalized recovery models. Phase 1 requires only derived assessment, reportable signals, recalculation-trigger integration, and humane revision suggestions.

**Consequences:**

- `UBU-Q0042` is resolved for Phase 1 modeling.
- No new canonical MVP object is required solely for plan quality.
- Human-complete plan-quality reports remain inspectable and recalculable from existing core objects.
- Failure handling should repair plans and estimates instead of blaming users.
- Risk reports gain affect-fragility findings without making Risk first-class in MVP.
- Rich longitudinal growth modeling remains post-MVP.

---


## UBU-D0093: Public recruitment invites several serious contributors into bounded paths

**Status:** Accepted

Resolved question: `UBU-Q0041`.

UbU's public recruitment copy should invite a small core cohort of serious, self-directed contributors, not a single co-builder, founding slot, or privileged insider. Seriousness is shown by concrete public follow-up: a workflow example, design review, fixture/test contribution, model-committee artifact review, narrow implementation-ready issue, or repeated reviewed work on a bounded subsystem.

Baseline public copy:

> UbU is looking for a small core cohort of serious, self-directed contributors. Good first contributions include workflow examples, design review, synthetic or redacted fixtures, parser or validation tests, model-committee artifact review, and narrow implementation-ready issues. If the work keeps the planning kernel inspectable, privacy-first, and useful for dogfooding, there is room for multiple contributors to earn bounded ownership over subsystems.

Public materials may name the contributor stages from onboarding: workflow informant, design reviewer, fixture/test contributor, implementation contributor, and bounded module owner. They may also route prototype funders and design partners into discovery, but prototype funding is not a contributor rank and must remain governed by the self-governance funding red lines.

The distinction between serious contribution and passive interest should be concrete rather than exclusionary. Passive interest is welcome when it produces workflow examples, design feedback, useful introductions, prototype-funder leads, public issue comments, or future contributor candidates. Serious contributor language should emphasize bounded public work, tests or fixtures, reviewed artifacts, and eventual subsystem ownership.

Avoid public phrases that imply scarcity or competition for one role, including `the co-builder`, `highest-priority contact`, `one founding slot`, `only serious builder`, `competing for a role`, `exclusive inner circle`, `prove you belong`, `hand-picked elite`, and similar language. If `co-builder` is ever used informally, it should not be singular or described as the single highest-priority outcome.

ETHConf and similar follow-up should classify people by their most useful next concrete action: send one workflow example, review a model-committee artifact, comment on a public design question, contribute a fixture/test, take a narrow implementation-ready issue, introduce a serious contributor, or discuss a trunk-compatible prototype sponsorship. Enthusiasm alone is not validation until it becomes one of these follow-ups.

**Consequences:**

- `UBU-Q0041` is resolved for Phase 1 public recruitment language.
- Derived public-facing files can use the baseline copy without reopening the recruitment question.
- Contributor recruitment can be selective about commitment while remaining welcoming to multiple serious contributors.
- ETHConf follow-up should be triaged by concrete next action rather than raw excitement.
- Public copy should preserve the open-core, privacy-first, and trunk-first boundaries already accepted for onboarding and funding.

---

## UBU-D0094: Release Outreach Pipeline makes releases explain themselves

**Status:** Accepted

Direct project directive.

UbU accepts the Release Outreach Pipeline feature bundle, with the tagline:

> UbU should make every release explain itself.

Release management in UbU should treat public and project-facing explanation artifacts as first-class release outputs. In addition to code, tests, changelogs, builds, and deployment artifacts, a meaningful release may require user-facing release notes, developer-facing release notes, screenshots, scripted UI-demo captures, video scripts, narration text, captions, YouTube metadata, public posts, known-limitations summaries, and contributor calls-to-action.

For UbU-runs-UbU, each minor release should normally produce a release outreach package when there is enough change to explain. The package should be derived from current repo state, release notes, accepted decisions, closed issues, updated design files, automated UI screenshots, scripted demo recordings, test fixtures, and explicitly labeled future plans.

Generated outreach must be evidence-bound. Claims about implemented behavior should be traceable to implemented features, accepted decisions, closed issues, release notes, test artifacts, screenshots, demo recordings, or other recorded evidence. Mock behavior, future plans, and speculative goals must be labeled as such.

The pipeline should support a fast public explanation path for nontechnical or lightly technical users and a sharper developer call-to-action path for serious contributors. A video can show the simple user-facing loop - bootstrap, one next task, explanation, feedback, and humane relationship or goal prompts - then close by showing UbU dogfooding its own GitHub issues, design docs, release tasks, and contributor needs.

The feature generalizes beyond UbU's own outreach. Project-management configurations should be able to define communication Objectives for users, developers, maintainers, funders, internal stakeholders, customers, community members, or other audiences. Release communication should become ordinary project work, not an afterthought.

Publication is gated by default. UbU may draft, assemble, render, and prepare outreach artifacts automatically, but external publication requires explicit human approval unless a project has configured a narrow trusted auto-publication policy. The pipeline must respect Compartment, Identity, export, and public-projection boundaries, and it must not leak private planning notes, contributor communications, personal data, or sensitive screenshots into public artifacts.

The implementation should be staged:

- Phase 0: manually structured release notes, screenshot lists, scripts, and calls-to-action.
- Phase 1: script and release-copy generation from repo state, release notes, closed issues, design decisions, and manually approved screenshots.
- Phase 2: automated screenshot and demo-flow capture from UI tests or approved fixtures.
- Phase 3: structured release outreach packages containing scripts, narration text, captions, storyboard, assets, render plan, platform metadata, and review checklist.
- Phase 4: automated rough video rendering for human review.
- Phase 5: gated publication workflow for YouTube, blogs, release pages, newsletters, and social posts.

**Consequences:**

- Release communication becomes part of the UbU project-management model.
- UbU-runs-UbU must eventually explain its own releases using the same planning and artifact-provenance principles it applies to other work.
- Future design should define the release outreach artifact schema, screenshot/demo provenance model, review gates, publication policy, and Compartment export checks.
- `UBU-Q0049` tracks the remaining implementation and schema questions for the Release Outreach Pipeline.

---

## UBU-D0095: Worker authority uses scoped capability grants

**Status:** Accepted

Resolved question: `UBU-Q0007`.

Automation Worker authority is represented through explicit capability grants associated with a worker Identity. The Identity is the external-facing actor and credential subject; the capability grant is the authoritative object that says what the worker may do for a specific parent UbU instance.

Phase 1 capability verbs are `task.read`, `objective.read`, `universe_state.read_subset`, `external_event.append`, `snapshot.submit`, `mutation_request.submit`, `recalculation.request`, and `projection.github.request_update`. Direct creation or mutation of Tasks, Objectives, UniverseState, `pipeline_state`, or GitHub projection state is not granted to workers in Phase 1. Workers submit mutation or projection requests, and the canonical instance validates, applies, rejects, and logs the result.

Capability grants may be scoped by object ID, Objective subtree, Task set, Compartment, external integration, operation kind, and time window. Compartment policy is a hard upper bound on any worker grant: a grant cannot authorize cloud LLM routing, external export, worker handoff, or payload disclosure that the relevant Compartment forbids.

Workers can be revoked by disabling or deleting grants and invalidating or rotating credentials. Revocation affects future access and submissions only; prior Log entries remain append-only history. Credential rotation creates a new credential version for the worker Identity while preserving audit continuity unless the underlying grants are changed.

A worker may serve multiple organization-mode or user-mode parent instances only through separate parent-specific grants, credentials, and audit trails. Cross-parent data sharing is forbidden unless each parent explicitly grants the route and all relevant Compartment policies allow it. User-mode workers are allowed, but access to affect or other personal data must use narrow read-subset grants and obey Compartment and low-security disclosure rules.

**Consequences:**

- `UBU-Q0007` is resolved for Phase 1 security modeling.
- Worker authority is least-privilege, revocable, auditable, and parent-specific.
- Worker mutation and projection behavior remains routed through request/validation/logging flows instead of direct canonical writes.
- `UBU-Q0008`, `UBU-Q0009`, and `UBU-Q0010` can refine assignment, mutation request, and GitHub token custody without reopening the basic worker capability model.

---

## UBU-D0096: Phase 1 requires bootstrap interview and next-action focus UX

**Status:** Accepted

Direct project directive.

UbU Phase 1 must include a minimal first-person user-facing loop, not merely an internal planner, GitHub importer, model-committee loop, or project-state analyzer.

Phase 1 requires two user-facing UX primitives:

1. **Bootstrap interview**: UbU begins by asking a small number of questions that help form an initial model of the user, current context, important Objectives, relevant constraints, current or stale affect Snapshot, and immediate dogfooding/project context.

2. **Next-action focus mode**: UbU can present one recommended next Task at a time, with an explanation of why that Task matters now. The full Plan remains inspectable, but the default user experience may reduce immediate cognitive load by showing a single next action.

The Phase 1 next-action screen should include, at minimum:

- the recommended Task;
- estimated duration or work window when available;
- why this Task matters now;
- what inputs or constraints UbU considered;
- current affect or stale-affect status when relevant;
- dependency, deadline, or risk explanation when relevant;
- user controls to start, complete, reject, snooze, decompose, or request more explanation;
- a feedback prompt after completion, failure, rejection, or override.

This UX requirement applies first to UbU-runs-UbU dogfooding. The first recommended Tasks may be GitHub, design-document, model-committee, release-management, or Release Outreach Pipeline Tasks.

Phase 1 must not claim full personal-data ingestion, full email/text/file understanding, therapeutic authority, autonomous life coaching, or complete privacy isolation merely because the bootstrap and next-action UX exist. The bootstrap interview may collect explicit user answers and may use approved fixtures or explicitly configured integrations, but broad personal-data ingestion remains future work unless separately implemented and disclosed.

**Consequences:**

- Phase 1 public demos should show the bootstrap interview and next-action focus mode.
- The Phase 1 implementation path must include a minimal user-facing UI surface, not only CLI or backend artifacts.
- The next-action UI becomes the primary nontechnical explanation of UbU.
- The full Plan must remain inspectable so that one-task focus does not become opaque automation.
- Release Outreach Pipeline scripts should treat this loop as the main public demonstration pattern.
- `UBU-Q0050` tracks the remaining product and implementation-detail questions for the minimum useful bootstrap interview and next-action focus mode.

---

## UBU-D0097: Phase 1 MVP scope is frozen around single-user GitHub dogfooding

**Status:** Accepted

Resolved question: `UBU-Q0001`.

Phase 1 is frozen as the minimum single-user `user_mode` implementation that proves UbU can coordinate UbU's own development through explicit state, an inspectable Plan, one recommended next action, feedback, recalculation, and bounded GitHub projection.

The exact Phase 1 feature set is:

- local single-user UbU instance for UbU-runs-UbU;
- bootstrap interview, current or stale affect Snapshot handling, and initial Objective/Task seed creation;
- live or fixture-backed GitHub import for issues, PRs, reviews, CI events, milestones, comments, and source links;
- ExternalReference-style mapping between GitHub objects and UbU Objectives, Tasks, External Events, and Logs;
- MVP Objective, Preference, Task, Container, UniverseState, Snapshot, Plan, Calendar, Log, Identity, Relationship, Compartment, Automation Worker, External Event, External Reference, and deferred Association-related schemas only to the depth required for the dogfooding loop;
- schedulable Static and Dynamic Tasks with Objective links, duration, dependency/precondition/effect fields, lifecycle status, and moot handling;
- lightweight UniverseState mutation and precondition evaluation sufficient for Task effects, affect, relationship-relevant facts, and GitHub/project facts;
- append-only per-instance Logs with provenance, correction, annotation, worker-submission, and recalculation-trigger entries;
- Plan and Calendar generation for the next work window, including a default Plan and inspectable explanation;
- next-action focus mode with start, done, snooze, reject, decompose, explain-more, and feedback controls;
- derived risk and human-complete plan-quality reports covering deadline risk, dependency fragility, worker bottlenecks, stale affect, affect-margin, destructive pressure, and post-plan depletion warnings;
- minimal Compartment guardrails, low-security labeling, cloud-LLM/export blocking for protected content, and logged boundary decisions;
- Automation Worker Identity, scoped capability grants, explicit assignment/status, and mutation or projection request submission without direct canonical writes;
- clearly marked GitHub projection previews or human-approved writes for UbU-managed labels, comments, or blocks, plus reconciliation reporting;
- manually structured Release Outreach Pipeline work items and artifact records for release notes, screenshots, scripts, and contributor calls-to-action.

Phase 2 explicitly defers:

- multi-device local-first sync;
- partial replication across Devices, Zones, or Compartments;
- secure cross-device Compartment propagation;
- sync conflict handling;
- cross-device worker or enclave coordination beyond the single local instance boundary.

Phase 3 explicitly defers:

- multi-human coordination;
- shared or partially shared truth between user instances;
- user-to-user Identity commitments, capabilities, and limited disclosure;
- multi-party governance, invitation, revocation, or trust protocols.

Abstractions documented but not implemented in Phase 1 include:

- Technique as a first-class planning object;
- full Compact Calendar planner grammar and high-coverage transport format;
- complete Zone and Device system beyond the current local execution enclave;
- organization-mode and worker-mode web admin consoles;
- richer relationship-management, personal CRM, and longitudinal affect/growth models;
- full Release Outreach Pipeline video generation, rendering, and publication workflow;
- broad email, text-message, file, invoice, note, or personal-data ingestion;
- adaptive model-committee weighting, automatic patch application, GitHub mutation, and direct cloud-provider APIs.

The Phase 1 stop rule is:

> A new abstraction may be added to Phase 1 only when it is required to complete the single-user GitHub dogfooding loop, enforce an accepted hard invariant, or avoid a known irreversible schema contradiction. Otherwise it must be documented as a Phase 2, Phase 3, or post-MVP concern and must not block Phase 1 implementation.

The minimum dogfooding loop that proves UbU's core model is:

1. bootstrap the operator, project context, available work window, constraints, and current or stale affect Snapshot;
2. import or load a curated UbU GitHub fixture with issues, PR/review/CI signals, milestone context, and source links;
3. map those inputs into Objectives, Tasks, External Events, Logs, UniverseState facts, and External References;
4. generate a Calendar with a default Plan for the next work window;
5. present one recommended next Task with an explanation of Objective value, dependencies, deadlines, affect constraints, worker status, and risk findings;
6. record completion, failure, snooze, rejection, decomposition, or override as Log evidence and trigger recalculation when appropriate;
7. preview or perform a human-approved UbU-managed GitHub projection update;
8. show a reconciliation or risk summary that makes the changed model inspectable.

**Consequences:**

- `UBU-Q0001` is resolved for Phase 1 scope freeze.
- Phase 1 implementation may begin without resolving every remaining MVP-important schema detail.
- Future-compatible abstractions may remain in the design, but implementation must stay limited to the dogfooding loop and accepted hard invariants.
- Detailed follow-up questions for GitHub mapping, mutation schemas, Compact Calendar grammar, risk reports, recalculation triggers, worker requests, Release Outreach artifacts, and bootstrap UX remain valid only as bounded implementation questions.
- New abstractions require explicit proof that they are necessary for the Phase 1 loop or must be deferred.
- Public claims must describe Phase 1 as a narrow single-user dogfooding MVP, not as full sync, full multi-user coordination, complete privacy isolation, or broad personal-data automation.

---

## UBU-D0098: GitHub external links use first-class External References

**Status:** Accepted

Resolved question: `UBU-Q0003`.

GitHub-to-UbU links are represented by first-class `ExternalReference` objects rather than by embedding all many-to-many source links directly on core objects. Lightweight `external_refs` fields may still appear on Log entries, provenance payloads, or import artifacts as convenience references, but they are not the authoritative external-link model.

MVP `ExternalReference` required fields are `external_reference_id`, `external_system`, `external_object_type`, `external_object_id`, `ubu_object_type`, `ubu_object_id`, `relation_type`, `confidence`, `created_by_identity_ref`, `created_at`, `last_verified_at`, `sync_policy`, `projection_policy`, and `provenance`.

Phase 1 external references may target Objectives, Tasks, External Events, and Log entries. This supports GitHub Issues mapping to multiple Objectives, Objectives mapping to multiple Issues, PRs and CI runs being retained as External Events, and comments or reviews acting as evidence for Tasks, Objective transitions, reconciliation, or projection decisions.

MVP relation types are `represents`, `supports`, `evidence_for`, `source_event_for`, `projection_of`, `duplicate_of`, and `supersedes`. Relation types are schema-controlled enums in MVP, not free-form labels.

Duplicate detection uses a normalized uniqueness key over `external_system`, `external_object_type`, `external_object_id`, `ubu_object_type`, `ubu_object_id`, and `relation_type`. Importers must normalize equivalent GitHub identifiers such as repository name, issue or PR number, node ID, URL, comment ID, run ID, and webhook delivery ID before comparing. Reobserving the same external reference updates verification metadata or creates an idempotent no-op Log entry rather than duplicating the external reference. Distinct relation types between the same objects are allowed.

Automation Workers cannot directly create or mutate canonical External References in Phase 1. They may submit external-reference mutation requests only through authorized `mutation_request.submit` capability grants. The canonical instance validates authority, Compartment/export policy, duplicate keys, expected prior version, and provenance, then logs applied or rejected outcomes.

**Consequences:**

- `UBU-Q0003` is resolved for Phase 1 GitHub dogfooding.
- `UBU-Q0002`, `UBU-Q0004`, and `UBU-Q0005` can build on a stable External Reference object instead of reopening source-link representation.
- GitHub import, reconciliation, and projection can preserve traceability without overloading Objective, Task, or External Event schemas.
- Worker-created external-reference changes stay inside the accepted mutation-request authority boundary.

---

## UBU-D0099: Psychological theory inputs are calibration, discovery, preview, and review layers

**Status:** Accepted

Direct project directive.

UbU should not expose internally computed utility values as user-facing truth. Derived utils remain transient computational artifacts used for scheduling, ranking, and comparison. User-facing value remains grounded in explicit Preferences, user declarations, Logs, Snapshots, review, and later correction.

Psychological and philosophical decision-theory inputs should usually enter Phase 1 through calibration, discovery, Calendar preview, Log review, reports, and reusable Tasks rather than through a large new psychology ontology.

Prospect-theory implications are accepted as preference-calibration requirements, not as an exposed utility model. UbU may show default preference examples and common-situation emotional-value examples during onboarding, Calendar preview, or Log review so the user can make more thoughtful Preference statements. These examples are grounding aids. They do not become canonical Preferences unless accepted by the user.

Temporal discounting is usually part of Preference for short-horizon Phase 1 planning. Long-horizon Objectives may later require explicit future-self or commitment-device modeling, but this is not a Phase 1 blocker.

Habit-related behavior should be handled through discovery mode, Logs, Snapshots, configured integrations, sensor-derived observations, and later clarification prompts. Discovery mode is a user-selectable workflow state that the user may choose at any time, especially from a mobile app with useful embedded sensors. Discovery mode supports later Log review and UbU-directed reconciliation for undetailed or under-specified time periods.

The Calendar is advisory. User overrides remain authoritative and should be treated as model evidence, not disobedience. Repeated overrides may trigger review, preference recalibration, Task decomposition, Objective reconsideration, or habit-pattern hypotheses only after appropriate user-visible reconciliation.

Calendar preview and Log review are notable Tasks that should run on a regular basis. They help verify whether UbU is correctly modeling the user's intended behavior, actual behavior, affective constraints, and preference judgments. These review Tasks should remain inspectable, interruptible, and adjustable by the user.

Self-determination theory and theory of planned behavior should primarily inform Calendar preview, Log review, reporting annotations, and optional user comments about motivation, autonomy, competence, relatedness, attitude, subjective norms, perceived control, and expected execution. Detailed modeling of those constructs remains open unless required by a concrete MVP workflow.

Narrative identity is partly addressed through Objectives and Reports. Social identity theory, social choice theory, and game theory are important post-MVP open-question areas and should be tracked explicitly without blocking Phase 1 implementation.

**Consequences:**

- `UBU-D0011` remains authoritative: derived utils are transient artifacts, not canonical user values.
- Preference calibration is MVP important, but not an MVP blocker.
- `UBU-Q0050` remains focused on the minimum bootstrap interview and next-action focus UX.
- Preference calibration, discovery-mode semantics, and Calendar preview / Log review annotations require separate MVP open questions.
- Social identity theory, social choice theory, and game theory impacts are accepted as post-MVP research/open-question areas.
- Calendar preview and Log review should be represented as regular user-facing Tasks or recurring review workflows, not hidden background judgments.
- Discovery mode must preserve user sovereignty: it may collect evidence for later reconciliation, but the user remains the final authority over what occurred and what it meant.


---

## UBU-D0100: Snapshots are immutable partial observed assertions

**Status:** Accepted

Resolved question: `UBU-Q0025`.

Snapshots are partial observed assertions over specific UniverseState fields. They are not full assertions of all UniverseState and do not imply that omitted fields are absent, unchanged, or unknown. Applying a Snapshot updates only the fields included in that Snapshot.

Snapshot records are immutable once accepted into the append-only Log. The original Snapshot observation is never edited or deleted as canonical history. Annotation, correction, and revocation are represented by later Log entries that point to the original Snapshot observation or Log entry.

MVP confidence is stored at both levels: a required snapshot-level confidence summarizes the observation as a whole, and optional per-field confidence overrides may be present when different observed dimensions have different reliability. If a field has no per-field confidence, it inherits the snapshot-level confidence. For affect Snapshots, the existing MVP rule remains: affect confidence may be treated globally across affect dimensions, with per-dimension confidence deferred unless a Snapshot explicitly provides per-field confidence.

Conflict resolution is field-local. Latest observed Snapshot data overrides simulated state for conflicting fields. User-declared Snapshots have top priority over sensor-derived, imported, inferred, or worker-submitted observations in MVP. If two user-declared Snapshots conflict on the same field, the latest `effective_at` or Snapshot timestamp wins unless a later correction supersedes it. For non-user observations, the application algorithm may use source priority, effective timestamp, and confidence, but confidence does not defeat an explicit user declaration in MVP.

A Snapshot can be corrected or revoked, but only through a new Log entry. Correction that replaces the observed state creates a new Snapshot and links it to the corrected Snapshot or Log entry. Revocation without replacement creates a correction/revocation Log entry that excludes the original Snapshot from corrected query views while preserving the historical claim.

**Consequences:**

- `UBU-Q0025` is resolved for Phase 1 Snapshot application semantics.
- Sparse observations, affect reports, sensor evidence, GitHub-derived facts, and review corrections can share one Snapshot model without requiring full UniverseState replacement.
- Snapshot query APIs must distinguish raw historical views from corrected/current views that follow correction and revocation links.
- Snapshot correction aligns with accepted append-only Log semantics and preserves user sovereignty without erasing historical evidence.
- Detailed source-priority tables for non-user observations may be refined alongside discovery mode, worker mutation requests, and import-specific schemas.

---


## UBU-D0101: Organization mode uses shared objects without intrinsic affect

**Status:** Accepted

Resolved question: `UBU-Q0012`.

Organization mode uses the shared UbU core object model except where fields or behavior are intrinsically personal-affect-specific. Objective, Preference, Task, Container, UniverseState, Snapshot, Plan, Calendar, Log, Identity, Relationship, Compartment, Automation Worker, External Event, External Reference, and deferred Association-related objects are available in organization mode to the depth required by the organization or project planning workflow.

Organization mode does not model intrinsic affect. In mode-specific schemas, intrinsic affect fields are absent. In shared implementation schemas that contain affect-capable fields for storage or migration convenience, those fields are disabled in organization mode and validators must reject organization-created intrinsic-affect values rather than silently treating them as unused.

Relationship objects may exist in organization mode without affect dimensions. Organization-mode Relationships represent structured UniverseState between Identities such as contributors, maintainers, workers, projects, vendors, integrations, or external organizations. Non-affect relationship-relevant project information belongs in ordinary UniverseState facts, External Events, Logs, External References, candidate AssociationAttestations, Objectives, Tasks, or risk reports. Organization mode must not claim that the organization has a private emotional state toward another Identity.

Organization-created Objectives, Preferences, and Tasks require `authority_source` metadata. In MVP this metadata may be coarse, but it must identify the authority path for the object, such as an admin-equivalent operator Identity, imported project policy, imported external event, Automation Worker submission, or human-approved import/projection action. The detailed vocabulary remains open in `UBU-Q0013`.

Before RBAC exists, organization-mode human users are represented as operator Identities with admin-equivalent authority over the instance. This is an MVP simplification only. Their actions must still be logged with actor Identity and provenance so future RBAC can be introduced without rewriting history.

Organization-mode instances may later receive limited signals from personal user-mode instances only through explicit user-controlled sharing, Identity-mediated authorization, Compartment/export checks, and clear provenance. Phase 1 does not implement personal-to-organization cross-instance sharing. Future designs should prefer structural signals such as availability, commitment status, task completion, or user-approved projection summaries rather than raw affect, private relationship state, or broad personal context.

**Consequences:**

- `UBU-Q0012` is resolved for MVP organization-mode object availability and affect exclusion.
- Organization mode can reuse the core planning model without inventing a separate organization ontology.
- Affect-bearing user-mode behavior remains excluded from organization-mode schemas and validators.
- Organization-mode Relationship payloads are valid without affect dimensions.
- `authority_source` is required on organization-created Objectives, Preferences, and Tasks, while `UBU-Q0013` remains responsible for the exact vocabulary and other authority-bearing objects.
- Admin-equivalent MVP operation is represented through operator Identities and Logs rather than premature RBAC.
- Later personal-to-organization signal sharing must be explicit, structural, consented, and bounded by Compartment/export policy.

---

## UBU-D0102: Phase 1 bootstrap and next-action UX stays narrow and inspectable

**Status:** Accepted

Direct project directive refining `UBU-D0096`, `UBU-D0097`, and `UBU-Q0050`.

The Phase 1 bootstrap interview and next-action focus UX are the first user-facing proof that UbU is more than an internal planner, GitHub importer, or automation loop. They must stay narrow, inspectable, and honest about implemented capability.

The bootstrap interview should ask only the minimum useful set of questions needed to seed the current user, context, available work window, important Objectives, relevant constraints, and current or stale affect Snapshot. It should not imply broad personal-data ingestion, therapeutic authority, complete life modeling, or autonomous coaching unless those capabilities have been separately implemented and disclosed.

The next-action focus mode should present one recommended Task at a time with a clear explanation of why that Task matters now. The full Plan must remain inspectable. One-task focus is a cognitive-load reduction pattern, not permission to hide the planner, omit Calendar preview, or turn UbU into opaque automation.

This decision is compatible with the Compact Calendar planning architecture. The default Plan supplies the inspectable ordered context behind the next-action recommendation, while reactive recalculation keeps the recommendation responsive when reality diverges. The planning layer should support the narrow UX rather than expanding Phase 1 scope beyond the single-user dogfooding loop.

**Consequences:**

- `UBU-D0096` remains authoritative for the Phase 1 bootstrap and next-action requirement.
- `UBU-D0097` remains authoritative for the Phase 1 single-user GitHub dogfooding scope freeze.
- `UBU-Q0050` remains open for exact bootstrap questions, next-action screen details, and implementation sequencing.
- Phase 1 public demos should show the narrow loop: bootstrap, one recommended next Task, explanation, feedback, recalculation, and inspectable Plan context.
- New planning architecture decisions must not be interpreted as permission to overclaim broad personal-data ingestion, full autonomous life management, complete privacy isolation, multi-device sync, or multi-user coordination in Phase 1.

---

## UBU-D0107: Default Plan selection uses Plan probability over deterministic optimized Plans

**Status:** Accepted

Direct project directive.

Plan optimization and default Plan selection are distinct operations.

Each Plan represented on a Calendar is deterministic. Once materialized, it is a time-independent representation of predicted Actions/Tasks, similar in shape to a future-facing Log projection. A Plan may eventually include predicted sensor states and expected UniverseState transitions, but it does not internally evaluate its own probability after representation.

Each candidate Plan should be individually optimized for value while satisfying the constraints applicable to the modeled branch that produced it. These constraints include dependencies, deadlines, preconditions, Calendar Logic, affect constraints in `user_mode`, and user Preferences.

The planning algorithm models probabilistic parameters such as Task duration distributions, Task success or failure, external events, interruptions, availability changes, affect uncertainty, and sensor predictions. A particular modeled combination of those probabilistic inputs yields a deterministic candidate Plan. UbU may ascribe a **Plan probability** to that candidate Plan: the probability mass of the branch or parameter combination that yields it.

The default Plan is the deterministic candidate Plan, or one of multiple equal candidate Plans, with the highest Plan probability overall.

**Consequences:**

- UbU should not describe the default Plan as merely the highest expected-value Plan.
- UbU should not treat Plan probability as an internal mutable property of a represented Plan.
- The default Plan remains user-facing and explainable: Calendar preview should show the ordered Tasks and the reason each Task appears.
- Practical algorithms may approximate the ideal through pruning, greedy heuristics, bounded finite Task instances, and adaptive resource limits.

---

## UBU-D0108: Skeletonization and legitimization precede default Plan candidate search

**Status:** Accepted as provisional planning architecture

This decision supersedes the narrower framing that a DFS or DFS-like process directly produces the full default Plan as the conceptual foundation of Compact Calendar planning. DFS-like, BFS-like, greedy, local-search, GPU-parallel, or solver-backed methods may still be used as implementation techniques, but the planning architecture now begins with explicit skeletonization and legitimization.

The planner first creates a **skeleton Plan**. The skeleton Plan affixes Static Tasks, walks backward through dependency DAGs from terminal Static Tasks to dependency roots, and schedules prerequisites before dependents. It is a dependency-valid causal foundation, not an optimized or fully human-viable Plan.

The planner then performs **legitimization**: the process of adding the minimum constraints and support Tasks required to make the skeleton Plan plausibly executable by a real user. This includes affect, recovery, transition, rest, sustainability, and similar human-viability constraints.

The **legitimized skeleton Plan** is the minimum feasible baseline against which richer candidate Plans are compared. Candidate Plan generation, Plan probability assignment, optional Task filling, value optimization, and reactive branch construction occur after this baseline exists.

A short-horizon reactive layer, likely BFS-like or policy/repair based, remains necessary for near-term divergence involving duration variation, early completion, late completion, interruptions, external events, affect shifts, user overrides, and recalculation triggers. The provisional reactive branch horizon remains one hour, with a provisional short-horizon coverage target of `0.99` probability mass. These are configurable heuristics, not immutable design law.

**Consequences:**

- The default Plan must be rooted in a skeleton Plan and legitimized skeleton Plan, not treated as a bare DFS artifact.
- DFS-like candidate construction remains allowed, but it is now one possible implementation technique after skeletonization and legitimization.
- The greedy mean-duration/value-density algorithm remains useful only as a deliberately unintelligent benchmark for comparing more serious planners.
- The reactive branch layer should be bounded by horizon, coverage target, resource mode, and device capability, but mobile UX must not depend solely on BFS precomputation.
- `UBU-Q0016` remains open but should be reframed around the Compact Calendar planner grammar and execution profile rather than only DFS grammar.

---

## UBU-D0109: Early completion pulls the next valid Dynamic Task forward

**Status:** Accepted as provisional runtime behavior

When a Task completes earlier than expected, UbU should normally pull the next valid Dynamic Task forward to the current time, provided that dependencies, preconditions, affect constraints, location constraints, Calendar Logic, and user-visible policy allow it.

This supports conservative duration estimates. If the scheduler avoids overly optimistic durations, then early completion is easy to absorb: the next Dynamic Task can begin immediately instead of forcing a disruptive full replanning cycle.

Static Tasks keep fixed start times. If the next Static Task is not yet available and all predetermined Dynamic Tasks before it have been completed or blocked, UbU may offer gap-filling suggestions. The exact evergreen Task model remains open.

**Consequences:**

- Early completion is a first-class recalculation event but should often be handled by simple forward-pull behavior.
- Conservative duration bias can improve user experience by making early completion common and easy to handle.
- Gap filling before Static Tasks depends on future evergreen Dynamic Task semantics.

---

## UBU-D0110: Compact Calendar planning supports adaptive time granularity

**Status:** Accepted as provisional default policy

Compact Calendar planning should support configurable time deltas. The provisional defaults are:

- full-detail planning delta: `1 minute`;
- mobile moderate delta: `5 minutes`;
- mobile low-power or offline delta: `15 minutes`;
- reactive branch horizon: `1 hour`;
- short-horizon branch coverage target: `0.99` probability mass.

A one-minute delta aligns with common calendar behavior and should be available when resources permit. Mobile-only, low-power, or offline modes may use coarser deltas to preserve battery, reduce computation, and keep local recalculation responsive.

Known offline windows, such as flights or planned disconnection, should trigger preparatory precomputation when connectivity and compute resources are available. Unexpected offline operation should degrade gracefully to cached explicit state, local planning, coarser deltas, and reduced branch depth.

**Consequences:**

- Mobile-only UbU must preserve the core UbU experience, but may use coarser planning granularity, shallower branch coverage, reduced analysis depth, and fewer LLM-assisted features.
- Coarser mobile or offline planning is a designed execution mode, not a failure mode.
- Compact Calendars should carry enough repair metadata for mobile devices to preserve legitimacy without performing full replanning. MVP-friendly metadata includes protected/flexible/disposable Task criticality, basic decision envelopes, cached explanations, conflict severity, and last-legitimate-Plan references.
- Finer granularity and deeper analysis may be made available through user-owned workers, desktops, laptops, dedicated appliances, or cloud/external compute.

---

## UBU-D0111: External compute is optional and backend-agnostic for the open-core planning loop

**Status:** Accepted

Cloud or external compute may improve performance, granularity, analysis depth, stochastic branch coverage, and expensive legitimization, but it must not be a hidden mandatory dependency for the open-core planning loop.

The FOSS core should be indifferent to the execution backend. Planning work may run on a mobile device, a local desktop or laptop, a Phase 2 user-owned worker, a dedicated user-owned appliance, an UbU corporate hosted service, a third-party compatible provider, or a future privacy-preserving compute backend.

Execution-provider selection should treat GPU suitability as a first-class criterion. Many practical devices have much more parallel arithmetic capacity in GPU-like hardware than in CPU-bound exact solvers. UbU should therefore prefer hybrid algorithms in which CPU or conservative exact logic certifies skeleton validity, hard constraints, and explanations, while GPU-capable search, simulation, scoring, and learned-model inference evaluate large candidate sets, robustness, affect load, and premium cloud planning. GPU search may propose; exact or conservative validation must certify.

External execution must be mediated by explicit APIs, capability grants, Compartment policy, provenance, user-visible routing decisions, and privacy controls. PII stripping, encryption, redaction, compartment-aware payload minimization, and future privacy-preserving compute such as practical FHE-backed or comparable encrypted computation are strategic directions, but not Phase 1 guarantees unless implemented and disclosed. Cloud planning payloads should transmit the structured timing, dependency, value, constraint, criticality, and legitimacy information needed by the algorithm while stripping or compartmentalizing unnecessary personal detail. Compact Calendar results should return small references, IDs, decision envelopes, explanations, and repair metadata rather than raw personal context where possible.

**Consequences:**

- Corporate cloud can be a product offering, but not the philosophical core of UbU.
- Third-party providers should be able to offer compatible execution services through the same open interfaces.
- User-owned personal worker devices are Phase 2.
- Dedicated appliances, managed hosted compute, compute monetization, and FHE/private encrypted compute are future commercial or strategic-research directions.
- Public FOSS contributors should not need private hosted services to inspect, run, modify, or self-host the open-core planning loop.

---

## UBU-D0112: Cloud LLM integration is provider-neutral, local-first, and policy-routed

**Status:** Accepted

Direct project directive.

UbU's premier LLM execution path remains local-first use of a user-controlled local model provider such as `ollama`, but cloud LLMs are accepted as optional execution providers when the user, Compartment policy, cost policy, and task sensitivity allow them.

The core architecture should model LLM execution through a provider-neutral routing layer rather than treating a local `ollama` call as the only conceptual interface. Supported or planned provider classes include local model providers, user-configured BYOK cloud APIs, optional UbUCorp managed gateways, user-owned remote workers, and future compatible third-party providers.

Cloud LLM execution is not semantically equivalent to local execution. It crosses an external trust boundary and must be governed by Compartment policy, context minimization, redaction where appropriate, cost controls, provenance, visible routing decisions, and output validation. Cloud LLM output remains advisory unless transformed into canonical UbU state through explicit accepted objects and Logs.

UbUCorp may offer managed hosted inference, model routing, support, integrations, enterprise controls, and commercial provider relationships. That convenience service must not become a hidden dependency of the FOSS core, the open-core planning loop, or the UbU protocol. A commercial exclusive provider relationship for UbUCorp's hosted service is acceptable only if the core remains local-capable, provider-neutral, BYOK-capable, and self-hostable.

**Consequences:**

- The FOSS core should expose an LLM provider abstraction rather than hard-coding cloud vendors or local-only semantics.
- `no_cloud_llm` Compartment content must not be sent to cloud LLM routes.
- BYOK cloud mode and user-owned remote worker mode are philosophically preferred over mandatory UbUCorp inference for technical users.
- UbUCorp managed inference may be a mass-market convenience layer, not the source of user authority or canonical planning state.
- Public outreach should describe cloud LLMs as optional, policy-governed execution providers.

---

## UBU-D0113: Associations are Identity-scoped perceived coordination structures

**Status:** Accepted

Direct project directive.

UbU adopts **Association** as the canonical term for the earlier social-formation concept. An Association is an Identity-scoped model of an emergent group-like coordination pattern. It may represent a friend group, party, amateur league, FOSS project, contributor crew, skill network, marketplace, nonprofit, company, DAO-like project, or other formal or informal group.

Associations are not assumed to have globally objective membership, authority, boundaries, or interpersonal identity. By default, an Association exists as a local, perspective-bound model perceived by an Identity and supported by evidence. Other Identities may maintain overlapping but non-identical models of what they call the same Association.

UbU should represent Association facts through local perception, AssociationAttestations, Relationships, shared Objectives, commitments, norms, Logs, and External References. Legal entities, corporate filing numbers, GitHub organizations, websites, event pages, chat rooms, contracts, payment addresses, and other institutional or external records are External References or evidence, not the complete social reality of the Association.

A future SharedAssociationDescriptor may provide a signed or reviewable shared artifact that multiple Identities can reference, but it is not a God's-eye truth object. It is a coordination artifact that can be accepted, disputed, superseded, or interpreted differently by different Identities.

**Consequences:**

- `External Association` is renamed to `External Reference` everywhere in the design language.
- Association membership and authority should be treated as claims or attestations, not globally authoritative list fields by default.
- Legal organizations are special cases with strong External References, not exceptions to perspective-bound social modeling.
- Social identity, social choice, and game-theory open questions should build on Association, AssociationAttestation, External Reference, and SharedAssociationDescriptor concepts.
- Phase 1 may use the Association concept for EthConf/outreach dogfooding without implementing full multi-user Association reconciliation.

---

## UBU-D0114: Organizational introspection is a first-class UbU feature

**Status:** Accepted

Direct project directive.

UbU should treat organizational introspection as a first-class feature, not merely as a side effect of project management or future Association modeling.

Organizational introspection is UbU's ability to analyze evidence-bearing records from an Association, such as documentation, meeting notes, issue trackers, pull requests, governance discussions, chat logs, board minutes, public Discord or IRC history, outreach notes, and other permitted records, then generate reviewable, provenance-backed AssociationAttestations and feedback questions about the Association's actual behavior.

The goal is to help an Association inspect whether its real priorities, overrides, undocumented roles, decision paths, commitments, and work patterns are consistent with its declared mission, values, objectives, and public claims. Generated claims are candidate attestations with evidence, confidence, provenance, review status, and disclosure policy. They are not authoritative social truth.

This feature mirrors personal UbU introspection. For a person, UbU asks whether actual behavior matches stated values and Objectives. For an Association, UbU asks whether actual work, decisions, and resource allocation match declared mission and commitments.

**Consequences:**

- Association introspection should generate structured review artifacts, not just free-form insights.
- Every generated claim needs provenance linking it to source records, prompt/model metadata when applicable, confidence, and review/dispute status.
- Public or permissioned sources are the proper default boundary. UbU must not become a tool for illicit surveillance, doxxing, adversarial social-graph extraction, or managerial coercion.
- EthConf outreach should dogfood this feature by treating notes, follow-ups, and UbU project artifacts as evidence for whether UbU is actually pursuing its stated outreach goals.
- The public hook may ask whether a project has evidence-backed proof that it is committed to achieving its stated goals, but design docs should clarify that this means operational proof through evidence trails, not mathematical certainty.

---

## UBU-D0115: EthConf outreach uses one core pitch plus lightweight audience lanes

**Status:** Accepted

Direct project directive.

EthConf outreach should not splinter into many separate campaigns. The project should use one core UbU thesis with lightweight audience variants for FOSS contributors, prototype funders, general EthConf attendees, and a modest cypherpunk/privacy-builder lane.

The shared thesis is that UbU is local-first, user-sovereign AI planning and coordination infrastructure. It can run locally for privacy, use optional cloud LLM execution when policy allows, and eventually help Associations coordinate through explicit Identities, commitments, evidence, and bounded disclosure.

The cypherpunk/privacy lane should frame **Skill Barter marketplace** as a future specialization of Association modeling: lawful, privacy-preserving skill barter and skilled-work coordination through pseudonymous Identities, scoped work agreements, reputation without unnecessary doxxing, commitments, and user-chosen settlement references where lawful. It must not be framed as an illicit marketplace, sanctions-evasion tool, tax-evasion tool, or token-first product.

**Consequences:**

- Outreach should prioritize FOSS contributors while keeping funder, general attendee, and cypherpunk variants prepared.
- The cypherpunk lane is a recruiting hook for privacy-minded builders, not the center of the project.
- Skill barter and private settlement remain future/post-MVP specializations, not Phase 1 commitments.
- Public language should prefer `Skill Barter marketplace`, `voluntary privacy-preserving skilled-work coordination`, `pseudonymous skill barter`, and `lawful private settlement` over anonymity/evasion framing.
- EthConf follow-up should be classified by concrete next action, not enthusiasm alone.

---

## UBU-D0116: EthConf outreach dogfoods Association formation and organizational introspection

**Status:** Accepted

Direct project directive.

UbU's EthConf outreach is itself an Association-forming workflow. The project owner is attempting to form an ad hoc Association around the UbU project through conversations with contributors, reviewers, funders, workflow informants, privacy/cypherpunk builders, and possible design partners.

This outreach should be treated as dogfooding, not mere marketing. Notes, follow-ups, contact classifications, public artifacts, private/redacted observations, and subsequent commitments can be modeled as Objectives, Tasks, Logs, Relationships, External Events, External References, and candidate AssociationAttestations.

The outreach process should later be submitted to LLM-assisted or manually reviewed organizational introspection. UbU should ask whether the actual outreach behavior proves that the project pursued its stated goals: recruiting serious contributors, pressure-testing the design, finding workflow examples, identifying compatible funding, and preserving the privacy-first self-governance mission.

**Consequences:**

- Phase 1 can use EthConf outreach as a manually structured dogfooding fixture without implementing full Association automation.
- Redacted outreach retrospectives can become public proof that UbU applies its own introspection discipline to itself.
- The strongest outreach challenge is: `Can your project prove from its records that it is actually committed to achieving its stated goals?`
- The challenge should be memorable but not accusatory; it should invite shared discipline rather than imply that other maintainers are hypocrites.
- Follow-up artifacts should convert social interest into explicit Tasks, commitments, contributor paths, and review questions.

---

## UBU-D0117: Context-rich cross-user messaging is a premier Phase 3 feature

**Status:** Accepted

Direct project directive.

Phase 3 minimal multi-user coordination should include a limited but meaningful form of cross-user contextual messaging. This should be treated as a premier Phase 3 feature, not merely as an incidental transport detail.

A UbU message is not only flat text. It is a communication event that may carry structured planning context. Even a minimal Phase 3 message envelope can help the receiving UbU instance decide whether a message should interrupt the current Plan, be deferred to a later review window, become a Task, update an Objective, or remain ordinary communication history.

A minimal Phase 3 **Message Context Envelope** should include only fields that are safe, useful, and policy-permitted, such as:

- sender and receiver Identity references or external references;
- source system or transport;
- raw or human-readable message body;
- message kind, such as request, status update, question, commitment, blocker, reminder, or FYI;
- topic or associated Objective/Task/Association references when disclosure policy allows them;
- requested response kind and any explicit deadline;
- priority and interrupt recommendation;
- known assumptions and ambiguities;
- provenance and confidence fields;
- disclosure and Compartment policy metadata.

Richer relationship reconstruction, subjective social context, long-term Relationship history exchange, Association synchronization, and detailed multi-party trust semantics may remain post-MVP.

**Consequences:**

- Phase 3 is not only about shared objects and commitments; it should include context-aware asynchronous communication.
- The receiving UbU instance should be able to triage messages against its Calendar and current Plan.
- Minimal metadata is valuable even before UbU can exchange deep subjective relationship models.
- Metadata sharing must remain bounded by Identity, Compartment, and disclosure policy.

---

## UBU-D0118: Legacy messaging adapters may upgrade flat messages into UbU contextual messages

**Status:** Accepted as product and interoperability direction

UbU should be able to ingest and, where permitted, send through legacy communication systems such as WhatsApp, SMS, email, Discord, IRC, Slack, Matrix, or similar systems.

When only one side uses UbU, the legacy message remains a flat external input. UbU may scan, classify, summarize, and convert it into local candidate Tasks, Events, Logs, Relationship observations, or Association evidence, subject to user permission and integration policy.

When both sides use UbU, the two instances should be able to translate the legacy exchange into a UbU-native contextual message format. Depending on the transport and policy, this may happen through a side channel, an attached envelope, an agreed encoding, a linkable External Reference, or another adapter-specific mechanism. The raw legacy text remains the user-visible message; the UbU envelope supplies structured context.

This creates a practical bridge from legacy systems into richer UbU-to-UbU communication without requiring the rest of the world to abandon existing messaging platforms first.

**Consequences:**

- UbU should define a stable internal message-envelope schema before binding it to any one legacy transport.
- Legacy adapters must preserve user consent, platform constraints, and Compartment boundaries.
- UbU-to-UbU metadata must not silently leak private Relationship, Objective, Task, or Association context.
- This interoperability can become an adoption path: legacy contacts can experience the benefit of richer coordination and may choose to install UbU.

---

## UBU-D0119: Structured message extraction is a bounded LLM-assisted normalization layer

**Status:** Accepted as architectural direction

UbU will ingest large volumes of unstructured direct-message and group-chat text from legacy systems. A dedicated **Message Context Extractor** should normalize those inputs into strict UbU JSON structures.

The extractor should take raw message text plus available metadata, such as source system, channel type, channel purpose, sender, receiver, Identity mapping, Association mapping, timestamp, thread context, Relationship context, and Compartment policy. It should output bounded structures describing message kind, topic, priority, interrupt level, candidate Tasks, Objective links, assumptions, ambiguities, actionability, response expectation, confidence, and provenance.

The extractor is not the canonical planner and must not silently mutate canonical state. Its outputs are candidate interpretations that pass through schema validation, provenance marking, confidence scoring, repair loops, and user or policy acceptance where required.

Phase 3 and early post-MVP implementations should begin with general LLMs constrained by strict schemas, grammar-constrained output where practical, validation, and repair. Fine-tuned, distilled, or adapter-trained extractor models may become attractive after UbU has stable schemas and enough corrected examples. Training a new foundation model from scratch is not currently justified.

**Consequences:**

- UbU should treat message ingestion as semantic compilation from unstructured communication into planning-relevant candidate state.
- Every extracted field should distinguish explicit source facts from inferred, guessed, or user-confirmed facts.
- Custom extractor models are plausible later for privacy, latency, cost, and reliability, but should not block MVP or Phase 3 schema work.
- Group-channel interpretation should use channel and Association metadata where available, but must remain uncertainty-aware when context is missing.

---

## UBU-D0120: Personalized voice/TTS descriptors are optional consent-gated communication metadata

**Status:** Accepted as future product direction, not Phase 1 scope

UbU may eventually support optional voice or pronunciation descriptors so that a receiving UbU instance can render text messages using text-to-speech that approximates the sender's usual voice, pronunciation, cadence, or expressive style.

This can be viewed as a communication-compression feature: instead of sending a noisy audio recording, a user may send text plus a voice descriptor or voice-profile reference, allowing the receiver's device to synthesize a locally rendered spoken version. The same idea may also help accessibility, hands-free interaction, language learning, and more expressive asynchronous updates.

Voice data is sensitive. A voice descriptor or voice profile must be opt-in, revocable where practical, policy-governed, and clearly separated from authentication. UbU should not treat a synthesized voice as proof that a human actually spoke the words. Implementations should consider visible disclosure, watermarking or provenance markers, anti-impersonation controls, and restrictions on cross-context reuse.

**Consequences:**

- Personalized TTS belongs to communication UX and accessibility, not canonical planning correctness.
- Voice profiles are biometric-like sensitive data and should require strong Compartment controls.
- Legacy flat text can become richer on the receiving side without forcing the sender to transmit full audio.
- This feature is post-MVP unless a very narrow accessibility-oriented version becomes necessary earlier.

---

## UBU-D0121: Messaging interoperability can support value-led viral outreach without coercive growth loops

**Status:** Accepted as outreach/product direction

Legacy messaging integration can create a natural adoption path. A UbU user interacting with a non-UbU contact may receive immediate value from local extraction, prioritization, task creation, and planning integration. If both people install UbU, they can exchange richer structured context and reduce ambiguity, missed requests, and priority confusion.

This is a plausible viral outreach mechanism: the product becomes more useful when counterparties also use it. However, UbU should not use manipulative dark patterns, spammy invitations, forced signatures, or guilt-based prompts. The adoption message should be value-led: richer coordination, clearer priority, less lost context, and better respect for both users' time.

**Consequences:**

- Public messaging may describe UbU as a way to make legacy communication more actionable.
- Invitation flows should be optional, user-authored or clearly user-approved, and respectful of the recipient.
- Viral adoption should follow from real coordination value, not from artificial network pressure.
- Cross-user features must preserve UbU's privacy and sovereignty commitments.

---

## UBU-D0122: Greedy mean-duration planning is a benchmark, not the canonical planner

**Status:** Accepted as baseline algorithm policy

UbU may define a deliberately unintelligent greedy baseline planner for comparison. The baseline inserts Static Tasks first, places modeled External Events at their expected mean-point start time where applicable, ranks Dynamic Tasks by temporary value-per-minute from the Preference DAG divided by expected mean duration, and fills time from the earliest available slot forward while checking only local viability. It does not backtrack and should be expected to be inefficient, brittle, and strategically myopic.

This baseline is useful because later planners can be evaluated against a simple deterministic reference: total value, missed deadlines, affect burden, dependency failures, fragility under interruption, and explanation quality should improve over the baseline.

**Consequences:**

- The greedy algorithm is allowed as a regression benchmark, smoke-test planner, or fallback demonstration.
- It should not be presented as the serious Compact Calendar planning architecture.
- Greedy value-per-minute selection is expected to over-select short Tasks and under-select long strategic Tasks; that pathology is a benchmark feature, not a design target.

---

## UBU-D0123: Calendar planning begins from explicit UniverseState assumptions

**Status:** Accepted as provisional planning-model requirement

Every Calendar planning run must begin from an initial UniverseState. For MVP, the preferred case is a deterministic initial UniverseState in which planner-relevant starting facts are known, assumed, or explicitly unresolved. A future probabilistic initial UniverseState may assign probabilities to known possible starting states, but that mode is more complex and likely beyond MVP.

Skeleton Plan generation must check whether dependencies are already satisfied in the initial UniverseState before inserting prerequisite Tasks. A dependency does not automatically mean that a new Task should be scheduled; it means that a required state must be true before the dependent Task begins.

If the planner cannot create a viable skeleton Plan, normal planning should halt and UbU should immediately present a diagnostic explanation. The user should see the failed dependency, conflicting Static Task, impossible timing, cyclic dependency, missing state, or unavailable resource, plus selectable alternatives where possible.

**Consequences:**

- Deterministic initial UniverseState is the MVP-compatible default.
- Probabilistic initial UniverseState remains a later research mode.
- Skeleton Plan failure is a critical model-consistency failure, not a minor optimization failure.
- Diagnostic explanation and user clarification are required when the skeleton Plan cannot be made viable.

---

## UBU-D0124: Legitimization makes skeleton Plans human-viable before optional optimization

**Status:** Accepted as provisional planning architecture

**Legitimization** is the planning phase that takes a skeleton Plan and adds the minimum additional constraints and support Tasks required to make the Plan plausibly executable by the user. It converts a dependency-valid but potentially unrealistic skeleton Plan into a minimally human-viable Plan.

Legitimization may add or enforce affect constraints, recovery Tasks, breaks, meals, rest, sleep, transition buffers, setup/teardown time, context-switch limits, motivation constraints, and other human sustainability requirements. It is distinct from later optimization: it asks whether the Plan could be realistically performed, not whether all available value has been added.

The legitimized skeleton Plan is the baseline feasible Plan. Optional Dynamic Tasks, gap-filling work, and higher-value candidate Plans should be compared against it.

If full legitimization is cheap, it can be used as a frequent validity oracle while adding and removing optional Tasks. If full legitimization is expensive, UbU needs semi-legitimization heuristics such as affect-budget estimates, slack preservation, dependency-fragility scoring, user-mode compatibility checks, local repair checks, and legitimacy-delta estimates before invoking full legitimization on finalist candidates.

**Consequences:**

- Planning phases are skeletonization, legitimization, candidate expansion, finalist validation, and user-facing explanation.
- Affect and recovery are not decorative wellness features; they can be required for Plan legitimacy.
- Semi-legitimization becomes an important algorithmic open question if full legitimization is expensive.

---

## UBU-D0125: Compact Calendar search is GPU-aware hybrid planning

**Status:** Accepted as implementation direction

UbU should not assume that the central planning engine is a CPU-heavy exact solver. Solver/library selection should treat GPU suitability as a first-class criterion across mobile devices, laptops/desktops, user-owned workers, and cloud providers.

The preferred architecture is hybrid. CPU or conservative exact logic handles dependency graph traversal, skeleton validity, hard constraints, contradiction diagnosis, final validation, and explanation. GPU-capable methods handle large candidate expansion, stochastic scenario simulation, affect scoring, robustness scoring, learned-model inference, and premium cloud planning.

Existing CPU-oriented solvers such as CP-SAT, SMT/MaxSMT, or local-search systems may remain useful for prototypes, exact finalist validation, contradiction explanation, and desktop/server experiments. They should not become the only planning path if GPU-friendly search, simulation, or scoring better matches available compute.

**Consequences:**

- GPU search may propose candidate Plans, but hard constraints and final validity should be certified by exact or conservative validation.
- Mobile and cloud planning should favor batch evaluation, scenario simulation, and scoring methods that map to GPU-like hardware.
- Premium cloud planning can offer wider horizons and more candidate evaluation without becoming the source of user authority.

---

## UBU-D0126: Mobile planning is real-time stewardship, not full global optimization

**Status:** Accepted as mobile planning UX direction

A mobile device has the least computational headroom but the highest demand for immediate user-facing adaptation. Mobile UbU therefore should not be designed as the full global planner. Its role is real-time stewardship of Plan legitimacy, user agency, and next-action clarity.

Beyond short-horizon BFS precomputation, compact Calendars should support decision envelopes, protected/flexible/disposable region metadata, last-legitimate-Plan repair, precomputed repair recipes, fast local policy selection, progressive planning feedback, cached explanations, conflict severity levels, next-best-action mode, opportunistic idle/charging computation, optional remote assist without dependency, and uncertainty-aware UI.

The MVP-friendly subset is narrower: Task criticality, last legitimate Plan storage, simple repair rules, conflict severity levels, cached explanations, next-best-action mode, and basic decision envelopes.

**Consequences:**

- Mobile should preserve hard commitments, legitimacy, and user agency even without cloud or desktop help.
- Mobile should provide credible next actions and explanations quickly, then refine when more compute becomes available.
- BFS branch caching remains useful but is not the only fast-changing-plan UX mechanism.

---

## UBU-D0127: VoxPopuli is an optional EthConf demo, not a Phase 1 replacement

**Status:** Accepted as optional outreach/demo concept

UbU may demonstrate an optional **VoxPopuli** flow at EthConf: before structured bootstrap questions, a user speaks freely about what they wish would happen, what feels disorganized, or what kind of planning help they want. An LLM-assisted extractor converts that natural-language input into candidate Objectives, Tasks, constraints, preferences, and planning assumptions for the user to inspect, correct, accept, or reject.

The value of this flow is demonstration and trust-building. It shows that LLMs can help turn abstract human concerns into explicit structured planning material, while UbU remains the inspectable planning system that consumes accepted structures.

This must not override the Phase 1 narrow bootstrap requirement. VoxPopuli is optional, experimental, and useful for EthConf/public demonstrations only if it does not displace higher-priority dogfooding, contributor, or funder deliverables.

**Consequences:**

- VoxPopuli can be presented as a populist hook for general users and funders.
- It must remain inspectable: LLM output is candidate state, not canonical truth.
- It should not imply broad autonomous life modeling, therapeutic authority, or complete personal-data ingestion in Phase 1.

---

## UBU-D0128: Planning horizons may exceed visible Calendar windows and should front-load fragile prerequisites

**Status:** Accepted as provisional planning architecture

The user-visible Calendar window and the internal planning horizon do not have to be identical. If the user asks for a one-day Calendar, UbU may need to reason beyond that visible window to avoid cutting dependency chains, Techniques, deadlines, or preparation sequences at the boundary.

Within reasonable detailed planning windows, such as one day to roughly one week, UbU may use a bias toward completing fragile prerequisite work as early as reasonably viable. This is intended to reduce last-minute impossible choices, especially when later interruptions, affect deterioration, external events, or user overrides would otherwise threaten a tight dependency chain.

This early-preparation bias is not unlimited. Beyond a reasonable detailed horizon, preparation may be too premature or speculative. Long-horizon preference and temporal-discounting questions remain separate from short-horizon operational planning. For short operational windows, UbU may treat time discounting as negligible by default, while still respecting explicit user Preferences and current affect.

**Consequences:**

- Internal look-ahead may exceed the visible Calendar window.
- Fragile prerequisite chains should be protected from just-in-time scheduling when practical.
- Early preparation is a risk-reduction bias, not an authorization to fill all future time with preparatory work.
- Detailed planning beyond roughly one week remains a higher-cost or premium/research direction rather than a Phase 1 default.


---

## UBU-D0129: Phase 1 bootstrap and next-action UX uses explicit object-backed minimum loop

**Status:** Accepted

Resolved question: `UBU-Q0050`.

The minimum Phase 1 bootstrap interview asks only enough to recommend one useful dogfooding Task from explicit state. The required questions are:

1. `What are you trying to move forward right now?`
2. `Which project context should UbU use for this first session?`
3. `How much usable time do you have for the next work window?`
4. `Is there a deadline, meeting, release target, or external event that changes what matters today?`
5. `What work should UbU consider first?`
6. `What is already blocked, unavailable, or not worth recommending right now?`
7. `How are your energy, stress, and mood right now?`
8. `When choosing between useful work, what should UbU favor today?`

The answers map into existing Phase 1 objects. Project context, availability, deadlines, constraints, fixture/import source, and hard blockers become UniverseState facts, External Events, Tasks, External References, and Log entries as appropriate. Affect answers become a user-declared Snapshot; skipped or stale affect data creates or prioritizes an affect-collection Task. Initial work answers seed Objectives and Tasks. Tradeoff answers become Preferences only when UbU presents an explicit Preference statement and the user accepts it; otherwise they remain Log notes, Objective annotations, or noncanonical preview/review evidence.

The minimum data required to recommend one next Task is: a user or operator Identity, at least one active Objective, at least one active schedulable Task linked to that Objective, a current work window or available time, current or explicitly stale affect state, and known blockers, deadlines, dependencies, and source references for the recommended Task when available. If that minimum is missing, UbU should recommend a clarification, import, Calendar preview, Log review, or affect-collection Task rather than pretending to optimize.

The next-action screen shows one recommended Task by default, but full Plan inspection remains one action away. The screen must show the Task title, Objective link, estimated duration or work window, status, provenance/source label, why it matters now, and what UbU considered. The explanation must include the served Objective, timing reason, dependency or blocker status, affect or stale-affect status, and the most relevant risk or opportunity considered. It should expose candidate Tasks, blocked Tasks, constraints, worker/projection state, and fixture/import source links through an inspector rather than hiding them.

The required controls are `start`, `done`, `snooze`, `reject`, `decompose`, `override`, and `explain more`. Completion feedback asks whether the estimate and effect were correct and whether affect changed. Failure feedback asks which assumption failed: dependency, duration, affect, interruption, clarity, priority, or other. Snooze asks for a time or condition and reason. Rejection asks whether the Task is wrong, not valuable now, blocked, too large, already done, duplicate, or moot. Override records the chosen action and asks whether this should update Preferences, availability, estimates, Objective status, or only the current Plan. All outcomes write Logs and trigger recalculation when they change modeled state.

Fixture-backed and mock app behavior must be labeled at the point of use. Public demos and Release Outreach Pipeline scripts should use this loop as the main nontechnical proof: bootstrap, one recommended next Task, explanation, feedback, recalculation, and full-Plan inspection. They must distinguish implemented planner behavior from hardcoded or fixture-backed behavior.

Public materials must avoid claims that Phase 1 already performs broad personal-data ingestion, complete email/text/file understanding, therapeutic care, autonomous life coaching, complete planning automation, complete privacy isolation, Phase 2 sync, or Phase 3 multi-user coordination. The honest Phase 1 claim is that UbU can recommend one meaningful next action and explain it from explicit user-approved state, fixtures, imports, Logs, Snapshots, Objectives, Tasks, and Plans.

**Consequences:**

- `UBU-Q0050` is resolved for Phase 1 product scope and demo treatment.
- No new canonical object type is required for the bootstrap or next-action UX.
- Phase 1 implementation can proceed with existing Objectives, Preferences, Snapshots, Tasks, Logs, UniverseState facts, Plans, and External References.
- Preference calibration, discovery mode, Calendar preview and Log review annotations, VoxPopuli, and broader message or file ingestion remain in their separate questions.
- The mock app may be fixture-backed only when it visibly labels fixture behavior and does not present it as completed planner implementation.

---

## UBU-D0130: UniverseState mutations use dotted targets and envelope-level provenance

**Status:** Accepted

Resolved question: `UBU-Q0014`.

MVP UniverseState mutation items use dotted string targets. The first target segment names the UniverseState collection: `facts`, `numeric_values`, `set_memberships`, or `event_markers`. Remaining segments form the lightweight namespaced key within that collection. Examples include `facts.github.issue.14.pipeline_state`, `numeric_values.affect.energy`, `set_memberships.github.issue.14.labels`, and `event_markers.relationship.rel_123.interactions`.

A mutation item has required `operation` and `target` fields. `payload` is required for all operations except `clear_fact`. `note` is optional for human-readable context. Mutation items do not carry item-level `confidence`, `source`, or `provenance` in MVP; those belong on the containing Task effect, Snapshot, Log entry, worker mutation request, External Reference, import artifact, or projection envelope.

Payload rules are operation-specific. `set_fact` accepts any JSON-compatible value. `clear_fact` has no payload. `increment_numeric` and `decrement_numeric` require numeric delta payloads. `add_membership` and `remove_membership` require JSON scalar member payloads, usually strings. `append_event_marker` requires a JSON object payload representing the lightweight marker.

Mutation lists are unconditional once the containing Task effect succeeds. Per-item conditions are not part of the MVP mutation schema; conditional behavior belongs in Task preconditions, effect success probability, planner branching, or worker/request validation. Implementations should validate the full mutation list before application and apply valid items in list order.

Mutation targets may include affect UniverseState keys in `user_mode`, subject to Snapshot precedence and user sovereignty rules. Organization-mode and worker-mode validators must reject intrinsic-affect mutations. Mutation targets may include Relationship-relevant UniverseState keys, including relationship interaction markers and maintenance facts, but they must respect Compartment policy, mode rules, provenance/logging envelopes, and user-acceptance requirements for private or inferred relationship claims. Task effects, workers, imports, and LLM-assisted flows must not silently overwrite user-declared private affect or Relationship truths.

**Consequences:**

- `UBU-Q0014` is resolved for Phase 1 implementation.
- Task effects, worker mutation requests, Snapshots, and Logs can share a compact mutation vocabulary without duplicating provenance on every item.
- `UBU-Q0015` can use the same dotted target convention for preconditions.
- `UBU-Q0009` can wrap these mutation items in worker mutation requests that provide authority, expected prior version, evidence, confidence, idempotency, and provenance.
- Future schema migrations may replace dotted strings with typed paths or JSON Pointer, but MVP implementations should not block on that stricter ontology.


---

## UBU-D0131: Task preconditions use recursive all_of/any_of predicates

**Status:** Accepted

Resolved question: `UBU-Q0015`.

MVP Task preconditions use a recursive boolean object with `all_of` and `any_of` arrays for simple AND/OR composition. A precondition node may be a group node or a leaf predicate. A group node contains `all_of` or `any_of`, each holding one or more precondition nodes. A leaf predicate contains `target`, `predicate`, and optional `expected`.

Precondition targets use the same dotted UniverseState target convention accepted for mutations. The first segment names the UniverseState collection: `facts`, `numeric_values`, `set_memberships`, or `event_markers`. Remaining segments form the lightweight namespaced key inside that collection.

MVP predicates are `equals`, `member_of`, and `absent`. `equals` compares the target value to a JSON-compatible `expected` value. `member_of` checks whether the JSON scalar `expected` value is present in the target set membership. `absent` checks that the target is not present or has been cleared, and does not use `expected`. Numeric comparisons such as greater-than, less-than, ranges, thresholds, and arithmetic expressions are not in MVP.

Preconditions may reference `event_markers` for deterministic marker presence or equality checks. Preconditions may reference affect-related UniverseState keys in `user_mode`, subject to Snapshot precedence and user sovereignty rules; organization-mode and worker-mode validators must reject intrinsic-affect preconditions. Preconditions may reference Relationship-relevant UniverseState keys, including relationship interaction markers and maintenance facts, but private or inferred relationship claims remain subject to Compartment policy, mode rules, provenance/logging envelopes, and user acceptance where required.

A failed precondition makes the Task blocked for planning and execution. It does not make the Task invalid. `unschedulable` is a derived planner result when an otherwise valid Task cannot be placed in the current Calendar scope while satisfying preconditions and Calendar Logic. `invalid` is reserved for malformed Tasks, malformed precondition schema, forbidden targets, or canonical-state contradictions. Unknown, unavailable, or partially modeled preconditions are treated as absent in MVP unless the user or importer explicitly records a deterministic predicate.

**Consequences:**

- `UBU-Q0015` is resolved for Phase 1 implementation.
- Preconditions and mutations share the same dotted target convention, keeping Task effects and Task gating aligned.
- Phase 1 gets deterministic blocked/not-blocked evaluation without adding numeric comparison logic or a richer ontology.
- Event markers, affect keys, and Relationship-relevant keys are usable only within existing mode, Compartment, provenance, and user-acceptance boundaries.
- Planner diagnostics can distinguish blocked, unschedulable, and invalid Tasks without treating ordinary failed preconditions as schema errors.

---

## UBU-D0132: Realtime multimodal LLMs are optional interaction backends, not authoritative planners

**Status:** Accepted

Direct project directive.

Realtime multimodal LLMs may power live voice, video, interruption detection, meeting capture, discovery mode, pronunciation or activity feedback, and short-horizon task monitoring. They are interaction backends and perceptual/extraction aids, not the authoritative UbU planner.

Realtime model output must enter UbU as structured, provenance-bearing candidate updates. Examples include `ObservedEvent`, `UserInterruption`, `TaskProgressDelta`, `AffectSignal`, `PlanDeviation`, `ExternalConditionChange`, `ClarificationQuestion`, `WorkItemCandidate`, `LogEntryCandidate`, and `AssociationAttestationCandidate`.

UbU distinguishes **model-time awareness** from **planner-time semantics**. A realtime model may notice elapsed time, silence, overlapping speech, interruption, or a changing audiovisual scene. UbU's planner remains responsible for deciding whether that observation changes Task state, Calendar validity, Plan legitimacy, Logs, Objectives, or recalculation triggers.

Realtime operation requires explicit user-visible modes, such as passive/off, text-only, voice session, active discovery mode, meeting/logging mode, high-privacy local-only mode, and cloud-assisted mode. Continuous capture must not become covert surveillance or an implied authorization to mutate canonical state.

**Consequences:**

- Realtime LLMs should be swappable providers behind a policy-routed interaction interface.
- Realtime-derived observations are candidate evidence until admitted through UbU validation, review policy, and Logs.
- The planner, Compartment policy, Identity model, and user-review rules remain authoritative.
- UX should show when realtime/discovery/privacy modes are active and what kind of data may be captured, retained, or routed.

---

## UBU-D0133: LLMs are replaceable cognitive backends and structured outputs are candidate updates

**Status:** Accepted

Direct project directive.

UbU should treat LLMs as replaceable cognitive backends. They may interpret, summarize, classify, translate, transcribe, propose structures, critique plans, call tools, generate UI drafts, and assist extraction. They do not own canonical truth, canonical value, canonical memory, or canonical planning state.

Strict schemas and structured outputs are necessary but not sufficient. A JSON object that satisfies a schema may still be semantically wrong, policy-invalid, Compartment-invalid, dependency-invalid, affect-invalid, stale, maliciously influenced, or unsupported by evidence.

The admission pipeline is therefore:

```text
LLM output
  -> schema validation
  -> semantic validation
  -> policy and Compartment validation
  -> provenance attachment
  -> conflict detection
  -> user-review classification
  -> planner or Log admission
```

Memory must remain typed, scoped, provenance-bearing, and correctable. UbU should prefer explicit objects such as `Preference`, `Objective`, `Identity`, `Association`, `TaskPattern`, `AffectPattern`, `PlanningConstraint`, `ExternalReference`, `Attestation`, `Snapshot`, `LogEntry`, and `Evidence` over vague assistant personalization.

**Consequences:**

- LLM output is a candidate state update unless accepted through explicit UbU logic.
- Corrections should preserve an audit trail and mark dependent interpretations stale where appropriate.
- Generic model memory features do not replace UbU's typed memory model.
- The FOSS core should avoid vendor-specific assumptions about model identity, memory behavior, or structured-output guarantees.

---

## UBU-D0134: Context assembly is a privacy-relevant governed act

**Status:** Accepted

Direct project directive.

As LLM context windows grow, UbU must not assume that sending more context is automatically better. Context assembly is itself a privacy-relevant action that may cross Identity, Compartment, Association, provider, and retention boundaries.

A future `ContextBundle` should describe why context was assembled and what it exposed:

```text
ContextBundle
  - purpose
  - source object references
  - Compartments included
  - Identities exposed
  - Association references exposed
  - provider or model destination
  - redaction/minimization rules
  - retention and expiration policy
  - user-visible summary
  - downstream candidate updates supported
```

**Consequences:**

- Long-context models weaken naive RAG assumptions but strengthen the need for context-governance metadata.
- Context minimization remains a core privacy principle even when a model can technically ingest a huge repository, chat archive, or life-log segment.
- Compartment policy and disclosure rules apply to context construction, not only to final outputs.

---

## UBU-D0135: UbU should be both an MCP-style client and an MCP-style server with capability boundaries

**Status:** Accepted

Direct project directive.

UbU should support MCP-style integration boundaries in both directions.

As a client, UbU can connect to external tools and data sources such as GitHub, calendars, email, local scripts, file stores, home automation, and model/agent services.

As a server, UbU may expose narrow, scoped, reviewable affordances to outside agents, such as:

- create candidate Task;
- read a current Plan summary;
- append or submit a Log candidate;
- request user clarification;
- submit a proposed Plan repair;
- query Objective status;
- submit a candidate AssociationAttestation;
- request a Delegation Substrate review packet.

Every exposed tool must be bounded by Identity, Compartment, Objective, capability grant, operation kind, time window, provenance, and review policy. The dangerous pattern is letting an external AI agent access the user's life model as a broad ambient authority. The UbU pattern is exposing narrow capability surfaces under user-owned law.

**Consequences:**

- MCP-style interoperability belongs in the architecture, but it does not override Compartments or user sovereignty.
- External agents should generally submit candidate updates, not direct canonical writes.
- Tool exposure is part of the Delegation Substrate and should be auditable.

---

## UBU-D0136: Delegated agency is first-class in planning

**Status:** Accepted

Direct project directive.

UbU Tasks may be performed by the user, a local agent, a cloud agent, a tool, another human Identity, an Association, or a delegated coordinator. The executor is part of the planning problem and must not be hidden inside an opaque automation step.

A delegated Task should distinguish:

- Task intent;
- authorization source;
- executor;
- observer;
- reviewer;
- granted authority;
- expected output;
- completion evidence;
- privacy/Compartment scope;
- reversible and irreversible side effects;
- failure and escalation path.

An agent completing a Task is not semantically identical to the user completing it. Delegation changes trust, responsibility, review, provenance, affect cost, and side-effect risk.

**Consequences:**

- Task assignment should evolve from a simple user/worker field into an executor and authority model.
- Computer-use agents, remote agents, human helpers, and Associations all require explicit scope and evidence rules.
- Delegation belongs in the planning model even before a public marketplace exists.

---

## UBU-D0137: Delegation Substrate is the near-term model for preparing Task delegation

**Status:** Accepted

Direct project directive.

Use **Delegation Substrate** as the near-term tool/model for preparing Task delegation. It is not the full Skill Barter marketplace. It is the explicit representation that makes a Task ready to be performed, reviewed, or handed off by clarifying purpose, executor, authority, expected output, evidence, constraints, and completion criteria.

The Delegation Substrate is also valuable for Tasks the user intends to perform solo. Formalizing the same fields can act as a self-reminder of how and why the Task needs to be performed, what evidence would show completion, what authority is being used, and what constraints matter.

A minimum Delegation Substrate packet may include:

```text
DelegationPacket
  - Task or Objective reference
  - intended executor type
  - purpose / why this matters
  - expected output
  - authority granted or self-authority note
  - required evidence of completion
  - review requirement
  - privacy and Compartment scope
  - allowed tools or integrations
  - deadline / timebox
  - failure and escalation path
```

**Consequences:**

- Phase 1 may include Delegation Substrate-compatible fields when needed for dogfooding, worker assignments, or self-reminder clarity.
- The full Skill Barter marketplace remains future scope.
- Delegation Substrate should integrate naturally with Automation Workers, MCP-style tools, Logs, and capability grants.

---

## UBU-D0138: General Contractor is a first-class delegated coordination role

**Status:** Accepted

Direct project directive.

A **General Contractor** is an Identity, Agent, or Association delegated authority to coordinate multiple subordinate executors in order to satisfy an Objective or complete a Container of Tasks, subject to explicit authority, budget, privacy, review, evidence, and escalation constraints.

This role is distinct from an ordinary executor. A General Contractor may decompose work, assign subtasks, supervise human or agent executors, collect evidence, report status, and submit candidate updates. UbU must still model the General Contractor's authority as bounded and reviewable.

**Consequences:**

- General Contractor belongs in the Delegation Substrate as a high-value coordination specialization.
- General Contractor may be human, agentic, or Association-based.
- Subdelegation requires explicit authority, provenance, evidence, and review semantics.
- The role supports larger adaptive work campaigns without flattening humans, agents, and tools into a single undifferentiated actor type.

---

## UBU-D0139: Skill Barter marketplace is an outreach and future-market direction, not a Phase 1 marketplace commitment

**Status:** Accepted

Direct project directive.

The **Skill Barter marketplace** should be presented as a future marketplace direction and EthConf NYC outreach hook, especially for cypherpunk and privacy-oriented audiences. It signals that UbU preserves much of the original cryptocurrency ethos: voluntary coordination, sovereign identity, privacy, open markets, FOSS development, pseudonymous capability, and user-controlled settlement references where lawful.

Skill Barter can attract younger developers with drive, time, and interest in FOSS contribution by showing that UbU is not merely another productivity app. It is a coordination substrate that could eventually support privacy-preserving skilled-work exchange among human and agentic executors.

A mature Skill Barter marketplace would naturally create demand for FHE, ZK, secure compute, private reputation, private escrow-like commitments, selective disclosure, and other high-privacy technologies compatible with the future Ethereum ecosystem. This should remain an architectural and outreach signal, not a token-first or speculation-first positioning.

**Consequences:**

- EthConf outreach may include Skill Barter as a cypherpunk “cool factor” lane.
- MVP implements Delegation Substrate primitives, not a public marketplace.
- Public language should avoid illicit-market, tax-evasion, sanctions-evasion, dark-market, worker-classification, or exploitative labor framing.
- Skill Barter should be framed as voluntary, lawful, privacy-preserving coordination and FOSS contributor discovery.

---

## UBU-D0140: Computer-use and background agents require authority, audit, rollback, and prompt-injection handling

**Status:** Accepted

Direct project directive.

Computer-use agents and background agents are high-risk external actors, not ordinary pure functions. They may operate browsers, accounts, files, credentials, APIs, and external systems where prompt injection, irreversible side effects, disclosure, or stale assumptions can cause harm.

Future `AgentAction` or `BackgroundProcess` models should record:

```text
AgentAction / BackgroundProcess
  - executor Identity or agent reference
  - trigger or schedule
  - authority scope
  - credentials or integrations used
  - Compartment and Identity scope
  - external surface touched
  - irreversible side-effect flag
  - prompt-injection exposure level
  - compute/cost budget
  - notification policy
  - rollback or mitigation path
  - completion evidence
  - failure and escalation policy
```

**Consequences:**

- Background tasks are not automatically Calendar events because they may consume compute, credentials, money, privacy budget, or attention without occupying user time.
- External agents should generally submit candidate updates and evidence rather than silently mutating canonical state.
- Prompt-injection exposure should be tracked when agents read untrusted webpages, messages, documents, or tool outputs.

---

## UBU-D0141: Local/on-device inference is a first-class execution tier

**Status:** Accepted

Direct project directive.

UbU should treat local and on-device inference as a first-class execution tier, not merely a fallback for unavailable cloud models. Local inference supports privacy, offline use, lower marginal cost, responsiveness, and user sovereignty.

A provisional execution hierarchy is:

```text
Tier 0: deterministic local code
Tier 1: small local/on-device model
Tier 2: user-owned desktop or worker model
Tier 3: user-selected cloud model via BYOK
Tier 4: optional UbUCorp-managed hosted service
```

Local models may handle first-pass extraction, privacy classification, simple message triage, candidate Task/Log creation, affect journaling summaries, and compartment routing. Cloud or larger models may be reserved for high-complexity planning, deep design review, organizational introspection over large archives, difficult ambiguity resolution, and expensive multimodal reasoning when policy allows.

**Consequences:**

- The FOSS core should remain useful without mandatory hosted inference.
- Provider routing should consider sensitivity, cost, latency, offline state, task complexity, and available local hardware.
- Cloud assistance is a capability upgrade, not the philosophical center of UbU.

---

## UBU-D0142: UbU UX should evolve into a state-transition cockpit

**Status:** Accepted

Direct project directive.

UbU should not be framed as chat plus calendar. The long-term UX should become a **state-transition cockpit**: a user interface that presents the current WorkItem, relevant state, candidate transitions, constraints, explanations, evidence, and review controls.

The Phase 1 one-next-Task UX remains the narrow proof. Later interfaces may adapt the visible control surface to the current state transition:

- reply to a message;
- choose or start the next Task;
- review a Log discrepancy;
- repair a Plan conflict;
- inspect a Delegation Substrate packet;
- approve or reject an agent action;
- review an AssociationAttestation;
- run organizational introspection;
- publish a projection.

**Consequences:**

- Generative UI and chat-native app surfaces can be interaction layers, but the user should remain oriented around explicit state transitions.
- The main interface should preserve one-next-action clarity while allowing deeper inspection.
- The UX should make candidate versus canonical state visually and operationally distinct.

---

## UBU-D0143: Community-specific EthConf briefs are derived presentation layers

**Status:** Accepted

Direct project directive.

UbU should maintain a small set of community-specific derived documents for EthConf and adjacent outreach when the audience has a materially different trust barrier, motivation, or call to action.

The durable derived audience documents are:

- `README.md` for upcoming technical contributors and technically serious readers who need the project entry point;
- `OUTREACH.md` for FOSS maintainers and general software engineers who may become technical contributors;
- `PM_BRIEF.md` for project leads, technical PMs, protocol leads, release coordinators, and people coordinating autonomous contributors;
- `FUNDER_BRIEF.md` for grantmakers, sponsors, hackathon judges, aligned funders, and prototype funders;
- `SOVEREIGN_COORDINATION.md` for cypherpunks, privacy engineers, Ethereum privacy builders, FHE/ZK/secure-compute researchers, and sovereign-coordination audiences;
- `ORG_INTROSPECTION_BRIEF.md` for mission-driven projects, FOSS maintainers, nonprofits, DAOs, foundations, and teams that want evidence-backed mission alignment.

These files are presentation layers. They must not introduce new design authority. Their source of truth remains `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`.

**Consequences:**

- Audience-specific documents may reframe accepted decisions, but should not create new canonical claims.
- Consistency checks should include all derived audience documents.
- When a derived audience document conflicts with canonical design files, the derived document should normally be patched.
- The documentation set should remain small; new audience files require a materially distinct audience frame or call to action.
- EthConf outreach can route different communities to different briefs without fragmenting UbU's source of truth.

---

## UBU-D0144: Inter-instance protocol is a generic envelope family with worker API profiles

**Status:** Accepted

Resolved question: `UBU-Q0011`.

UbU should have one generic inter-instance protocol family for communication between UbU instances, worker-mode instances, and future compatible peers. The protocol is a family of typed envelopes with shared authority, provenance, Compartment, identity, idempotency, versioning, and review semantics, not one undifferentiated endpoint that treats every payload as the same kind of action.

The protocol should eventually support at least these payload families:

- contextual messages and Message Context Envelopes;
- worker assignments and assignment responses;
- status updates and check-ins;
- mutation requests and projection requests;
- capability grant issuance, acknowledgement, rotation, and revocation;
- External Event submission;
- Snapshot or Log candidate submission where authorized;
- recalculation requests;
- clarification requests and responses.

Phase 1 worker communication is a separate MVP API surface in implementation terms, but it is intentionally a narrow profile of the future inter-instance protocol. The MVP worker API should not try to implement native user-to-user messaging, peer discovery, Association reconciliation, or generic multi-user transport. It should, however, use compatible envelope concepts wherever cheap: parent instance reference, sender Identity, receiver or parent Identity, capability grant reference, payload kind, target references, expected prior version or idempotency key where relevant, provenance, Compartment/export decision, and required review policy.

Workers still do not receive direct canonical write authority in Phase 1. Worker payloads submit External Events, Snapshots, mutation requests, projection requests, status updates, or recalculation requests to the canonical instance. The canonical instance validates authority and policy, then applies or rejects the candidate update and writes the Log entry.

Phase 3 multi-user Identity coordination should extend the same protocol family rather than invent a second unrelated transport. User-to-user requests, status updates, questions, commitments, blockers, and contextual messages are peer payloads under the same envelope discipline. They may carry different review defaults and disclosure rules from worker payloads, but they still obey Identity, Compartment, capability, provenance, admission, and user-sovereignty boundaries.

This decision resolves the architecture-level question only. Concrete schemas for worker mutation requests, worker assignment, Message Context Envelopes, legacy adapter upgrade paths, capability grant exchange, and Association-related coordination remain in their dedicated open questions.

**Consequences:**

- `UBU-Q0011` is resolved at the architecture level.
- MVP worker communication remains implementable as a small local or parent-specific API without blocking on the full Phase 3 protocol.
- The MVP worker API should approximate future inter-instance envelopes enough to avoid a future schema contradiction.
- Phase 3 cross-user communication can reuse shared envelope semantics while adding user-to-user disclosure, message, commitment, and Association-specific payloads.
- Direct canonical writes remain forbidden for workers unless a later accepted decision changes the authority boundary.

---

## UBU-D0145: Phase 1 risk reports are derived artifacts, not canonical risk objects

**Status:** Accepted

Resolved question: `UBU-Q0018`.

Risk reports in MVP are derived, recalculable analyses over Calendars, Plans, Tasks, Logs, Snapshots, External Events, worker status, External References, and compact Calendar metadata. Risk remains reportable state, not a first-class canonical object.

The Phase 1 MVP risk-report set is:

- `p90_completion_time`;
- `critical_path`;
- `deadline_miss_probability`;
- `affect_constraint_violation_probability`;
- `low_compact_calendar_coverage_warning`;
- `dependency_fragility`;
- `worker_or_automation_bottleneck`;
- `stale_affect_warning`;
- `destructive_pressure_warning`;
- `post_plan_depletion_warning`.

Additional findings may be computed when source data is already available, but they are not required Phase 1 reports: relationship-maintenance neglect, preference uncertainty, repeated override or deviation patterns, motivation mismatch, stale or missing discovery-mode reconciliation, and overdue Calendar preview or Log review.

Risk reports are computed on demand from the current Calendar or Plan. Implementations may cache a risk-report artifact with a Calendar, Plan, run artifact, release package, or UI view for auditability and performance. Cached reports are derived state and must be invalidated or marked stale when relevant Tasks, Logs, Snapshots, External Events, worker status, compact Calendar coverage, or recalculation triggers change.

Automation Workers may compute or refresh risk-report artifacts only through explicit capability grants. Worker-produced risk reports are advisory until admitted by the canonical instance. Workers may submit report artifacts, refresh requests, mutation requests, or projection requests according to authority; they do not create canonical Risk objects or directly mutate Tasks.

Risk reports may recommend follow-up Tasks or submit Task candidates through the normal request/review path, but they must not silently create canonical Tasks in MVP. Typical follow-ups include clarification, affect collection, dependency repair, worker retry or escalation, Calendar regeneration, Log review, Calendar preview, and GitHub projection or reconciliation.

Risk reporting is part of UbU-runs-UbU release ceremonies. Release readiness and Release Outreach Pipeline packages should include deadline risk, critical path, dependency fragility, worker or automation bottleneck, and low coverage warnings when inputs exist, while respecting Compartment, Identity, export, and public-projection boundaries.

UbU's PERT-superiority demonstration should be precise: Phase 1 should not claim to replace every PERT use. It should show that UbU handles the planning dimensions PERT leaves out: explicit preconditions and UniverseState, affect constraints, worker status, compact Calendar coverage, recalculation from Logs and Snapshots, and actionable Plan repair or next-Task recommendations.

**Consequences:**

- `UBU-Q0018` is resolved for Phase 1 implementation.
- Risk remains non-canonical derived analysis rather than a new MVP entity.
- MVP implementation can expose the required report set without settling every future risk category.
- Risk-report caches and release artifacts are reviewable derived artifacts, not accepted design state or canonical user value.
- Follow-up Tasks from risk findings use ordinary Task creation, worker mutation request, or user approval paths.
