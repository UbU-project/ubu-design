# UbU Design

Public design notes, decisions, and open questions for the **UbU** project.

UbU is a privacy-first planning and coordination system intended to help people and organizations convert messy real-world inputs—tasks, calendar events, messages, external events, constraints, preferences, and affective state—into explicit, recalculable plans.

UbU is being designed as a local-first, user-sovereign alternative to conventional productivity and project-management tools. Its goal is not merely to store tasks, but to model what the user wants, what constraints exist, what risks threaten those outcomes, and what plan should be followed next.

This repository is the public design workspace for UbU.

---

## Project status

UbU is in the **pre-MVP design stage** with active scope definition underway.

Phase 1 MVP scope is **not yet frozen**. The current focus is to define a small enough data model and implementation scope to begin building a working MVP, while preserving compatibility with the project’s long-term architecture.

The first MVP target is **dogfooding**: using UbU to coordinate UbU’s own design, development, release, and maintenance.

---

## Core idea

UbU treats planning as an explicit model of possible futures.

A user has Objectives. Objectives have user-defined value. Tasks and other WorkItems affect the state of the world. Plans arrange Tasks over time while respecting constraints. A Calendar is a set of possible Plans. As time passes, one possible Plan is realized into history, while others expire or become irrelevant.

UbU’s planning logic should remain explicit and recalculable outside of LLMs.

LLMs may assist with interpretation, structuring, candidate suggestions, screenshots, external-system workflows, and advisory analysis, but they are not the canonical decision engine.

---

## MVP release phases

The current MVP is expected to proceed in three phases:

### Phase 1: Single-user GitHub dogfooding

A single user uses UbU to coordinate work on UbU itself.

Initial integrations focus on GitHub issues, pull requests, reviews, CI events, milestones, and project-maintenance work.

GitHub is treated as a projection of UbU state, not the canonical source of truth.

### Phase 2: Single-user multi-device synchronization

A single user runs UbU across multiple devices or execution enclaves.

This phase validates local-first synchronization, partial replication, device roles, and Zone/Compartment boundaries.

A useful design rubric is:

> Phase 2 should feel like multi-agent coordination, but all agents happen to agree.

### Phase 3: Minimal multi-user / Identity coordination

Multiple users coordinate through explicit Identities, capabilities, commitments, and limited disclosure.

The goal is coordination without requiring surveillance, shared global truth, or centralized ownership of user data.

---

## Major design themes

### Self-governance

UbU is designed to help users govern their own time, attention, commitments, and constraints.

The user remains the final authority over what they want and what occurred.

### Explicit value

Value is not hidden inside prompts or inferred silently by an AI model.

UbU represents value explicitly through Objectives and user-defined Preference relations. Numeric utilities may be derived for planning, but those numbers are transient computational artifacts.

### Explicit planning

Dependencies, constraints, preconditions, effects, Tasks, Plans, and Calendars are represented explicitly.

The system should be inspectable, recalculable, and explainable.

### Privacy-first architecture

UbU is intended to support local-first operation, multiple Identities, Zones, Compartments, and strict containment of sensitive data.

Sensitive data should not leak merely because planning metadata is useful.

### Affect-aware planning

Human beings are not machines.

In user mode, affective state—energy, stress, mood, tiredness, and related constraints—is part of the planning problem. UbU should respect emotional and physical constraints rather than treating them as inconvenient noise.

### Dogfooding

UbU should be useful for managing its own development.

The project’s GitHub workflow should eventually be coordinated by UbU itself, making the system’s strengths and weaknesses visible to contributors.

### Open design

This repository exists so that contributors can review, critique, and improve the design before and during MVP development.

---

## Repository structure

This repository intentionally starts simple.

```text
README.md
DESIGN.md
DECISIONS.md
OPEN_QUESTIONS.md
OUTREACH.md
LICENSE.txt
