# Firmware Application (`firmware/app`)

**Status: Placeholder** - the application has not been created yet.

## Purpose

This directory will contain the main nRF Connect SDK / Zephyr application for BearingGuard AI: the
entry point, the application state machine, thread setup, inter-module messaging, and the build and
configuration files that tie the drivers, DSP, Edge AI, and Bluetooth modules together.

## Expected files

| File | Planned content |
|---|---|
| `CMakeLists.txt` | Zephyr application build definition; adds `src/` sources and links the `dsp`, `edge_ai`, `bluetooth`, and driver modules |
| `prj.conf` | Base Kconfig: Bluetooth peripheral role, logging, settings/NVS, sensor subsystem, PDM/ADC drivers, floating-point support, stack sizes |
| `Kconfig` | Application-specific options, e.g. `CONFIG_BGAI_EVAL_PERIOD_MS`, `CONFIG_BGAI_BASELINE_DURATION_S`, `CONFIG_BGAI_PULSES_PER_REV`, feature-set selection |
| `sample.yaml` or `app.yaml` | Optional Twister metadata for build tests |
| `src/main.c` | Boot sequence, subsystem initialisation, start of worker threads, watchdog |
| `src/app_state.c/.h` | State machine: `INIT`, `SELF_TEST`, `BASELINE_LEARNING`, `MONITORING`, `DIAGNOSTIC_CAPTURE`, `FAULT` |
| `src/app_pipeline.c/.h` | Processing thread: pulls windows from acquisition buffers, calls DSP and Edge AI, publishes results |
| `src/app_events.h` | Event and message definitions exchanged between threads (zbus channels or message queues) |
| `src/app_indication.c/.h` | RGB LED patterns for condition levels, learning mode, fault, and BLE connection state |
| `src/app_storage.c/.h` | Settings handlers for baseline statistics, thresholds, calibration, and device configuration |
| `src/app_selftest.c/.h` | Sensor presence, sampling-rate, and RPM-signal checks performed at start-up |
| `boards/` (symlink or reference) | Board overlays live in [`../boards/`](../boards/README.md) |

## Planned implementation notes

- **Threading**: a high-priority acquisition thread, a medium-priority processing thread, the Zephyr
  Bluetooth host thread, and a low-priority housekeeping thread (see
  [`../README.md`](../README.md)). Communication via `zbus` channels or `k_msgq` message queues.
- **Timing**: a fixed evaluation period (preliminary: one evaluation every few seconds) at which a
  complete multisensor feature vector is formed and scored.
- **Fail-safe behaviour**: any sensor or storage failure moves the state machine to `FAULT`, sets the
  Device Status characteristic, and shows a distinct LED pattern. The device never attempts to control
  the machine.
- **Baseline learning**: started and reset only through an authenticated BLE write; progress is reported
  through the Device Status characteristic; results are persisted via the settings subsystem.
- **Logging**: Zephyr `LOG` subsystem over RTT or UART; raw sample streaming for data capture will be a
  separate build configuration (see [`../../tools/data_capture/README.md`](../../tools/data_capture/README.md)).

## Planned configuration (preliminary, subject to change)

| Parameter | Preliminary value | Rationale |
|---|---|---|
| Vibration sample rate | TODO (several kHz) | Must cover bearing defect frequencies and their harmonics at the planned speed range |
| Acoustic sample rate | TODO (for example 16 kHz) | Covers audible friction and impact content; limited by RAM and processing time |
| Window length | TODO | Trade-off between frequency resolution and reaction time |
| Evaluation period | TODO | Determines notification rate and power consumption |
| Baseline learning duration | TODO | Must cover the full planned speed and load range |

## Current status

- No files have been created.
- Values in the configuration table are placeholders and will be set after the signal analysis phase.

## TODO

- [ ] Create the application skeleton (`CMakeLists.txt`, `prj.conf`, `Kconfig`, `src/main.c`) once the SDK release is pinned.
- [ ] Implement the state machine and inter-thread messaging.
- [ ] Define the LED indication patterns and document them in [`../../docs/architecture.md`](../../docs/architecture.md).
- [ ] Add a data-capture build configuration for raw sample streaming.
- [ ] Add a watchdog and fault-handling policy.
