# Phase 1 Contract Boundaries

## Status

This document is canonical prose documentation for the major Phase 1 implementation contract boundaries across the UbU repo constellation.

It defines where authority lives between `ubu-schemas`, `ubu-core`, `ubu-store`, `ubu-github-adapter`, the planning crates, `ubu-orchestrator`, `ubu-ui`, `ubu-devshell`, and `ubu-brand`. It does not add runtime behavior, generated schemas, or repo-local implementation shortcuts.

## Repo constellation

Phase 1 is split into separate public repos under `UbU-project/*`:

```text
ubu-design
ubu-schemas
ubu-core
ubu-store
ubu-github-adapter
ubu-planning-kernel
ubu-orchestrator
ubu-ui
ubu-devshell
ubu-brand
```

The split is intended to maximize code generation, reviewability, reuse, and dogfooding. Each repo has a bounded contract and should avoid silently absorbing authority or semantics from another repo.

Code repos use the MIT license. `ubu-brand` uses MIT for repo docs/scripts and CC-BY-ND-4.0 for logo and brand assets through a separate asset license.

## Design authority boundary

`ubu-design` is the canonical prose design authority.

It defines design rationale, accepted decisions, unresolved questions, phase boundaries, implementation plans, codegen strategy, and cross-repo contract boundaries. It should not contain runtime implementation code, generated schemas, hidden operational behavior, private user data, or repo-specific implementation shortcuts.

Implementation repos may refine local APIs, but they should not silently redefine canonical UbU semantics.

## JSON Schema canonical boundary

`ubu-schemas` is the canonical machine-readable schema authority for Phase 1.

Phase 1 schemas use JSON Schema Draft 2020-12 with `$id` values rooted at:

```text
https://schemas.ubunow.net/phase1/
```

Cross-file `$ref` values use those `$id` URIs. Validation and TypeScript generation must resolve schemas from local bundled files during Phase 1; tooling must not require network access to fetch schema IDs.

The ID registry is a single source of truth in `ubu-schemas`. It defines both the allowed prefix set and the prefix-to-object-type mapping. Canonical IDs use prefixed lowercase unhyphenated UUIDv7 strings with `_` as the delimiter:

```regex
^<prefix>_[0-9a-f]{12}7[0-9a-f]{3}[89ab][0-9a-f]{15}$
```

`AuthoritySource` is also canonical in `ubu-schemas` as the closed enum:

```text
user
user_override
delegated
automation_worker
policy
system
```

`user` represents ordinary user authority. `user_override` is reserved for explicit user override of another proposed, delegated, automated, policy, or system-derived action. Automation, policy, and system authority sources must not be treated as unconstrained autonomous user-equivalent authority.

TODO Phase 2: support hosted or publish-time schema bundling without weakening local offline validation and generation.

## Rust type compatibility boundary

`ubu-core` is the shared Rust domain foundation.

It provides hand-written Rust types, ID parsing, timestamp validation, provenance helpers, Compartment labels, authority-source mirrors, GPU advisory wire types, and serialization conventions compatible with `ubu-schemas`.

Rust types are intentionally hand-written and fixture-tested against canonical schemas. This preserves an explicit serde-to-schema lockstep during Phase 1. `ubu-core` includes `ubu-schemas` as a pinned git submodule for fixture round-trip tests. A thin local-only `build.rs` may wire fixture paths, but it must perform no network fetch.

TODO at 1.0: revisit whether additional schema/type generation or stricter `additionalProperties` conventions should replace part of the hand-maintained serde/schema lockstep.

`ubu-core` should remain boring and reusable. It must not contain database logic, GitHub API logic, planning algorithms, UI behavior, Tauri behavior, GPU execution behavior, or canonical state mutation.

## Store admission boundary

`ubu-store` is the canonical local state admission and persistence boundary for Phase 1.

Only `ubu-store` mutates canonical local state directly. Other repos submit candidate records, planning results, imported external references, projection previews/results, worker submissions, user action events, logs, and snapshots for admission.

`ubu-store` admission enforces ID prefix-to-object-type consistency using the `ubu-schemas` id-registry mapping as the canonical source. It must reject records whose prefix and declared object type disagree.

The Phase 1 database is SQLite via `sqlx`. Append-only logs are enforced at the application layer only in Phase 1. Raw SQLite table layout is an implementation detail, not the Phase 2 replication contract.

Future replication must operate over explicit store-level records, admitted-object envelopes, log entries, provenance-bearing events, snapshots, and Compartment-aware export/import APIs, not by assuming raw SQLite table compatibility.

Phase 1 preserves stable prefixed UUIDv7 IDs, schema versions, object versions, timezone-bearing timestamps, provenance, authority source, object references, and logical Compartment metadata so that Phase 2 replication can be added without redefining canonical state semantics.

Phase 1 does not implement multi-device replication, CRDT merging, encrypted per-Compartment SQLite files, remote wipe, or transport protocols.

## Planning authority boundary

The `ubu-planning-kernel` repo owns Phase 1 planning implementation, but there is no `ubu_planning_kernel` crate.

The repo contains planning crates with distinct authority:

- `ubu_planning_core` owns the public API: `plan`, `repair`, `validate_plan`, and `explain_plan`.
- `ubu_planning_core` owns authoritative deterministic validation and legitimization.
- `ubu_planning_core` defines the `PlannerStrategy` trait.
- `plan` and `repair` take an explicit strategy argument. There is no default strategy in core, which avoids a core-to-CPU dependency cycle.
- `ubu_planning_cpu` implements the default strategy.

The orchestrator depends on `ubu_planning_core` and `ubu_planning_cpu`.

Final plan validity must always be certified by `ubu_planning_core::validate_plan`. Strategy crates may propose or repair candidates, but they do not own the final authority boundary.

## GPU advisory non-authority boundary

The GPU advisory backend is scaffolded immediately as a no-op Python JSON process over stdin/stdout. The default implementation is stdlib-only. `torch` is an optional future extra.

GPU advisory wire types are canonical in `ubu-core`; the advisory protocol crate depends on them.

The future GPU strategy crate and Python process are absent from default builds. When added, the GPU path implements the same `PlannerStrategy` trait as a candidate proposer. Its candidates are always certified by `ubu_planning_core::validate_plan`; it never certifies final validity.

The GPU advisory path must not:

- certify final Plan validity;
- bypass dependency validation;
- bypass deterministic legitimization;
- bypass static task constraints;
- bypass Compartment/export rules;
- mutate canonical store state;
- become required for default Phase 1 builds or fixture mode.

## GitHub projection approval boundary

`ubu-github-adapter` owns GitHub import, normalization, projection preview, approved write execution, and reconciliation.

GitHub is an external source/projection, not the canonical UbU state store.

Phase 1 approved writes may include:

- applying UbU-managed labels;
- removing UbU-managed labels;
- creating UbU-managed comments;
- creating UbU-managed issues.

Writes require approval per `ProjectionPreview` batch. There are no autonomous writes.

Missing managed labels must be represented as preflight operations in `ProjectionPreview` or fail approval with a `MissingManagedLabel` diagnostic. Only these managed labels may be auto-created in Phase 1:

```text
ubu
ubu-managed
```

No arbitrary label creation is allowed.

The GitHub adapter uses `octocrab`. GitHub token handling supports:

1. developer mode: `GITHUB_TOKEN` environment variable;
2. desktop session mode: user pastes a token into the UI, the UI sends it to the orchestrator for in-memory session use only.

Tokens, Authorization headers, pasted session tokens, and octocrab auth configuration must never be persisted or logged.

TODO Phase 2: add GitHub App auth and OS keychain-backed token storage where appropriate.

## UI and orchestrator boundary

`ubu-orchestrator` is the local service layer connecting store, GitHub adapter, planner, and UI.

Phase 1 uses a local HTTP API built with `axum` and documented with `utoipa`. It must bind to `127.0.0.1` only. Mutating endpoints, especially projection approval, are dangerous even on loopback because local processes or malicious local web content may attempt requests.

Phase 1 intentionally defers per-run bearer-token and CSRF defenses because the HTTP bridge is temporary and expected to be superseded by a Tauri command bridge. The implementation must include explicit code commentary and TODO warnings about loopback mutating endpoint risks.

`ubu-ui` is a Tauri v2 desktop UI using React, Vite, and TypeScript.

The first scaffold uses the local HTTP API exposed by `ubu-orchestrator`. It consumes generated API clients from the orchestrator OpenAPI specification and generated TypeScript types from locally bundled `ubu-schemas`.

`ubu-ui` must not directly mutate GitHub or directly mutate the store. It submits user actions, token-session configuration, and projection approvals through the orchestrator.

TODO Phase 2: replace or supplement the local HTTP boundary with a Tauri command bridge and stronger local authority model.

## Compartment Phase 1 limitation

Phase 1 preserves logical Compartment metadata as labels and policy summaries only.

It does not provide physical isolation, per-Compartment SQLite files, per-Compartment encryption, cryptographic compartment boundaries, or separate storage engines. Code and UI must not describe Phase 1 Compartments as providing physical isolation or encryption.

TODO Phase 2: add per-Compartment SQLite and encryption design and implementation.

## Devshell boundary

`ubu-devshell` is a multi-repo developer harness.

It may clone, update, test, run, and coordinate the Phase 1 repo constellation. It may generate local `[patch]` overrides and codegen issue text. It must not contain canonical schema definitions, planner semantics, store semantics, production deployment behavior, or private fixtures.

Cross-repo Rust dependencies are committed as git dependencies pinned to explicit revs. Local development overrides use gitignored, devshell-generated `.cargo/config.toml` `[patch]` entries.

TODO(workflow): re-verify this dependency workflow if the scaffold or CI workflow changes. The fallback is commit plus rev bump for each iteration.

## Brand boundary

`ubu-brand` stores public brand assets.

Runtime/code repos should not duplicate brand assets except where packaging requires it.

Repo docs/scripts may use MIT licensing. Logo assets intentionally use a separate CC-BY-ND-4.0 asset license. A trademark/logo-use policy remains a TODO before broad external adoption.

## Phase 2 TODO summary

Phase 2 or later work includes:

- per-Compartment SQLite and encryption;
- Tauri command bridge and stronger local authority model;
- OS keychain support;
- GitHub App auth;
- restoring `clippy -D warnings` per crate after scaffold tickets land;
- revisiting `additionalProperties` and serde/schema lockstep at 1.0;
- hosted or publish-time schema bundling.

## Phase 1 non-goals across boundaries

Phase 1 does not implement:

- multi-device replication;
- Phase 2 transport;
- CRDT merge semantics;
- vector clocks;
- encrypted per-Compartment SQLite files;
- raw SQLite file sync;
- remote wipe;
- heartbeat-based retention;
- broad email/SMS/file ingestion;
- autonomous GitHub writes;
- arbitrary GitHub label creation;
- hidden LLM planning authority;
- GPU-certified planning;
- mobile app support;
- cloud backend dependency.

## Documentation impact

Implementation prompts and repo scaffolds should reference these boundaries where relevant. The addition of `ubu-store/docs/PHASE1_STORE_CONTRACT.md` does not significantly alter the repo split, dependency graph, or scaffold priority. It does require minor reference-level prompt updates so `ubu-store`, `ubu-design`, and cross-repo contract documentation point to the store contract explicitly.
