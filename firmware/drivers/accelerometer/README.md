# Accelerometer Driver (`firmware/drivers/accelerometer`)

**Status: Placeholder** - no driver code exists yet.

## Purpose

This directory will contain the integration of the three-axis digital accelerometer that measures
bearing-housing vibration. Vibration is the primary sensing channel for detecting imbalance,
misalignment, looseness, and rolling-element or raceway defects, so this driver must deliver
continuous, gap-free, accurately timed samples at a sufficiently high output data rate.

## Expected files

| File | Planned content |
|---|---|
| `accel.h` | Public API: `accel_init()`, `accel_start_stream()`, `accel_stop_stream()`, `accel_read_block()`, configuration structure (range, output data rate, FIFO watermark) |
| `accel_<part>.c` | Sensor-specific implementation using the Zephyr sensor API (`sensor_sample_fetch`, RTIO/streaming API if supported) or a direct SPI FIFO reader |
| `accel_selftest.c` | Start-up checks: WHO_AM_I / device ID, self-test routine if the sensor offers one, orientation sanity check (gravity on the expected axis at standstill) |
| `Kconfig` | `CONFIG_BGAI_ACCEL_ODR_HZ`, `CONFIG_BGAI_ACCEL_RANGE_G`, `CONFIG_BGAI_ACCEL_FIFO_WATERMARK` |
| `CMakeLists.txt` | Adds the sources to the application build |

## Planned sensor requirements

| Requirement | Preliminary target | Rationale |
|---|---|---|
| Axes | 3 | Radial (two directions) and axial vibration |
| Output data rate | Several kHz (TODO: final value) | Bearing defect frequencies and their harmonics must lie well below Nyquist at the maximum rig speed |
| Measurement range | Selectable, e.g. +/-8 g or +/-16 g (TODO) | Avoid saturation during impulsive events while keeping resolution for small deviations |
| Noise density | As low as practical | Small early-stage deviations are the target |
| Interface | SPI preferred (I2C acceptable for lower rates) | High-rate FIFO reads |
| FIFO | Required | Allows batched, DMA-friendly reads and reduces interrupt load |
| Mounting | Rigid, stud or adhesive mount on the housing | Mounting compliance limits usable bandwidth |

## Planned implementation notes

- Prefer a sensor that already has a Zephyr in-tree driver with FIFO/streaming support to minimise
  custom code; otherwise implement a thin SPI driver with interrupt-driven FIFO draining.
- Samples will be timestamped with the system clock at FIFO watermark events; the acquisition thread
  will push fixed-size blocks into a ring buffer consumed by the DSP module.
- Range and output data rate will be Kconfig options so that the data-capture firmware and the
  monitoring firmware share the same driver.
- Axis orientation relative to the bearing (radial-horizontal, radial-vertical, axial) will be documented
  in the mechanical sensor-mount drawings and in the recording metadata.

## Current status

- No sensor has been selected; no code has been written.
- Requirements in the table above are preliminary planning values.

## TODO

- [ ] Shortlist candidate accelerometers (bandwidth, noise, FIFO depth, Zephyr support).
- [ ] Decide on SPI versus I2C based on the chosen output data rate.
- [ ] Define the ring-buffer block size together with the DSP window length.
- [ ] Specify the start-up self-test and its failure handling.
- [ ] Write the driver and a host-side Ztest for the block-handling logic.
