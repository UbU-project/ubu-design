# UbU for Project Leads and Technical PMs

**Status:** Derived audience-facing brief — updated for Phase 0 / ETHConf NYC 2026  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, `PLANNING_KERNEL_CONTRACT.md`, and `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`  
**Audience:** Ethereum project leads, protocol leads, FOSS maintainers with coordination duties, engineering managers, release coordinators, grants/milestone coordinators, and technical PMs who coordinate autonomous contributors

---

## Why this audience should care

High-agency technical teams do not fail only because nobody wrote a ticket. They fail because the project loses track of why work matters, what state changed, which dependencies are real, which commitments are stale, which contributors are overloaded, and which plans have quietly become fiction.

UbU is designed for that failure mode.

UbU is a privacy-first planning, coordination, and self-governance system for implementing life logistics. Its project-management value is derivative of the same core model used for personal self-governance: Objectives, Tasks, Plans, Calendars, Logs, Preferences, Resources, Skills, Techniques, Identities, Relationships, Compartments, Associations, external events, and reviewable state transitions.

The goal is not to make autonomous contributors easier to surveil. The goal is to make coordination explicit enough that people can act with more autonomy, less ambiguity, and better evidence.

---

## The problem UbU addresses

Most project tools represent workflow state: an issue is open, a pull request is waiting, a deadline is approaching, a task is assigned, or a milestone is partially complete. That is useful, but incomplete.

Technical coordination also needs to model:

- what Objective the work is meant to satisfy;
- which dependencies must be true before work is useful;
- which external events changed the plan;
- which commitments are real rather than aspirational;
- when a plan should be recalculated;
- what information can be disclosed safely;
- whether the project is actually acting toward its stated mission.

UbU treats those as first-class planning concerns rather than informal context scattered through chat, GitHub comments, calendars, private notes, and maintainer memory.

---

## What UbU is

UbU is intended to become a planning kernel for individuals and organizations.

For technical teams, that means UbU can eventually help convert messy project inputs into explicit planning state: GitHub issues, PRs, reviews, CI failures, milestones, contributor commitments, availability disclosures, design decisions, open questions, release tasks, meeting notes, project risks, dependency chains, and bounded projections back into GitHub or other team systems.

GitHub is not the whole project model. It is one external surface where selected coordination state can be projected.

---

## Resource and Skill readiness for project work

Although UbU's root product is individual life logistics, the same primitives matter to project work. A Task can be blocked because a contributor lacks a credential, file, hardware device, test fixture, API key, review authority, budget, or necessary Skill. Resource and Skill readiness make those blockers explicit instead of leaving them hidden in chat history or a maintainer's head.

For technical teams, this later supports better onboarding, clearer delegation packets, realistic DIY-versus-external-vendor decisions, and evidence-backed skill development without turning the system into employee surveillance.

---

## Build sequencing and the feature-to-data map

Two disciplines from UbU's own project management are worth surfacing for this audience, because they are exactly the kind of thing leads spend effort recovering after the fact.

First, build order is driven by *bootstrap dependency*, not by feature value or by which feature is cheapest to ship. Circular-reference foundations such as UniverseState are implemented first — useful in isolation or not — because everything else references them. The Phase 1 dogfooding MVP follows the same logic: it is the smallest loop that lets UbU help coordinate the rest of UbU. This is why a feature-priority menu has limited use in early phases; sequencing is constrained by what must exist before what, not by demand ranking. That changes during the full 1.0 cycle, when lower-dependency, higher-choice features become schedulable.

Second, the project is introducing an explicit *feature-to-data map*: for each feature, the data components it actually invokes at runtime versus those merely present in the model. As a worked example, the smart-Focus-mode decision invokes UniverseState, introspected affect, declared rules, divergence detection, dependency resolution (indirectly), and legitimization — and does not invoke extrospection, commitment tracking, or the privacy wire. For a coordinating lead, the map is a legibility instrument: it makes "this feature needs nearly everything" falsifiable, prevents quiet scope creep, and gives reviewers a precise picture of what a slice depends on. It is a planned full-product artifact rather than a Phase 1 deliverable.

---

## What UbU is not

UbU should not become a manager-first surveillance dashboard, a generic Jira/Linear/Asana/Trello/Monday replacement, a productivity telemetry system, a capacity-scoring system for squeezing contributors, an opaque autonomous agent that mutates project state without review, or a token-first coordination product.

Project-management functionality is valuable only when it preserves contributor sovereignty and builds the same primitives needed for the personal self-governance product.

---

## Personal introspection versus organizational introspection

Project leads will often care most about organizational introspection, but UbU's foundation is personal self-governance.

**User introspection** helps an individual compare their actual behavior, Logs, Plans, affect, and overrides against their own Objectives, Preferences, constraints, and values. This should remain private by default and should not become manager-visible telemetry.

**Organizational introspection** helps an Association inspect whether actual work, decisions, resource allocation, overrides, and informal structure match declared mission and commitments. It uses reviewable AssociationAttestations with provenance and status.

The project-management value comes from respecting this boundary: private human state remains private unless explicitly disclosed, while selected coordination facts can still be shared.

---

## Associations and autonomous teams

UbU treats organizations broadly as Associations: Identity-scoped, evidence-backed models of emergent coordination.

A FOSS project, grant-funded team, protocol working group, conference cohort, DAO-like project, contributor crew, company, or informal volunteer group can all be modeled as Associations without pretending there is one globally authoritative member list or objective social truth.

This matters for Ethereum and FOSS teams because much of the real organization exists outside formal charts: who actually reviews work, who carries release risk, who has informal authority, where decisions really happen, which mission statements guide behavior, and which stated priorities are being ignored.

---

## Organizational introspection hook

One of UbU's strongest project-lead hooks is:

> Can your project prove from its own records that it is actually committed to achieving its stated goals?

Candidate AssociationAttestations can be generated from permitted records such as docs, meeting notes, GitHub activity, issue comments, public chat logs, governance forums, calendars, and outreach notes. A human or project policy then accepts, rejects, edits, or disputes the candidate interpretation.

This is especially relevant for teams that receive grants, coordinate public goods, steward protocols, or ask contributors to trust their mission.

---

## Phase 0 and Phase 1 relevance

### Phase 0: the ETHConf NYC demo

Phase 0 is a live, runnable UbU demo, now up and running for demo usage at `ubu-phase0-demo` commit `9daffa7`, targeting **ETHConf NYC, June 8–10, 2026**. It is the canonical pre-Phase-1 milestone.

The demo creates a new user, completes the bootstrap interview, connects to a pre-configured dummy GitHub environment (a clone of `ubu-design`), runs affect calibration questions, ingests dummy GitHub Issues as Tasks, generates an affect-legitimized Plan with breaks and recovery constraints, and displays the result in Calendar preview and next-issue UI. `model-committee` runs occur during public demonstration ceremonies.

The primary value demonstrated is **association introspection**: UbU using its own planning model to coordinate the UbU project, live and inspectable by conference attendees.

Phase 0 is a standalone demo. Phase 1 implementation begins after ETHConf, informed and accelerated by the working Phase 0 patterns and experience.

### Phase 1: post-ETHConf GitHub dogfooding

Phase 1 design is now frozen as of commit `cc8b339`. Phase 1 does not need to solve full multi-user project management. The first MVP is single-user GitHub dogfooding: using UbU to coordinate UbU's own design, development, release, open questions, review artifacts, planning-kernel contract, contributor outreach, and `model-committee` v0.3 automation artifacts.

That still tests the primitives project leads care about:

- issue and PR ingestion;
- design-question tracking;
- open-decision governance;
- next-action planning;
- Calendar preview and Log review;
- bounded projections back to GitHub;
- release outreach as ordinary project work;
- organizational introspection over the UbU project itself.

A technical PM or project lead does not need to believe in the full future system to provide valuable feedback. The most useful feedback is where their current coordination process breaks down.

---

## Useful EthConf conversations

At ETHConf NYC (June 8–10, 2026), UbU will be demonstrating Phase 0, now up and running for demo usage at `ubu-phase0-demo` commit `9daffa7`: a live running instance that onboards a user, ingests GitHub Issues as Tasks, generates an affect-legitimized Plan, and shows Calendar preview — all applied to the UbU project itself.

UbU is seeking concrete examples and feedback, not generic praise.

Good project-lead conversations include:

- Where do GitHub issues stop representing the real plan?
- Which commitments go stale without anyone noticing?
- What project risks live only in someone's head?
- What recurring coordination failure wastes senior contributor time?
- What should never be visible to a manager, funder, or public issue tracker?
- What should a project be able to prove from its own records?
- Which next-action recommendation would actually be trusted?

---

## Where to go next

- Technical contributors should read `README.md`.
- General FOSS maintainers and software engineers should read `OUTREACH.md`.
- Mission-driven projects should read `ORG_INTROSPECTION_BRIEF.md`.
- Funders and sponsors should read `FUNDER_BRIEF.md`.
- Privacy and cypherpunk builders should read `SOVEREIGN_COORDINATION.md`.
