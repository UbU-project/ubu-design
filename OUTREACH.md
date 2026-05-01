# UbU: A FOSS Self-Governance Engine for Reality-Aware Planning

UbU is a free and open-source software project for building the next generation of personal and collaborative planning tools. It is not merely a task manager, calendar app, habit tracker, project board, or AI assistant. UbU is an attempt to model planning as a living relationship between values, actions, constraints, uncertainty, and real-world consequences.

Most planning software asks a narrow question:

> What tasks do you want to do, and when?

UbU asks a deeper question:

> Given what you value, what state of the world are you trying to reach, what actions could move you there, what constraints govern those actions, and how well do your possible plans cover the futures you actually care about?

This makes UbU both a practical software project and an applied research project. It is intended for people who care about privacy, self-governance, FOSS infrastructure, local-first design, AI agents, stochastic planning, project management theory, and human-centered computing.

UbU is early. Its ontology is still evolving. That is exactly why this is the right time for serious FOSS developers, researchers, and technically minded contributors to get involved.

---

## Why UbU Exists

Modern productivity tools flatten human life into lists, due dates, events, and notifications. They help users remember obligations, but they do not model why those obligations matter, what dependencies they have, what state of the world they require, or whether completing them actually improves the user’s life.

A conventional task manager can tell you:

> Call Alex.

UbU should eventually be able to say:

> You say this relationship matters to you. Your history shows that long silences make reconnection harder, but short check-ins reliably improve the relationship. A low-friction check-in today preserves future relationship options at low emotional and time cost.

A conventional project board can tell a maintainer:

> Release Alpha is scheduled for June 1.

UbU should eventually be able to say:

> The June 1 release is only well-covered if the data model stabilizes this week and contributor review capacity remains available. The largest coverage risk is not implementation time; it is unresolved design uncertainty and maintainer fatigue. The highest-value next action is to resolve the WorkItem schema before adding new features.

That is the core difference. UbU does not merely track work. It tries to help users and teams govern themselves.

---

## Current Design Status

UbU is actively evolving. The project has moved from pure exploration to **structured decision-making**.

**Design status:**
- **55 architectural decisions** have been formally accepted (see `DECISIONS.md`)
- **30 open questions** remain, with clear MVP blockers identified (see `OPEN_QUESTIONS.md`)
- **Phase 1 MVP scope is not yet frozen**, but the core model is stable enough for implementation to begin

This is the ideal time to contribute. The design is concrete enough to review and critique, but flexible enough to incorporate fresh perspectives.

Recent accepted decisions include:
- User sovereignty as foundational
- Explicit value and planning constraints
- Privacy-first architecture
- Three mutually exclusive UbU modes (user/organization/worker)
- GitHub as a projection of UbU state, not the source of truth

---

## The Core Model

UbU begins with the idea that a user wants to move the world from one state to another.

An **Objective**—sometimes informally called a goal—is a desired state of the world. An Objective may be concrete, like “file my taxes,” or abstract, like “maintain a healthy relationship with my sibling,” “release UbU Alpha,” or “live according to my values.”

A **Technique** is a way to satisfy or complete an Objective. A Technique consists of **Steps**, which can be instantiated into concrete **Tasks**.

A **Task**—sometimes abstractly called a WorkItem—is an action or unit of work with explicit constraints. It may have dependencies, required preconditions, expected effects, duration distributions, cost distributions, affective impacts, resource requirements, privacy restrictions, identity boundaries, and resulting changes to the modeled state of the world.

A **Plan** is a possible ordered realization of Tasks. A **Log** is what actually happened. A **Calendar**, in the UbU sense, is not merely a Google-style event grid. It is a set of possible Plans and their realizations. A compact Calendar is a storage/transport representation of that possibility space. A Calendar can be evaluated by how much of its possibility space satisfies the Objective or constraints under consideration.

This gives UbU a powerful general planning structure:

```text
Objectives define desired states.
Techniques describe ways to reach them.
Tasks perform state transitions.
Plans order Tasks.
Calendars compactly represent possible realized Plans.
Logs record reality.
Feedback updates future modeling.
```

This structure can support ordinary personal planning, FOSS project management, relationship maintenance, health tracking, household logistics, software release planning, collaborative commitments, and AI-assisted automation.

---

## PERT as a Special Case of UbU Calendars

UbU has an important relationship to project management theory.

PERT was one of the early inspirations for UbU’s planning model. PERT’s central insight was that project schedules should not pretend the future is certain. Task durations are uncertain, dependencies matter, and a responsible planning system should represent completion as a distribution rather than a single date.

That insight remains correct. But UbU generalizes it.

A traditional PERT model can be represented as a simplified projection of a UbU Calendar:

```text
PERT activity        → UbU Task
PERT duration        → UbU duration PDF
PERT dependency      → UbU dependency / precondition subset
PERT project network → UbU Calendar projection
PERT completion date → UbU Calendar coverage query
```

In PERT, dependencies are often encoded implicitly through events and graph structure. In UbU, dependencies and preconditions are explicit. A Task can require not merely that another task has finished, but that the relevant state of the world exists.

For example, a Task might require:

```text
The design decision has been accepted.
The user has enough available energy.
The relevant identity has permission to act.
The privacy compartment allows export.
The collaborator has committed to review.
The external API token is valid.
The required relationship context is not in conflict.
```

PERT-style optimistic, likely, and pessimistic estimates are also only a low-information form of UbU’s probability model. UbU can support full mathematically continuous PDFs with parameters, provenance, confidence, and update rules. P10/P50/P90 estimates are not primitive planning concepts in UbU; they are derived summaries from richer distribution objects.

This means UbU can answer PERT-like questions:

> What is the probability this release completes by June 1?

But it can also ask much richer questions:

> What percentage of possible release plans preserve maintainer capacity?
>
> Which Task most improves Calendar coverage?
>
> Which dependency causes the largest failure mass?
>
> Which commitment destroys useful option value?
>
> Which public roadmap promise is unsafe given private project uncertainty?
>
> Which plan satisfies both external delivery and internal human constraints?

UbU does not discard PERT. It preserves PERT as a useful projection while embedding it in a more expressive model of reality.

---

## Why This Matters for Project Management Theory

Most project management tools still operate as if work is deterministic. Gantt charts, issue boards, kanban columns, and spreadsheets are useful visualizations, but they are usually weak models of reality. They often hide uncertainty, collapse disagreement, ignore affective cost, and treat deadlines as facts rather than claims about possible futures.

UbU is designed to support a richer project management model.

A serious project management system should represent:

```text
Uncertain duration
Uncertain cost
Uncertain quality
Uncertain contributor availability
Dependencies and preconditions
External events
Resource limits
Human energy and attention
Privacy constraints
Conflicting estimates
Option value
Decision timing
Actual-vs-predicted feedback
```

UbU can model these through explicit Tasks, Calendars, Logs, probability distributions, and coverage evaluation.

For small teams and FOSS projects, this is especially important. Large organizations often have internal planning, risk, finance, and forecasting machinery. Small teams usually have issue trackers, spreadsheets, chat rooms, and hope. UbU’s long-term opportunity is to bring richer planning theory to individuals and small teams without requiring enterprise infrastructure or centralized control.

That makes UbU relevant to several overlapping markets and research areas:

```text
FOSS project management
AI-assisted planning
local-first software
privacy-preserving personal data systems
stochastic project management
human-centered productivity
affective computing
self-hosted collaboration
agentic software workflows
decision-support systems
```

UbU’s project management ambitions are not limited to software projects. The same primitives can apply to household renovation, health routines, job searches, travel planning, relationship maintenance, research programs, and personal life design.

---

## UbU Runs UbU

UbU should dogfood itself aggressively.

The project’s own development should become one of the first serious test cases for UbU-style planning. Issues can become Tasks. Milestones can become Calendars. Design notes can become Objectives, Techniques, and open questions. Merged pull requests can become Logs. Contributor availability can become a resource constraint. Documentation gaps can become generated Tasks. Release plans can be evaluated for coverage rather than treated as fixed promises.

This is the “UbU runs UbU” principle.

It means the project should progressively use its own model to manage:

```text
roadmap design
issue triage
release planning
documentation gaps
contributor onboarding
project-support Objectives
maintainer capacity
dogfooding reports
design-decision records
risk and uncertainty
```

This is more than a slogan. It is a validity test.

If UbU cannot help manage UbU, then UbU has not yet become the system it claims to be. If UbU can manage UbU, then the project becomes a living demonstration of its own philosophy.

---

## AI Agents and SuperAutomation

UbU is designed for a world where AI agents can transform messy real-world data into structured, reviewable planning objects.

An AI agent should not replace the user’s values. It should help apply the user’s values to the world. UbU’s automation model should therefore distinguish between:

```text
What the user values
What the world currently appears to be
What actions could change the world
What constraints govern those actions
What risks and uncertainties exist
What the user has authorized the system to do
```

This creates the basis for **SuperAutomations**: user-authorized workflows that transform real-world inputs into structured UbU state.

Examples:

```text
Meal photo → nutrition estimate → health Measurement → user correction → future calibration
GitHub issue → Task → dependency graph → release Calendar
Email thread → obligation candidate → Objective or Task
Calendar history → relationship maintenance signal
Design conversation → architecture memo → implementation issues
Receipt photo → expense classification → financial log
```

SuperAutomations are not just scripts. They are structured pipelines from observation to interpretation to user-authorized state update.

For FOSS developers, this opens many contribution paths: connectors, local-first storage, LLM pipelines, schema design, privacy boundaries, review workflows, agent orchestration, UI, and formal planning semantics.

---

## Privacy and Identity

UbU’s model is privacy-first by necessity. The system may eventually reason over extremely sensitive data: calendars, messages, relationship histories, health logs, work habits, finances, affective diaries, and private project notes.

That means privacy cannot be added later.

UbU’s identity model treats people, accounts, roles, pseudonyms, institutions, and collaborators carefully. A human may have multiple identities. A relationship may involve different identities in different contexts. A project may expose public state while preserving private constraints. A user may want to disclose that a delay exists without disclosing the personal reason for the delay.

UbU’s compartment model should allow data to be segmented by context and policy:

```text
personal
family
health
financial
work
FOSS
pseudonymous
public
private project operations
```

A Task, Objective, Distribution, Measurement, or Log entry should carry information about what compartment it belongs to, where it may be processed, and whether it may be shared, exported, summarized, or used by agents.

This is essential for trust. UbU should never become a surveillance graph. It should help users govern their own data and actions.

---

## Why FOSS Developers Should Care

UbU is a large, ambitious project, but it has many approachable contribution surfaces.

Potential contributors can work on:

```text
Rust/TypeScript core systems
local-first data storage
task and calendar schemas
PDF/distribution modeling
GitHub integration
LLM agent pipelines
privacy compartments
UI prototypes
documentation
project management theory
relationship maintenance models
health and measurement automations
release-planning dogfooding
testing and simulation
```

The project is intellectually rich because it combines practical software engineering with deep modeling questions:

```text
What is a task?
What is a plan?
What is a commitment?
What does it mean for a plan to cover a desired future?
How should software represent uncertainty?
How should AI agents act without replacing user values?
How should private constraints affect public collaboration?
How can a FOSS project maintain itself without burning out contributors?
```

This is not a CRUD app with a productivity skin. It is an attempt to build self-governance infrastructure.

---

## Core Open Questions Blocking Phase 1

These four areas need design input before implementation can accelerate. If you want to influence UbU's direction, these are the highest-leverage contribution points:

### 1. **GitHub ↔ UbU Association Model**
How do many-to-many relationships between GitHub objects (Issues, PRs, reviews) and UbU objects (Objectives, Tasks) get represented and synchronized? This directly affects dogfooding.

**Relevant discussion:** `OPEN_QUESTIONS.md` #3

### 2. **Automation Worker Identity and Capabilities**
Worker-mode UbU instances need bounded authority. What capabilities can workers receive? How are they scoped and revoked? This enables scaling UbU's planning beyond a single person.

**Relevant discussion:** `OPEN_QUESTIONS.md` #7

### 3. **Worker Mutation Request Schema**
How do workers submit changes back to canonical UbU state safely? This needs a schema that prevents accidental overwrites, enables auditing, and supports retries.

**Relevant discussion:** `OPEN_QUESTIONS.md` #9

### 4. **Compact Calendar DFS Grammar**
The compact Calendar representation is crucial for recursive self-analysis and device sync. Should it use deterministic expansion or probability-seeded sampling? What is the grammar?

**Relevant discussion:** `OPEN_QUESTIONS.md` #16

If you have strong opinions on any of these, the project needs your input. These are not settled, and fresh perspectives are valuable.

---

## The Long-Term Vision

UbU’s long-term ideal is a system that helps users and teams move from values to action with increasing autonomy, without surrendering agency.

For individuals, UbU should help answer:

```text
What do I care about?
What am I neglecting?
What actions would improve my world?
What plans are realistic?
What patterns contradict my declared values?
What should I learn from what actually happened?
```

For teams, UbU should help answer:

```text
What are we trying to achieve?
What commitments have we made?
Where is uncertainty hiding?
Which dependencies matter most?
Which contributors are overloaded?
Which plans preserve useful options?
Which release promises are realistic?
What should we do next?
```

For the UbU project itself, UbU should help answer:

```text
What should UbU build next?
Which design questions block progress?
Which features best dogfood the model?
Where is maintainer effort being wasted?
What public contribution opportunities exist?
How can UbU become better at managing UbU?
```

That is the vision: a privacy-first, FOSS, AI-assisted self-governance engine that treats planning as reality-aware, value-aware, uncertainty-aware, and human-aware.

UbU is for people who believe software should not merely capture tasks.

It should help users govern their lives, projects, relationships, and communities with clarity, dignity, and agency.

---

## How to Contribute Now

You don't need to wait for a finished codebase. UbU needs contributors at every level:

### **Design & Modeling**
- Review and critique `DESIGN.md` and `DECISIONS.md`
- Propose solutions to open questions in `OPEN_QUESTIONS.md`
- Contribute domain expertise (project management, stochastic planning, privacy, LLMs)
- Sketch UI/UX concepts
- Write threat models for privacy architecture

### **Architecture & Planning**
- Help define Phase 1 MVP scope boundaries
- Design schemas for UniverseState mutations, Task preconditions, and Worker requests
- Model dogfooding workflows: how should UbU manage its own GitHub issues and releases?
- Prototype the compact Calendar representation

### **Coding (When Scope Freezes)**
- Rust/TypeScript core systems
- Local-first data storage and sync
- GitHub integration
- Planning algorithms and Calendar evaluation
- UI prototypes

### **FOSS & Community**
- Documentation and tutorials
- Help onboard new contributors
- Test proposals and report friction
- Connect UbU to adjacent projects (local-first tools, AI safety, project management theory)

**Start here:** Read `DESIGN.md` (full design), then `OPEN_QUESTIONS.md` (what needs debate). Join the conversation.

---

## Join Us

UbU is built in public. The design process is transparent. Your voice matters.

- **Read:** Start with `README.md` (overview), then `DESIGN.md` (full model), then `OPEN_QUESTIONS.md` (where you can contribute)
- **Discuss:** Open GitHub Issues to propose ideas, critique designs, or ask clarifying questions
- **Contribute:** Help resolve open questions, refine schemas, or prototype ideas
- **Follow:** This repository evolves frequently as decisions are made and feedback arrives

This is the right time to get involved in UbU. The foundation is solid enough to build on, but flexible enough to shape. Large design decisions remain open. Serious contributors can influence what UbU becomes.

UbU is for you if you believe software should help people govern themselves, not surveil them. If you think planning should model uncertainty, not hide it. If you want to build infrastructure that respects privacy, agency, and autonomy.

Welcome. We're building something real.

