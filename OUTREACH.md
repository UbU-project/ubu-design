# UbU Outreach

**Status:** Derived public-facing outreach document  
**Source of truth:** `DESIGN.md`, `DECISIONS.md`, and `OPEN_QUESTIONS.md`  
**Audience:** FOSS developers, project maintainers, planning-tool researchers, privacy engineers, and automation builders

---

## Build software that helps humans govern their own time

UbU is a privacy-first planning, coordination, and self-governance system.

It is designed for people who are tired of tools that merely collect tasks, display calendars, or summarize messages without understanding the deeper question:

> Given what matters, what constraints exist, what has changed, and what human limitations are real, what should happen next?

UbU aims to become a planning kernel for individuals and organizations. It models Objectives, Tasks, Preferences, Plans, Calendars, Logs, UniverseState, external events, worker automation, privacy compartments, and human affect. It turns messy real-world inputs into explicit, inspectable, recalculable plans.

The first MVP is intentionally practical: UbU should help coordinate the development of UbU itself.

That means using UbU to manage its own GitHub issues, open questions, pull requests, reviews, CI events, release milestones, design changes, contributor relationships, and automation loops.

UbU’s first proving ground is its own project.

---

## Why UbU matters

Most productivity systems fail because they treat the user like a machine.

They assume that if a task appears on a list or calendar, the user can simply execute it. They rarely model energy, stress, attention, boredom, emotional load, uncertainty, dependencies, external interruptions, or changing reality.

Project-management systems have a related failure mode. They often represent status, assignment, and deadlines, but they do not model the full decision problem:

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

This matters because serious planning systems inevitably touch sensitive data: personal relationships, health-related affect, work obligations, financial priorities, private messages, calendars, and organizational strategy.

UbU’s privacy model is not an afterthought. It is part of the planning model.

---

## Human-aware planning

UbU treats human limitations as real constraints.

In `user_mode`, affect belongs to UniverseState. Energy, tiredness, stress, mood, and related signals are part of the planning problem.

This does not mean the system should constantly interrogate the user. Affect collection is itself modeled as planned work. If affect information is missing or stale, UbU may create an Objective or Task to collect it.

The goal is not emotional surveillance. The goal is self-governance.

A system that ignores fatigue, boredom, stress, and attention is not helping a human plan. It is producing fiction.

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

UbU may write selected information back to GitHub through clearly marked managed labels, comments, or issue-body blocks. Other GitHub edits are treated as external events.

This allows FOSS contributors to keep using normal GitHub workflows while UbU maintains a richer canonical model internally.

---

## Model-committee: the bootstrap automation project

Before the main UbU MVP is implemented, the project is preparing a bootstrap automation tool called `model-committee`.

`model-committee` is an early dogfooding system. It helps the project use LLMs and local automation to resolve design questions, propose changesets, and move toward implementation.

It is not the canonical decision engine. Accepted design state exists only when committed to the canonical repository.

The v0.1 loop is deliberately constrained:

1. Parse `OPEN_QUESTIONS.md`.
2. Run consistency checks.
3. Rank answerable questions.
4. Generate a ChatGPT work prompt.
5. Launch an external ChatGPT browser workflow.
6. Run configured local Ollama models.
7. Import and validate candidate work proposals.
8. Mechanically validate patches.
9. Generate a ChatGPT scoring prompt.
10. Launch the external ChatGPT scorer workflow.
11. Select a winning patch.
12. Write `selected.patch`, `commit_message.txt`, `review.md`, and logs.

This keeps the process auditable.

The work phase is changeset-based. It should not hide implementation inside VS Code, an editor agent, or undocumented human magic. Models produce concrete changesets. A scorer evaluates them. The selected result becomes a reviewable artifact.

That same loop can later generalize from design-doc patches to code changes, bug fixes, tests, refactors, release checks, and issue triage.

---

## The prioritized recursive loop

UbU’s self-automation model is organized around three priorities:

1. **System-wide consistency check**
2. **Question/problem prioritization selection**
3. **Work**

Consistency comes first because an inconsistent project state invalidates future planning.

Prioritization comes second because the system must choose the next intended state transition.

Work comes third because work should implement only a selected and justified transition.

This principle is important. The system should not blindly generate more work. It should first understand whether the current state is coherent, then decide what is answerable and worth doing, then perform the chosen work.

This is the project’s own philosophy applied to its development process.

---

## Question decomposition and automation

UbU does not treat every increase in open questions as failure.

Sometimes a hard question should not be answered directly. It should be decomposed.

A question blocked by unresolved dependencies may be split into several smaller questions if at least one new question has fewer dependencies, simpler dependencies, or no dependencies.

The relevant metric is not raw question count. The relevant metric is unresolved design burden.

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
- generate ChatGPT and Ollama prompts;
- import structured model responses;
- mechanically validate patches;
- run a scoring prompt;
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
- JSON schema validation;
- Ollama integration;
- external-process provider integration;
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
- release engineering.

---

## Technical direction for `model-committee`

The first `model-committee` implementation should be intentionally boring.

Recommended stack:

- Python 3.12+
- `uv`
- `typer`
- `pydantic`
- `pytest`
- `ruff`
- custom Markdown parser for `OPEN_QUESTIONS.md`
- external-process ChatGPT provider
- local Ollama provider
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
- readiness score updates to `README.md`.

The goal is to get a small, auditable loop working first.

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

UbU is ambitious, but the immediate next step is modest: build the bootstrap tool that helps the project finish becoming buildable.

---

## Project stance

UbU should empower users.

It should not trap them in a platform, hide decisions inside opaque AI behavior, centralize their private data, or pretend humans are machines.

The project’s long-term goal is self-governance: software that helps people and groups understand their constraints, choose their actions, and revise their plans when reality changes.

That starts with UbU learning to govern its own development.