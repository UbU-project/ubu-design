# Mobile device testing

`UBU-D0290` requires parity and stewardship measurements on a physically
connected rooted LineageOS device. An AVD is useful for app behavior, but its
host hardware/software graphics path cannot reproduce the phone's GPU driver,
vendor extensions, thermals or timings. It therefore cannot supply the hardware
evidence needed by `UBU-Q0160`. See Android's [emulator graphics documentation](https://developer.android.com/studio/run/emulator-acceleration).

The measured workload is deterministic skeletonization, exact hard-constraint
checks, local repair recipes and a short-horizon branch cache, compared with the
CPU reference path under `UBU-D0283`'s exact structural parity and named numeric
tolerances. It is not full desktop chunked search. Plans are CPU-certified on
the device before presentation. This document defines the future harness's
procedure; this ticket runs no device commands and claims no hardware results.

## Connection and capabilities

After physical connection and host authorization, establish the transport:

```text
adb tcpip 5555
adb connect <device>:5555
adb -s <device>:5555 get-state
```

Subsequent device work selects that TCP endpoint explicitly. The host talks to
its local adb server and the server reaches the device by plain TCP; USB
device-node permissions no longer govern that established connection. Initial
setup still needs physical access. Check reconnection after any adbd restart.

The [AOSP adb manual](https://android.googlesource.com/platform/packages/modules/adb/+/refs/heads/main/docs/user/adb.1.md)
defines these operations; availability on the chosen rooted build must be
verified, not inferred from the word “rooted”:

| Operation | Reachable capability |
| --- | --- |
| `adb root` | Restart adbd with root privileges where the build permits it |
| `adb remount` | Request writable partitions where the build permits it |
| `adb shell dumpsys gfxinfo <package>` | App rendering diagnostics |
| `adb shell perfetto ...` | Capture available system/device trace sources |
| `adb reboot` | Reboot to the system |
| `adb reboot recovery` | Request recovery |
| `adb reboot bootloader` | Request bootloader |
| `adb reboot sideload` | Request recovery's sideload mode |
| `adb sideload <ota.zip>` | Transfer an OTA package in a supported sideload session |

Rooted application access does not guarantee root adbd: its build-property
requirements are described in [AOSP's root documentation](https://android.googlesource.com/platform/packages/modules/adb/+/refs/heads/main/docs/dev/root.md).
A rooted test build can expose fuller diagnostics, but tool permissions and trace
sources remain build-specific. Diagnostics stay local; no vendor telemetry
service is part of this procedure.

**No device procedure may leave the phone in a state that needs a cable to
recover.** A command's existence does not prove that Wi-Fi, TCP adbd or a return
path survives it. Before a reboot, recovery, bootloader, remount or OTA operation,
the harness must have a verified cable-free return path for that exact build and
mode. Without one, stop before the transition. In particular, do not assume a
normal Android TCP connection persists in recovery or bootloader, or that OTA
sideload is available over that connection. Ordinary parity runs need none of
those transitions. The capability list is not a sequence to execute.

## What genuinely needs hands

- Physical connection and initial setup.
- The first host-authorization prompt after a wipe or a new host key.
- Re-enabling Developer Options after a factory reset.
- Unlocking the screen when a test touches the UI.
- Thermal and battery recovery: let the device cool or charge it.
- Recovery-menu confirmation on builds that require it.

An agent cannot supply those actions or infer that they happened after a delay.

## Mandatory device gate

The future harness must run a scripted pre-flight before **any device work**,
including after reconnection or a build/mode change. Pre-flight itself performs
read-only observations. It uses bounded timeouts and the explicit selected TCP
serial. Check in this order and stop at the first unmet condition:

| Check | Required observation | Example single-line failure instruction |
| --- | --- | --- |
| Host tooling/server and `adb get-state` | adb is available, server reachable, selected device reports `device` | `Connect the test phone and authorize this host, then rerun pre-flight.` |
| `adb shell getprop ro.build.fingerprint` | Exact fingerprint matches the harness's recorded device profile | `Select the phone with the configured build fingerprint, then rerun pre-flight.` |
| `adb shell dumpsys battery` | A real battery reading meets the profile's minimum charge | `Charge the test phone to the configured minimum, then rerun pre-flight.` |
| `adb shell dumpsys thermalservice` | Thermal status is known and within the profile's measured limit | `Let the test phone cool to the configured thermal limit, then rerun pre-flight.` |
| Build-specific keyguard/screen-lock observation | Lock state is known; UI-touching runs require an unlocked screen | `Unlock the test phone's screen, then rerun pre-flight.` |

The harness supplies device-specific parsers and recorded thresholds; this
document does not invent battery percentages, thermal budgets or universal
keyguard output fields. Unknown or unsupported readings fail closed with an
instruction to configure that specific observation. A missing adb executable,
unreachable server or unauthorized host gets its own precise instruction, not
a generic timeout. On failure, exit non-zero and emit exactly **one line** naming
the next human action, with detailed raw observations kept in the local log.
On success, exit zero and record fingerprint, battery, thermal and lock state
with the run's provenance. No destructive repair, reset or reboot is a pre-flight
fallback. API choice stays blocked until this gate and the parity measurements
exist.

## Working assumption, not a decision

The agent running future device procedures is expected to be Claude Code rather
than Codex: device work needs a shell with `adb` on PATH, localhost access to the
adb server, and a reachable device. The working assumption is that the intended
Claude Code setup has those without further sandbox questions. Confirm this
when the harness is built; it is not a product decision or a verified claim
about either agent's universal permissions.
