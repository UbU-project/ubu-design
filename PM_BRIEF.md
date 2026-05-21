# UbU for Project Leads and Technical PMs

**Status:** Derived audience-facing brief  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`  
**Audience:** Ethereum project leads, protocol leads, FOSS maintainers with coordination duties, engineering managers, release coordinators, grants/milestone coordinators, and technical PMs who coordinate autonomous contributors

---

## Why this audience should care

High-agency technical teams do not fail only because nobody wrote a ticket.

They fail because the project loses track of why work matters, what state changed, which dependencies are real, which commitments are stale, which contributors are overloaded, and which plans have quietly become fiction.

UbU is designed for that failure mode.

UbU is a privacy-first planning, coordination, and self-governance system. Its project-management value is derivative of the same core model used for personal self-governance: Objectives, Tasks, Plans, Calendars, Logs, Preferences, Identities, Compartments, Associations, external events, and reviewable state transitions.

The goal is not to make autonomous contributors easier to surveil. The goal is to make coordination explicit enough that people can act with more autonomy, less ambiguity, and better evidence.

---

## The problem UbU addresses

Most project tools represent workflow state:

- an issue is open or closed;
- a pull request is waiting for review;
- a deadline is approaching;
- a task is assigned to someone;
- a milestone is partially complete.

That is useful, but incomplete.

Technical coordination also needs to model:

- what Objective the work is meant to satisfy;
- which dependencies must be true before work is useful;
- which external events changed the plan;
- what the project believes will happen next;
- which commitments are real versus aspirational;
- when a plan should be recalculated;
- what information can be disclosed safely;
- whether the project is actually acting toward its stated mission.

UbU treats those as first-class planning concerns rather than informal context scattered through chat, GitHub comments, calendars, private notes, and memory.

---

## What UbU is

UbU is intended to become a planning kernel for individuals and organizations.

For technical teams, that means UbU can eventually help convert messy project inputs into explicit planning state:

- GitHub issues, PRs, reviews, CI failures, and milestones;
- contributor commitments and availability disclosures;
- design decisions and open questions;
- release tasks and outreach tasks;
- meeting notes and follow-up commitments;
- project risks and dependency chains;
- bounded projections back into GitHub or other team systems.

UbU’s model makes a strict distinction between canonical internal planning state and lower-dimensional projections into existing tools. GitHub is not the whole project model. It is one external surface where selected coordination state can be projected.

---

## What UbU is not

UbU should not become:

- a manager-first surveillance dashboard;
- a generic Jira, Linear, Asana, Trello, or Monday replacement;
- a productivity telemetry system;
- a capacity-scoring system for squeezing contributors;
- an opaque autonomous agent that mutates project state without review;
- a token-first coordination product.

Project-management functionality is valuable only when it preserves contributor sovereignty and builds the same primitives needed for the personal self-governance product.

---

## The coordination model

UbU models work as state transition.

A Task is not merely a note. It is an action or action bundle that assumes some preconditions, consumes time or attention, and should change the modeled universe if completed.

A Plan is an ordered, feasible set of WorkItems. A Calendar can hold multiple Plans and identify a default Plan. Logs and Snapshots record what actually happened, allowing the model to be corrected.

For a project lead, this makes coordination more inspectable:

- why is this the next Task?
- what does it unblock?
- which Objective does it serve?
- what would make this Plan invalid?
- what changed since the last planning pass?
- what should be disclosed to the team?
- what should remain private to an Identity or Compartment?

---

## Associations and autonomous teams

UbU treats organizations broadly as **Associations**: Identity-scoped, evidence-backed models of emergent coordination.

A FOSS project, grant-funded team, protocol working group, conference cohort, DAO-like project, contributor crew, company, or informal volunteer group can all be modeled as Associations without pretending there is one globally authoritative member list or objective social truth.

This matters for Ethereum and FOSS teams because much of the real organization exists outside formal HR charts:

- who actually reviews work;
- who carries release risk;
- who has informal authority;
- where decisions really happen;
- which mission statements guide behavior;
- which stated priorities are being ignored.

UbU should make that evidence reviewable without converting informal trust into managerial surveillance.

---

## Organizational introspection

One of UbU’s strongest project-lead hooks is organizational introspection:

> Can your project prove from its own records that it is actually committed to achieving its stated goals?

UbU should eventually help Associations inspect whether their actual work, decisions, resource allocation, overrides, and undocumented structure align with their declared mission and commitments.

The mechanism is evidence-backed review, not accusation. Candidate AssociationAttestations can be generated from permitted records such as docs, meeting notes, GitHub activity, issue comments, public chat logs, governance forums, calendars, and outreach notes. A human or project policy then accepts, rejects, edits, or disputes the candidate interpretation.

This is especially relevant for teams that receive grants, coordinate public goods, steward protocols, or ask contributors to trust their mission.

---

## Phase 1 relevance

Phase 1 does not need to solve full multi-user project management.

The first MVP is single-user GitHub dogfooding: using UbU to coordinate UbU’s own design, development, release, open questions, review artifacts, contributor outreach, and model-committee v0.2 cross-scored automation artifacts.

That still provides useful project-lead validation because it tests the same primitives:

- issue and PR ingestion;
- design-question tracking;
- open-decision governance;
- next-action planning;
- Logs and review;
- bounded projections back to GitHub;
- release outreach as ordinary project work;
- organizational introspection over the UbU project itself.

A technical PM or project lead does not need to believe in the full future system to provide valuable feedback. The most useful feedback is where their current coordination process breaks down.

---

## Useful EthConf conversations

UbU is seeking concrete examples, not generic praise.

Good project-lead conversations include:

- Where do GitHub issues stop representing the real plan?
- Which commitments go stale without anyone noticing?
- What project risks live only in someone’s head?
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
