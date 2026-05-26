# UbU

**Status:** Active pre-MVP dogfooding / implementation-first Phase 1  
**Repository:** `ubu-design`  
**Primary purpose:** Canonical public design state for the UbU project  
**Derived file:** This README is a technical contributor entry point. The canonical design authority is `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, and `PLANNING_KERNEL_CONTRACT.md`.

---

## What is UbU?

UbU is a privacy-first planning, coordination, and self-governance system.

It is intended to convert messy real-world inputs - tasks, calendar events, messages, external events, user preferences, physical and affective state, GitHub/project data, realtime interaction streams, agent or worker outputs, and integration data - into explicit, inspectable, recalculable plans.

UbU is not merely a task list, calendar application, chat assistant, or project-management dashboard. It aims to become a planning kernel for individuals and organizations: a system that models desired outcomes, constraints, risks, dependencies, available time, and human limitations, then helps determine what should happen next.

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
