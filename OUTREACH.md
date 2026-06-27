# UbU Outreach

**Status:** Derived public-facing outreach document — Phase 1 feature-complete; canonical design files win on any conflict  
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

Phase 1 feels like UbU to a nontechnical user: it asks a few bootstrapping questions, uses preference-calibration examples when helpful, previews the candidate Calendar, recommends one next action, explains why that action matters now, and learns from the user's response through Log review.

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

## Where UbU sits: the generative goal-and-values layer

The agentic-AI ecosystem is filling in fast, and it helps to be precise about which layer UbU occupies. Execution agents — local and hosted assistants that run tools, send messages, and act across services — are proliferating. So is the governance tooling beneath them: runtime policy engines, agent identity and authorization, verifiable action logs, and personalized oversight layers that check an agent's proposed plan against user-declared values before it runs. Standards work and regulation are moving in the same direction.

UbU is not competing with any of those. It sits one layer above them. Those systems are largely *reactive* and *constraint-shaped*: they bound, filter, or audit what an agent has already decided to do. UbU is *generative*: it originates what is worth doing in the first place — from the user's own Objectives, commitments, affect, attention, and constraints — and treats agents as downstream executors of a plan it produced. A constraint layer asks "is this agent's plan allowed by your values?" UbU asks "what should happen, given your life?" The two are complementary; the second is the under-occupied slot.

A related distinction matters technically. Most context-aware systems infer the user's state from *sensors*. UbU works from the user's *introspected* state — what the person reports and reconciles about their own goals, energy, and attention — because the parts of the planning problem that matter most (affect, intent, what is worth protecting) are not sensor-readable. The contribution is not a problem nobody has noticed: personalized value alignment, agent authorization, and context-aware interruption are all active fields with existing work. The contribution is the *integration* — a user-sovereign, generative layer that holds the person's real-world values and turns them into plans, not yet assembled as an open, local-first whole.

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

## Attention sovereignty (full-product direction)

One concrete expression of the generative layer — slated for the full-product track, not Phase 1 — is attention sovereignty: cross-channel, values-driven, context-aware governance of interruptions. Whether a given notification should reach the user *now* depends on two things current tools split apart: who the message is from and how it ranks (which per-channel AI filters already do), and what the user is doing and wants to protect (which only a life-model holds). UbU unifies these across email, chat, SMS, and calls, because users experience interruption as attention spent, not one app at a time.

The hard part is not sensing — phones cannot read mental state — but reconciliation. UbU merges a *modeled* state (what the Plan and UniverseState imply the user is doing) with a *declared* state (what the user reports), and the UX is the user collaborating with the model to keep the two aligned; intentionally mis-modeling one's own state is treated as an anti-pattern. On mobile, an interruption can trigger Discovery mode, which surfaces and records divergence between modeled and actual behavior. When UniverseState is modeled well, interruptions become predictable rather than reactive. Permissiveness is graded, not binary: as a focus window nears its end and a break is due anyway, the value of "take a break soon" and the value of "let this message through" sum, so the gate loosens toward the boundary. This is "smart Focus mode" as a smart home provides switchless lights — predict, prepare, adjust, adapt — rather than a manual toggle that is indistinguishable from airplane mode and never answers the question of why the phone is on at all.

Attention sovereignty has the same status as Resource/Skill readiness: central to the full vision, explicitly outside Phase 1 scope.

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

The first runnable UbU demo, Phase 0, frozen at `ubu-phase0-demo` commit `9daffa7`, was demonstrated at **ETHConf NYC, June 8–10, 2026**.

The Phase 0 demo creates a new user, runs the bootstrap onboarding interview, connects to a dummy GitHub environment (a pre-configured clone of the `ubu-design` repository), asks affect calibration questions, ingests dummy GitHub Issues as Tasks, generates a Plan with affect-legitimized breaks and recovery constraints, and displays that Plan in a Calendar preview and next-issue UI.

`model-committee` runs occurred during public demonstration ceremonies. The primary demonstration is **association introspection in action**: UbU coordinating the UbU project using its own planning model, live and inspectable.

Phase 0 is a standalone demo milestone, now complete. Phase 1 is now feature-complete, accelerated by the experience and patterns from the working Phase 0 demo.

### Phase 1: GitHub dogfooding (implementation in progress)

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

At ETHConf NYC (June 8–10, 2026), UbU demonstrated Phase 0, frozen at `ubu-phase0-demo` commit `9daffa7`: a live, running UbU instance that creates a user, onboards GitHub access, ingests Issues as Tasks, generates an affect-legitimized Plan, and shows Calendar preview — all applied to the UbU project itself. This was not a slide deck describing future features. It was a working demo of the core loop.

The goal is not to convert UbU into a conventional project-management product. The goal is to learn whether self-governance primitives can improve the work lives of autonomous contributors while also making project coordination more truthful.

---

## Build discipline: bootstrap order and the feature-to-data map

Two internal disciplines are worth stating because they explain how UbU stays buildable without over-scoping.

First, build order is driven by *bootstrap dependency*, not by feature value or dependency-set size. Circular-reference foundations such as UniverseState are implemented first — useful in isolation or not — because everything else references them. The Phase 1 dogfooding MVP exists for the same reason: it is the smallest loop that lets UbU help build the rest of UbU.

Second, the project is introducing an explicit *feature-to-data map*: for each feature, the data components it actually invokes at runtime versus those merely present in the model. As a worked example, the smart-Focus-mode decision invokes UniverseState, introspected affect, declared rules, divergence detection, dependency resolution (indirectly, for predictable disruption), and legitimization — and does *not* invoke extrospection, commitment tracking, or the privacy wire. The map's value is legibility: it lets a contributor or reviewer see exactly which subsystems a feature requires, and it prevents "this needs nearly everything" from silently meaning "build everything." The map is a planned artifact for the full-product track rather than a Phase 1 deliverable.

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

UbU is at a concrete inflection point. Phase 1 design is frozen, and Phase 1 is now feature-complete across the `UbU-project` repo constellation. Phase 0 — a live, runnable demo — was demonstrated at ETHConf NYC, June 8–10, 2026, frozen at `ubu-phase0-demo` commit `9daffa7`; the Phase 1 feature set has since been built out in full, and UbU now runs its own development loop on real infrastructure.

This is the moment when early contributors can engage with a working end-to-end system that runs its own development loop, meet the project in person, and shape the hardening and the Phase 2 expansion. The design is coherent and the Phase 1 feature set is complete enough to build on; the project is early enough that concrete contributions still matter.

---

## ETHConf NYC hallway pitches (speculative, post-MVP)

> **Status: speculative, post-MVP.** These are *hooks* about what UbU could become, for hallway conversations — not descriptions of current state. Anyone who wants concrete, shipped specifics should read the canonical files. Nothing here is a Phase 1–3 commitment. Canonical source files remain authoritative; where they differ from this section, they win.

**The one-line throughline (works for everyone):** UbU helps you see the coherence between who you say you are and what you actually do — at every scale, from personal (nutrition, assets, time) to community (peer teaching, resource sharing, Associations) to global (marketplace interoperability). It makes Resource, Skill, and Technique explicit, compartmentalizes what flows where, and lets communities govern themselves. Your data stays yours; authority flows outward from you.

Audience cuts below are starting points, not scripts — combine them for people who wear more than one hat (a cypherpunk founder, an academic who maintains FOSS), and watch which framing actually lands.

**Young professionals (primary):** "See what's actually wasting your time and money — gear you own but never use, meals you plan but never cook, skills you say matter but don't practice. Build real capability with visible progression. Teach and learn from people you already know. No algorithm optimizing you."

**Privacy builders & cypherpunks:** "True multi-layer federation — independent networks that interoperate without merging into one graph. No pooled corpus. Compartment policy is a hard product boundary, not advisory. Super-connectors bridge contexts by choice; local authority is preserved at every scale. And we're honest that cloud is leak-*minimization*, not a zero-leak claim."

**Founders & entrepreneurs:** "Marketplaces emerge from genuine peer exchange instead of a forced platform. Settlement is pluggable — Ethereum, fiat, time-banking, barter scrip. No network-capture trap; communities thrive standalone. Revenue from value, not lock-in, because there's no pooled corpus to monetize."

**FOSS contributors:** "The Technique library is crowdsourced and contributor-owned. Your project or tool library coordinates with zero external dependencies. Global coordination is an opt-in bridge, not a forced registry. And UbU runs UbU — you can watch the planning model work on a real project, live."

**Organizational leaders & workplace culture:** "Work-life balance as a data primitive instead of a slogan — coordination that respects modeled capacity and focus, with the worker as a planning participant who has standing, not a node to optimize. Organizational introspection without surveillance: see bottlenecks and unsustainable commitments without monitoring individuals.

**Ethereum & crypto builders:** "Task-driven markets, not search-driven markets — the plan says what's needed before the user searches, and Ethereum settles it underneath. Pseudonymous skill profiles and selective-disclosure reputation without doxxing. A Delegation Substrate maps cleanly to escrow, deposits, and programmable agreements."

**Privacy researchers & security engineers:** "Compartments as a case study in schema-enforced data-boundary control, with inference-resistance as an explicit design goal — policy behavior must not become an inference channel back to raw state. Local-first sync with no canonical server; the sync-sovereignty invariant as a testable property; cryptographic substrate left agnostic."

**Academic & research communities:** "Multi-agent planning that combines individual Objectives, capability, and affect constraints into group Plans without reducing humans to optimization nodes. Capability modeling (skills that rust, unlock, transfer). Revealed preference inferred from what people keep, use, and trade — without pooling raw data."

**Individuals seeking change:** "Your calendar says one thing; your choices say another. UbU makes the gap visible — no judgment, just honest feedback. Own your stuff or let it go. Be part of something without your community being absorbed into a platform. Your data stays yours, always."
