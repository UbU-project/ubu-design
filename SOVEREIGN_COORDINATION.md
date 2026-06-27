# UbU for Sovereign Coordination

**Status:** Derived audience-facing brief — Phase 1 feature-complete; canonical design files win on any conflict  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, `OPEN_QUESTIONS.md`, `PLANNING_KERNEL_CONTRACT.md`, and `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`  
**Audience:** cypherpunks, privacy engineers, Ethereum privacy builders, FHE/ZK/secure-compute researchers, privacy-coin-adjacent developers, FOSS contributors, and people interested in voluntary private coordination

---

## The core idea

UbU is not just productivity software.

UbU is intended to become a sovereignty-preserving life-logistics and coordination layer for human and AI labor. It starts with personal self-governance: the user models Objectives, Tasks, Plans, Calendars, Logs, Identities, Compartments, external events, affect, Preferences, Resources, Skills, and Techniques so they can decide what should happen next without handing their life model to an opaque centralized service.

From that foundation, UbU can support broader coordination: FOSS projects, informal crews, privacy-preserving work agreements, delegated Tasks, user-owned agents, Association-level planning, and eventually lawful private skill exchange.

---

## Why this matters

The AI market is moving toward assistants that want broad context, persistent memory, tool authority, realtime interaction, and background agency. That creates a sovereignty problem.

A system that knows a user's goals, calendar, messages, emotional state, work commitments, relationships, and private constraints can become useful enough to matter and dangerous enough to govern. UbU's answer is not to trust one assistant harder. UbU's answer is to make planning state explicit, compartmentalized, inspectable, correctable, and user-governed.

LLMs, realtime models, local agents, cloud models, and external tools may help extract candidates or propose actions. They do not become the authority over canonical state.

---

## The layer UbU occupies, and why it must be sovereign

It is worth being precise about which layer UbU is. A governance ecosystem is forming around AI agents — authorization, identity, action auditing, and personalized oversight that checks an agent's plan against declared values before it acts. UbU is not that layer. Those systems are *reactive*: they bound or audit what an agent already decided to do. UbU is *generative*: it originates what is worth doing from the user's own goals, values, affect, and attention, and treats agents as executors of a plan it produced. It also works from *introspected* state — what the user reports and reconciles about themselves — rather than inferred sensor state, because intent and affect are not sensor-readable. The problem is not novel; the open, user-owned, generative integration of it is.

This layer is exactly where sovereignty is won or lost. The next generation of multimodal assistants will be able to ingest every sensor a person carries and reproduce much of what UbU does — by consuming the user wholesale into a corporate model. That is the brute-force route, and it is likely to become the default because it is the easiest to ship. UbU is the elegant route to the same end: the same capability, the opposite means, with data ownership and inspectable reasoning preserved. For this audience the stake is direct — whether a user-sovereign alternative exists at all before total ingestion becomes the norm. The realistic aim is not to out-distribute incumbents but to make the sovereign pattern exist, stay credible, and become influential enough to be a real fork.

---

## Why an incumbent can't simply absorb this

It is worth separating UbU from the category it is easiest to mistake it for. AI calendar assistants — Motion, Reclaim, Clockwise, and the like — are auto-schedulers: they take the to-do list and events you already have and optimize their placement, the *when* of an already-decided *what*. UbU is the generative layer above that, originating what is worth doing from your goals, values, and affect. That is a category difference, not a feature gap.

The sharper question this audience asks is why a well-capitalized incumbent can't just add a private mode and copy it. The honest answer is not that they technically can't — any of them could ship local-first — but that they won't, because matching UbU's guarantee means giving up the pooled corpus their business model and valuation are built on. That is an innovator's dilemma, not a moat made of code. And even a sincere private mode hits the wall UbU's architecture removes: a company whose core business is ingesting user data asserting "trust us, this part is private" is exactly the promise UbU replaces with verifiability — no server, open source, runs on your device, inspectable. The future extensions point the same way: a resource-and-skill market or a delegation layer bolted onto a surveillance platform is just more harvesting. The differentiation is not that incumbents are forbidden to follow; it is that following costs them the asset they exist to accumulate, and a partial copy can only offer a promise where UbU offers proof.

## Sovereignty principles

UbU's sovereignty framing depends on several accepted design commitments:

- local-first operation should remain a real execution tier;
- cloud inference is optional and governed by policy, not hidden dependency;
- users may use multiple Identities;
- Compartments constrain storage, disclosure, export, retention, integrations, and device eligibility;
- Phase 2 sync semantics are specified by `DEVICE_SYNC_AND_COMPARTMENT_CONTRACT.md`, including arbitrary-device architecture, Zones, partial replicas, SyncStatements, and Compartment-safe replication;
- external agents submit candidate updates and evidence rather than receiving ambient authority;
- GitHub, calendars, and other systems are projections or inputs, not the full canonical life model;
- user overrides remain authoritative;
- user introspection remains personal and privacy-sensitive by default;
- organizational introspection is Association-level evidence review, not contributor surveillance;
- provider-neutral LLM execution prevents lock-in to one cognitive backend;
- the Phase 1 planning kernel is specified by `PLANNING_KERNEL_CONTRACT.md` as a typed pure-function boundary;
- `model-committee v0.3` treats frontier models as reviewable providers rather than trusted authorities.

The purpose is practical control over sensitive planning state.

---

## No central server, no pooled corpus

The sovereignty claim reduces to a few concrete architectural facts. There is no central server. There is no unencrypted data on the wire or at rest. Per-user data is siloed by default, and any external flow crosses an explicit, consented boundary rather than an ambient one. The consequence that matters most: there is no pooled corpus of user data for a future business model to become dependent on monetizing. That is the structural answer to the oldest question asked of every privacy project — what stops it from becoming the thing it opposes — and it is an answer in architecture, not in policy.

Sovereignty runs in the user's favor, not only the project's. Because the data is genuinely the user's, the user may export or even sell their own information if they choose; the system cannot and should not prevent it. What the architecture refuses is the inverse — a default in which the project itself depends on that data flowing outward. The right to disclose belongs to the user; the temptation to require disclosure is designed out.

---

## Identity, Compartments, and bounded disclosure

UbU assumes that people operate through multiple Identities. A person may need a personal Identity, professional Identity, family Identity, pseudonymous Identity, project Identity, or compartment-specific Identity. These Identities should not be collapsed by default.

A Compartment can carry hard policy about storage backend, allowed devices, identity disclosure, export restrictions, integration bans, retention rules, audit expectations, and provider eligibility.

This matters for sovereign coordination because useful collaboration often requires sharing selected facts without exposing the whole person. A team may need to know that a commitment is blocked. It does not need raw affect history, private messages, unrelated Objectives, or another client's confidential payload.

---

## Identity and access standards: open at the boundary, sovereign at the core

UbU adopts external identity-and-access standards by layer, and the asymmetry matters for this audience. The local single-user core stays UbU-native; open standards are surfaced only where work crosses from the user's control plane to a counterparty, worker, hosted service, marketplace, federation partner, or commercial wire.

SPIFFE/SPIRE is the outward-facing conformance target: it gives cryptographically attestable, externally auditable identity for *workloads* — worker instances, hosted planning workers, Compartment-scoped boundary agents, delegation endpoints, and Devices exposed as execution enclaves. It does not represent the human. A SPIFFE ID or SVID authenticates a workload; it does not by itself prove human authority. Authority still requires UbU-native capability grants, `authority_source`, `authority_scope`, Compartment policy, and Log provenance. Collapsing workload identity into human authority is exactly the failure this separation prevents.

OPA, where used, is an inward-facing engine only; its allow/deny vocabulary never becomes UbU's. UbU speaks in graduated legitimization and enforcement gates rather than boolean authorization, so a bypassed advisory remains introspection evidence rather than a denied request. SAML/OIDC is boundary-only enterprise compatibility, OIDC preferred for greenfield federation; an external IdP never becomes the source of truth for user-sovereign Identity.

The privacy caveat is first-class, not a footnote. SPIFFE IDs, SVIDs, trust-domain names, federation bundles, issuance logs, and boundary telemetry are themselves correlating identifiers, so any SPIFFE/SPIRE profile must treat namespace shape, SVID lifetime, bundle exposure, logging, and federation scope as privacy-critical parameters — the identity layer can otherwise re-link what Compartments are meant to keep separate. Whether Compartments map to one sovereign trust domain, per-Compartment trust domains, or a hybrid control-plane root with purpose-scoped boundary federation is an open question whose resolution must not weaken the Compartment non-correlation promise.

None of this is required for Phase 1: no SPIFFE, SPIRE, OPA, OIDC, SAML, SVID issuance, or federation is needed for the dogfooding MVP. It is the boundary posture for when delegated and marketplace execution arrives.

---

## Delegation Substrate

UbU's near-term marketplace-relevant primitive is the Delegation Substrate.

A Task should be formalizable for execution by the user, a local agent, a remote/cloud agent, a tool, an Automation Worker, a human Identity, an Association, or a General Contractor role.

A Delegation Substrate packet should make purpose, executor, authority, expected output, evidence, privacy scope, review, and escalation explicit. This is useful even when the user performs the Task solo. It records why the work matters, what result is expected, and how completion will be recognized.

For sovereign coordination, it also creates a future path to private work agreements and bounded labor exchange without starting from a surveillance marketplace.

---

## Attention sovereignty: owning the interruption chokepoint

A full-product expression of sovereign coordination — outside Phase 1 scope — is attention sovereignty: cross-channel, values-driven, context-aware governance of interruptions. Today the interruption chokepoint is held by the platforms whose incentive is to capture attention, not protect it; a system you cannot trust to want your focus is the one currently governing it. UbU moves that decision under the user's control. Whether a message reaches the user now depends on who it is from and how it ranks — and on what the user is doing and wants to protect, which only a user-held life-model knows — unified across email, chat, SMS, and calls. It merges modeled state with user-declared state, detects divergence through a mobile Discovery mode, and grades permissiveness rather than toggling it. The deeper point for this audience: who controls the chokepoint where interruptions are decided — the attention economy or the person — is itself a sovereignty question, and the only trustworthy owner of it is the user.

---

## Resource, Skill, and Skill Barter future direction

Skill Barter is a future direction, not a Phase 1 marketplace commitment. The private Resource and Skill model should come first.

A Resource is something a Task needs access to. A Skill is an Identity-owned capability that can be learned, practiced, tested, evidenced, and allowed to rust. A Technique can describe how Resources and Skills produce useful work. This lets UbU support a user-sovereign skill tree for real life: learn useful abilities, unlock DIY Tasks, reduce dependence on paid services where appropriate, and eventually trade proven capability through voluntary markets.

The root marketplace idea is voluntary, privacy-preserving skilled-work coordination among autonomous Identities. A mature version could include pseudonymous skill profiles, scoped work agreements, reputation without unnecessary doxxing, explicit commitments and deliverables, privacy-preserving evidence of completion, dispute workflows, lawful settlement references, and agentic and human executors operating through the same delegation model.

This is not token-first speculation, a public Phase 1 product, or a closed ecosystem. Preferred framing is an open, user-sovereign skill economy: users should become more capable inside and outside UbU.

---

## Ethereum as a practical settlement and trust layer

The strongest Ethereum use case for UbU is not a token. It is the lower settlement and trust layer beneath a task-driven Resource and Skill exchange.

UbU is the planning layer: it knows what Resource the user needs, when they need it, why, and at what cost. Ethereum provides the settlement layer: escrow, deposits, payments, rental bonds, programmable agreements, reputation attestations, proof of return, selective disclosure, pseudonymous capability claims, and dispute evidence.

The pitch is not "UbU is a crypto app." The pitch is:

> **UbU provides the missing user-facing interface that makes decentralized Resource and Skill markets useful in everyday life. Ethereum provides the trust and settlement layer underneath.**

This is a practical Ethereum adoption story. Most Ethereum infrastructure solves a trust problem that has no user-facing planning context. UbU provides that context: a user has a specific Task, a specific Resource need, a specific time window, and a specific budget. Ethereum settles the exchange. Neither is useful without the other.

For ETHConf audiences, the hallway hook is:

> **Task-driven markets, not search-driven markets.**

Existing marketplaces ask users to search for what they need. UbU's model asks: what does this user's plan require, and what is the most sensible way to access it? The exchange is generated from the plan, not from a keyword query.

---

## Why privacy tech builders may care

UbU creates natural demand for privacy-preserving infrastructure once the planning model works.

Future versions could benefit from FHE and other privacy-preserving computation, ZK proofs for selective claims, private reputation and selective disclosure, secure enclaves where appropriate, encrypted local-first sync, user-owned worker devices, compartment-aware model routing, private coordination protocols, and auditable agent authority and rollback.

The important ordering is: first build the planning and delegation semantics; then apply advanced cryptography where it protects real coordination value.

---

## Strategic future directions

These directions are reasons the data model stays general. They are not Phase 1 commitments, and they do not justify over-scoping the MVP.

### Concurrent multi-scale coordination

The bottom-up and top-down pictures of coordination are not sequential phases; they coexist. UbU's primitives behave identically at every scale, so the same Compartment and Delegation semantics serve a two-person tool loan and a global exchange without translation. A neighborhood tool library, a small Association, and a regional or global marketplace can all operate at once: the local layer is fully self-contained, and any larger market is an optional integration point rather than a mandatory backbone. Neither requires the other; neither collapses the other.

### Super-connectors

Some Identities hold standing in several contexts simultaneously — a local library, a regional market, a global network. They are the permeable membrane between layers, not gatekeepers over them. A super-connector can project a redacted piece outward — "this Resource is available" — without exposing an Association's inventory, membership, or internal coordination; can be the only externally visible member of an otherwise-private Association; and carries reputation and Skill evidence across contexts under Compartment-safe redaction. Because no layer depends on a central authority, a super-connector can leave a layer without collapsing it. The result is multi-network interoperability without merging everything into one social graph: a local Association trusts only the bridge it chose, never a global market.

### Governance as an emergent subsystem

The hard parts of multi-scale coordination — super-connector load, value drift between layers, incentive design, accountability at bridge boundaries — are well-solved governance problems that communities have handled for centuries. UbU does not solve governance. Its role is narrower and structural: honest data boundaries, Compartment control over what flows where, and a settlement-agnostic Delegation Substrate (gift, barter, time-banking, Ethereum, or otherwise). Communities and marketplaces layer their own governance on top, and because the data model is honest about boundaries, that governance can work instead of being theater.

### Directional authority

Authority and intent originate at the individual and flow outward into coordination, never inward. This is the line between a legitimate social outgrowth of self-governance and self-governance absorbed into a coordination platform. From the schema's point of view those two look almost identical — the same Objectives, Associations, Delegations — and only the direction of authority distinguishes them. Naming it is what keeps the entire multi-scale picture legible as UbU rather than as scope creep wearing UbU's vocabulary.

### Eject-not-override for shared-authority compartments

For any compartment whose policy is not solely user-set, sovereignty is preserved at the device boundary rather than the field level: the user can always destroy or eject the compartment wholesale, but cannot selectively override its external policy while retaining that compartment's data. A voluntarily-accepted, always-destroyable container keeps the sovereignty claim intact. A compartment the user cannot destroy is the line where UbU would become the thing it opposes.

### Protective shared-authority compartments

An inversion of corporate device management: a user's private affect/stress state can constrain a counterparty's behavior — a work scheduler that refuses to book deep-work meetings against high modeled stress — while the counterparty never reads the raw signal. Control flowing in the protective direction extends the sovereignty thesis rather than betraying it. The viable form requires the eject-not-override principle above plus a strict asymmetry: private state is constraint-only, never report-only. Two conditions gate it and are not solved by cryptography. Consent under employment power asymmetry is a structural limit — EU data-protection law already treats employee consent as generally invalid for this reason. And the protective channel is dual-use and can leak by inference, since a policy's observable behavior reveals something about the state it acts on. The asymmetry must therefore be structurally guaranteed and inference-resistant, or the result is device management that should not wear the UbU name. (See `ORG_INTROSPECTION_BRIEF.md` for the work-life-balance application.)

### Premium compute is leak-minimization, not leak-elimination

UbU's cloud story everywhere is leak-minimization, not leak-elimination. Any cloud computation leaks proportional to its duration through access patterns, timing, and resource profile — FHE protects the plaintext, not the side channels. A long-horizon premium planning run is the largest instance of a leak the architecture already accepts when it is bounded and consented. The correct framing names the residual leak as residual and requires it to be ephemeral and compartment-scoped, rather than implying a zero-leak guarantee that "local-first, inspectable" can be misread as making.

---

## What UbU is not

UbU should not be framed as a darknet labor market, a tax-evasion or sanctions-evasion system, a token launch, a reputation casino, a generic AI agent marketplace, or a centralized assistant that asks users to upload their life into a black box.

Preferred framing includes lawful private settlement, pseudonymous skill barter, reputation without doxxing, voluntary skilled-work coordination, Delegation Substrate, compartment-aware planning, and user-sovereign coordination.

---

## EthConf conversation focus

At ETHConf NYC (June 8–10, 2026), UbU demonstrated **Phase 0**, frozen at `ubu-phase0-demo` commit `9daffa7`: a live, running UbU instance that creates a user, onboards dummy GitHub access, runs affect calibration, converts Issues to Tasks, generates an affect-legitimized Plan, and displays it in Calendar preview — all applied to the UbU project itself. This was the first public demonstration of UbU coordinating UbU.

The useful question for cypherpunk and privacy builders is:

> What would it take for AI-assisted coordination to preserve user sovereignty instead of consuming it?

Concrete subquestions:

- What planning state should never leave the user's device?
- What can be safely projected to a team or marketplace?
- What Skill evidence can be shared without exposing raw life-planning data?
- What claims could be proven without exposing raw private data?
- Which parts of reputation require cryptography versus social review?
- What authority should a local or cloud agent never receive?
- How can a user recover from a bad agent action?
- What privacy primitives become valuable only after the Task and delegation model exists?

---

## Where to go next

- Technical contributors should read `README.md`.
- General FOSS maintainers and software engineers should read `OUTREACH.md`.
- Project leads and technical PMs should read `PM_BRIEF.md`.
- Funders and sponsors should read `FUNDER_BRIEF.md`.
- Mission-driven projects should read `ORG_INTROSPECTION_BRIEF.md`.
