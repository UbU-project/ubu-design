# UbU Outreach

**Status:** Derived public-facing outreach document  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`  
**Audience:** FOSS developers, project maintainers, Ethereum project leads, privacy engineers, automation builders, planning-tool researchers, independent technical consultants, prototype funders, and technically curious contributors

---

## Build software that helps humans govern their own time

UbU is a privacy-first planning, coordination, and self-governance system.

It is designed for people who are tired of tools that merely collect tasks, display calendars, summarize messages, or report status without understanding the deeper question:

> Given what matters, what constraints exist, what has changed, and what human limitations are real, what should happen next?

UbU aims to become a planning kernel for individuals and organizations.

It models Objectives, Tasks, Preferences, Plans, Calendars, Logs, UniverseState, external events, worker automation, privacy compartments, Identities, and human affect.

It turns messy real-world inputs into explicit, inspectable, recalculable plans.

The first MVP is intentionally practical:

> UbU should help coordinate the development of UbU itself.

Phase 1 also needs to feel like UbU to a nontechnical user: it should ask a few bootstrapping questions, use preference-calibration examples when helpful, preview the candidate Calendar, recommend one next action, explain why that action matters now, and learn from the user’s response through Log review.

That means using UbU to manage its own GitHub issues, open questions, pull requests, reviews, CI events, release milestones, design changes, contributor relationships, and automation loops.

UbU’s first proving ground is its own project.

---

## Why UbU matters

Most productivity systems fail because they treat the user like a machine.

They assume that if a task appears on a list or calendar, the user can simply execute it.

They rarely model:

- energy;
- stress;
- attention;
- boredom;
- emotional load;
- uncertainty;
- dependencies;
- external interruptions;
- changing reality;
- hidden coordination cost.

Project-management systems have a related failure mode.

They often represent status, assignment, and deadlines, but they do not model the full decision problem:

- What is the actual objective?
- What dependencies block the work?
- What external events changed the plan?
- What is the risk of missing a deadline?
- Which tasks are meaningful versus merely noisy?
- Which work should be deferred?
- Which work should be decomposed?
- Which automation can be trusted?
- Which decisions are canonical?
- Which claims are just projections into another system?

UbU is designed to make those things explicit.

---

## The core idea

UbU models planning as a state-transition problem.

A task is not merely a note. It is a proposed action that begins from some assumed state of the universe and, if successful, changes that state.

A plan is not merely a calendar layout. It is a possible ordered sequence of actions that should satisfy constraints, respect dependencies, and move the modeled universe toward desired Objectives.

A log is not merely history. It is the canonical record of what actually happened, allowing the system to compare prediction against reality and improve future planning.

This makes UbU naturally suited to recursive self-governance:

1. Check the current state for consistency.
2. Decide which problem or question is answerable and worth addressing next.
3. Perform work as an explicit state transition.
4. Record the result.
5. Re-check consistency.
6. Repeat.

That loop is central to the project.

---

## Privacy-first by design

UbU is not designed around a centralized service owning user data.

The long-term architecture emphasizes:

- local-first operation;
- user-controlled sync;
- explicit Zones;
- execution-enclave Devices;
- first-class Compartments;
- compartment-scoped references instead of careless data embedding;
- multiple Identities;
- bounded disclosure;
- user sovereignty.

Sensitive content should not leak merely because structural planning metadata is useful.

A WorkItem should remain structurally usable even when sensitive compartmented content cannot be dereferenced.

This matters because serious planning systems inevitably touch sensitive data:

- personal relationships;
- health-related affect;
- work obligations;
- financial priorities;
- private messages;
- calendars;
- organizational strategy.

UbU’s privacy model is not an afterthought. It is part of the planning model.

---

## Human-aware planning

UbU treats human limitations as real constraints.

In `user_mode`, affect belongs to UniverseState. Energy, tiredness, stress, mood, motivation, boredom, emotional load, recovery needs, and related signals are part of the planning problem.

This does not mean the system should constantly interrogate the user. Affect collection, Calendar preview, and Log review are themselves planned work. If affect information is missing or stale, UbU may create an Objective or Task to collect it.

Discovery mode is a user-selectable workflow state, not covert surveillance. The user can choose it at any time, especially from a mobile app, so sensors and quick notes can help later Log review reconstruct under-specified periods. UbU must treat those signals as evidence for reconciliation, not as final truth against the user.

The goal is not emotional surveillance.

The goal is self-governance.

Most planning systems are affect-blind: they model tasks, deadlines, statuses, and calendar blocks, but not the emotional and physical reality of the person who must execute the plan.

A system that ignores fatigue, boredom, stress, attention, dignity, and recovery is not helping a human plan. It is producing fiction.

UbU should give users fast feedback when plans succeed or fail, suggest improvement after failure, respect dignity and emotional limits, and still help users grow beyond current limitations.

---

## The first user experience

The first UbU experience should be easy to understand even for people who do not think like programmers.

UbU starts by asking a few questions:

- What are you trying to make better?
- What are you trying to maintain?
- What is currently urgent?
- What drains or restores your energy?
- What kind of work can you realistically do right now?
- What information may UbU use?

Then UbU previews the candidate Calendar, lets the user correct obvious mismatches, and shows one recommended next action, not a giant intimidating list.

Example:

> **Next action:** Review the inspection document for 20 minutes.  
> **Why this matters now:** It blocks tomorrow’s decision, fits your current energy, and reduces later stress.  
> **UbU considered:** deadline pressure, current mood, available time, related obligations, and privacy rules.

The full Plan remains inspectable, but the default experience is humane: regular preview, one meaningful next action, later Log review, and a reasoned model update when reality disagrees with the plan.

---

## Dogfooding: UbU runs UbU

The Phase 1 MVP is focused on single-user GitHub dogfooding.

UbU should help coordinate the UbU project itself by observing and modeling:

- GitHub issues;
- pull requests;
- review requests;
- CI events;
- comments;
- labels;
- milestones;
- design questions;
- release-readiness checks;
- contributor interactions;
- automation-worker outputs.

GitHub is treated as a projection of UbU state, not the source of truth.

UbU may write selected information back to GitHub through clearly marked managed labels, comments, or issue-body blocks.

Other GitHub edits are treated as external events.

This allows FOSS contributors to keep using normal GitHub workflows while UbU maintains a richer canonical model internally.


---

## Release Outreach Pipeline

UbU should make every release explain itself.

The Release Outreach Pipeline is a future feature bundle that treats public explanation as part of release management. A release should not only produce code, tests, changelogs, and deployment artifacts. It should also produce explanation artifacts for the people who need to understand what changed and what to do next.

For UbU itself, a minor release should eventually generate a release outreach package with:

- user-facing release notes;
- developer-facing release notes;
- screenshots from automated UI runs or approved fixtures;
- scripted demo recordings;
- short public video scripts;
- narration text and captions;
- YouTube titles, descriptions, and chapter outlines;
- known limitations;
- concrete contributor calls-to-action.

The first public videos should be fast and concrete. They should show the user-facing loop - bootstrap, preference calibration, Calendar preview, one next task, explanation, Discovery mode when useful, Log review, feedback, and humane prompts - then briefly show UbU dogfooding its own GitHub issues, design docs, release tasks, and contributor needs.

The developer ending should not be a boring tutorial. It should show that the project is early enough for serious contributors to shape the planning kernel, privacy model, UI, local-first architecture, dogfooding loop, release pipeline, and automation workers.

Release outreach should be evidence-bound and privacy-aware. Claims should trace to implemented features, accepted decisions, closed issues, release notes, screenshots, demo recordings, or explicitly labeled future plans. Publication should remain gated by human or configured project-policy approval.

---

## ETHConf 2026 feedback focus

UbU is seeking feedback from people who coordinate highly autonomous technical teams, especially in Ethereum, FOSS, protocol engineering, developer tooling, privacy engineering, and infrastructure projects.

The project is especially interested in speaking with:

- FOSS maintainers;
- protocol leads;
- engineering managers;
- technical founders;
- DevRel and ecosystem leads;
- grants and milestone coordinators;
- senior autonomous contributors;
- people responsible for release coordination, reviews, audits, or contributor onboarding.

The question is not merely whether another project-management tool would be useful.

The question is whether autonomous contributors need a self-governance layer that helps them privately model work, constraints, dependencies, commitments, fatigue, and priorities, then selectively disclose only the coordination facts the team needs.

Useful coordination facts may include:

- blockers;
- real commitments;
- review needs;
- dependency status;
- milestone risk;
- selected availability;
- need for a decision;
- need for escalation;
- risk that a plan has become fiction.

Private human state should not become team telemetry.

---

## Problems we are testing

UbU outreach is currently testing whether autonomous developer teams have recurring problems that conventional tools do not model well:

- real work state split across GitHub, chat, calendars, private notes, maintainer memory, CI, and informal commitments;
- unclear distinction between aspirational work and real commitments;
- blocked issues or PRs that are not clearly visible;
- overloaded maintainers who do not want surveillance;
- async messages that imply work but never become explicit tasks;
- contributors who need autonomy but teams that still need coordination;
- project status projections that drift away from reality;
- tools that track assignment and deadline state but not objective, dependency, risk, uncertainty, or human constraint state.

Feedback is most useful when it describes a real workflow, failure mode, or coordination breakdown.

A single precise example is more useful than broad enthusiasm.

---

## What we want to learn from interviews

Useful interview information includes:

- what role the person plays in coordination;
- where the team’s real operational state lives;
- which tools the team actually uses;
- what current tools fail to represent;
- what work falls through the cracks;
- how blocked work is discovered;
- how overload is detected;
- how real commitments are distinguished from hopeful plans;
- what contributors would refuse to disclose;
- what contributors would willingly disclose to protect autonomy;
- what first integration would make UbU worth trying;
- what would make the tool valuable enough to fund or adopt.

The best conversations produce one or more of:

- a repeated pain point;
- a concrete workflow;
- a design-partner lead;
- a contributor lead;
- a funding or career lead;
- a clear objection that improves the pitch;
- a precise reason why UbU should not target a given market.

---

## How to help after meeting us

After a conversation, useful next steps include:

1. Send an anonymized example of a coordination failure from your project.
2. Review the repository and identify one unclear or incorrect design claim.
3. Describe your team’s current tool stack and where real work state is lost.
4. Help convert a workflow pain point into a precise open question or implementation-ready issue.
5. Volunteer for a narrow `model-committee v0.1` implementation area.
6. Review whether the Phase 1 dogfooding scope is concrete enough.
7. Identify a FOSS, Ethereum, protocol, or research project that would be a useful design partner.
8. Suggest a privacy-preserving boundary between private planning state and public coordination state.

The best early help is specific.

A single workflow example, failing tool-stack pattern, or precise patch is more valuable than general agreement.

---


## Current outreach posture

UbU is no longer only a design vision.

The `model-committee` v0.1 baseline provides the first runnable bootstrap path for dogfooding UbU’s own design process.

The outreach goal is therefore changing from “explain the vision” to “convert aligned people into concrete next actions.”

Useful next actions include:

1. Review a `model-committee` run artifact.
2. Help improve the question-and-answer dogfooding loop.
3. Provide a real autonomous-team coordination failure.
4. Help define the first consultant/prototype-funder workflow.
5. Contribute to a narrow implementation issue.
6. Discuss serious ongoing contributor involvement.

---

## Who we most want to meet now

UbU is seeking a small core cohort of serious, self-directed contributors.

The project is especially interested in people who want to help build the trunk of UbU rather than a distracting branch.

Strong contributor candidates may be people who:

- understand why planning must be explicit and recalculable;
- are skeptical of opaque AI productivity tools;
- care about local-first and privacy-first software;
- can turn abstract design into practical systems;
- want software that respects human emotion without surrendering discipline;
- are willing to own a bounded subsystem over time.

There is not a single slot. Several serious contributors could meaningfully accelerate the project.

Another high-priority contact category is prototype funders or design partners from the independent knowledge-worker market.

A further high-priority contact category is maintainers or autonomous-team leads who can provide concrete coordination failure cases.

---

## Prototype-funder beachhead

UbU is exploring a first commercial beachhead among independent knowledge workers who manage complex private professional obligations.

Examples include:

- independent technical consultants;
- freelance developers;
- security researchers;
- solo founders;
- independent academics;
- technical writers;
- privacy-sensitive professional advisors.

These users often manage work across multiple clients, projects, deadlines, contexts, and confidentiality boundaries.

They are a strong fit for UbU because their professional work already requires personal self-governance. They need planning that respects commitments, dependencies, attention, fatigue, confidentiality, and context switching.

UbU should not chase funding that requires surveillance features, generic enterprise dashboards, or a pivot away from personal self-governance.

---

## Technical essay project

UbU should publish a problem-first technical essay explaining why conventional planning tools fail humans.

Working title:

> The Planning Kernel: What Task Managers Leave Out

Core claim:

List, calendar, board, and opaque assistant tools are useful projections, but they are not enough for real planning unless objectives, state transitions, dependencies, constraints, logs, uncertainty, affect, and recalculation are explicit.

A humane planner must provide fast feedback from reality, suggest improvements after failure, respect dignity and emotional limits, and still help the user grow beyond current limitations.

The essay should argue that real planning requires explicit Objectives, state transitions, dependencies, constraints, logs, uncertainty, affect, and recalculation.

The essay should also explain why LLMs are useful but should remain advisory rather than canonical: they can interpret and suggest, but the planning model must remain inspectable.

The essay should point to `model-committee` as UbU’s first visible dogfooding loop and invite concrete participation.

---

## Model-committee: the bootstrap automation project

Before the main UbU MVP is implemented, the project is using a bootstrap automation tool called `model-committee`.

`model-committee v0.1` is the first runnable early dogfooding system. It helps the project use LLMs and local automation to resolve design questions, propose changesets, score candidate patches, and move toward implementation.

It is not the canonical decision engine.

Accepted design state exists only when committed to the canonical repository.

The v0.1 loop is deliberately constrained:

1. Parse `OPEN_QUESTIONS.md`.
2. Run consistency checks.
3. Rank answerable questions.
4. Generate a Codex work prompt.
5. Launch the Codex CLI work provider.
6. Run configured local Ollama proposal models sequentially by priority.
7. Import and validate candidate work proposals.
8. Mechanically validate patches.
9. Generate a Codex scoring prompt.
10. Launch the Codex CLI scoring provider.
11. Select a winning patch.
12. Write `selected.patch`, `commit_message.txt`, `review.md`, and logs.

This keeps the process auditable.

The work phase is changeset-based. It should not hide implementation inside VS Code, an editor agent, or undocumented human magic.

Models produce concrete changesets. A scorer evaluates them. The selected result becomes a reviewable artifact.

That same loop can later generalize from design-doc patches to code changes, bug fixes, tests, refactors, release checks, and issue triage.

---

## Codex-first, Ollama-secondary automation

`model-committee v0.1` is Codex-first and Ollama-secondary.

Codex CLI is the primary schema-constrained provider for:

- work proposal generation;
- work scoring.

Local Ollama models are secondary proposal providers.

They provide local diversity, dissent, fallback, and offline review.

If Ollama responses finish within timeout and validate, they are included in Codex scoring.

If an Ollama provider fails, the failure is logged and the run may continue if Codex produces at least one valid work proposal.

Codex scoring is required for automatic patch selection in v0.1.

Codex is not allowed to directly mutate canonical repo files in v0.1. It produces JSON work proposals and score results. Patches are validated and selected by `model-committee`, then written as review artifacts.

---

## Bounded automation, not runaway agents

`model-committee v0.1` is intentionally narrow.

It must not implement:

- direct OpenAI, Anthropic, or Gemini API calls;
- GitHub API calls;
- automatic patch application;
- auto-merge;
- auto-push;
- automatic pull request creation;
- adaptive model scoring;
- readiness-score updates to `README.md`;
- derived `README.md` or `OUTREACH.md` consistency updates;
- arbitrary network calls outside approved providers.

The tool may communicate only with:

- local Ollama `base_url`;
- Codex CLI subprocesses.

This constraint matters.

UbU’s automation should remain explicit, inspectable, and bounded.

The goal is not an uncontrolled agent that mutates the project.

The goal is a reviewable state-transition system.

---

## The prioritized recursive loop

UbU’s self-automation model is organized around three priorities:

1. **System-wide consistency check**
2. **Question/problem prioritization selection**
3. **Work**

Consistency comes first because an inconsistent project state invalidates future planning.

Prioritization comes second because the system must choose the next intended state transition.

Work comes third because work should implement only a selected and justified transition.

This principle is important.

The system should not blindly generate more work. It should first understand whether the current state is coherent, then decide what is answerable and worth doing, then perform the chosen work.

This is the project’s own philosophy applied to its development process.

---

## Question decomposition and automation

UbU does not treat every increase in open questions as failure.

Sometimes a hard question should not be answered directly. It should be decomposed.

A question blocked by unresolved dependencies may be split into several smaller questions if at least one new question has fewer dependencies, simpler dependencies, or no dependencies.

The relevant metric is not raw question count.

The relevant metric is unresolved design burden.

A good decomposition makes future work easier, clearer, less risky, or more automatable.

A bad decomposition creates more vague, coupled, or harder questions.

This distinction matters because UbU aims to automate not just task execution, but also the process of improving its own planning model.

---

## Why FOSS developers should care

FOSS development is full of hidden coordination costs.

Maintainers must juggle:

- issue triage;
- design decisions;
- release planning;
- CI failures;
- pull request review;
- contributor onboarding;
- roadmap drift;
- stale discussions;
- duplicated issues;
- ambiguous priorities;
- burnout risk;
- under-documented decisions;
- project governance.

Most projects rely on a mixture of GitHub issues, chat threads, ad hoc documents, maintainer memory, and personal judgment.

UbU wants to make that coordination explicit.

For FOSS projects, UbU can eventually help answer:

- Which issues are actually blocked?
- Which issues are underspecified?
- Which design decisions are already settled?
- Which open questions are answerable now?
- Which work is high-value but low-risk?
- Which PRs are waiting on review?
- Which contributors need responses?
- Which project claims are stale?
- Which release blockers are real?
- Which tasks are merely noise?
- Which automation can safely proceed?

That is directly useful to maintainers.

It is also a strong first use case because the UbU project can dogfood every part of the process in public.

---

## ETHConf and autonomous-team relevance

Ethereum and FOSS teams are useful early feedback sources because many of them are:

- remote or distributed;
- async-heavy;
- autonomy-heavy;
- GitHub-heavy;
- contributor-driven;
- cross-organizational;
- dependent on informal commitments;
- sensitive to surveillance and centralization;
- forced to coordinate across chats, governance forums, code review, audits, releases, and calendars.

That makes them a strong test case for UbU’s professional coordination thesis.

The goal is not to convert UbU into a conventional project-management product.

The goal is to learn whether self-governance primitives can improve the work lives of autonomous contributors while also making project coordination more truthful.

---

## What makes UbU different

UbU is not trying to be another task manager.

UbU combines several ideas that are usually separate:

- explicit objective modeling;
- preference-derived value;
- task preconditions and effects;
- UniverseState simulation;
- log-based feedback;
- affect-aware planning;
- privacy compartments;
- identity-mediated coordination;
- worker-mode automation;
- GitHub dogfooding;
- LLM-assisted but non-LLM-canonical planning;
- recursive project self-governance.

This combination is the point.

A task manager records things you might do.

A calendar shows where time might go.

A project board shows workflow state.

UbU aims to model why work matters, what it depends on, what state it changes, how it interacts with human constraints, and when the plan should be recalculated.

---

## Current development status

The project is currently preparing to move from design documentation into bootstrap automation and then MVP implementation.

The canonical design files are:

- `DESIGN.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`

Derived public-facing files include:

- `README.md`
- `OUTREACH.md`

The current immediate implementation target is `model-committee v0.1`.

The first practical development milestone is to build a Python CLI that can:

- parse canonical design files;
- validate question metadata;
- validate question dependency graphs;
- validate decision references;
- generate Codex and Ollama prompts;
- import structured model responses;
- mechanically validate patches;
- run Codex scoring;
- select a patch;
- write reviewable artifacts and logs.

---

## Where contributors can help

Contributors can help immediately by working on:

- `model-committee` parser design;
- single-line `OPEN_QUESTIONS.md` metadata parsing;
- consistency checks;
- dependency-DAG validation;
- decision-reference validation;
- prompt template design;
- JSON Schema validation;
- Pydantic model validation;
- Codex CLI provider integration;
- Ollama integration;
- fake provider mode;
- `doctor` command implementation;
- patch extraction and validation;
- filesystem log layout;
- test fixtures;
- review workflow;
- Phase 1 MVP scope freeze.

Later contributors will be needed for:

- GitHub ingestion and projection;
- Objective/Task/UniverseState data model implementation;
- planner algorithms;
- compact Calendar representation;
- risk reports;
- local-first sync;
- worker-mode execution;
- privacy compartments;
- UI/UX;
- Release Outreach Pipeline artifact schemas and review gates;
- automated screenshot and demo-flow capture;
- release engineering.

---

## Contributor ladder

UbU should scale carefully.

Early contributors should enter through bounded contribution paths:

1. **Workflow informant**

   Describe real coordination pain, tool-stack fragmentation, maintainer overload, or autonomous-team failure modes.

2. **Design reviewer**

   Identify contradictions, missing definitions, unclear Phase 1 scope, or risky assumptions.

3. **Small patch contributor**

   Propose precise changes to canonical design files or derived public-facing files.

4. **Implementation contributor**

   Help build isolated `model-committee v0.1` components.

5. **Module owner**

   Take responsibility for a bounded subsystem after trust, alignment, and technical fit are established.

This project should not grow faster than its architecture, privacy model, and governance process can absorb.

The project prefers concrete patches, structured issue proposals, test fixtures, and workflow examples over broad abstract discussion.

---

## First small tasks

Useful early tasks include:

- create parser fixtures for `OPEN_QUESTIONS.md`;
- test single-line question metadata parsing;
- test allowed sentinel values such as `TBD`, `Never`, `None`, and `Unresolved`;
- test question dependency DAG validation;
- test cycle detection;
- test decision-reference validation;
- design fake provider mode for deterministic tests;
- draft Codex work prompt templates;
- draft Codex scoring prompt templates;
- define Ollama provider timeout behavior;
- define provider-failure log formats;
- test `git apply --check` patch validation;
- define review-artifact directory layout;
- create example GitHub issue data that should become UbU WorkItems;
- create example PR-review queues that should become UbU planning inputs;
- document one real maintainer coordination failure that conventional tools failed to model;
- draft a fixture-backed release outreach package for a minor UbU release;
- define screenshot and demo-capture provenance metadata for the Release Outreach Pipeline.

These tasks are intentionally small.

Small, correct, reviewable work is more valuable than sweeping architectural enthusiasm.

---

## Technical direction for `model-committee`

The first `model-committee` implementation should be intentionally boring.

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
- local Ollama provider through configured `base_url`
- `git apply --check` for patch validation
- filesystem logs

The v0.1 implementation should not include:

- direct OpenAI, Anthropic, or Gemini APIs;
- GitHub API;
- automatic PR creation;
- auto-push;
- auto-merge;
- adaptive model scoring;
- derived `README.md` or `OUTREACH.md` consistency updates;
- readiness score updates to `README.md`;
- automatic patch application.

The goal is to get a small, auditable loop working first.

---

## Post-ETHConf scaling plan

If ETHConf or other outreach produces serious interest, the project should convert that interest into bounded artifacts:

- follow-up interviews;
- anonymized workflow examples;
- design-review comments;
- implementation-ready issues;
- test fixtures;
- small patches;
- isolated `model-committee v0.1` tasks.

The project should not convert interest directly into unstructured community growth.

A larger community is useful only if it reduces unresolved design burden, increases implementation velocity, or improves the self-governance model.

Good post-ETHConf outcomes include:

- repeated pain points from multiple teams;
- concrete examples of fragmented work state;
- clear disclosure-boundary preferences;
- a ranked first wedge for the PM-facing use case;
- one or more design partners;
- one or more serious implementation contributors;
- one or more possible funding or career paths compatible with UbU’s self-governance mission.

Bad post-ETHConf outcomes include:

- vague praise without follow-up;
- popularity without contributors;
- requests for surveillance dashboards;
- token-first proposals;
- pressure to become a generic PM clone;
- architecture debates that do not reduce design burden.

---

## Non-negotiable project boundaries

UbU’s project-management use case must remain subordinate to the self-governance mission.

UbU should not become:

- manager-first surveillance software;
- a productivity-scoring system for employees;
- a generic task-board clone;
- a centralized data trap;
- an opaque agent that mutates canonical state without review;
- a popularity-driven project that loses its self-governance core.

The professional and FOSS use cases are valuable when they help build the same primitives required by the personal self-governance product:

- Objectives;
- Preferences;
- WorkItems;
- Plans;
- Logs;
- UniverseState;
- Identities;
- Compartments;
- bounded disclosure;
- recalculable planning.

Professional opportunity is compatible with UbU only if it funds or accelerates the trunk of the project, not a distracting branch.

---


## Why this project may matter

UbU comes from a long-running attempt to solve a difficult problem: how software can help a person govern their own life without reducing them to tasks, metrics, reminders, or manager-visible productivity signals.

The idea has become more practical because modern LLMs can help interpret messy human context, while explicit planning logic can keep decisions inspectable and recalculable.

That combination creates a new opening.

UbU is not claiming inevitability. It is claiming that the time may finally be right to build a humane planning kernel: one that respects privacy, emotion, ambition, failure, learning, and growth.

For the right contributors, this is a chance to work on software that could matter for a long time.

---

## Why join now?

UbU is at the transition point where the design is coherent enough to begin implementation, but early enough that contributors can meaningfully shape the architecture.

This is a good project for developers interested in:

- privacy-first software;
- local-first systems;
- planning algorithms;
- AI-assisted development;
- LLM orchestration;
- FOSS governance;
- project-management theory;
- self-hosted automation;
- human-centered computing;
- applied software architecture;
- tools that help users govern themselves rather than manipulate them.

UbU is ambitious, but the immediate next step is modest:

> Build the bootstrap tool that helps the project finish becoming buildable.

That is the first practical path toward UbU running UbU.

---

## Project stance

UbU should empower users.

It should not trap them in a platform, hide decisions inside opaque AI behavior, centralize their private data, or pretend humans are machines.

The project’s long-term goal is self-governance: software that helps people and groups understand their constraints, choose their actions, and revise their plans when reality changes.

That starts with UbU learning to govern its own development.
