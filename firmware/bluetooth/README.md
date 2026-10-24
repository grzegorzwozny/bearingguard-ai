# Bluetooth Module (`firmware/bluetooth`)

**Status: Placeholder** - no Bluetooth code exists yet.

## Purpose

This directory will contain the Bluetooth Low Energy functionality of BearingGuard AI: the custom
**Bearing Health Service** (GATT), advertising, connection and security management, and the standard
Device Information Service. The authoritative, preliminary description of the service is in
[`../../docs/bluetooth_service_plan.md`](../../docs/bluetooth_service_plan.md); this module will
implement it.

## Expected files

| File | Planned content |
|---|---|
| `bhs.h` / `bhs.c` | Bearing Health Service definition using `BT_GATT_SERVICE_DEFINE`; characteristic value storage; notify helpers |
| `bhs_uuids.h` | 128-bit UUIDs for the service and characteristics (**TODO: allocate**; do not use placeholder UUIDs in released firmware) |
| `bhs_encode.c` | Encoding of health score, condition level, feature values, and status into the agreed little-endian wire formats |
| `bhs_control.c` | Handling of writes to Baseline Learning Control and Diagnostic Capture Control, including authorisation checks |
| `ble_adv.c` | Advertising data (device name, service UUID, optional condition level in manufacturer data), connectable advertising, reconnection behaviour |
| `ble_security.c` | Pairing and bonding using LE Secure Connections; authentication requirements for control characteristics |
| `ble_dis.c` | Device Information Service: manufacturer, model, firmware revision, hardware revision |
| `Kconfig` | Device name, notification interval, security level, maximum connections |
| `CMakeLists.txt` | Adds the sources to the build |

## Planned characteristics (summary)

Bearing Health Score, Condition Level, Vibration RMS, Vibration Crest Factor, Acoustic Energy,
Housing Temperature, RPM, Anomaly Score, Maintenance Recommendation, Device Status,
Baseline Learning Control, Diagnostic Capture Control.

Properties, formats, and update behaviour are defined in the service plan; UUID allocation is `TODO`.

## Planned implementation notes

- Peripheral role only; one central connection is sufficient for the first version.
- Notifications are rate-limited to the evaluation period; a client can subscribe to individual
  characteristics to reduce traffic.
- Writes to control characteristics require an encrypted and authenticated link; unauthenticated
  writes are rejected with an ATT error.
- Diagnostic capture streams a bounded feature history (not raw audio) through notifications on a
  dedicated characteristic, with flow control handled by the client.
- Bluetooth is a reporting and configuration channel only; nothing received over BLE can start, stop,
  or otherwise control the test rig motor.

## Current status

- No code exists. UUIDs have not been allocated. Wire formats are preliminary.

## TODO

- [ ] Allocate 128-bit UUIDs for the service and each characteristic and record them in the service plan.
- [ ] Finalise wire formats and units for each characteristic.
- [ ] Define the security model (pairing method, bonding, authorisation) and test it with a reference client.
- [ ] Implement the service and verify it with the planned dashboard (`tools/ble_dashboard/`).
