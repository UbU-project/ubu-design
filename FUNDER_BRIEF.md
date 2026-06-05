# UbU Funder Brief

**Status:** Derived audience-facing brief — updated for Phase 0 / ETHConf NYC 2026  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, `PLANNING_KERNEL_CONTRACT.md`, and `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`  
**Audience:** grantmakers, ecosystem sponsors, angels, hackathon judges, aligned funders, and prototype sponsors

---

## Summary

UbU is a privacy-first planning, coordination, and self-governance system for implementing life logistics. It is not merely a calendar app, task manager, project board, or chat assistant.

UbU is intended to become a planning kernel that converts messy real-world inputs into explicit, inspectable, recalculable Plans. The first MVP is deliberately narrow: use UbU to coordinate the development of UbU itself.

Funding is useful when it accelerates reusable open-core trunk capabilities: planning, local-first data, GitHub dogfooding, Logs, Calendars, Tasks, Objectives, privacy Compartments, bounded automation, reviewable projections, and planning-kernel contract implementation.

Funding is harmful when it pulls UbU into a bespoke private workflow, surveillance product, token-first marketplace, or funder-controlled roadmap.

---

## Why now

UbU has moved through pure concept work, active design dogfooding, and is now entering its first runnable milestone.

**Phase 1 design is frozen** as of commit `cc8b339`. The design repository has a stable canonical design set, a fully specified Phase 1 planning-kernel contract, a canonical Phase 2 device sync and Compartment contract, a complete accepted-decisions log, and a ranked open-questions queue. No further broad design changes are warranted.

**Phase 0** — the canonical pre-Phase-1 milestone — is a live, runnable demo now up and running for demo usage at `ubu-phase0-demo` commit `9daffa7`, targeting **ETHConf NYC, June 8–10, 2026**. The demo creates a new user, onboards dummy GitHub access, asks affect calibration questions, converts GitHub Issues to Tasks, generates an affect-legitimized Plan with breaks and recovery constraints, and displays the result in Calendar preview and next-issue UI. `model-committee` runs during public demonstration ceremonies.

Phase 0 is the first runnable public demonstration of the core UbU loop on the UbU project itself.

**Phase 1 implementation begins immediately after ETHConf.** The immediate opportunity is to convert a frozen, internally consistent design into a working Phase 1 prototype while the scope is still narrow enough to stay inspectable. The patterns and experience from the working Phase 0 demo directly accelerate that work.

---

## Why this matters now: the agent-governance moment

UbU's timing is tied to a shift already underway. As AI assistants gain tools, memory, and the authority to act, an entire layer of agent governance is forming around them — authorization, identity, action auditing, and personalized oversight that checks an agent's proposed plan against user-declared values. Standards bodies and regulators are moving in parallel. The components and the problem are not novel; several active fields and projects already work on pieces of this. What does not yet exist as an open, user-owned whole is the layer *above* all of it: a generative system that holds the individual's real-world values and goals and originates the plan that agents then execute. UbU's contribution is that integration — not the discovery of a new problem.

Beneath the feature story is a public-good stake that is the honest reason the project exists. The next generation of multimodal assistants will be able to consume every sensor a person carries and reproduce much of what UbU does — by pulling the user's whole life into a corporate model on someone else's servers. That is the brute-force path to a capable assistant, and it is likely to become the default because it is the easiest to build. UbU reaches the same destination by the opposite means: user-owned data, inspectable reasoning, the user's own goals. The window in which a user-sovereign alternative can be established — before total ingestion becomes the unquestioned norm — is what this funding is ultimately about.

---

## Theory of impact: what success means

UbU's success should be measured honestly. A solo, open-source, local-first project does not win the mass personal-assistant market against well-capitalized incumbents, and framing success that way would mislead. The realistic and worthwhile goal is narrower and durable: for the user-sovereign pattern to *exist*, be *credible*, and *influence* where the broader trajectory goes — to give people a real, auditable fork rather than a single default. That kind of public good is strengthened, not erased, when commercial assistants arrive, because it becomes the alternative people can point to and choose.

This also widens who UbU can serve. Because the system runs on hardware people already own, with no data-center dependency, it can reach users the commercial systems have no incentive to serve — including where the compute economics of the ingest-everything model simply do not reach. Accessibility here is an architectural property, not an add-on: self-governance built to run on a phone is self-governance that needs no subscription to a remote brain.

---

## What UbU is building

UbU is building a system that models Objectives and Preferences; Tasks, dependencies, preconditions, and effects; Plans and Calendars; Logs and Snapshots; external events and recalculation triggers; Identities, Relationships, RelationshipScopeTransitions, Associations, and bounded disclosure; Compartments and privacy policy; Automation Workers and agentic candidate updates; Delegation Substrate packets; extrospection as a future Relationship review pattern; user introspection as a personal Log/Plan review loop; organizational introspection as Association-level mission-alignment review; and projections into external systems such as GitHub.

The first version does not need every abstraction fully implemented. Phase 1 should prove that the core loop is useful, understandable, and extensible.

---

## Phase 0 demo and Phase 1 prototype focus

### Phase 0: ETHConf NYC demo

The Phase 0 demo shows the core UbU loop end-to-end in a self-contained dummy environment:

- user onboarding and bootstrap interview;
- dummy GitHub ingestion (pre-configured clone of `ubu-design`);
- affect calibration questions;
- GitHub Issues → Tasks conversion;
- Plan generation with affect-legitimized breaks and recovery constraints;
- Calendar preview and next-issue UI.

Phase 0 is a standalone demo. It demonstrates that the loop is real and inspectable, not that every Phase 1 capability is production-ready. Code reuse from Phase 0 into Phase 1 is not assumed; the value is demonstrated patterns, gained experience, and public evidence that UbU can coordinate itself.

### Phase 1 prototype focus

The Phase 1 MVP is single-user GitHub dogfooding.

A successful prototype should help one user coordinate the UbU project itself by:

- importing or observing GitHub issues, PRs, reviews, CI events, labels, and milestones;
- representing project work as Objectives, Tasks, dependencies, and Plans;
- recommending one next Task with an explanation;
- supporting regular Calendar preview and Log review;
- maintaining canonical-vs-derived document discipline;
- using `PLANNING_KERNEL_CONTRACT.md` as the explicit planning-kernel boundary;
- projecting selected low-dimensional state back into GitHub;
- producing reviewable release/outreach artifacts;
- preserving privacy, compartment, provenance, and authority boundaries.

This is intentionally narrower than a general productivity app.

---

## What funding can accelerate

Aligned funding can accelerate:

- implementation of the Phase 1 planning loop, targeting a local GPU desktop backend with a CPU reference path;
- planning-kernel request/response validation and fixtures;
- GitHub ingestion and projection;
- local-first storage and schema work;
- Task/Objectives/Calendar/Log implementation;
- bootstrap interview and one-next-Task UX;
- Calendar preview, Log review, and user introspection workflows;
- `model-committee v0.3` hardening and run-artifact discipline;
- privacy and Compartment guardrails;
- release outreach artifacts tied to actual implementation;
- contributor onboarding materials and implementation-ready issues.

The strongest funding target is work that becomes ordinary open-core trunk capability.

---

## Acceptable funding shapes

Compatible funding may include grants, hackathon prizes, sponsorship for a concrete Phase 1 implementation slice, prepaid prototype sponsorship, narrow design-partner retainers, paid discovery sessions that produce reusable trunk requirements, or infrastructure support that does not create hidden proprietary dependency.

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

## What structurally prevents capture

A reasonable funder asks how a privacy-first project avoids becoming the surveillance product it opposes once commercial pressure arrives. UbU's answer is architectural rather than a promise. There is no central server, and no unencrypted data on the wire or at rest; per-user data is siloed by default, with any external flow passing only through an explicit, consented boundary. This forecloses the usual failure mode — a pooled corpus of user data that a future business model becomes financially dependent on monetizing. The user retains the right to export or even sell their own data, because that is their sovereignty to exercise; what the architecture refuses is a default in which the project itself comes to depend on that data flowing outward. Formal commercial-entity governance is deliberately deferred until after the MVP, but the data-model and boundary decisions that make capture cheap-to-prevent rather than expensive-to-retrofit are being made now.

---

## Why Ethereum/FOSS funders may care

UbU is relevant to Ethereum and FOSS ecosystems because those communities contain autonomous contributors, complex dependency graphs, informal governance, grant and milestone commitments, privacy-sensitive coordination, open-source sustainability problems, AI-tooling pressure, and strong norms against centralized surveillance.

UbU is not primarily a crypto product, but Ethereum and adjacent FOSS ecosystems are good early validation environments for sovereign coordination infrastructure.

---

## The long-term investor thesis

UbU starts as a focused wedge into personal life logistics, but the long-term upside is becoming the **control layer for human goals, Resources, Skills, money, Tasks, and delegation**.

The market opportunity the full product touches:

- productivity and personal planning
- personal finance and inventory
- learning and skill acquisition
- home maintenance and DIY
- local services and freelance labor
- subscription and asset management
- library and community resource access
- resource rental and peer-to-peer markets
- resale and secondary markets
- government program navigation and benefits
- Web3 settlement and portable reputation

The key investor insight is that UbU creates demand from inside the user's actual life plan — not from a search interface. That is structurally different from generic marketplaces, which wait for a user to know what to look for. UbU knows what the user needs before they search for it.

---

## New market opportunities the full product unlocks

**Benefits and public resource navigation.** Billions of dollars in unclaimed benefits, grants, tax credits, weatherization programs, and public services go unused annually because navigation is cognitively overwhelming. UbU's government/public-resource symmetry model turns program eligibility into prerequisite Tasks with evidence requirements and deadlines — the difference between knowing a program exists and having a plan to get it.

**Remote diagnosis and expert knowledge packaging.** A Technique Request lets a user submit evidence about a specific problem; a skilled expert returns a custom Technique Package: diagnosis, parts list, step-by-step instructions, safety notes. This is a new market tier between generic guides and full-service labor. Retired tradespeople, experienced professionals, and domain experts can monetize situated knowledge without performing physical work.

**Household life operations.** When Resource tracking, Technique database, Expert-Guided DIY, public program navigation, and affect-aware planning combine, UbU becomes the operational layer for a household — not just a reminder app.

**Economic mobility and life transition support.** Career change, relocation, recovery, new child, aging parents — these are situations where Resource, Skill, financial, and institutional pictures change simultaneously. UbU's planning model is designed for exactly this kind of multi-variable constraint navigation.

**Community and cooperative resource networks.** Library tool loans, makerspaces, repair cafés, seed libraries, and community workshops are Resources most planning tools ignore. UbU's Library and Community Resource Mode makes these first-class inputs.

---

## Full-product expansion: Resource and Skill readiness

The full version 1.0 track is not just a smarter calendar. It should add Resource and Skill readiness: whether the user has the documents, tools, credentials, locations, money, access, and embodied capability needed to perform the work.

This creates a concrete consumer and prosumer feature path: household logistics, maintenance planning, digital-asset readiness, subscription/resource tracking, DIY-versus-hire tradeoffs, capability acquisition, and eventually a Skill Barter marketplace. Quicken-like financial management is a downstream extension only after Resources connect spending and ownership to Objectives, Tasks, Techniques, and Skills.

This strengthens UbU's market story because it moves the product from productivity software into life logistics and economic self-sufficiency.

---

## Strategic future directions

The following directions are important but should not be confused with Phase 1 commitments:

- multi-user UbU-to-UbU coordination;
- Association-level organizational introspection;
- Relationship-level extrospection;
- Delegation Substrate marketplace flows;
- Resource and Skill readiness;
- DIY-versus-purchase/hire planning;
- Technique database and real-life skill tree;
- Skill Barter marketplace;
- high-privacy compute using FHE, ZK, secure hardware, or other privacy-preserving techniques;
- user-owned worker devices and compute markets;
- richer realtime multimodal interaction;
- a UbU Corp premium long-horizon, high-granularity, high-compute planning tier;
- food, nutrition, and physiological-health planning;
- asset economics and true cost-of-ownership analysis;
- concurrent multi-scale coordination with super-connectors.

Two of these are worth elaborating as commercial directions. A **UbU Corp premium planning tier** would offer long-horizon, high-granularity planning over months or years using substantial compute — plan simulation for individuals or organizations with unusually complex needs. It complements rather than competes with the Ethereum-settlement and Skill Barter paths, and it requires no persistent pooled corpus, which preserves the structural answer to capture. One property travels with it: any extended cloud computation leaks proportional to its duration through access patterns and timing, which even FHE does not remove. The tier is therefore the largest instance of a leak the architecture already bounds and consents elsewhere; it stays ephemeral and compartment-scoped, and is described as leak-minimization rather than a zero-leak guarantee.

**Marketplaces emerge rather than being constructed.** Bottom-up peer exchange and top-down marketplaces run concurrently rather than sequentially, with settlement pluggable per community (see `SOVEREIGN_COORDINATION.md`). Revenue then comes from genuine coordination value rather than lock-in, and because there is no pooled corpus to monetize, the capture-resistance thesis holds as the product scales.

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
