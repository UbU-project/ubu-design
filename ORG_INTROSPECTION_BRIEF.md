# UbU Organizational Introspection Brief

**Status:** Derived audience-facing brief — updated for Phase 0 / ETHConf NYC 2026  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, and `PLANNING_KERNEL_CONTRACT.md`  
**Audience:** FOSS maintainers, DAOs, nonprofits, mission-driven software teams, grant-funded projects, foundations, research groups, protocol teams, and organizations that want evidence of mission alignment

---

## The hook

> Can your project prove from its own records that it is actually committed to achieving its stated goals?

This question should be provocative, but not accusatory.

UbU's organizational introspection feature is about evidence-backed self-governance for Associations. It should help a project inspect whether its actual work, decisions, overrides, resource allocation, and informal structure match its declared mission and commitments.

UbU should apply the same test to itself.

---

## Relationship to personal life logistics

Organizational introspection is an emergent use of UbU's personal self-governance model. The root product remains the individual life-logistics system: Objectives, Tasks, Plans, Logs, Resources, Skills, Techniques, Preferences, affect, Compartments, and user authority.

The organizational case becomes stronger when the same model can ask whether a project actually has the Resources and Skills required for its declared commitments, not only whether it has meetings or issues on a board.

---

## Distinction from personal introspection

Organizational introspection is not the whole introspection story in UbU.

**Personal or user introspection** asks whether an individual user's actual behavior, Logs, affect, overrides, and outcomes match that user's own Objectives, Preferences, constraints, and values. It belongs to personal self-governance, Calendar preview, Log review, and model correction.

**Organizational introspection** asks whether an Association's records support its declared mission, commitments, governance, and operating model. It belongs to Association review and uses AssociationAttestations.

The two patterns share evidence-backed review, but they must remain separate so that personal affect, private behavior, and relationship context do not become organizational telemetry by default.

---

## Why this matters

Many projects have a mission statement, roadmap, grant proposal, or public values statement. Fewer projects can show that their day-to-day behavior actually follows it.

The real project may be distributed across GitHub issues and pull requests, design documents, meeting notes, release notes, public chat logs, private or permissioned group chats, governance forums, calendars, funding reports, contributor onboarding discussions, and informal decisions made by high-context maintainers.

Humans can sometimes reconstruct this from memory. New contributors, funders, users, and even existing maintainers often cannot. UbU's purpose is to make the evidence reviewable.

---

## Associations

UbU models organizations broadly as Associations. An Association is not assumed to be a single objective legal object with authoritative membership. It is an Identity-scoped, perception-bound model of group-like coordination.

Associations may describe FOSS projects, protocol teams, informal contributor groups, grant-funded working groups, nonprofits, companies, conference cohorts, DAOs or DAO-like projects, skill networks, friend groups, or volunteer groups.

Legal entities, governance documents, GitHub organizations, fiscal sponsors, Discord servers, and public websites are evidence or External References. They are not the whole Association.

---

## AssociationAttestations

The core organizational-introspection mechanism is the AssociationAttestation: a reviewable claim about an Association, backed by evidence and provenance.

Examples:

- The project repeatedly prioritizes release stability over feature velocity.
- Most review authority currently flows through two maintainers.
- The stated onboarding priority is not reflected in issue labeling or maintainer response patterns.
- The grant milestone appears to drive more actual work than the public roadmap.
- Security review is treated as a release blocker despite not being stated as a top-level value.

These claims should not be silently treated as truth. They should have source references, confidence, status, review history, and a path for acceptance, rejection, editing, dispute, or supersession.

---

## Input records

Organizational introspection can use public or permissioned records, including:

- `README.md`, governance docs, design docs, roadmaps, and planning-kernel contracts;
- GitHub issues, pull requests, reviews, labels, and milestones;
- meeting notes and board notes;
- release notes and changelogs;
- public Discord, Matrix, IRC, Slack export, or forum records where allowed;
- grant proposals, milestone reports, or ecosystem updates;
- calendars and event notes;
- outreach notes and follow-up logs;
- `model-committee` review artifacts and score matrices.

Access policy matters. UbU should not collapse public, private, permissioned, personal, and compartmented records into one undifferentiated corpus.

---

## Workflow

A mature organizational introspection workflow might look like this:

1. Select an Association and a permitted evidence set.
2. Identify declared mission, goals, roadmap, constraints, and commitments.
3. Extract candidate events, decisions, priorities, dependencies, and informal authority patterns.
4. Generate candidate AssociationAttestations with source references and confidence.
5. Review, accept, reject, edit, or dispute each candidate.
6. Convert accepted insights into Tasks, Objective updates, risk reports, retrospective notes, or public explanations.
7. Repeat over time to detect drift.

The system should support uncomfortable questions without turning the LLM into an unaccountable judge.

---

## What this enables

Organizational introspection can help answer:

- Are we doing what we claim to be doing?
- Which stated priorities receive no actual work?
- Which undocumented priorities dominate the project?
- Which people or roles carry hidden coordination load?
- Which commitments have become fiction?
- Which decisions lack provenance?
- Which contributors cannot infer the real operating model?
- Which risks are visible in the record but ignored by the stated plan?

This is useful for maintainers, funders, contributors, and users, but the output should remain governed by disclosure policy.

---

## What this is not

Organizational introspection should not become automated blame assignment, social scoring, contributor surveillance, funder-controlled monitoring, LLM-declared truth about group motives, a replacement for governance, or a tool for exposing private conflict without consent.

The right framing is reviewable evidence, not automated judgment.

---

## UbU dogfooding

UbU uses organizational introspection on itself — and Phase 0 is the first public demonstration of this in action.

**Phase 0** is a live, runnable demo being built for ETHConf NYC, June 8–10, 2026. It creates a new user, onboards dummy GitHub access (a pre-configured clone of the `ubu-design` repository), runs affect calibration questions, converts GitHub Issues into Tasks, generates an affect-legitimized Plan, and displays that Plan in Calendar preview and next-issue UI. `model-committee` runs occur during public demonstration ceremonies.

The primary demonstration value of Phase 0 is exactly what this brief describes: **UbU applying its own planning and self-governance model to the UbU project, live, in public, in front of an audience that can inspect the result**. This is association introspection running on the association that built it.

Phase 1 implementation begins after ETHConf. The full organizational introspection loop — EthConf notes, outreach follow-ups, project artifacts, design decisions, open questions, `model-committee v0.3` cross-scoring artifacts, planning-kernel contract work, release work, and contributor interactions — will be reviewed to ask whether UbU actually pursued its stated goals.

This dogfooding matters because the project claims to support evidence-backed self-governance. UbU should be able to show its own alignment process before asking other projects to trust the concept.

---

## Relationship to other UbU documents

This brief is narrower than `OUTREACH.md`. `OUTREACH.md` explains why FOSS maintainers and software engineers may want to join or help UbU. This brief explains why a project might want UbU even before it adopts the full personal planning system: it can help the project inspect whether its real behavior matches its stated mission.

For the personal introspection case, technical contributors should read `README.md` and the canonical files.

---

## Where to go next

- Technical contributors should read `README.md`.
- General FOSS maintainers and software engineers should read `OUTREACH.md`.
- Project leads and technical PMs should read `PM_BRIEF.md`.
- Funders and sponsors should read `FUNDER_BRIEF.md`.
- Privacy and cypherpunk builders should read `SOVEREIGN_COORDINATION.md`.
