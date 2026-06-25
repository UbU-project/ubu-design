# UbU

**Status:** Phase 0 complete — demonstrated at ETHConf NYC, June 8–10, 2026 / Phase 1 implementation in progress: the `UbU-project` constellation is store-backed and the internal first-person loop is self-sustaining end to end — the bootstrap records the initial UniverseState facts, preconditions gate planning, a Monte-Carlo-rollout-ranked affect-legitimized Calendar with humane risk and plan-quality feedback recommends the next Task, and a completed Task's effects mutate the facts so the next plan reflects the acted-on world; GitHub projection writes are gated by a deny-by-default export boundary; live GitHub is the remaining feature  
**Repository:** `ubu-design`  
**Primary purpose:** Canonical public design state for the UbU project  
**Derived file:** This README is a technical contributor entry point. The canonical design authority is `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, `PLANNING_KERNEL_CONTRACT.md`, and `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`.

---

## What is UbU?

UbU is a privacy-first life-logistics engine: a system that helps an individual human being turn a desired outcome or real-world problem into a legitimate, executable plan by coordinating time, Tasks, Resources, Skills, Techniques, money, affect, external constraints, expert help, and available markets.

It is intended to convert messy real-world inputs — tasks, calendar events, messages, external events, user preferences, physical and affective state, GitHub/project data, realtime interaction streams, agent or worker outputs, and integration data — into explicit, inspectable, recalculable plans.

UbU is not merely a task list, calendar application, chat assistant, or project-management dashboard. Its root product is the individual human life-logistics engine: a system that models desired outcomes, constraints, risks, dependencies, available time, human limitations, Resource readiness, and Skill capability, then helps determine what should happen next. Organizational coordination is an important emergent property of the same model.

The canonical UbU use-case formula is:

> **Objective + Current State + Constraints + Resources + Skills + Techniques + Preferences + External Options → Legitimate Plan**

The deeper purpose is to help people build the capabilities, resources, routines, and relationships needed to actually live the life they choose — not just to schedule it.

The first MVP is deliberately narrow: use UbU to coordinate the design, development, release, and maintenance of UbU itself.

---

## Core philosophy

UbU is based on several design principles.

### User sovereignty

The user is the final authority over what the user wants, what occurred, and which candidate model updates are accepted. UbU can propose, explain, and warn, but it should not become an unaccountable authority over the user's life model.

### Explicit value

Value is attached to Objectives through user-defined Preferences. Numeric utilities may be derived for planning, but they are transient computational artifacts, not canonical user values. Preference-calibration examples can help during onboarding and review, but they become canonical only if the user accepts or edits them.

### Explicit planning

Planning must remain explicit, constraint-based, inspectable, and recalculable. LLMs may interpret messy inputs, generate candidates, score alternatives, or critique artifacts, but canonical planning logic should not be hidden inside opaque model behavior.

### Privacy-first architecture

UbU is designed around local-first operation, compartmentalized data, multiple Identities, bounded disclosure, explicit EvidenceUsePolicy, and user-controlled sharing. External tools, cloud models, and worker processes should receive narrow authority rather than ambient access to the user's life model.

### Affect-aware planning

In `user_mode`, human affect is part of the planning problem. Energy, stress, tiredness, mood, attention, boredom, emotional load, recovery, and related constraints matter because a plan that ignores the human executor can become fiction.

### Generative, introspective, and user-sovereign

UbU is a generative layer, not a reactive one. It originates what is worth doing from the user's own Objectives, values, affect, and attention, rather than only constraining or auditing what some agent already decided. It works from the user's *introspected* state — what the user reports and reconciles about themselves — rather than from inferred sensor data, because intent and affect are not sensor-readable. Agents and external models are downstream executors of plans UbU produced, never the authority over the user's life model. The novelty is not the problem but the integration: an open, user-owned, generative goal-and-values layer that does not yet exist as a whole.

### First-person legibility

Phase 1 must remain understandable as a simple first-person loop: answer a few bootstrapping questions, preview a candidate Calendar, receive one recommended next Task, inspect why it matters now, act or override, and let UbU learn from what actually happened.

### Resource and Skill readiness

Many life-planning failures happen because the user lacks something needed to do the work. UbU's long-term model treats **Resources** as external prerequisites and **Skills** as Identity-owned capabilities.

Resources include documents, tools, ingredients, credentials, software licenses, API keys, locations, payment methods, quiet spaces, and other stateful things a Task may need. Skills include capabilities the user can learn, test, forget, refresh, and evidence.

This is not Phase 1 scope, but it is central to the full product. Phase 3 should try to add a thin Resource/Skill-aware task-readiness layer. Phase 3B and Phase 4+ form the full version 1.0 release track, including richer Resource, Skill, Technique, DIY-versus-purchase/hire, inventory, financial-management, and Skill Barter features.

Resources also include community and public Resources: library tool loans, makerspace equipment, public workshops, community gardens, seed libraries, and repair cafés. UbU should eventually support a Library and Community Resource Mode that turns publicly accessible Resources into first-class planning inputs.

### Attention sovereignty

A full-product direction (outside Phase 1 scope, like Resource and Skill readiness) is attention sovereignty: cross-channel, values-driven, context-aware governance of interruptions. Because only a user-held life-model knows what the user is doing and wants to protect — information no sensor can read — UbU can decide whether a given notification should arrive now, across email, chat, SMS, and calls. It merges modeled and declared state, surfaces divergence through a mobile Discovery mode, and grades permissiveness as a focus window closes rather than acting as a binary on/off switch. The interruption chokepoint, today held by attention-capturing platforms, moves under the user's control.

### Government and public-resource symmetry

Any institution that can constrain a user's plan may also provide Resources, permissions, remedies, or procedures that improve the user's plan. UbU must model both sides.

This means UbU should not only surface regulations, permits, and legal constraints — it should also surface grants, subsidies, benefit programs, weatherization assistance, workforce training, legal aid, public infrastructure, and other government- or community-supported Resources. Many of these are conditionally unlockable: a user may need to apply for a benefit, collect documentation, or file an appeal before the Resource becomes available. UbU can generate those prerequisite Tasks automatically.

### Identity, authority, and external standards

UbU adopts external identity-and-access standards by layer. The local single-user core remains UbU-native. Standards earn their keep when work crosses from the user's control plane to a counterparty, worker, hosted service, marketplace, federation partner, or commercial wire.

- **SPIFFE/SPIRE is outward-facing.** It is a conformance target for workload identity, worker identity, hosted planning workers, boundary agents, delegation endpoints, marketplace execution, and commercial-wire auditability. SPIFFE does not replace human Identity or user-sovereign Identity.
- **OPA is inward-facing.** OPA may implement the policy checker, but OPA vocabulary does not become UbU vocabulary. UbU speaks in legitimization, adjudication, enforcement gates, capability grants, Compartment policy, and Log provenance.
- **SAML/OIDC is boundary-only.** External enterprise authentication may be supported at the commercial wire when required, with OIDC/OAuth2 preferred for greenfield federation. External IdPs never become the source of truth for user-sovereign Identity.

A SPIFFE ID / SVID authenticates a workload or boundary agent. It does not by itself prove human authority. Authority requires UbU-native capability grants, `authority_source`, `authority_scope`, Compartment policy, Log provenance, and admission/review rules.

No SPIFFE, SPIRE, OPA, OIDC, SAML, SVID issuance, enterprise federation, or commercial-wire identity implementation is required for Phase 1 dogfooding.

### Dogfooding

The Phase 1 MVP should help coordinate UbU's own GitHub issues, pull requests, reviews, CI events, release milestones, design questions, planning-kernel contracts, contributor interactions, and release/outreach artifacts.

---

## Three review patterns: introspection, organizational introspection, and extrospection

These concepts are related, but they should not be collapsed.

### User introspection

User introspection is the personal self-governance review loop. It compares the user's declared Objectives, Preferences, constraints, values, affective reports, Plans, Calendar previews, and Logs against what actually happened.

The goal is to help the user ask questions such as:

- Did I act in a way that served my stated Objectives?
- Did the Plan fail because the model was wrong, because reality changed, or because I chose differently?
- Are my Preferences, constraints, or affect assumptions stale?
- Did I bypass a safeguard, ignore a boundary, or accept discomfort in a way that should be reviewed later?
- Should the system create Tasks, Objective updates, calibration prompts, or revised planning assumptions?

User introspection is not organizational introspection. It is first-person, user-authoritative, privacy-sensitive, and tied to Calendar preview, Log review, affect calibration, and personal model correction.

### Organizational introspection

Organizational introspection is the Association-level version of evidence-backed review. It asks whether an Association's actual work, decisions, resource allocation, overrides, undocumented structure, and informal authority patterns match its declared mission and commitments.

The main mechanism is a reviewable `AssociationAttestation`: a provenance-backed claim about an Association that can be accepted, rejected, edited, disputed, superseded, or archived. Organizational introspection should be useful to mission-driven projects, FOSS maintainers, funders, and contributors, but it must not become managerial surveillance or LLM-declared social truth.

### Extrospection

Extrospection is the Relationship-level review pattern. It helps a user compare their Relationship model, scope assumptions, trust calibration, reciprocity expectations, boundary assumptions, and counterparty-perspective hypotheses against permitted evidence.

Extrospection is constrained by epistemic asymmetry: the user has first-person access to their own perspective, while UbU can only maintain evidence-backed hypotheses about another party's perspective. It should surface evidence in tension, not claim to know another person's inner state.

---

## Canonical and derived files

Canonical design authority is maintained in:

- `DESIGN.md` - canonical design summary
- `DECISIONS.md` - accepted design decisions and anti-regression memory
- `OPEN_QUESTIONS.md` - unresolved questions, prioritization metadata, and automation queue
- `PLANNING_KERNEL_CONTRACT.md` - Phase 1 planning-kernel request/response contract, GPU stage boundaries, duration semantics, affect constraints, and correlation-matrix rules
- `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md` - Phase 2 device sync, Zone, Compartment, partial-replica, and sync-statement contract
- `docs/PHASE1_CONTRACT_BOUNDARIES.md` - Phase 1 schema, Rust, store, planning, GitHub, UI/orchestrator, Compartment, and brand boundaries

Derived public-facing projection files summarize the canonical state for different audiences:

- `README.md` - technical contributor entry point and project summary
- `OUTREACH.md` - outreach document for FOSS maintainers and software engineers
- `PM_BRIEF.md` - project-lead and technical-PM brief
- `FUNDER_BRIEF.md` - grantmaker, sponsor, and prototype-funder brief
- `SOVEREIGN_COORDINATION.md` - cypherpunk, privacy, and sovereign-coordination brief
- `ORG_INTROSPECTION_BRIEF.md` - organizational-introspection brief for mission-driven projects
- `WHAT_IS_UBU.md` - mass-consumption public explanation of UbU's purpose and user-facing value proposition
- `NIKOS_TUESDAY.md` - far-horizon narrative projection of the full-product user experience; depicts Phase 2/3+ capabilities as lived experience

When a derived file conflicts with a canonical file, the canonical file wins.

---

## Current project status

### Phase 0: ETHConf NYC demo (complete)

Phase 0 is the canonical pre-Phase-1 milestone. The `ubu-phase0-demo` project, frozen at commit `9daffa7`, was demonstrated at the **ETHConf NYC conference, June 8–10, 2026**.

The Phase 0 demo covers the core UbU loop end-to-end using a self-contained dummy environment:

1. Create a new user and complete the onboarding bootstrap interview.
2. Onboard GitHub access using a hard-coded dummy GitHub user and pre-configured access token.
3. Select a repository (a dummy clone of `UbU-project/ubu-design`).
4. Answer affect calibration questions.
5. Ingest dummy GitHub Issues and convert them into Tasks.
6. Generate a Plan for those Tasks including affect-legitimized breaks and recovery constraints.
7. Display the Plan in Calendar preview and/or next-issue UI.

`model-committee` runs were performed during public demonstration ceremonies only, due to real AI provider costs.

Phase 0 is a standalone demo milestone, now complete. Code reuse into Phase 1 is not assumed, but the skills, experience, and demonstrated patterns acquired during Phase 0 accelerate Phase 1 development directly. The primary demonstration value is **association introspection**: UbU using its own planning and self-governance model to coordinate the UbU project in public.

### Phase 1 implementation (in progress)

Phase 1 design is frozen as of commit `cc8b339`. No further broad pre-MVP design automation is warranted. Remaining design activity should be limited to implementation-guidance gaps, open blocker certificates, or implementation feedback that reveals genuine Phase 1 scope issues.

Phase 1 implementation began on 2026-06-10 with the multi-repo scaffold under the `UbU-project` organization: `ubu-schemas`, `ubu-core`, `ubu-store`, `ubu-github-adapter`, `ubu-planning-kernel`, `ubu-orchestrator`, `ubu-ui`, `ubu-devshell`, and `ubu-brand`, initialized in bootstrap-dependency order with rev-pinned cross-repo dependencies and per-repo CI. Cross-repo authority boundaries are canonical in `docs/PHASE1_CONTRACT_BOUNDARIES.md`. The scaffold is a complete walking skeleton of the architecture; Phase 1 feature semantics are implemented incrementally against the frozen design in the priority order of `DESIGN.md` §4.1.6. The scaffold-reconciliation decisions `UBU-D0226` through `UBU-D0230` and the store-wiring decision `UBU-D0231` landed first, then the first user-facing slice (`UBU-D0232`): a bootstrap interview seeds Objectives, Preferences, and Tasks through admission, and a deterministic readiness-ordered next-action recommendation with act and override drives a one-next-Task loop. On that base, GitHub projection landed: preview → per-batch approval → worker write → reconciliation with conflict surfacing, restricted to managed labels and implementing `UBU-D0159` (`UBU-D0233`); and the export boundary was made real — a single authoritative Legitimizer issues a deny-by-default export permit, the orchestrator can reach no external write without it, and worker-authority and redaction-identity export-boundary invariants are enforced with standing hard-boundary checks (`UBU-D0234`, extending `UBU-D0230`). Phase A of the planning slice then landed (`UBU-D0235`): a canonical timed Plan, deterministic skeleton Compact Calendar generation, override-safe recalculation, and a fixed-seed golden-fixture corpus. Phase B added affect legitimization (`UBU-D0236`): the planning kernel's `full_legitimize` now applies the §6 sigmoid affect filter — per-dimension satisfaction against a separate AffectProfile and the snapshot observation, with `enforce` and `warn_only` modes — and `next_action` is sourced from the affect-legitimized Calendar. The `ubu-devshell` fixture smoke test exercises the full onboard-to-act loop, the gated projection loop including the deny path, and the affect-legitimized planning loop, offline against a mock GitHub backend. Phase C-1 then added the optimization layer (`UBU-D0237`): the kernel generates a bounded candidate set (the legitimized skeleton baseline plus deterministic slack-based perturbations, capped at sixteen), runs the affect filter per candidate, prunes with semi-legitimization (`UBU-D0211`), and value-scores survivors into a `scoring_policy`-weighted composite `total_score` with role-tagged alternatives; the default Calendar is the rank-1 candidate and `next_action` follows it. The same decision made the kernel contract types the planning surface and removed the stale thin `ubu-schemas` planning-request/response/task-spec stubs (C-1.5). The Monte Carlo rollout, probability estimation, live GitHub, and risk reports remain the next slices.

The operational target remains:

> Use UbU's explicit model, `model-committee`, GitHub dogfooding inputs, the Phase 1 planning-kernel contract, regular Calendar preview, regular Log review, and bounded projection artifacts to help UbU coordinate the development of UbU itself.

The project is seeking a small core cohort of serious, self-directed builders. It does not need popularity for its own sake. It needs concrete patches, test fixtures, design review, workflow examples, prototype funding, and sustained subsystem ownership.

### Phase 2 sync and Compartment contract

`DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md` is now the canonical boundary for pending Phase 2 synchronization work. It specifies the single-user multi-device model: Devices as execution enclaves, Zones as replication/work-context boundaries, Compartment-safe replication, partial replicas, SyncStatements, offline mutation admission, and sync-triggered Plan/Calendar invalidation.

This contract does not expand Phase 1 scope. Phase 1 remains a single-user local dogfooding MVP. The Phase 2 contract exists now to prevent early implementation decisions from assuming a central canonical server, a permanent primary device, or a two-device-only sync model.

---

## Development readiness

### Phase 0 readiness

Phase 0 was demonstrated at ETHConf NYC, June 8–10, 2026, frozen at `ubu-phase0-demo` commit `9daffa7`.

- [x] Phase 1 design is frozen at commit `cc8b339`.
- [x] Phase 0 demo scope is defined: new-user onboarding, dummy GitHub ingestion, affect calibration, Task generation, affect-legitimized planning, Calendar preview and/or next-issue UI.
- [x] Dummy GitHub environment (hard-coded user, token, and `ubu-design` clone) is specified.
- [x] Phase 0 demo app is runnable for demo usage at `ubu-phase0-demo` commit `9daffa7`.
- [x] Dummy GitHub Issues ingest and convert to Tasks in the demo app.
- [x] Affect calibration questions are implemented in the Phase 0 onboarding flow.
- [x] Plan generation with affect-legitimized breaks runs in the Phase 0 app.
- [x] Calendar preview and/or next-issue UI is implemented in the Phase 0 app.
- [ ] `model-committee` ceremony run is validated against the Phase 2 sync/Compartment contract and open questions.

### Phase 1 readiness (post-ETHConf)

The Phase 1 design baseline is frozen and implementation-first Phase 1 work has begun. `model-committee` dogfooding continues as an implementation-support and review-artifact workflow.

- [x] Broad pre-MVP design automation is closed by `UBU-D0175`.
- [x] The canonical design file set includes `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, `PLANNING_KERNEL_CONTRACT.md`, and `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`.
- [x] Phase 1 is scoped around single-user GitHub dogfooding rather than a general productivity suite.
- [x] Resource and Skill are recognized as core full-product abstractions while remaining out of Phase 1 implementation scope.
- [x] The planning-kernel boundary is specified as a typed request/response contract with a local GPU path and CPU reference path.
- [x] `model-committee` has advanced to the narrow v0.3 contract, including `PLANNING_KERNEL_CONTRACT.md` as a fourth model-committee input file.
- [x] `model-committee` remains advisory: it writes review artifacts, not accepted design state.
- [x] `model-committee` v0.3 keeps automatic patch application, auto-merge, auto-push, GitHub API use, direct OpenAI/Anthropic/Gemini API calls, adaptive model weights, and full planning-kernel work out of scope.
- [x] The Phase 1 repo constellation exists under `UbU-project` with rev-pinned cross-repo dependencies and per-repo CI (`Init` commits, 2026-06-10).
- [x] Cross-repo contract boundaries are canonical in `docs/PHASE1_CONTRACT_BOUNDARIES.md`.
- [x] The Phase 1 schema → core → store → orchestrator path is implemented and conformant to the frozen wire contract (snake_case fields, fifteen admissible object types, canonical Task lifecycle with derived readiness); scaffold-reconciliation decisions `UBU-D0226` through `UBU-D0230` landed.
- [x] The orchestrator persists and serves canonical state through the `ubu-store` admission boundary; the scaffold's in-memory `MemoryState` is removed (`UBU-D0231`).
- [x] A store-backed cross-repo fixture smoke test runs green via `ubu-devshell`.
- [x] The main UbU Phase 1 app exists as an end-to-end runnable prototype: onboarding, bootstrap-seed, a one-next-Task view, and act/override run end to end against the store-backed orchestrator over loopback, and the Tauri app builds (`UBU-D0232`).
- [x] A bootstrap interview seeds Objectives, Preferences, and Tasks through store admission, and act/override records append-only Log events.
- [x] The full onboard-to-act loop runs store-backed and offline via the `ubu-devshell` fixture smoke test.
- [ ] GitHub issue/PR/CI/milestone ingestion and projection are implemented in the main UbU app. *(Partial: fixture-driven issue ingestion runs through store admission; projection preview/approved-write/reconciliation are implemented against a mock GitHub backend; live ingestion and live GitHub remain pending.)*
- [x] GitHub projection writes only managed labels through preview → per-batch approval → worker write → reconciliation with conflict surfacing, implementing `UBU-D0159` (`UBU-D0233`).
- [x] GitHub projection writes pass a deny-by-default export boundary — a single authoritative gate, worker-authority and redaction-identity export-boundary invariants, bypass-resistance, and standing hard-boundary checks (`UBU-D0234`).
- [x] Objective, Task, Preference, Log, and the timed Plan/Calendar persist through store admission (`UBU-D0235`).
- [x] The Compact Calendar generates from admitted Tasks, recalculates on triggers with override-safe supersession, and renders in the UI (`UBU-D0235`).
- [x] Affect legitimization is implemented: `full_legitimize` applies the §6 sigmoid affect filter against a separate AffectProfile and the snapshot observation (`enforce`/`warn_only`), and `next_action` is sourced from the legitimized Calendar (`UBU-D0236`).
- [x] Value scoring is implemented: the kernel generates a bounded candidate set (cap 16), filters affect per candidate, prunes with semi-legitimization, and value-scores into a `scoring_policy`-weighted composite `total_score` with role-tagged alternatives; the default Calendar is the rank-1 candidate and `next_action` follows it (`UBU-D0237`).
- [x] The Monte Carlo rollout is implemented: the kernel samples correlated durations (§3 shifted-log-normal, §7 correlation matrix, positive-definite by construction) over the top-K finalists, producing feasibility, p10 robustness, and Wilson-interval probability, and re-ranks the default by the rollout-grounded composite (`UBU-D0238`); Tasks carry an optional duration estimate and correlation-group membership that flow through the store and orchestrator into the kernel (`UBU-D0239`), and the vestigial planning-envelope stub schemas were removed.
- [x] Derived risk and human-complete plan-quality reports are implemented: the orchestrator computes categorized risk findings (with a blocking set that drives recalculation) and the six §2.5.1 plan-quality signals from the kernel signals and store context, surfaced in non-blaming framing (`UBU-D0240`).
- [x] The UniverseState facts container is implemented: the §11.1 four-collection container with its seven-operation mutation vocabulary and deterministic precondition evaluator as pure `ubu-core` functions, admitted and persisted by the store; the planner/effect/bootstrap wiring is deferred (`UBU-D0241`).
- [x] Wiring-A — preconditions gate planning: the orchestrator evaluates each Task's `preconditions` against the current UniverseState via the pure `ubu-core` evaluator and partitions Tasks into eligible / blocked / invalid; only eligible Tasks reach the kernel, which is unchanged (`UBU-D0242`).
- [x] Wiring-B — effects mutate facts on completion: a completed Task's `effects` are applied to UniverseState through the pure `ubu-core` applicator and persisted by the store (a failed Task leaves it unchanged); the organization/worker-mode intrinsic-affect rejection is enforced for both preconditions and mutations (`UBU-D0242`).
- [x] Wiring-C — the bootstrap records the initial UniverseState facts (`operator`/`project` subjects under the `UBU-D0243` namespace convention), making the loop self-sustaining from onboarding; preconditions then gate and effects then mutate those bootstrap-seeded facts (`UBU-D0242`).
- [ ] The bootstrap interview, Calendar preview, one-next-Task view, and Log review loop are implemented in the main UbU app. *(Partial: bootstrap interview, the Compact Calendar preview, and one-next-Task view implemented; a Log review view is pending.)*
- [ ] Release Outreach Pipeline artifacts are generated from implemented release state.

---

## Phase 1 readiness report

**Report type:** Human-reviewed MVP readiness signal (required by `UBU-D0189`)  
**Evidence commit:** `bc4e534` — `ubu-design` HEAD; reflects Wiring-C, the bootstrap recording initial facts, and the `UBU-D0243` namespace convention  
**Report date:** 2026-06-24  
**Scorer:** Human review  
**Note:** Phase 1 design remains frozen at `cc8b339`. Since the prior report (evidence `bcb0074`, `mvp_readiness` 93), Wiring-C landed (`UBU-D0242`) and the namespace convention was recorded (`UBU-D0243`): the wiring program is complete and the internal loop is self-sustaining from onboarding. The bootstrap now builds the initial UniverseState from the answers it already collects — `facts.operator.work_style`, `facts.operator.attention_preference`, `facts.project.repository`, `facts.project.objective`, and `numeric_values.operator.planning_horizon_days` — and admits it through the store under bootstrap provenance, respecting the re-seed guard; preconditions then gate planning against those facts and a completed Task's effects mutate them. The `UBU-D0243` subject–predicate convention with its controlled subject vocabulary (`operator`, `project`, `github`, `affect`, `relationship`) and its subject-root rule now governs all UniverseState targets. Affect calibration is deliberately excluded from facts (it is AffectProfile tolerance data), and the AffectProfile/Snapshot seeding from the calibration answers is tracked separately. No live GitHub or CI signal was ingested, and constellation repo revs are not pinned in this report.

---

### Scores

| Signal | Score | Band |
|---|---|---|
| `scope_freeze_readiness` | **85 / 100** | Scope stable; frozen scope increasingly realized in conformant code; open questions remain implementation-guidance gaps |
| `mvp_readiness` | **94 / 100** | The internal loop is self-sustaining from onboarding; live GitHub is the remaining feature |

Score weights follow `UBU-D0189`. The cap-59 and cap-74 ceilings remain cleared. No hard cap currently binds; the score reflects genuine sub-score gaps — chiefly live GitHub (still mock), the interactive bootstrap interview, and public artifact/claim evidence. Note: public or outreach claims must carry evidence labels to avoid the cap-79 constraint.

---

### `scope_freeze_readiness`: 85

Phase 1 scope is formally frozen by `UBU-D0097` and `UBU-D0175`. The design model is internally consistent with no known hard failures in canonical files. The planning-kernel boundary contract (`PLANNING_KERNEL_CONTRACT.md`) is accepted and stable. The decisions `UBU-D0226`–`UBU-D0234` have since been implemented across the constellation without surfacing new scope questions, which empirically reinforces scope stability.

Three Phase 1 questions remain technically open:

- `UBU-Q0070` (skeleton Plan failure diagnostics) — answerability 90; implementation detail, not a scope question.
- `UBU-Q0071` (legitimization cost model) — answerability 90; implementation detail requiring empirical measurement once a planner exists.
- `UBU-Q0072` (GPU-aware planner kernels) — partially resolved; subquestions 1 (solver library selection), 3 (mobile GPU targets), and 5 (cloud GPU path) remain open and are deferred beyond Phase 1.

None of these carry a `UBU-D0175` blocker certificate. None reduce `scope_freeze_readiness` under the current rubric.

---

### `mvp_readiness`: 94

| Criterion (weight) | Evidence | Score |
|---|---|---|
| Scope and blocker discipline (15) | Scope frozen; no open blockers; `UBU-D0237`–`UBU-D0239` landed, the input-path gap that surfaced mid-wave was diagnosed and closed via scoped corrective tickets, and the vestigial planning-envelope stubs were removed (S13) | 13 / 15 |
| Implementation slice coverage (25) | The planning slice, the derived risk/plan-quality reports, and the full UniverseState facts loop are implemented — affect-legitimized, value-scored, Monte-Carlo-rollout-ranked planning with stochastic input; categorized risk findings and the six plan-quality signals; the §11.1 four-collection facts container with its mutation vocabulary and precondition evaluator as pure `ubu-core` functions, wired in all three directions (bootstrap records facts, preconditions gate planning, effects mutate facts) under the `UBU-D0243` namespace convention; bootstrap-seed and gated GitHub projection implemented; live GitHub (mock → live) is the remaining slice | 24 / 25 |
| User-facing loop evidence (15) | The full first-person loop runs end to end from a cold bootstrap over loopback: answer the bootstrapping questions → the bootstrap constructs the initial UniverseState context model → rollout-ranked affect-legitimized Calendar → next Task with its score breakdown, role-tagged alternatives, rollout probability with Wilson interval and robustness, and non-blaming risk/plan-quality signals → act or override → effects update the facts → recalculate; the interactive bootstrap interview is a remaining UX refinement of the onboarding step, not a missing loop step | 15 / 15 |
| Integration / projection / worker / privacy boundaries (15) | The deny-by-default export gate and its invariants hold; the stochastic input path is integration-tested end to end via D12; the UniverseState facts container is wired into the loop in both directions — the orchestrator partitions planning by preconditions and applies a completed Task's effects through the store (which owns persistence), with the organization/worker-mode intrinsic-affect rejection enforced on both; bootstrap fact-recording remains, projection is still mock GitHub, and enforcement is not generalized beyond export | 14 / 15 |
| Verification, fixtures, and deterministic tests (15) | A fixed-seed rollout golden corpus and property tests (PSD-by-construction, the `sigma`/`mu` derivation, Wilson bounds, p10, determinism, degraded branches) join the scoring, affect, and boundary suites, and the integration gate caught the wave's systemic defect; the degraded path is unit-only and unbuilt slices lack tests | 14 / 15 |
| Dogfooding / artifact / public-claim evidence (10) | A runnable store-backed first-person loop is self-sustaining from onboarding — the bootstrap seeds the initial facts, planning produces probability-ranked plans with rollout robustness and humane risk/plan-quality feedback, and completing Tasks mutates UbU's own UniverseState so subsequent planning reflects the acted-on world; plus `model-committee` artifacts; projection (mock GitHub) and public claims remain | 9 / 10 |
| Operational polish and contributor-run diagnostics (5) | `ubu-devshell` runs the full loop, the gated projection deny path, override-safe recalculation, the affect/scoring/rollout paths, and standing hard-boundary diagnostics | 5 / 5 |

**Total: 94 / 100**

---

### Per-slice status

| Phase 1 slice | Status |
|---|---|
| Bootstrap and seed model | Implemented (bootstrap questionnaire seeds Objectives, Preferences, and Tasks through admission) |
| GitHub import and External References | In progress (bootstrap-driven fixture ingestion through store admission; projection write now lands against mock GitHub; live ingestion pending) |
| Objective / Task / UniverseState / Log admission | Implemented (Objective/Task/Preference/Log admission exercised end to end; the UniverseState facts container is reshaped, admitted, and round-tripped with its mutation and precondition semantics, and its preconditions now gate planning via the orchestrator — `UBU-D0241`, `UBU-D0242`) |
| Plan / Calendar generation and explanation | Implemented (affect-legitimized, value-scored, multi-candidate Calendar with Monte Carlo rollout: correlated §3/§7 duration sampling over the top-K finalists, p10 robustness, Wilson-interval probability, and rollout-grounded re-rank of the default; external events deferred) |
| Next-action focus plus feedback / recalculation | Implemented (next action sourced from the rollout-re-ranked default Calendar with override-safe recalculation; refuses affect-infeasible recommendations under `enforce`) |
| Risk and human-complete plan-quality reports | Implemented (orchestrator-derived risk report with categorized findings and a recalculation-driving blocking set, plus the six `human_complete_plan_quality` signals with non-blaming revision suggestions; affect signals behind the `post_plan_affect_projection` seam) |
| Compartment, worker, and projection authority boundaries | Implemented for the export/projection boundary (single deny-by-default gate, worker-authority and redaction-identity export-boundary invariants, bypass-resistance, standing checks); enforcement not generalized to non-export Compartment operations |
| GitHub projection preview or approved write plus reconciliation | Implemented against mock GitHub (managed labels; preview → per-batch approval → gated write → reconciliation with conflict surfacing); live GitHub pending |
| Release outreach and public dogfooding artifact package | Not started |

---

### Failing gates and stale inputs

- **Planning kernel is feature-complete, with bounded deferrals.** The Monte Carlo rollout, probability estimation, and the stochastic input path are implemented and integration-tested. Remaining planning-side deferrals: semi-legitimization implements affect-budget and slack with the other four heuristics as named TODOs; external-event modeling is deferred; and the degraded-mode and strict-rejection paths are verified at the kernel unit level (unreachable through the API by the §7 positive-definite-by-construction guarantee).
- **GitHub projection is verified against a mock, not live GitHub.** The gated projection loop and the deny path run against a mock backend; no live GitHub write has been exercised.
- **Redaction-identity is enforced on the export path only.** Full cross-cutting serializer coverage of the redaction-identity invariant is a named TODO beyond the export boundary.

### Manual assumptions and boundaries

- Scores are based on file state at `ubu-design` `ed92e15` plus the landed derived risk and human-complete plan-quality reports (`UBU-D0240`) across the constellation; the reports are exercised by the offline fixture smoke test (D13) and orchestrator tests, not live GitHub or CI, and constellation repo revs are not pinned here.
- GitHub adapter behavior is verified against mocked fixtures, not live GitHub; no production data exists, as the store is pre-consumer.

---

### Next slice most likely to raise the score

**Live GitHub last.** The wiring program is complete and the internal loop is self-sustaining from onboarding; the only remaining Phase 1 feature is live GitHub projection (mock → live, gated write plus reconciliation), sequenced last by design since it is the only external-facing, cost-bearing test and is cheapest to run once everything provable against the mock is proven — a faithful mock first, a throwaway test repo, a fine-grained run-once revoked token, dry-run, batched and rate-limit-aware, a single confirmation pass. Any public or outreach use must keep evidence labels to stay clear of the cap-79 constraint.

---

## Planning kernel direction

UbU's Calendar model distinguishes layered planning responsibilities.

1. **Skeleton Plan:** place Static Tasks, walk backward through dependency DAGs, and schedule prerequisites before dependents.
2. **Legitimization:** add the minimum affect, recovery, transition, rest, and sustainability constraints needed to turn the skeleton Plan into a minimally human-viable baseline.
3. **Candidate generation and scoring:** add optional Dynamic Tasks, alternative placements, stochastic assumptions, Plan probabilities, value scoring, fragility scoring, and robustness checks.
4. **Short-horizon repair:** adapt quickly when reality diverges through early completion, late completion, interruptions, external events, affect shifts, or user overrides.

The default Plan remains deterministic, ordered, inspectable, and explainable. It is selected from legitimate candidate Plans whose modeled assumptions, value, and Plan probability have already been evaluated.

Phase 1 targets a local desktop or laptop GPU configured by the power user. The planning engine should be a pure function over typed `PlanningRequest` and `PlanningResponse` values, with no external calls, no I/O, and no mutable state. A CPU reference path is required for tests, CI, and contributors without GPU hardware. The schema and stage-boundary details live in `PLANNING_KERNEL_CONTRACT.md`.

---

## Human-complete planning

UbU treats affect as a core part of planning, not as a decorative wellness feature.

A plan that ignores fatigue, stress, boredom, motivation, emotional load, recovery, and dignity is incomplete. It may be actively misleading. UbU should help users receive fast feedback about whether a plan is working, revise plans when reality disagrees, and grow beyond current limits without treating themselves like machines.

The goal is neither comfort-maximization nor coercive productivity. The goal is humane self-governance: disciplined action that respects the user's emotional and physical reality.

---

## Phase 1 user-facing loop

Phase 1 should be usable as a simple first-person experience:

1. UbU asks a few bootstrapping questions, using preference-calibration examples when useful.
2. UbU builds an initial explicit model from the answers and approved dogfooding inputs.
3. UbU runs Calendar preview so the user can inspect and correct the candidate Plan.
4. UbU recommends one next Task.
5. UbU explains why that Task matters now.
6. The user acts, rejects, snoozes, overrides, decomposes, chooses Discovery mode, or asks for more explanation.
7. UbU records what happened, runs Log review when appropriate, and recalculates.

The full Plan remains inspectable, but the default mode may reduce cognitive load by showing one meaningful next action at a time.

---

## GitHub dogfooding

For dogfooding, GitHub is treated as a low-dimensional projection of canonical UbU state. UbU is the source of truth.

GitHub Issues, PRs, comments, labels, reviews, CI, and milestones must be interpreted into UbU objects and events. UbU may project selected state back into GitHub through clearly marked managed labels, comments, or body blocks. Other GitHub edits are treated as external events by default.

Missed GitHub updates are expected in MVP, so reconciliation is a first-class concern.

---

## `model-committee` bootstrap project

`model-committee` is the first runnable bootstrap automation project for active pre-MVP UbU dogfooding. It is an advisory Automation Worker pattern that reads canonical repo state, identifies answerable open questions, generates candidate changesets, scores those changesets, validates patches, and writes reviewable artifacts.

Accepted design state exists only when committed to the canonical `ubu-design` repository.

### v0.3 boundary

`model-committee` v0.3 implements the v0.2 frontier cross-scoring workflow and adds these important constraints:

- `PLANNING_KERNEL_CONTRACT.md` is the fourth model-committee input file, read by providers, injected into prompts, snapshotted in runs, and allowed in patches.
- `rank` may write `Answerability score:` and `Last scored:` back to `OPEN_QUESTIONS.md`; it does not update `Scored from commit:`.
- `work-generate` should prompt models to tombstone solved questions, remove duplicate information across source files, and compress content to the effective minimum.
- rendered prompt size at or above 90% of the configured warning limit must set `manifest.prompt_size_warning = true` and be surfaced in `review.md`.
- `manifest.schema_version` is `"0.3"`.
- Ollama remains a local work-proposal provider and does not score in v0.3.
- Fake provider mode remains deterministic and must not call Codex, Claude, or Ollama.

`model-committee` must remain bounded. It must not implement direct OpenAI, Anthropic, Gemini, or GitHub API calls; auto-merge; auto-push; automatic pull request creation; automatic artifact publication; automatic patch application; adaptive model weights; multi-turn Claude Code sessions; full Association automation; or UbU planning-kernel work.

---

## Question selection and design-burden reduction

`model-committee` uses answerability as the first gate. A question is eligible for ordinary work only if it has no dependencies, all dependencies are solved, or all dependencies are being answered in the same work item.

Blocked questions may be selected for decomposition work if decomposition should produce replacement questions with fewer, simpler, or no dependencies. UbU should not treat every increase in open-question count as failure. The relevant metric is unresolved design burden, not raw question count.

---

## Contributing

This repository is currently a design repository, not the main implementation repository.

Good contributions include:

- clarifying open questions;
- identifying contradictions in canonical files;
- proposing precise patches to `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, `PLANNING_KERNEL_CONTRACT.md`, or `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`;
- reviewing whether derived files remain consistent with canonical files;
- creating implementation-ready issues from accepted design state;
- producing fixtures for `OPEN_QUESTIONS.md` parsing, dependency validation, decision-reference validation, patch validation, provider outputs, and planning-kernel request/response contracts;
- providing real workflow examples from FOSS, Ethereum, protocol, research, independent-consulting, or other autonomous-team contexts;
- helping maintain and test `model-committee` v0.3 as an advisory, bounded, review-artifact workflow.

The project prefers concrete patches, structured issue proposals, test fixtures, workflow examples, review of dogfooding artifacts, and sustained subsystem ownership over broad abstract discussion.

### Current contribution path

Useful contributor roles currently include:

1. **Workflow informant:** describe real coordination pain, tool-stack fragmentation, maintainer overload, or autonomous-team failure modes.
2. **Design reviewer:** identify contradictions, underspecified concepts, ambiguous dependencies, or unclear scope boundaries.
3. **Small patch contributor:** improve canonical design files, derived public-facing files, or implementation-ready issue descriptions.
4. **Early implementation contributor:** help maintain, test, and extend the `model-committee` bootstrap loop and Phase 1 planning-kernel contract fixtures.
5. **Module owner:** take responsibility for a bounded subsystem after trust, alignment, and technical fit are established.

---

## Repository map

- `README.md` - derived technical contributor entry point and project summary
- `DESIGN.md` - canonical design summary
- `DECISIONS.md` - accepted design decisions and anti-regression memory
- `OPEN_QUESTIONS.md` - unresolved questions, prioritization metadata, and automation queue
- `PLANNING_KERNEL_CONTRACT.md` - Phase 1 planning-kernel request/response contract, GPU stage boundaries, duration semantics, affect constraints, and correlation-matrix rules
- `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md` - Phase 2 device sync, Zone, Compartment, partial-replica, and sync-statement contract
- `OUTREACH.md` - derived outreach document for FOSS maintainers and software engineers
- `PM_BRIEF.md` - derived brief for project leads and technical PMs
- `FUNDER_BRIEF.md` - derived brief for grantmakers, sponsors, and prototype funders
- `SOVEREIGN_COORDINATION.md` - derived brief for cypherpunks, privacy builders, and sovereign-coordination audiences
- `ORG_INTROSPECTION_BRIEF.md` - derived brief for mission-driven projects and organizational introspection
- `WHAT_IS_UBU.md` - derived mass-consumption public explanation of UbU's purpose and user-facing value proposition
