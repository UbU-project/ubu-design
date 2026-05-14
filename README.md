# UbU

**Status:** Active pre-MVP dogfooding / contributor and prototype-funder discovery  
**Repository:** `ubu-design`  
**Primary purpose:** Canonical public design state for the UbU project

---

## What is UbU?

**UbU** is a privacy-first planning, coordination, and self-governance system.

UbU is intended to convert messy real-world inputs - tasks, calendar events, messages, external events, user preferences, physical and affective state, GitHub/project data, and integration data - into explicit, inspectable, recalculable plans.

UbU is not merely a task list, calendar application, or project-management dashboard. It is intended to become a planning kernel for individuals and organizations: a system that models desired outcomes, constraints, risks, dependencies, available time, and human limitations, then helps determine what should happen next.

The first MVP is designed around **dogfooding**: using UbU to coordinate the design, development, release, and maintenance of UbU itself.

---

## Core philosophy

UbU is based on several design principles:

1. **User sovereignty**

   The user is the final authority over what the user wants and what occurred.

2. **Explicit value**

   Value is attached to Objectives through user-defined Preferences. Numeric utilities may be derived for planning, but they are transient computational artifacts, not canonical user values.

3. **Explicit planning**

   Planning must remain explicit and constraint-based. LLMs may assist, but canonical planning and decision logic must remain inspectable and recalculable outside the LLM.

4. **Privacy-first architecture**

   UbU is designed around local-first operation, compartmentalized data, multiple Identities, and user-controlled sharing.

5. **Affect-aware planning**

   In `user_mode`, human affective state is part of the planning problem. Energy, stress, tiredness, mood, and related human limitations are constraints that planning must respect.

6. **Dogfooding**

   The Phase 1 MVP should help coordinate UbU’s own GitHub issues, pull requests, reviews, CI events, release milestones, design questions, and contributor interactions.

---

## Canonical design files

The canonical public design state is maintained in:

- [`DESIGN.md`](DESIGN.md)
- [`DECISIONS.md`](DECISIONS.md)
- [`OPEN_QUESTIONS.md`](OPEN_QUESTIONS.md)

Derived public-facing projection files, such as `README.md` and `OUTREACH.md`, should summarize the canonical design state but are not themselves design authority.

When derived files conflict with canonical files, the canonical files win.

---

## Current project status

UbU is currently in **active pre-MVP dogfooding**.

The design has reached the point where additional broad philosophical elaboration has diminishing returns unless it directly supports implementation, recruitment, dogfooding, or market discovery.

The `model-committee` v0.1 baseline is now the first runnable bootstrap artifact for using model-assisted review to process UbU design questions and generate reviewable changesets.

The Phase 1 MVP scope is not yet fully frozen.

The current operational target is:

> Use `model-committee` and related dogfooding artifacts to help UbU coordinate the development of UbU itself.

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
- emotionally humane productivity tools.

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

## Human-complete planning

UbU treats affect as a core part of planning, not a decorative wellness feature.

A plan that ignores fatigue, stress, boredom, motivation, emotional load, recovery, and dignity is not merely incomplete. It may become actively misleading.

UbU should help users receive fast feedback about whether a plan is working, revise plans when reality disagrees, and grow beyond current limits without treating themselves like machines.

The goal is neither comfort-maximization nor coercive productivity. The goal is humane self-governance: disciplined action that respects the user’s emotional and physical reality.

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

Multiple humans coordinate through explicit Identities, capabilities, limited disclosure, and commitments.

Phase 3 should enable coordination without surveillance or shared global truth.

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
- Identity
- Relationship
- Zone
- Compartment
- Automation Worker
- External Event
- External Association

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

## GitHub dogfooding

For dogfooding, GitHub is treated as a low-dimensional projection of canonical UbU state.

UbU is the source of truth. GitHub Issues, PRs, comments, labels, reviews, CI, and milestones must be interpreted into UbU objects and events.

UbU may project selected state back into GitHub through clearly marked managed labels, comments, or body blocks. Other GitHub edits are treated as external events by default.

Missed GitHub updates are expected in MVP, so reconciliation is a first-class concern.

---

## Model-committee bootstrap project

`model-committee` is the first runnable bootstrap automation project for active pre-MVP UbU dogfooding.

The project is an early example of UbU dogfooding: UbU uses an automation loop to help coordinate its own design and development through reviewable run artifacts and changesets.

`model-committee` is not the canonical decision engine. It is an advisory Automation Worker pattern that reads canonical repo state, identifies open questions, generates candidate changesets, scores those changesets, and writes reviewable artifacts.

Accepted design state exists only when committed to the canonical repo.

---

## Model-committee v0.1 feature boundary

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

- direct OpenAI/Anthropic/Gemini API calls;
- GitHub API;
- auto-merge;
- auto-push;
- automatic PR creation;
- adaptive model scoring;
- readiness score updates to `README.md`;
- derived `README.md`/`OUTREACH.md` consistency;
- automatic patch application;
- arbitrary network calls outside approved providers.

---

## Model-committee execution model

The early `model-committee` loop is **Codex-first and Ollama-secondary**.

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

---

## Codex provider behavior

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

---

## v0.1 provider and network policy

`model-committee` v0.1 is a narrow local Python CLI.

It may communicate only with:

- local Ollama `base_url`;
- Codex CLI subprocesses.

It must not call:

- GitHub;
- OpenAI APIs directly;
- Anthropic APIs;
- Gemini APIs;
- arbitrary HTTP URLs.

`httpx` may be used only for the configured Ollama `base_url`. Codex must be invoked only through subprocess.

This no-network policy preserves the bootstrap architecture and prevents accidental API creep.

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
- run logs

VS Code or another editor may still be used for human review, but it is not part of the canonical committee loop.

`work-select` does not apply patches in v0.1. It writes review artifacts only.

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

The current design baseline supports continuing `model-committee` dogfooding and preparing the Phase 1 implementation path.

The first development milestone should be:

- parse canonical design files;
- validate question metadata;
- validate question dependency DAGs;
- validate decision references;
- generate Codex and Ollama work prompts;
- import structured model responses;
- mechanically validate patches;
- generate Codex scoring prompt;
- import scorer response;
- write selected patch and review artifacts.

---

## Recommended `model-committee` v0.1 stack

The first implementation should be intentionally boring.

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
- helping define narrow `model-committee v0.1` implementation tasks.

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

   Help maintain, test, and extend the `model-committee v0.1` bootstrap loop as active dogfooding continues.

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
- LLMs and automation workers should produce reviewable artifacts, not unreviewed canonical mutations.

### Post-ETHConf scaling note

If ETHConf or other outreach produces serious interest, new contributors should start through bounded paths:

- design review;
- workflow examples;
- test fixtures;
- implementation-ready issues;
- narrow patches;
- isolated `model-committee v0.1` components.

Major architectural changes should be proposed as explicit patches to canonical files, not as informal chat threads or private decisions.

If the contributor base grows, some material currently embedded in this `README.md` may later be extracted into dedicated files such as `CONTRIBUTING.md`, `ARCHITECTURE.md`, `ROADMAP.md`, or `GOOD_FIRST_ISSUES.md`.

Those files are not required yet.

---

## Repository map

- `README.md` - derived public-facing project summary
- `DESIGN.md` - canonical design summary
- `DECISIONS.md` - accepted design decisions and anti-regression memory
- `OPEN_QUESTIONS.md` - unresolved questions, prioritization metadata, and automation queue
- `OUTREACH.md` - derived public-facing outreach and recruiting document
