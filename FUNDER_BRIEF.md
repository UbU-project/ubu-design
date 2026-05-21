# UbU Funder Brief

**Status:** Derived audience-facing brief  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`  
**Audience:** grantmakers, ecosystem sponsors, angels, hackathon judges, aligned funders, and prototype sponsors

---

## Summary

UbU is a privacy-first planning, coordination, and self-governance system.

It is not merely a calendar app, task manager, project board, or chat assistant. UbU is intended to become a planning kernel that converts messy real-world inputs into explicit, inspectable, recalculable Plans.

The first MVP is deliberately narrow: use UbU to coordinate the development of UbU itself.

Funding is useful when it accelerates reusable open-core trunk capabilities: planning, local-first data, GitHub dogfooding, Logs, Calendars, Tasks, Objectives, privacy Compartments, bounded automation, and reviewable projections.

Funding is harmful when it pulls UbU into a bespoke private workflow, surveillance product, token-first marketplace, or funder-controlled roadmap.

---

## Why now

UbU has moved beyond pure concept work into active pre-MVP dogfooding.

The project has a public design repository with canonical design files:

- `DESIGN.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`

It also has a constrained dogfooding path through model-assisted review and GitHub-centered project coordination. The accepted v0.2 dogfooding direction adds independent frontier-provider cross-scoring so proposal agreement and disagreement become reviewable evidence rather than hidden model behavior. The immediate opportunity is to convert the design into a working Phase 1 prototype while the scope is still narrow enough to stay inspectable.

The funding question is therefore practical:

> Can a modest amount of funding accelerate a reusable open-core prototype without corrupting the self-governance mission?

---

## What UbU is building

UbU is building a system that models:

- Objectives and Preferences;
- Tasks, dependencies, preconditions, and effects;
- Plans and Calendars;
- Logs and Snapshots of what actually happened;
- external events and recalculation triggers;
- Identities, Relationships, Associations, and bounded disclosure;
- Compartments and privacy policy;
- Automation Workers and agentic candidate updates;
- Delegation Substrate packets for self, human, tool, or agent execution;
- projections into external systems such as GitHub.

The first version does not need every abstraction fully implemented. Phase 1 should prove that the core loop is useful, understandable, and extensible.

---

## Phase 1 prototype focus

The Phase 1 MVP is single-user GitHub dogfooding.

A successful prototype should help one user coordinate the UbU project itself by:

- importing or observing GitHub issues, PRs, reviews, CI events, labels, and milestones;
- representing project work as Objectives, Tasks, dependencies, and Plans;
- recommending one next Task with an explanation;
- supporting regular Calendar preview and Log review;
- maintaining canonical-vs-derived document discipline;
- projecting selected low-dimensional state back into GitHub;
- producing reviewable release/outreach artifacts;
- preserving privacy, compartment, and authority boundaries.

This is intentionally narrower than a general productivity app.

---

## What funding can accelerate

Aligned funding can accelerate:

- implementation of the Phase 1 planning loop;
- GitHub ingestion and projection;
- local-first storage and schema work;
- Task/Objectives/Calendar/Log implementation;
- bootstrap interview and one-next-Task UX;
- model-committee automation hardening, including v0.2 Claude Code cross-scoring and public run-artifact publication discipline;
- test fixtures and dogfooding workflows;
- privacy and Compartment guardrails;
- release outreach artifacts tied to actual implementation;
- contributor onboarding materials and implementation-ready issues.

The strongest funding target is work that becomes ordinary open-core trunk capability.

---

## Acceptable funding shapes

Compatible funding may include:

- grants;
- hackathon prizes;
- sponsorship for a concrete Phase 1 implementation slice;
- prepaid prototype sponsorship;
- narrow design-partner retainers;
- paid discovery sessions that produce reusable trunk requirements;
- infrastructure support that does not create hidden proprietary dependency.

Customer-specific configuration, hosting, packaging, support, or compliance work can be commercial when it stays outside the open-core boundary and does not become required for public dogfooding.

---

## Red lines

Funding should be rejected or renegotiated if it requires:

- surveillance of private affect, relationship, or compartment state;
- manager-visible productivity telemetry as a core feature;
- funder control over roadmap, licensing, contributor access, or accepted decisions;
- a private branch whose main value cannot become reusable trunk capability;
- token-first speculation before the planning model works;
- confidentiality that prevents honest public explanation of architectural constraints;
- urgency that displaces the Phase 1 prototype, dogfooding, or contributor recruitment.

The simple screen is:

> Does the funded deliverable make the open personal self-governance trunk better for independent knowledge workers, FOSS contributors, and future public dogfooding?

If yes, it may be worth considering. If no, it likely compromises the project.

---

## Why Ethereum/FOSS funders may care

UbU is relevant to Ethereum and FOSS ecosystems because those communities contain:

- autonomous contributors;
- complex dependency graphs;
- informal governance;
- grant and milestone commitments;
- privacy-sensitive coordination;
- open-source sustainability problems;
- AI-tooling pressure;
- strong norms against centralized surveillance.

UbU is not primarily a crypto product, but Ethereum and adjacent FOSS ecosystems are good early validation environments for sovereign coordination infrastructure.

---

## Strategic future directions

The following directions are important but should not be confused with Phase 1 commitments:

- multi-user UbU-to-UbU coordination;
- Association-level organizational introspection;
- Delegation Substrate marketplace flows;
- Skill Barter marketplace;
- high-privacy compute using FHE, ZK, secure hardware, or other privacy-preserving techniques;
- user-owned worker devices and compute markets;
- richer realtime multimodal interaction.

These directions explain why the Phase 1 planning kernel matters. They do not justify over-scoping the MVP.

---

## What a funder should ask

Useful due-diligence questions include:

- What concrete Phase 1 slice will the money complete?
- Which open-core files, schemas, tests, or workflows will change?
- How will the deliverable be dogfooded by UbU itself?
- What privacy or authority boundary does the work preserve?
- What would count as a failed prototype?
- Which future features become easier if this work succeeds?
- What should remain explicitly out of scope?

---

## Where to go next

- Technical contributors should read `README.md`.
- General FOSS maintainers and software engineers should read `OUTREACH.md`.
- Project leads and technical PMs should read `PM_BRIEF.md`.
- Mission-driven projects should read `ORG_INTROSPECTION_BRIEF.md`.
- Privacy and cypherpunk builders should read `SOVEREIGN_COORDINATION.md`.
