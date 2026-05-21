# UbU Organizational Introspection Brief

**Status:** Derived audience-facing brief  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`  
**Audience:** FOSS maintainers, DAOs, nonprofits, mission-driven software teams, grant-funded projects, foundations, research groups, protocol teams, and organizations that want evidence of mission alignment

---

## The hook

> Can your project prove from its own records that it is actually committed to achieving its stated goals?

This question should be provocative, but not accusatory.

UbU’s organizational introspection feature is about evidence-backed self-governance. It should help a project inspect whether its actual work, decisions, overrides, resource allocation, and informal structure match its declared mission and commitments.

UbU should apply the same test to itself.

---

## Why this matters

Many projects have a mission statement, roadmap, or grant proposal.

Fewer projects can show that their day-to-day behavior actually follows it.

The real project may be distributed across:

- GitHub issues and pull requests;
- design documents;
- meeting notes;
- release notes;
- public chat logs;
- private or permissioned group chats;
- governance forums;
- calendars;
- funding reports;
- contributor onboarding discussions;
- informal decisions made by high-context maintainers.

Humans can sometimes reconstruct this from memory. New contributors, funders, users, and even existing maintainers often cannot.

UbU’s purpose is to make the evidence reviewable.

---

## Associations

UbU models organizations broadly as **Associations**.

An Association is not assumed to be a single objective legal object with authoritative membership. It is an Identity-scoped, perception-bound model of group-like coordination.

Associations may describe:

- FOSS projects;
- protocol teams;
- informal contributor groups;
- grant-funded working groups;
- nonprofits;
- companies;
- conference cohorts;
- DAOs or DAO-like projects;
- skill networks;
- friend groups or volunteer groups.

Legal entities, governance documents, GitHub organizations, fiscal sponsors, Discord servers, and public websites are evidence or External References. They are not the whole Association.

---

## AssociationAttestations

The core introspection mechanism is the **AssociationAttestation**.

An AssociationAttestation is a reviewable claim about an Association, backed by evidence and provenance.

Examples:

- “The project repeatedly prioritizes release stability over feature velocity.”
- “Most review authority currently flows through two maintainers.”
- “The stated onboarding priority is not reflected in issue labeling or maintainer response patterns.”
- “The grant milestone appears to drive more actual work than the public roadmap.”
- “Security review is treated as a release blocker despite not being stated as a top-level value.”

These claims should not be silently treated as truth. They should have source references, confidence, status, and review history.

---

## Input records

Organizational introspection can use public or permissioned records, including:

- `README.md`, governance docs, design docs, and roadmaps;
- GitHub issues, pull requests, reviews, labels, and milestones;
- meeting notes and board notes;
- release notes and changelogs;
- public Discord, Matrix, IRC, Slack export, or forum records where allowed;
- grant proposals, milestone reports, or ecosystem updates;
- calendars and event notes;
- outreach notes and follow-up logs.

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

Organizational introspection should not become:

- automated blame assignment;
- social scoring;
- contributor surveillance;
- funder-controlled monitoring;
- LLM-declared truth about group motives;
- a replacement for governance;
- a tool for exposing private conflict without consent.

The right framing is reviewable evidence, not automated judgment.

---

## UbU dogfooding

UbU should use organizational introspection on itself.

EthConf notes, outreach follow-ups, project artifacts, design decisions, open questions, model-committee cross-scoring artifacts, release work, and contributor interactions can be reviewed to ask whether UbU actually pursued its stated goals.

This dogfooding matters because the project claims to support evidence-backed self-governance. UbU should be able to show its own alignment process before asking other projects to trust the concept.

---

## Relationship to other UbU documents

This brief is narrower than `OUTREACH.md`.

`OUTREACH.md` explains why FOSS maintainers and software engineers may want to join or help UbU.

This brief explains why a project might want UbU even before it adopts the full personal planning system: it can help the project inspect whether its real behavior matches its stated mission.

---

## Where to go next

- Technical contributors should read `README.md`.
- General FOSS maintainers and software engineers should read `OUTREACH.md`.
- Project leads and technical PMs should read `PM_BRIEF.md`.
- Funders and sponsors should read `FUNDER_BRIEF.md`.
- Privacy and cypherpunk builders should read `SOVEREIGN_COORDINATION.md`.
