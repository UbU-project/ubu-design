# P1B-26 Part 1 verification

Starting design revision: `1a64e6b00de09d709cde2ee0c40675c91a09fbb7`.
Branch: `p1b-26-routine-effects`. A–E each have a separate documentation commit.

Added decision **UBU-D0290** and open question **UBU-Q0160**. The latter depends
on UBU-Q0156 and is blocked on real-device stewardship parity measurements.
DESIGN.md §16.10.6 now specifies mobile execution. §16.8's backend list and all
existing authority/certification boundaries are unchanged. The contract adds
mobile provenance names; no implementation of provenance or device harness is
claimed. The procedure records a mandatory pre-flight and cable-free recovery
rule, with the future agent choice explicitly an unverified working assumption.

The contract version did not change. The ticket calls it 0.1, but the starting
file already records baseline `planning-kernel-contract/0.1` and Phase 1b
`planning-kernel-contract/0.2` for split-policy/partial-placement. Both are
preserved; these additive, contract-only enum members introduce no bump.
Another literal-reading adjustment: §16.10.6 was already “Correlation groups
and rollout matrix,” followed by §16.10.7 “Solver selection and deferred backend
targets.” Those became §16.10.7 and §16.10.8, preserving their bodies, to give the
requested new subsection exactly §16.10.6.

No other repository was touched during Part 1. In particular, the schemas'
eleven-line contract subset and the kernel's implementation-facing CONTRACT.md
remain unchanged. All other eleven repositories retain their starting revisions
and clean trees at the Part 1 landing boundary. This documentation repository
has no Cargo workspace, lockfile, Clippy target or executable test suite.
Validation: `git diff --check`, unique decision/question numbers and subsection
headings, unchanged version declarations and §16.8 text, and a diff limited to
the six requested Markdown files. No executable code or device commands ran.

No disagreement with the six architectural judgment calls. Two operational
qualifications prevent false guarantees: rooted LineageOS does not universally
permit root adbd or every diagnostic, and TCP connectivity need not survive
recovery/bootloader transitions. The document lists the requested capabilities
but gates those operations on a verified cable-free return path. AVD results do
not count as hardware parity evidence. Battery/thermal thresholds and screen-lock
parsing are harness/device-profile inputs, not measurements invented here.
