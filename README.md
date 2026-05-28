# UbU

**Status:** Active pre-MVP dogfooding / implementation-first Phase 1  
**Repository:** `ubu-design`  
**Primary purpose:** Canonical public design state for the UbU project  
**Derived file:** This README is a technical contributor entry point. The canonical design authority is `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, and `PLANNING_KERNEL_CONTRACT.md`.

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

### First-person legibility

Phase 1 must remain understandable as a simple first-person loop: answer a few bootstrapping questions, preview a candidate Calendar, receive one recommended next Task, inspect why it matters now, act or override, and let UbU learn from what actually happened.

### Resource and Skill readiness

Many life-planning failures happen because the user lacks something needed to do the work. UbU's long-term model treats **Resources** as external prerequisites and **Skills** as Identity-owned capabilities.

Resources include documents, tools, ingredients, credentials, software licenses, API keys, locations, payment methods, quiet spaces, and other stateful things a Task may need. Skills include capabilities the user can learn, test, forget, refresh, and evidence.

This is not Phase 1 scope, but it is central to the full product. Phase 3 should try to add a thin Resource/Skill-aware task-readiness layer. Phase 3B and Phase 4+ form the full version 1.0 release track, including richer Resource, Skill, Technique, DIY-versus-purchase/hire, inventory, financial-management, and Skill Barter features.

Resources also include community and public Resources: library tool loans, makerspace equipment, public workshops, community gardens, seed libraries, and repair cafés. UbU should eventually support a Library and Community Resource Mode that turns publicly accessible Resources into first-class planning inputs.

### Government and public-resource symmetry

Any institution that can constrain a user's plan may also provide Resources, permissions, remedies, or procedures that improve the user's plan. UbU must model both sides.

This means UbU should not only surface regulations, permits, and legal constraints — it should also surface grants, subsidies, benefit programs, weatherization assistance, workforce training, legal aid, public infrastructure, and other government- or community-supported Resources. Many of these are conditionally unlockable: a user may need to apply for a benefit, collect documentation, or file an appeal before the Resource becomes available. UbU can generate those prerequisite Tasks automatically.

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

Derived public-facing projection files summarize the canonical state for different audiences:

- `README.md` - technical contributor entry point and project summary
- `OUTREACH.md` - outreach document for FOSS maintainers and software engineers
- `PM_BRIEF.md` - project-lead and technical-PM brief
- `FUNDER_BRIEF.md` - grantmaker, sponsor, and prototype-funder brief
- `SOVEREIGN_COORDINATION.md` - cypherpunk, privacy, and sovereign-coordination brief
- `ORG_INTROSPECTION_BRIEF.md` - organizational-introspection brief for mission-driven projects

When a derived file conflicts with a canonical file, the canonical file wins.

---

## Current project status

UbU is in active pre-MVP dogfooding. Broad pre-MVP design automation is closed by `UBU-D0175`; remaining design work should support concrete Phase 1 implementation slices, recruitment, dogfooding, market discovery, or blocker-certificate review.

The current operational target is:

> Use UbU's explicit model, `model-committee`, GitHub dogfooding inputs, the Phase 1 planning-kernel contract, regular Calendar preview, regular Log review, and bounded projection artifacts to help UbU coordinate the development of UbU itself.

The project is seeking a small core cohort of serious, self-directed builders. It does not need popularity for its own sake. It needs concrete patches, test fixtures, design review, workflow examples, prototype funding, and sustained subsystem ownership.

---

## Development readiness

The design baseline supports beginning implementation-first Phase 1 work while continuing `model-committee` dogfooding as an implementation-support and review-artifact workflow.

- [x] Broad pre-MVP design automation is closed by `UBU-D0175`.
- [x] The canonical design file set includes `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, and `PLANNING_KERNEL_CONTRACT.md`.
- [x] Phase 1 is scoped around single-user GitHub dogfooding rather than a general productivity suite.
- [x] Resource and Skill are recognized as core full-product abstractions while remaining out of Phase 1 implementation scope.
- [x] The planning-kernel boundary is specified as a typed request/response contract with a local GPU path and CPU reference path.
- [x] `model-committee` has advanced to the narrow v0.3 contract, including `PLANNING_KERNEL_CONTRACT.md` as a fourth canonical source file.
- [x] `model-committee` remains advisory: it writes review artifacts, not accepted design state.
- [x] `model-committee` v0.3 keeps automatic patch application, auto-merge, auto-push, GitHub API use, direct OpenAI/Anthropic/Gemini API calls, adaptive model weights, and full planning-kernel work out of scope.
- [ ] The main UbU Phase 1 app exists as an end-to-end runnable prototype.
- [ ] GitHub issue/PR/CI/milestone ingestion and projection are implemented in the main UbU app.
- [ ] Objective/Task/Calendar/Log persistence is implemented in the main UbU app.
- [ ] The bootstrap interview, Calendar preview, one-next-Task view, and Log review loop are implemented in the main UbU app.
- [ ] Release Outreach Pipeline artifacts are generated from implemented release state.

---

## Phase 1 readiness report

**Report type:** Human-reviewed MVP readiness signal (required by `UBU-D0189`)  
**Evidence commit:** `c3b61b0`  
**Report date:** 2026-05-27  
**Scorer:** Human review

---

### Scores

| Signal | Score | Band |
|---|---|---|
| `scope_freeze_readiness` | **85 / 100** | Scope stable; open Phase 1 questions are implementation-guidance gaps, not scope questions |
| `mvp_readiness` | **22 / 100** | Design complete; no runnable end-to-end prototype exists yet |

Score weights follow `UBU-D0189`. Active caps: *no runnable end-to-end dogfooding loop (cap 59)* — score is already below this ceiling and reflects honest implementation absence, not a cap artifact.

---

### `scope_freeze_readiness`: 85

Phase 1 scope is formally frozen by `UBU-D0097` and `UBU-D0175`. The design model is internally consistent with no known hard failures in canonical files. The planning-kernel boundary contract (`PLANNING_KERNEL_CONTRACT.md`) is accepted and stable.

Three Phase 1 questions remain technically open:

- `UBU-Q0070` (skeleton Plan failure diagnostics) — answerability 90; implementation detail, not a scope question.
- `UBU-Q0071` (legitimization cost model) — answerability 90; implementation detail requiring empirical measurement once a planner exists.
- `UBU-Q0072` (GPU-aware planner kernels) — partially resolved; subquestions 1 (solver library selection), 3 (mobile GPU targets), and 5 (cloud GPU path) remain open and are deferred beyond Phase 1.

None of these carry a `UBU-D0175` blocker certificate. None reduce `scope_freeze_readiness` under the current rubric.

---

### `mvp_readiness`: 22

| Criterion (weight) | Evidence | Score |
|---|---|---|
| Scope and blocker discipline (15) | Scope frozen; no certified blockers; design model consistent | 12 / 15 |
| Implementation slice coverage (25) | No runnable app; all Phase 1 slices are design-complete, not implemented | 3 / 25 |
| User-facing loop evidence (15) | No bootstrap interview, Calendar preview, or next-Task loop implemented | 0 / 15 |
| Integration / projection / worker / privacy boundaries (15) | Compartment, worker-authority, and GitHub-projection checks are designed but not implemented | 0 / 15 |
| Verification, fixtures, and deterministic tests (15) | `model-committee` has partial fixture support; no planning-kernel test suite exists | 2 / 15 |
| Dogfooding / artifact / public-claim evidence (10) | `model-committee` v0.3 produces reviewable dogfooding artifacts; no main-app dogfooding | 4 / 10 |
| Operational polish and contributor-run diagnostics (5) | `model-committee` is contributor-runnable; no main-app diagnostics | 1 / 5 |

**Total: 22 / 100**

---

### Per-slice status

| Phase 1 slice | Status |
|---|---|
| Bootstrap and seed model | Not started |
| GitHub import and External References | Not started |
| Objective / Task / UniverseState / Log admission | Not started |
| Plan / Calendar generation and explanation | Not started |
| Next-action focus plus feedback / recalculation | Not started |
| Risk and human-complete plan-quality reports | Not started |
| Compartment, worker, and projection authority boundaries | Not started |
| GitHub projection preview or approved write plus reconciliation | Not started |
| Release outreach and public dogfooding artifact package | Not started |

---

### Failing gates and stale inputs

- **No runnable end-to-end dogfooding loop.** This is the primary gate. Until a prototype exists that can import GitHub state, generate a Calendar, and recommend one Task, no higher `mvp_readiness` score is warranted.
- **No fixture-backed planning-kernel test suite.** `PLANNING_KERNEL_CONTRACT.md` specifies the typed request/response boundary, but no deterministic CPU reference path or test harness exists yet.
- **No Compartment / GitHub-projection hard-boundary checks.** These are required before `mvp_readiness` can exceed 74 even with a working loop.

### Manual assumptions and boundaries

- Scores are based on file state at `c3b61b0`; no live GitHub or CI signal was ingested.
- Implementation evidence is inferred from the Development readiness checklist above and from open/solved question counts; no fixture or test output was verified.

---

### Next slice most likely to raise the score

**Bootstrap and seed model.** This slice unblocks every other implementation slice. A working bootstrap interview with explicit Objective/Task seed creation is the minimum evidence needed to move `mvp_readiness` from the 0–39 band into the 40–59 band. Completing it alongside even a stub GitHub import and a single-step Calendar preview would move `mvp_readiness` to approximately 35–45 depending on test coverage.

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

- `PLANNING_KERNEL_CONTRACT.md` is a fourth canonical source file, read by providers, injected into prompts, snapshotted in runs, and allowed in patches.
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
- proposing precise patches to `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, or `PLANNING_KERNEL_CONTRACT.md`;
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
- `OUTREACH.md` - derived outreach document for FOSS maintainers and software engineers
- `PM_BRIEF.md` - derived brief for project leads and technical PMs
- `FUNDER_BRIEF.md` - derived brief for grantmakers, sponsors, and prototype funders
- `SOVEREIGN_COORDINATION.md` - derived brief for cypherpunks, privacy builders, and sovereign-coordination audiences
- `ORG_INTROSPECTION_BRIEF.md` - derived brief for mission-driven projects and organizational introspection
