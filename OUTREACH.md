# UbU Outreach

**Status:** Derived public-facing outreach document — updated for Phase 0 / ETHConf NYC 2026  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, `PLANNING_KERNEL_CONTRACT.md`, and `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`  
**Audience:** FOSS developers, project maintainers, Ethereum project leads, privacy engineers, automation builders, planning-tool researchers, independent technical consultants, prototype funders, and technically curious contributors

---

## Build software that helps humans govern their own time

UbU is a privacy-first planning, coordination, and self-governance system for implementing life logistics.

It is designed for people who are tired of tools that merely collect tasks, display calendars, summarize messages, or report status without understanding the deeper question:

> Given what matters, what constraints exist, what has changed, and what human limitations are real, what should happen next?

UbU aims to become a planning kernel for individuals and organizations. It turns messy real-world inputs into explicit, inspectable, recalculable plans: Objectives, Tasks, Preferences, Plans, Calendars, Logs, UniverseState, external events, worker automation, Delegation Substrate packets, privacy Compartments, Identities, Relationships, Associations, realtime/agentic candidate updates, and human affect.

The first MVP is intentionally practical:

> UbU should help coordinate the development of UbU itself.

Phase 1 also needs to feel like UbU to a nontechnical user: it should ask a few bootstrapping questions, use preference-calibration examples when helpful, preview the candidate Calendar, recommend one next action, explain why that action matters now, and learn from the user's response through Log review.

---

## Why UbU matters

Most productivity systems fail because they treat the user like a machine. They assume that if a task appears on a list or calendar, the user can simply execute it.

They rarely model energy, stress, attention, boredom, emotional load, uncertainty, dependencies, external interruptions, changing reality, hidden coordination cost, or the difference between a real commitment and a hopeful note.

Project-management systems have a related failure mode. They represent status, assignment, and deadlines, but they often miss the real decision problem: what Objective is being served, what dependency changed, what risk matters now, which work is merely noise, and which automation can be trusted.

UbU is designed to make those things explicit.

---

## The core idea

UbU models planning as a state-transition problem.

A Task is not merely a note. It is a proposed action that begins from some assumed state of the universe and, if successful, changes that state. A Plan is not merely a calendar layout. It is an ordered sequence of WorkItems that should satisfy constraints, respect dependencies, and move the modeled universe toward desired Objectives. A Log is not merely history. It is the record of what actually happened, allowing the system to compare prediction against reality and improve future planning.

This makes UbU naturally suited to recursive self-governance:

1. Check the current state for consistency.
2. Decide which problem or question is answerable and worth addressing next.
3. Perform work as an explicit state transition.
4. Record the result.
5. Re-check consistency.
6. Repeat.

That loop is central to the project.

---

## User introspection, organizational introspection, and extrospection

UbU has three related evidence-backed review patterns.

**User introspection** is the personal loop. It asks whether the user's actual behavior, Logs, affect, overrides, and outcomes match the user's stated Objectives, Preferences, constraints, and values. It supports Calendar preview, Log review, model correction, preference calibration, and personal self-governance.

**Organizational introspection** is the Association-level loop. It asks whether actual project work, decisions, resource allocation, overrides, undocumented authority, and informal structure match declared mission and commitments. It uses reviewable AssociationAttestations, not LLM-declared truth.

**Extrospection** is the Relationship-level loop. It compares the user's Relationship model, scope assumptions, trust calibration, reciprocity assumptions, boundary expectations, and counterparty-perspective hypotheses against permitted evidence, while respecting epistemic asymmetry.

These features share a review pattern, but their subjects and safety constraints differ. Outreach should avoid using organizational introspection as if it covered user introspection.

---

## The planning kernel has to be fast enough to trust

UbU's Calendar preview depends on a complete default Plan. The user should be able to inspect the ordered path ahead and ask why each Task is there.

The planner direction is explicit rather than agentic magic:

- a skeleton Plan first places Static Tasks and dependency chains;
- legitimization makes that skeleton Plan minimally human-viable by adding affect, recovery, transition, and sustainability constraints;
- candidate Plans add optional Dynamic Tasks and are compared by value, fragility, legitimacy, and modeled Plan probability;
- internal look-ahead may exceed the visible Calendar window so fragile prerequisites are not scheduled just in time;
- short-horizon repair handles likely near-term divergence;
- GPU-parallel candidate generation and stochastic simulation may be used, while exact or conservative CPU validation certifies hard constraints.

The Phase 1 planning-kernel schema and stage boundary are specified in `PLANNING_KERNEL_CONTRACT.md`.

---

## Compute choice is part of user sovereignty

UbU should not force one execution provider.

A user may run locally on mobile, use a laptop or desktop as a personal worker, later use a dedicated worker appliance, or opt into a hosted service. A third-party provider should be able to offer compatible execution without becoming the canonical owner of the UbU model.

Phase 1 embodies this concretely: the planning engine is a pure function over typed inputs and outputs, with no external calls, no ambient authority, and no hidden cloud dependency. Mobile and cloud backends are deferred beyond Phase 1. The FOSS core should stay backend-agnostic.

---

## Privacy-first by design

UbU is not designed around a centralized service owning user data.

The long-term architecture emphasizes local-first operation, user-controlled sync, explicit Zones, execution-enclave Devices, first-class Compartments, compartment-scoped references, multiple Identities, bounded disclosure, provenance, and user sovereignty. The Phase 2 sync boundary is now explicit in `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`; this does not expand Phase 1, but it prevents early code from assuming a central canonical server or permanent primary device.

Sensitive content should not leak merely because structural planning metadata is useful. A WorkItem should remain structurally usable even when sensitive compartmented content cannot be dereferenced.

---

## Human-aware planning

UbU treats human limitations as real constraints. In `user_mode`, affect belongs to UniverseState.

Energy, tiredness, stress, mood, motivation, boredom, emotional load, recovery needs, and related signals are part of the planning problem. Affect collection, Calendar preview, and Log review are themselves planned work. Discovery mode is a user-selectable workflow state, not covert surveillance.

The goal is not emotional surveillance. The goal is self-governance.

---

## Resource and Skill readiness: gamifying real life

UbU's long-term product is not only about arranging time. It should help a user become more capable in the real world.

A Resource is something the user needs access to: a document, tool, ingredient, credential, file, software license, payment method, workspace, or other stateful prerequisite. A Skill is something an Identity can do: a capability that can be learned, tested, practiced, refreshed, evidenced, and allowed to rust.

Together with a Technique database, these objects let UbU build a real-life capability graph. The user can see which Skills unlock which DIY tasks, maintenance work, professional capabilities, and future barter/labor opportunities. UbU can compare buying, hiring, doing it yourself, learning first, bartering, or deferring.

The outreach hook is strong when kept honest:

> UbU gamifies real life not by adding fake points, but by turning real Objectives, Resources, Skills, Techniques, constraints, and evidence into a capability tree the user can actually live inside.

---

## Library and Community Resource Mode

Many communities offer tool libraries, makerspaces, seed libraries, community workshops, sewing machines, kitchen equipment, and other Resources that most planning tools ignore entirely.

UbU should treat these as first-class Resource providers. A user can say "I want to fix small things around my apartment" and UbU can generate a plan that includes library tool loans, local workshop scheduling, Skill acquisition Tasks, and DIY projects using borrowed Resources — complete with return deadlines and future Skills unlocked.

Strong marketing lines for this feature:

> **UbU turns your library card into a real-life skill tree.**

> **Borrow the tool. Learn the skill. Do the project. Keep the capability.**

> **Own less. Do more. Learn more. Waste less.**

---

## Government and public-resource symmetry

Most planning tools model institutions only as sources of constraints: permits you need, regulations you must follow, taxes you owe. UbU models them from both sides.

Any institution that can constrain a user's plan may also provide Resources, permissions, remedies, or procedures that improve that plan. Grants, subsidies, weatherization programs, workforce training, legal aid, public small-business resources, hardship waivers, appeal processes, and benefit programs are all Resources that can be conditionally unlocked through the right prerequisite Tasks.

UbU can generate those Tasks automatically: apply for this benefit, collect these documents, file by this deadline, request this waiver. This turns complex institutional navigation into a scheduled, executable plan rather than an overwhelming wall of bureaucracy.

---

## Expert-Guided DIY and Technique Commissioning

When a user lacks the Skill to solve a problem themselves, UbU should not only offer "hire a professional." There is a middle tier that currently barely exists:

- **Tier 1:** Generic guides — free, generic, no diagnosis
- **Tier 2 (new):** Expert diagnosis + custom Technique Package — paid, specific to your situation
- **Tier 3:** Hire someone to do the whole job — expensive

A Technique Request lets the user submit evidence about their specific problem: photos, measurements, model numbers, symptoms, skill level, available tools. A skilled expert — a retired tradesperson, an experienced professional — reviews the situation and returns a Technique Package: diagnosis, parts list, tool list, step-by-step instructions, safety warnings, and the conditions under which to stop and call a professional.

This is not generic AI advice. It is expert delegation that produces a custom, executable artifact. The user gets situated expertise at a fraction of a service call; the expert generates income without physical labor.

UbU's Delegation Substrate, evidence model, and Technique objects make this a natural first-class primitive.

---

## Concrete use case: managing life with a young child

Parenthood is one of the most logistically complex, resource-intensive, emotionally loaded situations a person can be in — and it is almost entirely unsupported by existing tools.

UbU handles it. It knows what childcare subsidies the user might qualify for and generates the application steps. It tracks the car seat that expires in eight months and prompts a replacement plan before it is needed. It models the co-parenting relationship as a real coordination structure, surfacing when shared commitments are drifting out of alignment. It knows when a pediatric well-visit is due and finds a slot that fits around school pickup. And it knows that at 9pm on a Thursday after a hard week, the right next task is not "organize the school paperwork" — it is rest, so the user can actually function the next day.

This is the product in action, applied to one of the hardest and most universal situations people face.

---

## Dogfooding: UbU runs UbU

### Phase 0: ETHConf NYC demo

The first runnable UbU demo is up and running for demo usage as Phase 0 at `ubu-phase0-demo` commit `9daffa7`, targeting **ETHConf NYC, June 8–10, 2026**.

The Phase 0 demo creates a new user, runs the bootstrap onboarding interview, connects to a dummy GitHub environment (a pre-configured clone of the `ubu-design` repository), asks affect calibration questions, ingests dummy GitHub Issues as Tasks, generates a Plan with affect-legitimized breaks and recovery constraints, and displays that Plan in a Calendar preview and next-issue UI.

`model-committee` runs occur during public demonstration ceremonies. The primary demonstration is **association introspection in action**: UbU coordinating the UbU project using its own planning model, live and inspectable.

Phase 0 is a standalone demo milestone. Phase 1 implementation begins after ETHConf, accelerated by the experience and patterns from the working Phase 0 demo.

### Phase 1: GitHub dogfooding (post-ETHConf)

The Phase 1 MVP is focused on single-user GitHub dogfooding. UbU should help coordinate the UbU project itself by observing and modeling GitHub issues, pull requests, review requests, CI events, comments, labels, milestones, design questions, release-readiness checks, contributor interactions, planning-kernel work, and automation-worker outputs.

GitHub is treated as a projection of UbU state, not the source of truth. This allows FOSS contributors to keep using normal GitHub workflows while UbU maintains a richer canonical model internally.

---

## Release Outreach Pipeline

UbU should make every release explain itself.

The Release Outreach Pipeline is a future feature bundle that treats public explanation as part of release management. For UbU itself, a meaningful minor release should eventually produce user-facing release notes, developer release notes, screenshots, scripted demo captures, short video scripts, narration text, captions, metadata, known limitations, and concrete contributor calls-to-action.

Release outreach should be evidence-bound and privacy-aware. Claims should trace to implemented features, accepted decisions, closed issues, release notes, screenshots, demo recordings, fixtures, or explicitly labeled future plans.

---

## Model-committee: the bootstrap automation project

Before the main UbU MVP is implemented, the project is using a bootstrap automation tool called `model-committee`.

`model-committee` is not the canonical decision engine. It is an advisory Automation Worker pattern that reads canonical repo state, selects answerable open questions, asks approved model providers to propose concrete changesets, cross-scores those proposals, validates patches, and writes reviewable artifacts. Accepted design state exists only when committed to the canonical repo.

The current target is `model-committee v0.3`. It includes the v0.2 frontier cross-scoring workflow and adds `PLANNING_KERNEL_CONTRACT.md` as a fourth model-committee input file. It also adds rank-time answerability writes, prompt-size warnings, `manifest.schema_version = "0.3"`, duplicate-removal and tombstoning instructions for generated work, and a patch allowlist that includes the planning-kernel contract.

`model-committee` remains intentionally bounded. It must not directly call OpenAI, Anthropic, Gemini, or GitHub APIs; apply patches automatically; publish artifacts automatically; auto-merge; auto-push; create pull requests automatically; use adaptive model weights; run multi-turn Claude Code sessions; perform full Association automation; or implement UbU planning-kernel work.

---

## Why FOSS developers should care

FOSS development is full of hidden coordination costs: issue triage, design decisions, release planning, CI failures, pull request review, contributor onboarding, roadmap drift, stale discussions, duplicated issues, ambiguous priorities, burnout risk, under-documented decisions, and project governance.

For FOSS projects, UbU can eventually help answer:

- Which issues are actually blocked?
- Which issues are underspecified?
- Which design decisions are already settled?
- Which open questions are answerable now?
- Which PRs are waiting on review?
- Which contributors need responses?
- Which release blockers are real?
- Which tasks are merely noise?
- Which automation can safely proceed?

That is directly useful to maintainers, and it is a strong first use case because the UbU project can dogfood the process in public.

---

## ETHConf and autonomous-team relevance

Ethereum and FOSS teams are useful early feedback sources because many are remote, async-heavy, autonomy-heavy, GitHub-heavy, contributor-driven, cross-organizational, dependent on informal commitments, sensitive to surveillance and centralization, and forced to coordinate across chats, governance forums, code review, audits, releases, and calendars.

At ETHConf NYC (June 8–10, 2026), UbU will demonstrate Phase 0, now up and running for demo usage at `ubu-phase0-demo` commit `9daffa7`: a live, running UbU instance that creates a user, onboards GitHub access, ingests Issues as Tasks, generates an affect-legitimized Plan, and shows Calendar preview — all applied to the UbU project itself. This is not a slide deck describing future features. It is a working demo of the core loop.

The goal is not to convert UbU into a conventional project-management product. The goal is to learn whether self-governance primitives can improve the work lives of autonomous contributors while also making project coordination more truthful.

---

## Where contributors can help

Useful early work includes:

- parser and metadata tests for `OPEN_QUESTIONS.md`;
- dependency-DAG and decision-reference validation;
- fake provider mode and provider-failure fixtures;
- Codex and Claude Code provider integration tests;
- cross-scoring and quorum tests;
- `PLANNING_KERNEL_CONTRACT.md` fixtures and request/response validation examples;
- patch-validation tests;
- review-artifact format design;
- examples of GitHub issue/PR state that should become UbU WorkItems;
- examples of maintainer coordination failures that conventional tools fail to model;
- example message snippets that should compile into Tasks, priority decisions, or clarification requests.

Small, correct, reviewable work is more valuable than sweeping architectural enthusiasm.

---

## Non-negotiable project boundaries

UbU should not become manager-first surveillance software, adversarial social-graph extraction, hidden organizational surveillance, employee productivity scoring, a generic task-board clone, a centralized data trap, an opaque agent that mutates canonical state without review, or a popularity-driven project that loses its self-governance core.

Professional and FOSS use cases are valuable when they help build the same primitives required by the personal self-governance product: Objectives, Preferences, WorkItems, Plans, Logs, UniverseState, Resources, Skills, Techniques, Identities, Compartments, bounded disclosure, and recalculable planning.

---

## Why join now?

UbU is at a concrete inflection point. Phase 1 design is frozen. Phase 0 — a live, runnable demo — is up and running for demo usage at `ubu-phase0-demo` commit `9daffa7` for ETHConf NYC, June 8–10, 2026. Phase 1 implementation begins immediately after.

This is the moment when early contributors can watch a working end-to-end demo, meet the project in person, and shape Phase 1 implementation while the architecture is still malleable. The design is coherent enough to act on; the code is early enough that concrete contributions matter.
