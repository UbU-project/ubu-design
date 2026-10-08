# Local multimodal security and OPSEC boundary

**Status:** Design requirements and future capability examples. This document refines existing Identity, Compartment, context, admission and worker boundaries; it does not claim a shipped perception stack or security agent.

## The capture boundary

The primary MVP camera-and-voice path performs inference on the operator's own hardware, without uploading its raw images to a hosted model. Local processing avoids that external disclosure, but endpoint compromise can expose the same intimate context. Local-first is not a guarantee against a malicious administrator, compromised model/tool, insecure storage or an unauthorized camera/microphone reader.

Apply least privilege to capture devices, storage, model runtimes, local agents and tools. A capture session declares source scope, purpose, Identity/Compartment, permitted devices, processing route and retention. Continuous AV still requires the explicit mode, review, disclosure and approval in DESIGN.md §12.2. Pause, cancellation and revocation must stop further authorized acquisition and tool access; exact enforcement is implementation work.

## Context and egress

Resolve an image against only the context permitted for that purpose. Cross-Identity resolution is not ambient access to every record. Camera views, spoken instructions, labels, documents and scene text are untrusted inputs: they cannot expand capability grants, override Compartment denials or issue tool commands merely by appearing in model context.

Bound local tool interfaces to required frames, intervals, selectors and operations. Recheck current grants and policy at execution and admission; stale context must not silently authorize a change. Disable unnecessary egress from perception/agent processes and apply the existing export boundary to any later allowed transfer. An operator's separately approved disclosure is distinct from the primary local inference path. Hard `no_cloud_llm` and `no_external_export` rules cannot be overridden by a convenient interaction mode.

Raw AV, extracted text, thumbnails, summaries, hashes and intermediate model/tool artifacts all need purpose-bound retention. A summary or hash can reveal a sensitive relationship or enable correlation; deleting raw media does not make those derivatives safe to publish. Keep reconstructible private media out of the immutable audit path and retain minimized linked correction/deletion metadata instead. Storage protection, deletion mechanics and audit minimization need verification before any enforcement claim.

## Future local hygiene and device maintenance

A possible future local agent can assist with operator-authorized credential hygiene, reuse checks, authentication settings, software integrity and updates. Secret access must be explicit, capability-scoped, Compartment-limited and revocable; a general task description is not authority to open credential stores. Prefer narrow checks and redacted findings over passing secret contents into broad context. Proposed changes remain reviewable and must preserve recoverability where possible.

Maintaining another trusted device adds device eligibility, sync, identity, observed-version and remote-action gates; local ownership alone does not confer unrestricted control. This family depends on the relevant Compartment, delegation and device work. No agent is implemented or activated here, and no online-versus-local impossibility claim substitutes for an enforced boundary. The public documentation records these controls only.

## Evidence and operational honesty

Model confidence cannot authorize a security change or certify an outcome. Keep inference separate from instrument readings, operator assertions and actual derivations, as required by `UBU-D0293`. Escalate unresolved consequential interpretations rather than presenting an advisory finding as verified state.

Acceptance for future implementations must exercise granted/denied access, injection boundaries, egress, revocation, stale context, retention and audit minimization on supported local hardware. Those are required behaviors to verify, not results obtained by this documentation ticket. See [the interaction model](MULTIMODAL_INTERACTION.md), DESIGN.md §21/§23 and `UBU-Q0165`–`UBU-Q0172`.
