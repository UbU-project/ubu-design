# UbU

**Status:** Phase 0 complete — demonstrated at ETHConf NYC, June 8–10, 2026 / Phase 1 implementation in progress: the `UbU-project` repo constellation is conformant to the frozen wire contract and the orchestrator is store-backed; no user-facing loop yet  
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

Phase 1 implementation began on 2026-06-10 with the multi-repo scaffold under the `UbU-project` organization: `ubu-schemas`, `ubu-core`, `ubu-store`, `ubu-github-adapter`, `ubu-planning-kernel`, `ubu-orchestrator`, `ubu-ui`, `ubu-devshell`, and `ubu-brand`, initialized in bootstrap-dependency order with rev-pinned cross-repo dependencies and per-repo CI. Cross-repo authority boundaries are canonical in `docs/PHASE1_CONTRACT_BOUNDARIES.md`. The scaffold is a complete walking skeleton of the architecture; Phase 1 feature semantics are implemented incrementally against the frozen design in the priority order of `DESIGN.md` §4.1.6. The scaffold-reconciliation decisions `UBU-D0226` through `UBU-D0230` have landed across the constellation: snake_case wire fields, the fifteen-object-type ID registry, the canonical Task lifecycle with derived readiness, the AuthoritySource and provenance split, and Compartment-guardrail policy members with logged boundary decisions. Building on that, `UBU-D0231` removes the orchestrator's ephemeral `MemoryState`: the orchestrator now opens `ubu-store` on startup and serves every canonical read and write through the store admission boundary, and the `ubu-devshell` cross-repo fixture smoke test runs green against the store-backed orchestrator. No user-facing loop — bootstrap interview, Calendar preview, next-Task view, or Log review — is implemented yet; that is the next slice.

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
- [ ] The main UbU Phase 1 app exists as an end-to-end runnable prototype.
- [ ] GitHub issue/PR/CI/milestone ingestion and projection are implemented in the main UbU app. *(Partial: fixture-driven issue ingestion into UbU objects runs through store admission; live ingestion and projection write/reconciliation are pending.)*
- [ ] Objective/Task/Calendar/Log persistence is implemented in the main UbU app. *(Partial: Objective, Task, and Log persistence runs through store admission; Calendar persistence awaits the planning slice.)*
- [ ] The bootstrap interview, Calendar preview, one-next-Task view, and Log review loop are implemented in the main UbU app.
- [ ] Release Outreach Pipeline artifacts are generated from implemented release state.

---

## Phase 1 readiness report

**Report type:** Human-reviewed MVP readiness signal (required by `UBU-D0189`)  
**Evidence commit:** `5b7ae735` — `ubu-design` HEAD; reflects the landed constellation conformance pass and store-backed orchestrator  
**Report date:** 2026-06-15  
**Scorer:** Human review  
**Note:** Phase 1 design remains frozen at `cc8b339`. Since the prior report (2026-05-28, design-freeze evidence), the constellation has landed the scaffold-reconciliation decisions `UBU-D0226`–`UBU-D0230` and `UBU-D0231` (orchestrator on `ubu-store`, `MemoryState` removed, fixture smoke test repointed). Scores below are re-scored against that implementation state. They move `mvp_readiness` out of the 0–39 band into the 40–59 band but remain under the *no runnable end-to-end dogfooding loop* cap of 59, because no user-facing loop yet exists. No live GitHub or CI signal was ingested, and constellation repo revs are not pinned in this report.

---

### Scores

| Signal | Score | Band |
|---|---|---|
| `scope_freeze_readiness` | **85 / 100** | Scope stable; frozen scope now partially realized in conformant code; open questions remain implementation-guidance gaps |
| `mvp_readiness` | **43 / 100** | Backend walking skeleton implemented and store-backed; no user-facing end-to-end loop yet (cap 59) |

Score weights follow `UBU-D0189`. Active caps: *no runnable end-to-end dogfooding loop (cap 59)* — score is already below this ceiling and reflects honest implementation absence, not a cap artifact.

---

### `scope_freeze_readiness`: 85

Phase 1 scope is formally frozen by `UBU-D0097` and `UBU-D0175`. The design model is internally consistent with no known hard failures in canonical files. The planning-kernel boundary contract (`PLANNING_KERNEL_CONTRACT.md`) is accepted and stable. The scaffold-reconciliation decisions `UBU-D0226`–`UBU-D0231` have since been implemented across the constellation without surfacing new scope questions, which empirically reinforces scope stability.

Three Phase 1 questions remain technically open:

- `UBU-Q0070` (skeleton Plan failure diagnostics) — answerability 90; implementation detail, not a scope question.
- `UBU-Q0071` (legitimization cost model) — answerability 90; implementation detail requiring empirical measurement once a planner exists.
- `UBU-Q0072` (GPU-aware planner kernels) — partially resolved; subquestions 1 (solver library selection), 3 (mobile GPU targets), and 5 (cloud GPU path) remain open and are deferred beyond Phase 1.

None of these carry a `UBU-D0175` blocker certificate. None reduce `scope_freeze_readiness` under the current rubric.

---

### `mvp_readiness`: 43

| Criterion (weight) | Evidence | Score |
|---|---|---|
| Scope and blocker discipline (15) | Scope frozen; no certified blockers; `UBU-D0226`–`UBU-D0231` landed consistently | 13 / 15 |
| Implementation slice coverage (25) | Schema, core, store, adapter, and orchestrator implemented and conformant; store-backed persistence; ~3 of 9 slices in progress, no planner or UI loop | 11 / 25 |
| User-facing loop evidence (15) | No bootstrap interview, Calendar preview, or next-Task loop; UI types reconciled only | 0 / 15 |
| Integration / projection / worker / privacy boundaries (15) | Store admission boundary, `authority_source`/provenance, and logged Compartment boundary decisions exist; projection write/reconciliation and full enforcement-gate runtime pending | 5 / 15 |
| Verification, fixtures, and deterministic tests (15) | Per-repo `cargo test`, serde↔schema lockstep CI, orchestrator integration test on a temp store, store-backed cross-repo smoke test; no planning-kernel reference test suite | 6 / 15 |
| Dogfooding / artifact / public-claim evidence (10) | `model-committee` v0.3 artifacts plus a runnable store-backed constellation smoke test; no main-app dogfooding loop | 5 / 10 |
| Operational polish and contributor-run diagnostics (5) | `ubu-devshell` provides rev-pin, signed-commit, check/test, codegen, and fixture-demo diagnostics; no main-app diagnostics | 3 / 5 |

**Total: 43 / 100**

---

### Per-slice status

| Phase 1 slice | Status |
|---|---|
| Bootstrap and seed model | Not started |
| GitHub import and External References | In progress (fixture ingestion through store admission; no live ingestion or projection write) |
| Objective / Task / UniverseState / Log admission | In progress (store admission live for Objective/Task/Log; UniverseState facts container pending) |
| Plan / Calendar generation and explanation | Not started (contract conformant; no CPU reference planner) |
| Next-action focus plus feedback / recalculation | Not started |
| Risk and human-complete plan-quality reports | Not started |
| Compartment, worker, and projection authority boundaries | In progress (policy members, logged boundary decisions, `authority_source`/provenance; full enforcement-gate runtime pending) |
| GitHub projection preview or approved write plus reconciliation | Not started (managed-label preflight only) |
| Release outreach and public dogfooding artifact package | Not started |

---

### Failing gates and stale inputs

- **No runnable end-to-end dogfooding loop.** This is the primary gate and the active cap (59). The store-backed cross-repo fixture smoke test is a smoke test, not the user-facing loop; until the app can run bootstrap → Calendar → one next Task → Log review, no higher `mvp_readiness` score is warranted.
- **No planning-kernel reference implementation or test suite.** `PLANNING_KERNEL_CONTRACT.md` and the envelope/version conformance exist, but no deterministic CPU reference planner, Calendar generation, or fixture-backed kernel test suite exists yet.
- **No GitHub projection write or reconciliation.** Managed-label preflight exists in the adapter; the approved-write and reconciliation loop does not, which keeps the projection-boundary gate (cap 74) unmet for that slice.
- **UniverseState facts container not yet implemented.** Per `UBU-D0229` the current `universe-state` schema models a snapshot view; the facts container is first-slice implementation work.

### Manual assumptions and boundaries

- Scores are based on file state at `ubu-design` `5b7ae735` plus the landed conformance pass and `UBU-D0231` store wiring across the constellation; no live GitHub or CI signal was ingested, and constellation repo revs are not pinned here.
- GitHub adapter behavior is verified against mocked fixtures, not live GitHub; no production data exists, as the store is pre-consumer.

---

### Next slice most likely to raise the score

**Bootstrap-and-seed loop wired to the store-backed orchestrator through the Tauri UI, plus a single next-Task view.** The backend admission boundary now exists, so the highest-leverage move is the first user-facing slice: a bootstrap interview that seeds explicit Objectives and Tasks, a one-next-Task view, and the Tauri app building and running against the orchestrator over loopback with the paste-token UX. This is the slice that breaks the cap-59 ceiling; combined with even a stub Calendar preview it would move `mvp_readiness` into the 60–74 private-dogfooding band.

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
