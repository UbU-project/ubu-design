# P1B-75: design catch-up and multimodal MVP scope

## Result and scope

Only `ubu-design` changes. The design now records the atomic Stage 1 envelope exception, makes local camera-and-voice perception the primary MVP interaction surface, maps perceptual evidence onto the unchanged provenance enum, and catches up with the advisory, human-authoring and capture behavior. The unresolved details are questions, not claims of delivered functionality.

All twelve sibling repositories were clean on `main` before work. The accepted P1B-74 devshell, kernel and orchestrator changes were confirmed ancestors of local `main` and fetched `origin/main`. `ubu-design` started at `7313e82f7fb835965bc18521b10f897b238b65dc`. The documentation branch is `p1b-75-design-multimodal-mvp`. No Cargo, npm, build, rehearsal, rank, code, schema, pin or rev change is part of this ticket. No packages were installed.

The routing and baseline inventories were read in full, as was the supplied multimodal delta. They remain outside the public repository; the held scenario library was not copied, split into requirements or individually promoted into decisions. Unverified statistics were not researched or published. Scenario value ranges and monetary illustrations were omitted entirely.

## Grounding and governing sentences

The source quotations below governed the changes, rather than granting a model new authority.

| Section | Read first / governing sentence | Constraint applied |
|---|---|---|
| All | Routing: “File it as an amending `UBU-D` that refines `UBU-D0132`, not as a new thesis beside it.” | Correct the existing record and file D0292 as its amendment. Atomic-envelope repair precedes elevation, provenance and the inherited review pattern. |
| All | DECISIONS preamble: “Details belong in `DESIGN.md`; unresolved matters belong in `OPEN_QUESTIONS.md`.” | Decisions describe agreed boundaries; unresolved evidence, implementation and scope details stay questions. IDs/status conventions were read; numbering begins at D0292 and Q0161. |
| A | D0283: “The semantic contract remains a pure planning function over `PlanningRequest` and `PlanningResponse`.” | Record the approved internal profile without changing public planning semantics or CPU authority. |
| A | Python Stage 1 header: “The internal stage1-atomic-v1 envelope is an explicitly approved exception to D0283's complete-response envelope. Canonical PlanningStreamFrame is unchanged.” | Amend D0283's envelope sentence and record the minimized request/order/masks/tagged sampling/padded-array scope explicitly. |
| A | Kernel CONTRACT, legacy invocation: “The approved invocation wrapper transports the completed CPU answer after the existing PlannerStrategy pipeline.” | Distinguish the legacy completed-CPU-answer transport from independent Stage 1 and canonical streaming. A framework gate is not a completed tensor exchange. |
| A | D0132: “Realtime model output must enter UbU as structured, provenance-bearing candidate updates.” | Primary interaction still proposes candidates, with operator admission and the kernel as planner. DESIGN §2.13's optional-surface phrasing is updated, not left alongside its amendment. |
| B | Core ProvenanceKind: “How a value in a `UniverseState` was established.” | Keep source kind separate from perceptual confidence and verification. |
| B | Core FactProvenance: “How one value was established, and when. Deliberately nothing else: no confidence number and no free text.” | No invented confidence/verification fields; use existing candidate/Discovery evidence. The schema mirror has exactly `asserted`, `measured`, `derived`, `proposed`. |
| B | D0291: “Extending that governed set still requires a recorded amending `UBU-D` decision.” | Preserve governed subject vocabulary and closed-vocabulary discipline; no root or enum member is minted. This quotation governs subjects; the actual provenance enum and mirror govern B's kinds. |
| C, A1+A7 | ADVISORY: “Proposals never mutate canonical Task state. The advisor only enqueues candidates; admission is an explicit operator act.” | Record name-only vocabulary, no values sent, operator admission, producer-specific proposal bounds and refusal threshold. |
| C, A2+A3 | Admission review: “A dismissal is a snooze, never permanent.” Baseline A3: “The finite snooze applies only to reviews of already-admitted requirements.” | Finite escalating admitted-review holds stay distinct from durable suppression of a rejected new proposal. |
| C, A4 | Baseline: “The candidate carries a target and no value; admission requires a value the operator supplies and writes through the ordinary `UniverseState` mutation path with `asserted` provenance.” | D0296 preserves the name/value sovereignty boundary and current non-use of proposed value provenance. |
| C, A5 | Calendar capture: “Longer notes are refused whole, never truncated.” | Record the bounded initialization of an empty description, preservation of existing text, title capture despite refusal and no reverse notes export. |
| C, A8 | ADVISORY's approved correction: “This is a safe subset contract, not equality of the two accepted sets.” | D0299 uses the approved subset wording and records both rehearsal scars; it does not weaken the established validator. |
| C, B1 | STAGE1_WORKER: “The following is P1B-71's explicit implementation decision for a future stochastic Stage 1, not a claim it is implemented today.” | Record the specified Philox/AS241/fdlibm stream before activation, with exact structural parity and unchanged later-stage tolerances. |
| C, B2 | Core Measured: “An instrument or a reading.” | Human form policy offers assertions/readings, not claims that UbU derived or an advisor proposed a value. |
| D | DESIGN §12.2: “Any later use of those sources requires a separate explicit mode, Compartment review, routing disclosure, and user approval.” | Refine the existing capture boundary with local processing and selective retention; primary interaction does not imply continuous consent. |
| D | DESIGN §12.1: “Corrections and revocations remain append-only.” | Distinguish deletion of raw media from minimized immutable evidence and linked corrections/tombstones about it. |
| D, H | DESIGN phase scope: “Phase 1 keeps these abstractions documented for compatibility but does not implement them.” | Resource/Skill/Technique scenarios remain dependent on phased, unimplemented planning objects. Capture receives a Phase 1b MVP backlog assignment and an explicit sequencing question. |
| E | Q0151 current direction: “Segments live on the Container.” | Attach the operator's split-point/no-split CPU answer to existing subquestion 6; preserve D0278's solved resolution. |
| E | Q0128: “UbU should remain the harness, context controller, policy layer, and action authority.” | Answer the architecture/MVP scope, correct the phase field, absorb broader naming and keep detailed audio policies Open. |
| F | Delta: “Structured internal state does not imply structured human data entry.” | The new interaction document makes voice ordinary, asks only consequential uncertainty and retains useful forms/text. |
| F | Delta: “Users receive value while onboarding rather than paying an onboarding cost before receiving value.” | Record the first-use value goal without claiming recognition or onboarding success is implemented. |
| F | Delta: “The operator did not suggest positioning UbU primarily as an accessibility product.” | Guided camera acquisition improves access as part of ordinary life logistics; no narrow product category or universal accessibility claim. |
| G | README: “When a derived file conflicts with a canonical file, the canonical file wins.” | Every audience projection labels the new MVP target and keeps canonical authority and future dependencies visible. |
| G | WHAT_IS_UBU: “The decisions remain yours, always.” | Perception and voice remain instruments under the person; local hardware suitability is an unresolved requirement, not a modern-phone guarantee. |
| G | OUTREACH: “Claims should trace to implemented features, accepted decisions, closed issues, release notes, screenshots, demo recordings, fixtures, or explicitly labeled future plans.” | Separate release commitment, current dogfooding evidence and future motivating examples. No statistic or savings forecast is introduced. |
| G | FUNDER_BRIEF: “Funding is useful when it accelerates reusable open-core trunk capabilities: planning, local-first data, GitHub dogfooding, Logs, Calendars, Tasks, Objectives, privacy Compartments, bounded automation, reviewable projections, and planning-kernel contract implementation.” | Extend the economic-mobility/DIY thesis with qualitative, conditional impact and compute access; avoid professional replacement or poverty-cure claims. |
| G | PM_BRIEF: “The goal is to make coordination explicit enough that people can act with more autonomy, less ambiguity, and better evidence.” | Camera input does not become project telemetry or authority over contributors. |
| G | ORG_INTROSPECTION_BRIEF: “The two patterns share evidence-backed review, but they must remain separate so that personal affect, private behavior, and relationship context do not become organizational telemetry by default.” | Personal perception does not automatically create organizational evidence or authorize its disclosure. |
| G | SOVEREIGN_COORDINATION: “LLMs, realtime models, local agents, cloud models, and external tools may help extract candidates or propose actions. They do not become the authority over canonical state.” | The primary local surface retains admission, capture and egress boundaries. Local processing is not an endpoint-security guarantee. |
| H | DESIGN §4.1: “Phase 3 is the bridge from the bootstrap MVP toward the full personal life-logistics product.” | Keep existing minimal readiness/Technique expansion and richer Phase 4 integration assignments, rather than calling them unphased. |

### Approved corrections and precise grounding

The operator approved two wording corrections before this continuation. First, A8's literal language-equality claim conflicted with the approved P1B-64 conservative subset. Restricting the full validator would break established authoring/admission; expanding the small-model grammar would withdraw its intentional restrictions. The chosen correction preserves the validator and documents/tests subset containment. D0299 carries it explicitly.

Second, H and the routing analysis called Resource/Skill/Technique dependencies unphased, despite existing Phase 3 minimal readiness/Technique-based Objective expansion and Phase 4 richer integration. Calling them phased but unimplemented preserves the roadmap while making unresolved implementation details visible; inventing new phase assignments or declaring these objects MVP-ready would misstate both scope and readiness.

Other precision choices follow grounding: the Rust type is `ProvenanceKind::Proposed` on `FactProvenance.kind`; B2 is the implemented human form policy; the future stream is the already-specified Philox4x32-10/AS241/fdlibm choice; timed expanded recurrence instances already capture; and C2 concerns decomposition, not an implemented Clarify split-marker producer. None changes code or grants new authority. The Phase 1b assignment uses the existing MVP-extension backlog rather than inventing a phase label; Q0183 keeps exact capture coverage and implementation sequence unresolved, and the switch criteria are preserved. Existing historical Phase 1 readiness scores were not recalculated or presented as readiness of the enlarged release.

## Identifiers and destinations, in filing order

Before new identifiers, D0283 is amended for baseline A9 and D0132's effective priority is corrected. New decisions follow the routing dependencies and baseline order:

| ID | Record | Destination/detail |
|---|---|---|
| UBU-D0292 | Primary camera/voice MVP scope; amends D0132 | DECISIONS; DESIGN §2.13/§4.2/§12.2/§21; MULTIMODAL_INTERACTION |
| UBU-D0293 | Explicit perceptual provenance mapping | DECISIONS; DESIGN §11.2/§21.1; MULTIMODAL_INTERACTION |
| UBU-D0294 | Admitted-precondition review and proposal rejection | DECISIONS; DESIGN §21.2.2; baseline A2+A3 |
| UBU-D0295 | Precondition producer and attention bounds | DECISIONS; DESIGN §21.2.2; baseline A1+A7 |
| UBU-D0296 | UniverseTarget names without values | DECISIONS; DESIGN §11.2/§21.2.2; baseline A4 |
| UBU-D0297 | Exact future stochastic Stage 1 stream; refines D0171 | DECISIONS; DESIGN §16.10.2; baseline B1 |
| UBU-D0298 | Empty-description calendar-note initialization | DECISIONS; DESIGN §9.2; baseline A5 |
| UBU-D0299 | Safe producer grammar with documented subset | DECISIONS; DESIGN §21.2; baseline A8 |
| UBU-D0300 | Human assertion/measurement form policy | DECISIONS; DESIGN §11.2; baseline B2 |

A6 is a DESIGN §9.2 operator-authorship line, rather than a redundant decision. Q0128 then receives the architectural answer, corrected Phase 1b field and unselected broader naming question. The new interaction document supplies the UX destination. Q0183 and expanded Q0160 carry the capture-phase and mobile-role implications before derived claims are read as commitments. Statistics verification was intentionally skipped under the ticket's embargo; the public/funder track is qualitative.

Every new question goes to `OPEN_QUESTIONS.md`, remains Open and carries unranked metadata:

| ID | Question / source |
|---|---|
| UBU-Q0161 | Lossless prose descriptions; baseline C1 |
| UBU-Q0162 | Append-only Log enforcement gap; baseline C3 |
| UBU-Q0163 | Recurring-busy workaround removal; baseline C4 |
| UBU-Q0164 | Deliver primary surface with alternatives; delta §17.1 |
| UBU-Q0165 | Exact observation-to-candidate contract; §17.3 |
| UBU-Q0166 | Preserve perceptual qualifiers with fixed enum; §17.4 |
| UBU-Q0167 | Consequence-sensitive corroboration; §17.5 |
| UBU-Q0168 | Latency classes; §17.6 |
| UBU-Q0169 | Local segmentation/tool interfaces; §17.7 |
| UBU-Q0170 | Default raw-media retention; §17.8 |
| UBU-Q0171 | Discard/summary/hash/clip/export controls; §17.9 |
| UBU-Q0172 | Completion-compatible evidence versus proof; §17.10 |
| UBU-Q0173 | Skill evidence and competence; §17.11 |
| UBU-Q0174 | Guidance stop/professional escalation; §17.12 |
| UBU-Q0175 | Minimal expert handoff; §17.13 |
| UBU-Q0176 | Procedure-to-draft-Technique capture; §17.14 |
| UBU-Q0177 | Secure local hardware profile; §17.15 |
| UBU-Q0178 | Economically accessible compute; §17.16 |
| UBU-Q0179 | Future audience routing; §17.17 |
| UBU-Q0180 | Empirical economic benefit; §17.18 |
| UBU-Q0181 | Local metrics/opt-in research; §17.19 and baseline D5 |
| UBU-Q0182 | Guided-camera accessibility framing; §17.20 |
| UBU-Q0183 | Full realtime capture phase/coverage/sequence; explicit roadmap question |

Delta §17.2 is folded into existing Q0128; no separate name or decision is filed. Existing Q0151 subquestion 6 receives C2's operator answer and keeps its solved D0278 resolution. Existing Q0160 receives camera-first mobile-role questions; D0290 remains unchanged. Questions about already-decided surface priority and provenance are implementation follow-ups, not reopened scope/enum votes.

## The contradictions are closed

D0283's amended envelope rule begins “Except for the explicitly approved internal `stage1-atomic-v1` profile below” and the exception paragraph states: “The canonical `PlanningStreamFrame` is unchanged.” It now agrees with the running worker's approved internal handoff without weakening CPU certification, pure planning or the public stream.

D0132 now says: “Amended by `UBU-D0292`: local camera-and-voice perception is the primary interaction surface and part of the MVP release.” D0292 closes the priority/authority distinction directly: “Multimodal perception becomes the primary interaction surface without becoming an authoritative planner. The camera proposes candidate state; the kernel still plans; admission is still the operator's.” Q0128's Phase field is Phase 1b, not Phase 3. Its architectural answer is recorded while detailed restricted-attention and naming questions stay Open.

## Explicit provenance mapping

| Perceptual word | Existing kind / qualifier |
|---|---|
| observed | Unconfirmed visual interpretation: proposed candidate; instrument reading: measured; person's report: asserted. None bypasses admission. |
| inferred | Unconfirmed perceptual candidate: proposed; actual computation from facts: derived with evidenced inputs/derivation. |
| operator_confirmed | Personal assertion: asserted; operator-recorded reading may be measured. Confirmation is not proof of measurement. |
| externally_verified | Evidence qualifier preserving underlying asserted/measured/derived source, rather than an enum upgrade or admission. |
| measured | Instrument/reading only, never the top of a confidence ladder. |

Current advisors still propose no values, so Proposed stays unused by that policy. Future perceptual inferred values can legitimately use that candidate classification without being written into canonical state. Confidence/verification belongs in existing candidate and Discovery evidence, not new FactProvenance fields. No enum, schema, code, pin or rev moved.

## Baseline inventory disposition

| Item | Filed/deferred destination | Reason or preserved limitation |
|---|---|---|
| A1 | D0295; DESIGN §21 | Implemented precondition advice, recorded-target-only vocabulary and operator admission. |
| A2 | D0294; DESIGN §21 | General inherited review contract and implemented finite precondition-review holds. |
| A3 | D0294 | Durable new-proposal suppression differs from finite admitted-value review. |
| A4 | D0296; DESIGN §11/§21 | Name-only target advice preserves operator value authorship. |
| A5 | D0298; DESIGN §9 | Bounded empty-description initialization with no overwrite/export. |
| A6 | DESIGN §9.2 | Direct human read/write/clear, collection predicates and readable/clearable trees. |
| A7 | D0295 | At-most-three proposals and producer-specific ten-candidate refusal; not a hard queue ceiling. |
| A8 | D0299; DESIGN §21 | Approved safe-subset relationship, independently tested producer boundary and rehearsal scars. |
| A9 | Amended D0283; DESIGN §16.10 | Existing approved atomic-envelope exception reconciled with design. |
| B1 | D0297; DESIGN §16.10 | Decided future exact stream; not implemented or activated here. |
| B2 | D0300; DESIGN §11 | Existing human form offers assertions and readings, not derived/proposed claims. |
| C1 | Q0161 | Desired prose is not yet a lossless synthesis/retention decision; implementation remains deferred. |
| C2 | Existing Q0151 subquestion 6 | Operator answer attaches to its existing resolved question; no duplicate decision or claim of Clarify implementation. |
| C3 | Q0162 | Append-only is already required; offending edit paths/remediation need an implementation audit, not a new rule. |
| C4 | Q0163 | Known temporary uncaptured-busy workaround; removal depends on verified occupancy without duplicate blockers. Timed expanded instances already capture. |
| D1 | OUTREACH | Qualitative bureaucratic dependency/lead-time/deadline example, not a new feature requirement. |
| D2 | OUTREACH; FUNDER_BRIEF | Future maintenance, condition evidence, readiness, weather and executable repair/replacement examples with phased dependencies. |
| D3 | FUNDER_BRIEF | Future user-authorized care-packet preparation for a professional; no monitoring, diagnosis or professional-replacement claim. |
| D4 | MULTIMODAL_SECURITY | Generic future local-hygiene/device-maintenance capabilities and controls only; no private verbal rationale. |
| D5 | FUNDER_BRIEF; Q0181 | Speculative opt-in field research; consent, validity and privacy unresolved. No trial-replacement or clinical-efficacy claim. |

The delta's full scenario library remains together in its supplied private source. The evidence-sensitive examples excluded by the ticket were not introduced into audience documents. New naming proposals remain unselected. No operator Task, calendar event, fact key/value, protected artifact content or artifact filename was copied into this repository.

## Static verification and publication boundary

The checks for this ticket are document consistency and disclosure checks, not a rehearsal or operator acceptance. Whitespace, decision/question uniqueness and consecutive new numbering, metadata vocabulary, new reference resolution, relative Markdown links, protected-data/path audit, audience-added-prose digit checks and all-read-only repository comparisons were checked. No ranking or score mutation was run. D0290 and both planning/device contracts remain byte-identical to baseline. All other repositories and their pins/revs remain unchanged; the devshell inventory is intentionally not refreshed under the one-repository/no-pin instruction.

The statistic check uses a private pattern file derived from the delta's statistics section and omitted scenario illustration, without copying those figures into public command text or this report:

```text
rg -n -i -f "$PRIVATE_STATISTIC_PATTERNS" --glob '*.md' ubu-design
Result: no matches (exit 1).
```

All new audience-document additions contain no digits and no statistics. A separate review of the security and audience additions confirms that they state controls and scope rather than reconstructing an absent private verbal argument. A grep cannot prove absence of an argument never supplied as text; that distinction is preserved. Known operator keys and local excluded-artifact names are checked internally without opening the protected artifacts or printing their names.

The published branch is a reviewable documentation deliverable; no merge or operator reading is claimed. The companion interaction and security documents are linked from README and DESIGN. This report records the approved corrections, their reasons and alternatives, rather than silently rewriting them.

Operator acceptance has not been performed; it is a reading rather than a run, and what is under test is whether the records say what he decided.
