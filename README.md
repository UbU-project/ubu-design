# UbU

**Status:** Active pre-MVP dogfooding / implementation-first Phase 1  
**Repository:** `ubu-design`  
**Primary purpose:** Canonical public design state for the UbU project

---

## What is UbU?

**UbU** is a privacy-first planning, coordination, and self-governance system.

UbU is intended to convert messy real-world inputs - tasks, calendar events, messages, external events, user preferences, physical and affective state, GitHub/project data, realtime interaction streams, agent or worker outputs, and integration data - into explicit, inspectable, recalculable plans. A message should eventually be treated as a context-bearing communication event, not merely a flat text string.

UbU is not merely a task list, calendar application, or project-management dashboard. It is intended to become a planning kernel for individuals and organizations: a system that models desired outcomes, constraints, risks, dependencies, available time, and human limitations, then helps determine what should happen next.

UbU models organizations broadly as **Associations**: Identity-scoped, evidence-backed coordination structures that may be formal or informal. A FOSS project, contributor crew, friend group, event cohort, skill network, nonprofit, company, DAO-like project, or marketplace can all be modeled as an Association when coordinated through shared Objectives, Relationships, commitments, norms, and bounded disclosure.

The first MVP is designed around **dogfooding**: using UbU to coordinate the design, development, release, and maintenance of UbU itself.

---

## Core philosophy

UbU is based on several design principles:

1. **User sovereignty**

   The user is the final authority over what the user wants and what occurred.

2. **Explicit value**

   Value is attached to Objectives through user-defined Preferences. Numeric utilities may be derived for planning, but they are transient computational artifacts, not canonical user values. UbU may use preference-calibration examples during onboarding and review, but those examples become canonical only if the user accepts or edits them.

3. **Explicit planning**

   Planning must remain explicit and constraint-based. LLMs may assist, but canonical planning and decision logic must remain inspectable and recalculable outside the LLM.

4. **Privacy-first architecture**

   UbU is designed around local-first operation, compartmentalized data, multiple Identities, and user-controlled sharing.

5. **Affect-aware planning**

   In `user_mode`, human affective state is part of the planning problem. Energy, stress, tiredness, mood, and related human limitations are constraints that planning must respect.

6. **First-person legibility**

   Phase 1 must be understandable as a simple first-person loop: answer a few bootstrapping questions, receive one recommended next Task, inspect why it matters now, act or override, and let UbU learn from the result.

7. **Dogfooding**

   The Phase 1 MVP should help coordinate UbU’s own GitHub issues, pull requests, reviews, CI events, release milestones, design questions, and contributor interactions.

8. **Association-aware coordination**

   UbU treats formal organizations, informal groups, and ad hoc project communities as Associations rather than assuming every group has a single objective member list or central authority.

9. **Organizational introspection**

   UbU should help Associations inspect whether their real work, decisions, overrides, and undocumented structure align with their declared mission and commitments.

10. **Extrospection and Relationship self-governance**

   UbU should help users review whether their Relationship models, scope assumptions, trust calibration, reciprocity expectations, and boundary assumptions are supported by permitted evidence, while never claiming authoritative access to another person's inner state.

11. **Provider-neutral LLM execution**

   Local LLM execution remains the privacy-preserving baseline, but optional cloud LLMs, BYOK providers, UbUCorp managed inference, and user-owned workers should be routed through explicit policy rather than hidden dependency.

12. **Context-rich communication**

   Phase 3 should include minimal UbU-to-UbU contextual messaging so messages can carry priority, topic, response expectation, assumptions, ambiguities, provenance, and disclosure policy instead of forcing the receiver to infer everything from flat text.

13. **Realtime and agentic AI boundary**

   Realtime, multimodal, tool-using, and memory-bearing models are useful interaction backends, but they emit candidate updates. UbU's planner, Logs, Compartments, Identities, and review rules remain authoritative.

14. **Delegation Substrate**

   UbU should prepare Tasks for delegation by formalizing purpose, executor, authority, expected output, evidence, privacy scope, review, and escalation. The same structure is useful for solo Tasks as a self-reminder of how and why the Task should be performed.

15. **MCP-style interoperability**

   UbU should eventually operate as both an MCP-style client and server, exposing only narrow, capability-scoped, Compartment-aware tool surfaces.

16. **Skill Barter future direction**

   Skill Barter is a future privacy-preserving skilled-work marketplace direction and EthConf outreach hook. The MVP should implement Delegation Substrate primitives, not a public marketplace.

---

## Canonical design files

The canonical public design state is maintained in:

- [`DESIGN.md`](DESIGN.md)
- [`DECISIONS.md`](DECISIONS.md)
- [`OPEN_QUESTIONS.md`](OPEN_QUESTIONS.md)
- [`PLANNING_KERNEL_CONTRACT.md`](PLANNING_KERNEL_CONTRACT.md) - Phase 1 planning-kernel request/response and GPU pipeline contract

Derived public-facing projection files should summarize the canonical design state but are not themselves design authority.

Current derived public-facing files are:

- [`README.md`](README.md) - technical contributor entry point and project summary
- [`OUTREACH.md`](OUTREACH.md) - outreach document for FOSS maintainers and software engineers
- [`PM_BRIEF.md`](PM_BRIEF.md) - project-lead and technical-PM brief
- [`FUNDER_BRIEF.md`](FUNDER_BRIEF.md) - grantmaker, sponsor, and prototype-funder brief
- [`SOVEREIGN_COORDINATION.md`](SOVEREIGN_COORDINATION.md) - cypherpunk, privacy, and sovereign-coordination brief
- [`ORG_INTROSPECTION_BRIEF.md`](ORG_INTROSPECTION_BRIEF.md) - organizational-introspection brief for mission-driven projects

When derived files conflict with canonical files, the canonical files win.

---

## Current project status

UbU is currently in **active pre-MVP dogfooding** with broad design automation stopped by `UBU-D0175`; remaining design work should support concrete Phase 1 implementation slices.

The design has reached the point where additional broad philosophical elaboration has diminishing returns unless it directly supports implementation, recruitment, dogfooding, or market discovery.

The `model-committee` v0.1 baseline is the first runnable bootstrap artifact for using model-assisted review to process UbU design questions and generate reviewable changesets. The accepted v0.2 direction adds Claude Code CLI as a second frontier provider, schema-native structured output, cross-scoring, disagreement flags, and operator-run publication of run artifacts.

The Phase 1 MVP scope is frozen around single-user GitHub dogfooding, with Delegation Substrate-compatible fields only where they support dogfooding, worker assignment, or solo Task self-reminder clarity.

The current operational target is:

> Use UbU's explicit model, `model-committee`, GitHub dogfooding inputs, regular Calendar preview, regular Log review, and bounded projection artifacts to help UbU coordinate the development of UbU itself.

---

## Current recruitment priority

UbU is seeking a small core cohort of serious, self-directed builders.

The project does not need popularity for its own sake, but it can productively absorb multiple committed contributors who are willing to work on the trunk of the project: the planning kernel, dogfooding loop, privacy model, local-first architecture, and self-governance UX.

Good early collaborators may have experience with:

- local-first software;
- privacy-preserving systems;
- developer tooling;
- planning or scheduling systems;
- GitHub automation;
- LLM orchestration;
- FOSS maintenance;
- high-autonomy technical work;
- emotionally humane productivity tools;
- organizational introspection and evidence-backed project review;
- privacy-preserving identity, reputation, and coordination systems.

Casual interest is welcome, but the highest-value contributions are concrete: code, test fixtures, design review, workflow examples, prototype funding, and sustained subsystem ownership.

---

## Prototype-funder hypothesis

A plausible first commercial beachhead is privacy-sensitive independent knowledge work: independent technical consultants, freelance developers, security researchers, solo founders, independent academics, technical writers, and similar workers who manage complex multi-client obligations.

This group is strategically relevant because it combines:

- real deadline and dependency complexity;
- strong privacy and compartmentalization needs;
- willingness to pay for tools that improve professional leverage;
- direct experience with self-governance failures;
- overlap with UbU’s long-term personal planning mission.

Prototype funding is compatible with UbU only if it funds trunk features needed by the personal self-governance product.

---

## Planning kernel direction

UbU's Calendar model now distinguishes layered planning responsibilities.

First, the planner creates a **skeleton Plan**: a dependency-valid foundation built by placing Static Tasks, walking backward through dependency DAGs, and scheduling prerequisites before dependents. A skeleton Plan is not enough by itself; it can be structurally valid while still being unrealistic for a human.

Second, UbU performs **legitimization**. Legitimization adds the minimum affect, recovery, transition, rest, and sustainability constraints needed to turn the skeleton Plan into a minimally human-viable baseline. The legitimized skeleton Plan becomes the baseline feasible Plan against which richer candidate Plans are compared.

Third, the planner generates and evaluates candidate Plans with optional Dynamic Tasks, alternative placements, stochastic assumptions, and Plan probabilities. DFS-like search may be one implementation technique, but it is no longer the conceptual foundation by itself.

Fourth, the runtime needs short-horizon reactive repair so the system can adapt when reality diverges. Early completion, late completion, interruptions, external events, affect shifts, and user overrides should not require an expensive whole-world reanalysis before the user can continue.

The default Plan remains deterministic, ordered, inspectable, and explainable. It is selected by **Plan probability** among deterministic candidate Plans that have already been made legitimate and value-evaluated for their modeled branch. The internal planning horizon may look beyond the visible Calendar window, and fragile prerequisites may be scheduled earlier to reduce last-minute impossible choices.

---

## Mobile-first, local-first, and scalable compute

UbU should remain useful in mobile-only mode, but mobile should not be treated as the full global optimizer. A mobile device should act as the real-time steward of Plan legitimacy, user agency, and next-action clarity.

Provisional Compact Calendar defaults are:

- one-minute full-detail planning delta;
- five-minute moderate mobile delta;
- fifteen-minute low-power or offline delta;
- one-hour reactive branch horizon;
- `0.99` short-horizon branch coverage target.

For MVP, the mobile-friendly planning subset is Task criticality, last legitimate Plan storage, simple repair rules, conflict severity levels, cached explanations, next-best-action mode, and basic decision envelopes. Rich BFS branch packaging, learned local policies, and extensive stochastic repair are post-MVP by default.

The Phase 1 performance target is a local desktop or laptop GPU configured by the power user. The GPU planning engine is a pure function over a typed `PlanningRequest` and `PlanningResponse`, with no external calls, no I/O, and no mutable state. It runs four pipeline stages in PyTorch: `skeleton_sampling`, `affect_legitimacy_filter`, `value_scoring`, and `monte_carlo_rollout`. `MAX_PLANNING_TASKS = 256` is the Phase 1 planning window ceiling. Future premium or wide-horizon tiers may raise this ceiling by scalar configuration, subject to memory, scenario-count, correlation-matrix, validation-cost, and backend performance limits. A CPU reference path is required alongside the GPU backend for tests, CI, and contributors without GPU hardware. Mobile and cloud planner backends are deferred beyond Phase 1. The Phase 1 schema and stage-boundary details are specified in `PLANNING_KERNEL_CONTRACT.md`.

Task durations use either fixed duration or a shifted log-normal distribution parameterized by optimistic lower support, most-likely duration, and P95 high estimate. The accessible framing: a stop-light model where delay sources stack asymmetrically and early completion is absorbed cheaply by pulling the next eligible Task forward rather than triggering a global replan.

CPU or conservative exact logic certifies skeleton validity, hard constraints, contradiction diagnostics, and explanations. GPU search proposes; CPU validates.

Cloud or external compute may improve performance, granularity, branch coverage, and analysis depth, but must not be a hidden mandatory dependency for the open-core planning loop. Future execution backends may include Phase 2 personal worker devices, dedicated appliances, UbU hosted services, third-party compatible providers, and future privacy-preserving compute such as practical encrypted computation. Cloud planning payloads should minimize PII and transmit only the structured timing, dependency, value, constraint, criticality, and legitimacy information needed by the provider.

Cloud LLMs are optional execution providers, not the canonical planner. UbU should support local providers such as `ollama`, user-configured BYOK cloud APIs, optional UbUCorp managed inference, and user-owned remote workers through one policy-governed routing layer.

---

## Human-complete planning

UbU treats affect as a core part of planning, not a decorative wellness feature.

A plan that ignores fatigue, stress, boredom, motivation, emotional load, recovery, and dignity is not merely incomplete. It may become actively misleading.

UbU should help users receive fast feedback about whether a plan is working, revise plans when reality disagrees, and grow beyond current limits without treating themselves like machines.

The goal is neither comfort-maximization nor coercive productivity. The goal is humane self-governance: disciplined action that respects the user’s emotional and physical reality.

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

This is the public-facing shape of the product. The full Plan remains inspectable, but the default mode may reduce cognitive load by showing one next action at a time.

---

## ETHConf 2026 / autonomous-team feedback focus

UbU is preparing to gather feedback from FOSS maintainers, Ethereum project leads, protocol teams, and other people who coordinate highly autonomous technical contributors.

The project is especially interested in workflows where the real state of work is split across GitHub, calendars, chat, private notes, maintainer memory, CI, reviews, release obligations, audit constraints, and informal commitments.

The immediate goal is not to replace existing project-management tools. The immediate goal is to understand how a privacy-first self-governance system can help contributors plan privately while publishing only the coordination facts a team actually needs:

- blockers;
- commitments;
- dependency status;
- review needs;
- milestone risks;
- selected availability;
- explicit requests for decisions or intervention.

This feedback should improve the Phase 1 dogfooding target: UbU coordinating the development of UbU itself.

UbU will also use EthConf outreach as an organizational-introspection dogfooding case. Notes, follow-ups, project artifacts, and public retrospectives can be reviewed to ask whether UbU actually pursued its stated outreach goals. The provocative but evidence-bound question is: can a project prove from its records that it is actually committed to achieving its stated goals?

An optional EthConf **VoxPopuli** demo may be used if cheap enough relative to higher-priority deliverables. In that flow, a user speaks freely about what they wish would happen, and an LLM-assisted extractor produces candidate Objectives, Tasks, constraints, preferences, and assumptions for inspection. This is a public demonstration hook, not a replacement for the narrow Phase 1 bootstrap loop.


---

## Release Outreach Pipeline

UbU accepts the **Release Outreach Pipeline** as a future feature bundle:

> UbU should make every release explain itself.

For UbU-runs-UbU, a meaningful minor release should eventually produce a release outreach package: public release notes, developer release notes, screenshots, scripted demo captures, short video scripts, narration text, captions, YouTube metadata, known limitations, and contributor calls-to-action.

These artifacts should be grounded in evidence from repo state, release notes, accepted decisions, closed issues, UI-test screenshots, demo recordings, fixtures, and clearly labeled future plans. UbU should not let generated outreach drift into unsupported hype.

The pipeline should begin manually and become more automated over time: script generation, screenshot capture, demo-flow export, storyboard generation, narration preparation, rough video rendering, and gated publication. Publication to external channels should require human or explicit policy approval by default.

This feature is not only for UbU marketing. Project-management configurations should be able to define communication Objectives for users, developers, maintainers, funders, community members, internal stakeholders, and other audiences.

---

## What UbU is not

UbU should not become:

- a generic Jira, Linear, Asana, Trello, or Monday replacement;
- an employee-surveillance dashboard;
- a centralized productivity telemetry system;
- a manager-first capacity scoring system;
- a tokenized coordination product before the planning model works;
- an opaque autonomous agent that mutates canonical project state without review;
- a popularity-driven project that loses its personal self-governance core.

Project-management functionality is a derivative use case. It is valuable only when it helps build the same primitives needed by the personal self-governance product.

---

## MVP release phases

### Phase 1: Single-user GitHub dogfooding

A single user uses UbU to coordinate the UbU project.

Primary goals:

- import or observe GitHub issues, PRs, reviews, CI events, and milestones;
- represent them in UbU’s Objective/Task/Calendar model;
- generate useful Plans;
- run a minimal bootstrap interview to seed the user/project context;
- use preference-calibration examples as MVP-important onboarding and review aids;
- run regular Calendar preview and Log review Tasks to keep the model aligned with the user's behavior;
- allow the user to select Discovery mode at any time, especially from a mobile app with useful sensors;
- show a next-action focus screen with one recommended Task and an explanation of why it matters now;
- update GitHub as a low-dimensional projection of UbU state;
- expose limitations and open questions through dogfooding.

### Phase 2: Single-user multi-device synchronization

A single user runs UbU across multiple devices or execution enclaves.

Phase 2 validates:

- local-first sync;
- partial replication;
- Zone and Compartment boundaries;
- device roles;
- conflict handling.

### Phase 3: Minimal multi-user / Identity coordination

Multiple humans coordinate through explicit Identities, capabilities, limited disclosure, contextual messages, and commitments.

Phase 3 should enable coordination without surveillance or shared global truth. A premier Phase 3 feature is a minimal Message Context Envelope that lets a receiver's UbU triage asynchronous messages by priority, interrupt level, topic, response expectation, and actionability.

---

## Core model summary

The UbU model currently includes:

- Objective
- Technique
- Preference
- WorkItem
- Task
- Container
- UniverseState
- Snapshot
- Plan
- Calendar
- Log
- Message Context Envelope
- Message Extraction Result
- Voice Profile Descriptor
- Identity
- Relationship
- RelationshipScopeTransition
- ExtrospectionFinding
- Zone
- Compartment
- Automation Worker
- External Event
- External Reference
- Association
- AssociationAttestation
- SharedAssociationDescriptor

Some entities are intended for Phase 1 implementation. Others are documented now to avoid future contradiction.

---

## Operating modes

Each UbU instance runs in exactly one mode:

- `user_mode`
- `organization_mode`
- `worker_mode`

### `user_mode`

A personal UbU instance operated for an autonomous human user.

Only `user_mode` models intrinsic human affect.

### `organization_mode`

An organizational UbU instance operated on behalf of a project or organization.

Organization mode does not model intrinsic affect. For MVP, organization-mode users may be treated as admin-equivalent to avoid premature RBAC complexity.

### `worker_mode`

A worker-mode instance performs delegated work assigned by another UbU instance.

Worker mode is used by Automation Workers and may perform LLM calls, GitHub processing, document analysis, external API work, or other delegated tasks.

---



## Contextual messaging and legacy communication

UbU should eventually make communication more efficient by attaching structured context to messages.

A legacy message such as a WhatsApp text, Discord post, IRC line, SMS, email, or Slack message is usually flat. It includes text, sender, time, and maybe a channel label, but it rarely carries the planning context that determines what the receiver should do with it.

UbU-to-UbU communication can include a bounded Message Context Envelope: message kind, topic, related Objective or Task when shareable, Association context when appropriate, priority, interrupt recommendation, response expectation, assumptions, ambiguities, provenance, and disclosure policy.

This is valuable even in minimal Phase 3 form because it helps the receiving UbU decide whether to interrupt the current Plan, create a Task, update an Objective, or defer the message to a communication-review window.

Legacy integrations can still help one-sided users by extracting candidate structure from flat messages. When both parties use UbU, the same legacy transport may be upgraded through an attached, linked, or side-channeled UbU envelope.

Structured message extraction should begin with schema-constrained LLMs or local models plus validation and repair. Fine-tuned extractor models may become useful later after UbU has stable schemas and corrected examples.

Optional personalized TTS or voice descriptors are a future communication/accessibility direction, but voice metadata is sensitive and must be opt-in, compartmentalized, separated from authentication, and designed to avoid deceptive impersonation.

---

## Association and organizational introspection

An **Association** is UbU's term for a group-like coordination structure as perceived by an Identity. It can be a formal organization, informal project, contributor crew, event cohort, friend group, skill network, or future marketplace.

Associations are evidence-backed and perspective-bound by default. UbU should represent membership, roles, authority, priorities, norms, and commitments as claims and attestations with provenance rather than pretending every group has one objective global member list.

Organizational introspection is the Association-level version of personal Log review. UbU can analyze permitted records - design docs, GitHub issues, meeting notes, chat logs, outreach notes, roadmaps, and public governance discussions - to generate reviewable AssociationAttestations and feedback questions about whether actual behavior matches declared mission and commitments.

For UbU itself, EthConf outreach is the first concrete dogfooding case: the project will try to turn conversations into explicit follow-up Tasks, contributor paths, funding signals, and a redacted retrospective about whether the outreach actually served UbU's stated goals.

---

## Relationships and extrospection

A **Relationship** is UbU's perspective-bound model of interaction between Identities. Relationships have **epistemic asymmetry**: the user can report their own declarations, experiences, and reflections, but UbU can only maintain evidence-backed hypotheses about another party's perspective.

**Extrospection** is the Relationship-level review pattern. It compares the user's counterparty-perspective hypotheses, scope declarations, trust assumptions, reciprocity assumptions, affective experience, and boundary expectations against permitted evidence. It should surface evidence in tension rather than claim to know what another person thinks.

Users may also create Objectives to change Relationship scope. A `RelationshipScopeTransition` is an Objective target for user-controlled actions such as disclosures, invitations, boundary-setting, availability changes, or clarification attempts. Counterparty response remains autonomous evidence, not user success or failure.

Relationship safeguards are default-on advisory checks, not paternalistic hard gates. Structurally enforceable privacy, Compartment, authorization, EvidenceUsePolicy, provenance, audit, and integration boundaries remain hard. Behavioral-risk checks such as manipulation-risk, power-asymmetry risk, or rumination risk are fallible and should generally be overrideable, uncertainty-aware, and introspection-relevant when bypassed.

---

## GitHub dogfooding

For dogfooding, GitHub is treated as a low-dimensional projection of canonical UbU state.

UbU is the source of truth. GitHub Issues, PRs, comments, labels, reviews, CI, and milestones must be interpreted into UbU objects and events.

UbU may project selected state back into GitHub through clearly marked managed labels, comments, or body blocks. Other GitHub edits are treated as external events by default.

Missed GitHub updates are expected in MVP, so reconciliation is a first-class concern.

---

## Model-committee bootstrap project

`model-committee` is the first runnable bootstrap automation project for active pre-MVP UbU dogfooding. After `UBU-D0175`, it should focus on implementation-support dogfooding rather than open-ended design expansion.

The project is an early example of UbU dogfooding: UbU uses an automation loop to help coordinate its own design and development through reviewable run artifacts and changesets.

`model-committee` is not the canonical decision engine. It is an advisory Automation Worker pattern that reads canonical repo state, identifies open questions, generates candidate changesets, scores those changesets, and writes reviewable artifacts.

Accepted design state exists only when committed to the canonical repo.

---

## Model-committee v0.1 and v0.2 feature boundaries

`model-committee` v0.1 must implement:

- parse `OPEN_QUESTIONS.md`;
- run consistency checks;
- rank answerable questions;
- generate Codex work prompts;
- launch Codex CLI work provider;
- run configured Ollama work models sequentially by priority;
- import and validate candidate work proposals;
- mechanically validate patches;
- generate Codex scoring prompts;
- launch Codex CLI scoring provider;
- select winning patch;
- write `selected.patch`, `commit_message.txt`, `review.md`, and logs;
- support fake provider mode for tests;
- include a `doctor` command for environment checks;
- include a `version` command.

`model-committee` v0.1 must not implement:

- direct OpenAI/Anthropic/Gemini API calls by `model-committee` itself;
- GitHub API;
- auto-merge;
- auto-push;
- automatic PR creation;
- adaptive model scoring;
- readiness score updates to `README.md`;
- derived `README.md`/`OUTREACH.md` consistency;
- automatic patch application;
- arbitrary network calls outside approved providers.

`model-committee` v0.2 must add:

- Claude Code CLI as a second frontier work and scoring provider;
- schema-native Claude output using `--json-schema` and `structured_output` parsing;
- Codex-to-Claude and Claude-to-Codex cross-scoring;
- score-matrix artifacts;
- disagreement flags in `review.md`;
- a Claude Code config block;
- updated quorum logic;
- `doctor` checks for Claude CLI availability and structured-output support;
- operator-run artifact-publication instructions for `../model-committee-artifacts`.

`model-committee` v0.2 must not add multi-turn Claude sessions, GitHub API integration, adaptive model weights, automatic artifact push, automatic patch application, or UbU planning-kernel work.

---

## Model-committee execution model

The v0.1 `model-committee` loop is **Codex-first and Ollama-secondary**.

1. Parse `OPEN_QUESTIONS.md`.
2. Run consistency checks.
3. Rank answerable questions.
4. Generate the Codex work prompt.
5. Launch the Codex CLI work provider.
6. Run configured local Ollama work models sequentially by priority.
7. Import and validate candidate work proposals.
8. Mechanically validate candidate patches.
9. Generate the Codex scoring prompt.
10. Launch the Codex CLI scoring provider.
11. Select the winning patch.
12. Write reviewable artifacts and logs.

Codex CLI is represented as the primary schema-constrained proposal and scoring provider.

Local Ollama models are secondary proposal providers. If Ollama responses finish within timeout and validate, they are included in Codex scoring. If an Ollama provider fails, the failure is logged and the run may continue if Codex produces at least one valid work proposal.

Codex scoring is required for automatic patch selection in v0.1.

In v0.2, the execution model becomes frontier cross-scoring. Codex and Claude Code may both produce work proposals. Codex scores Claude-authored proposals, and Claude Code scores Codex-authored proposals. A provider's self-score may be logged as diagnostic metadata but does not count as quorum evidence.

A valid automated v0.2 selection requires at least one valid work proposal, at least one valid cross-score from a different frontier provider, no hard validation failure on the selected patch, and no critical disagreement flag unless manually overridden outside automatic selection. Default human-review triggers are a frontier score gap of 25 or more points, selected score below 70, no valid frontier cross-score, or any selected patch validation failure.

---

## Codex and Claude Code provider behavior

`model-committee` v0.1 calls `codex exec` with schema-constrained output.

Runtime Codex calls:

- pass prompts through stdin;
- write final responses to JSON files;
- preserve JSONL event streams;
- preserve stderr output;
- always pass `--skip-git-repo-check`;
- do not use deprecated `--disable web_search` flags;
- do not directly modify canonical repo files.

If Codex web search must be disabled, that is handled through Codex configuration or profile state outside `model-committee`.

Codex produces JSON work proposals and score results. Patches are validated and selected by `model-committee`, then written as review artifacts.

Claude Code v0.2 provider calls should use schema-native structured output through `--json-schema`. When `--output-format json` and `--json-schema` are used, the schema-conforming payload should be parsed from `structured_output`. Claude tool authority should be explicitly restricted with no tools by default, or `--tools Read` only when file inspection is required; `--allowedTools` alone is not a sandbox boundary.

---

## Provider and network policy

`model-committee` v0.1 is a narrow local Python CLI.

It may communicate only with:

- local Ollama `base_url`;
- Codex CLI subprocesses.

v0.2 may also invoke the Claude Code CLI as an explicitly configured subprocess provider.

`model-committee` itself must not call:

- GitHub;
- OpenAI APIs directly;
- Anthropic APIs directly;
- Gemini APIs;
- arbitrary HTTP URLs.

`httpx` may be used only for the configured Ollama `base_url`. Cloud frontier providers are accessed through approved CLI subprocess boundaries rather than direct API calls by `model-committee`.

This provider policy preserves the bootstrap architecture and prevents accidental API creep while allowing explicitly configured provider CLIs to use their upstream authentication and billing.

---

## Question selection policy

`model-committee` uses answerability as the first gate.

A question is eligible for ordinary work only if:

- it has no dependencies;
- all dependencies are solved;
- or all dependencies are being answered in the same work item.

Blocked questions may still be selected for decomposition work if decomposition is expected to produce replacement questions with fewer, simpler, or no dependencies.

After answerability is established, questions are ranked by:

1. automation-likelihood score;
2. importance score;
3. risk score ascending.

---

## Question metadata format

`OPEN_QUESTIONS.md` may use single-line metadata.

The metadata fields always appear in the same order and use exact, case-sensitive labels:

```text
Status:
Priority:
Phase:
Decision type:
Auto-choice eligibility:
Importance score:
Automation-likelihood score:
Risk score:
Answerability score:
Depends on:
Blocks:
Resolved by:
Last scored:
Scored from commit:
```

Optional fields may appear after `Scored from commit:`:

```text
Supersedes:
Superseded by:
Decomposes:
Decomposed into:
```

Allowed sentinel values include:

- `TBD`
- `Never`
- `None`
- `Unresolved`

---

## Changeset-based work

`model-committee` work is changeset-based.

The implementation step should not be hidden inside VS Code or another opaque external editor agent. Candidate models produce explicit changesets, usually as patches. A scoring model evaluates those changesets.

The selected result is written as reviewable artifacts:

- `selected.patch`
- `commit_message.txt`
- `review.md`
- score-matrix artifacts in v0.2
- disagreement flags in v0.2
- run logs

VS Code or another editor may still be used for human review, but it is not part of the canonical committee loop.

`work-select` does not apply patches in v0.1 or v0.2. It writes review artifacts only. In v0.2, `review.md` also includes an operator-run final step for copying the run directory to `../model-committee-artifacts`, committing it with a signed commit, and pushing from that sibling artifact repository. The generated command is an instruction, not an automatic action.

---

## Prioritized recursive loop

`model-committee` is expected to evolve into a prioritized recursive loop:

1. **System-wide consistency check**
2. **Question/problem prioritization selection**
3. **Work**

Consistency has the highest priority because an inconsistent project state invalidates future planning.

Prioritization is second because the system must choose the next intended state transition.

Work is third because work should implement only a selected and justified transition. Work should not proceed against a known-inconsistent repo unless the selected work item is specifically to repair that inconsistency.

---

## Direct project directives

The project owner may append direct accepted decisions to `DECISIONS.md`.

These directive decisions are treated as canonical once committed.

Directive decisions are a “word of God” mechanism for project governance, but they remain explicit repo state rather than hidden chat context.

If a directive decision creates inconsistency, the next system-wide consistency check should detect it and convert the inconsistency into a report, question update, or work item.

---

## Decomposition and design-burden reduction

`model-committee` should not treat every increase in open-question count as failure.

A hard, ambiguous, or blocked question may be validly split into multiple simpler questions when the replacement questions are clearer, narrower, lower-risk, or easier to automatically answer.

This is especially valuable when a blocked question can be decomposed into replacement questions where at least one replacement question has fewer dependencies, simpler dependencies, or no dependencies.

The relevant metric is unresolved design burden, not merely raw open-question count.

---

## Development readiness

The current design baseline supports beginning implementation-first Phase 1 work while continuing `model-committee` dogfooding as an implementation-support and review-artifact workflow. Broad pre-MVP design automation is closed; remaining design questions should not block a slice unless they satisfy the `UBU-D0175` blocker-certificate standard.

The first development milestone should be:

- parse canonical design files;
- validate question metadata;
- validate question dependency DAGs;
- validate decision references;
- generate Codex, Claude Code, and Ollama work prompts where enabled;
- import structured model responses;
- mechanically validate patches;
- generate frontier scoring prompts;
- import scorer responses;
- cross-score frontier proposals when v0.2 providers are enabled;
- record score matrices and disagreement flags;
- write selected patch and review artifacts.

---

## Recommended `model-committee` v0.1/v0.2 stack

The first implementation should be intentionally boring, and the v0.2 extension should preserve that discipline.

Recommended stack:

- Python 3.12+
- `uv`
- `argparse`
- `pydantic`
- `httpx`
- `pytest`
- `ruff`
- custom Markdown parser for `OPEN_QUESTIONS.md`
- Codex CLI provider through subprocess
- Claude Code CLI provider through subprocess in v0.2
- local Ollama provider through configured `base_url`
- JSON Schema/Pydantic validation for provider outputs
- `git apply --check` for patch validation
- filesystem logs
- score-matrix and disagreement-flag artifacts in v0.2

---

## Contributing

This repository is currently a design repository, not the main implementation repository.

The project welcomes a small core cohort of serious, self-directed contributors. It does not need popularity for its own sake. It needs precise help that reduces design burden, improves dogfooding, and moves the project toward implementation.

Good contributions include:

- clarifying open questions;
- identifying contradictions in the canonical design files;
- proposing precise patches to `DESIGN.md`, `DECISIONS.md`, or `OPEN_QUESTIONS.md`;
- helping convert open questions into implementation-ready issues;
- reviewing whether Phase 1 scope is sufficiently frozen;
- providing real workflow examples from FOSS, Ethereum, protocol, research, or other autonomous-team contexts;
- helping define narrow `model-committee v0.1` and v0.2 implementation tasks.

The project prefers explicit patches over hidden discussion.

### Current contribution path

Useful contributor roles currently include:

1. **Design reviewer**

   Identify contradictions, underspecified concepts, ambiguous dependencies, or unclear scope boundaries.

2. **Workflow informant**

   Describe real FOSS or autonomous-team coordination failures that UbU should eventually model.

3. **Small patch contributor**

   Improve canonical design files or create implementation-ready issue descriptions.

4. **Early implementation contributor**

   Help maintain, test, and extend the `model-committee` bootstrap loop, including v0.2 Claude Code cross-scoring, as active dogfooding continues.

5. **Module owner**

   Take responsibility for a bounded subsystem after trust, alignment, and technical fit are established.

The best early contributions are narrow, reviewable, and explicit. The project prefers concrete patches, structured issue proposals, test fixtures, workflow examples, review of dogfooding artifacts, and sustained subsystem ownership over broad abstract discussion.

### First useful contribution areas

Useful early work includes:

- parser tests for `OPEN_QUESTIONS.md`;
- metadata validation fixtures;
- question dependency DAG validation;
- decision-reference validation;
- fake provider mode design;
- Codex prompt-template review;
- Claude Code prompt/schema integration;
- cross-scoring and disagreement-threshold tests;
- Ollama provider timeout and failure behavior;
- patch-validation tests;
- review-artifact format design;
- examples of GitHub issue/PR state that should become UbU WorkItems;
- examples of maintainer coordination failures that conventional tools fail to model.

### Scope boundaries for early contributors

UbU is a personal self-governance system first. Project-management functionality is a derivative dogfooding and coordination use case.

Team coordination should emerge through explicit Identities, commitments, capabilities, and bounded disclosure. Private human state should not become manager-visible telemetry.

In particular:

- `user_mode` may model intrinsic human affect;
- `organization_mode` should not model intrinsic affect;
- project-management views should receive selected coordination facts, not raw private state;
- GitHub should remain a projection of richer UbU state, not the canonical planning model;
- LLMs and automation workers should produce reviewable artifacts, not unreviewed canonical mutations;
- organizational introspection should generate evidence-backed review questions, not managerial surveillance or LLM-declared social truth.

### Post-ETHConf scaling note

If ETHConf or other outreach produces serious interest, new contributors should start through bounded paths:

- design review;
- workflow examples;
- test fixtures;
- implementation-ready issues;
- narrow patches;
- isolated `model-committee` components, including v0.2 provider and cross-scoring tests.

Major architectural changes should be proposed as explicit patches to canonical files, not as informal chat threads or private decisions.

If the contributor base grows, some material currently embedded in this `README.md` may later be extracted into dedicated files such as `CONTRIBUTING.md`, `ARCHITECTURE.md`, `ROADMAP.md`, or `GOOD_FIRST_ISSUES.md`.

Those files are not required yet.

---

## Repository map

- `README.md` - derived technical contributor entry point and project summary
- `DESIGN.md` - canonical design summary
- `DECISIONS.md` - accepted design decisions and anti-regression memory
- `OPEN_QUESTIONS.md` - unresolved questions, prioritization metadata, and automation queue
- `PLANNING_KERNEL_CONTRACT.md` - Phase 1 planning-kernel request/response contract, GPU stage boundaries, duration semantics, affect constraints, and correlation matrix rules
- `OUTREACH.md` - derived outreach document for FOSS maintainers and software engineers
- `PM_BRIEF.md` - derived brief for project leads and technical PMs
- `FUNDER_BRIEF.md` - derived brief for grantmakers, sponsors, and prototype funders
- `SOVEREIGN_COORDINATION.md` - derived brief for cypherpunks, privacy builders, and sovereign-coordination audiences
- `ORG_INTROSPECTION_BRIEF.md` - derived brief for mission-driven projects and organizational introspection
