# Data Capture (`tools/data_capture`)

**Status: Placeholder** - no capture tool exists yet.

## Purpose

This tool will receive raw, timestamped sensor samples from the nRF54LM20 DK during recording campaigns
and store them as measurement runs with complete metadata. It is the gateway for every dataset in the
project, so correctness of timing, scaling, and metadata is more important than convenience features.

## Expected files

| File | Planned content |
|---|---|
| `capture.py` | Command-line entry point: connect to the device (USB-CDC/UART, RTT, or a dedicated BLE capture characteristic), start/stop a recording, write files |
| `protocol.py` | Framing and decoding of the capture stream: channel IDs, sample formats, timestamps, sequence numbers for gap detection |
| `writer.py` | Writes per-channel arrays plus a per-run metadata record following the template in `datasets/metadata/` |
| `metadata_prompt.py` | Interactive or argument-based entry of run metadata (bearing ID, condition, severity, RPM set-point, load, sensor positions, temperatures, notes) with validation against the controlled vocabularies |
| `requirements.txt` | Pinned dependencies |
| `README.md` | This file, with usage examples once the tool exists |

## Planned behaviour

1. The firmware is built in a **data-capture configuration** that streams raw accelerometer, acoustic,
   temperature, and RPM data instead of running inference.
2. The tool validates the stream continuously (sequence gaps, sample-rate drift, saturation) and marks a
   run as invalid if integrity checks fail.
3. Each run receives a `recording_id` of the form `<date>_<bearing_id>_<condition>_<severity>_<rpm>_<seq>`
   (final naming rule TODO in [`../../datasets/README.md`](../../datasets/README.md)).
4. Data is written to an **external data directory** given on the command line, never into the repository.
5. Raw audio is written only when explicitly enabled and is subject to the retention policy.

## Current status

- No code. The capture protocol will be defined together with the firmware capture build.

## TODO

- [ ] Choose the transport (USB-CDC, RTT, or BLE) based on required bandwidth.
- [ ] Define the stream framing and write `protocol.py` plus unit tests with synthetic frames.
- [ ] Implement writer and metadata validation against `recording_metadata_template.csv`.
- [ ] Document the recording procedure step by step.
