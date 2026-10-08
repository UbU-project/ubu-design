# Camera and voice in UbU

**Status:** Interaction design for the MVP release, not a shipped-feature claim. `UBU-D0292` amends `UBU-D0132`; `UBU-D0293` defines provenance mapping. Canonical design and decisions govern this document. Delivery details remain in `OPEN_QUESTIONS.md`.

## Show the world; keep the model inspectable

The camera is a perception layer, not an upload field. The intended interaction is:

> human shows world → UbU proposes candidate state → UbU resolves against persistent context → UbU asks only high-information clarifications.

Local inference runs on the operator's own hardware; raw images in this primary path do not go to a hosted model. Persistent context is purpose-scoped by Identity and Compartment, not an excuse to expose the entire life model. A photographed object is useful because UbU can ask what it means for the person's work and constraints, not just recognize its category.

Ask for bits of uncertainty, not records. UbU extracts structure and spends operator attention on ambiguity that matters: whether a visible object is the intended object, whether a condition still holds, or whether an interpretation would change the next action. It should not ask the user to fill an internal ontology merely because the database is structured. Ambiguous matches remain candidates; showing an object does not prove its ownership, state, availability or relevance.

The operator can inspect the proposed change, its source and its consequences; correct it, reject it, defer it or leave it unknown. The camera proposes candidate state; the kernel still plans; admission is still the operator's. An efficient confirmation surface must preserve that authority instead of hiding it behind a conversational response.

## Value-producing onboarding

The first photograph, spoken request or shown document should produce the first useful result. A person can start with “Show me the things you want help with,” receive a useful clarification or next step, and grow the private model while getting help. This is an interaction goal for the release, not a promise that every image is recognizable or actionable.

Avoid charging an inventory-entry debt before usefulness. Start from a concrete concern, propose the minimum structure needed, disclose uncertainty and ask only what changes the answer. Keep an inspectable path to the underlying Task, evidence and accepted state. Unavailable cameras, declined capture or unsuccessful interpretation must leave useful text, voice or form entry.

Ordinary activity can later refresh that context: a changed condition yields candidate evidence and, after validation and admission, a model update and recalculation. Rich household, maintenance, purchasing, Skill-evidence and tacit-expertise examples depend on first-class Resource, Skill and Technique work. Minimal readiness and Technique-based Objective expansion are already Phase 3; richer integration is Phase 4. This interaction document does not pull those objects or the held scenario library into MVP requirements.

## Voice as ordinary control

Voice is an ordinary conversational surface on the same smartphone, not only a driving mode or an accessibility option. Local speech recognition and synthesis should adapt to the user's vocabulary, speech patterns, preferred turn length, verbosity and pacing. Suitable hardware and latency still need evidence; no particular model or universal phone support is selected here.

Structured internal state does not imply structured human data entry. People should usually be able to speak, show, confirm or correct. Text and forms remain alternate precision surfaces when preferred or appropriate: a quiet room, inaccessible speech, sensitive context, a noisy environment, or a review requiring exact field values. These are meaningful choices, not a subordinate fallback the product neglects.

Restricted-attention interaction remains bounded by mode and action consequence. A generic “yes” must not turn an uncertain reference into permission to send, delete or make a commitment. Capture and defer complex review when attention is unavailable; silence and rest can be legitimate outcomes. `UBU-Q0128` retains the detailed audio/messaging/media policies and the broader naming choice. No new canonical name is selected.

## Guided acquisition and access

Voice plus guided camera acquisition can help a person who cannot conveniently frame or visually inspect a scene. UbU can ask for a changed angle, a nearer label or another view, explain what is still missing and let the person stop or use an alternate surface. Guidance should respond to uncertainty rather than demand repeated captures without explaining their purpose.

Accessibility is part of ordinary life logistics, rather than the sole category for the product. Test camera guidance alongside speech, text, forms and assistive technologies. Preserve controls for private, unknown, pause, resume, exit, inspect, correction and rejection. A primary surface is neither compulsory camera use nor always-on capture.

## Closed-loop execution and evidence

The architectural loop is **See → understand → plan → direct → observe → verify → learn → update**. Each arrow preserves the boundary between evidence, interpretation, admission and action. New observations can expose a missed prerequisite or changed condition; they can also be incomplete or wrong. Repetition, fluent narration and compatibility with an expected step do not prove completion or an effect.

`UBU-D0293` maps perceptual terms onto the unchanged `asserted / measured / derived / proposed` enum. Observation/inference stays a proposed candidate until reviewed; personal assertion, an instrument reading and computation from facts remain different sources. Confirmation or external verification is evidence about a claim, not a confidence rank that rewrites its provenance kind. Existing candidate/Discovery evidence holds confidence and corroboration; no new FactProvenance fields are invented.

Consequence-sensitive corroboration, streaming latency/segmentation, professional escalation, expert-handoff packets, procedure-to-Technique capture and Skill updates remain explicit questions. Technique-guided execution cannot be treated as implemented simply because perception becomes release scope. A professional's involvement supplements the user's plan; local guidance does not replace professional competence.

## Capture controls and retention

Continuous microphone or camera use refines the existing DESIGN.md §12.2 boundary: a separate explicit mode, Compartment review, routing disclosure and user approval. Show active sources and local routing, make pause/exit easy, and minimize retained raw material. Any later export is separately approved and must obey hard Compartment denials.

Raw-media deletion is distinct from editing history. An admitted claim remains auditable through minimized append-only evidence, correction, revocation and deletion/tombstone metadata; the Log does not automatically preserve a reconstructible raw stream. Deletion can make source evidence unavailable without making a claim true or generating a replacement observation. Retention defaults and enforcement are unsettled and unimplemented here. See [the local security boundary](MULTIMODAL_SECURITY.md) and [the open questions](OPEN_QUESTIONS.md).
