# BLE Dashboard (`tools/ble_dashboard`)

**Status: Placeholder** - no dashboard exists yet.

## Purpose

This directory will contain the Bluetooth LE client used to interact with the BearingGuard AI device:
discovering and connecting to it, displaying the live Bearing Health Score and condition level, plotting
feature trends, showing maintenance recommendations and alerts, and controlling baseline learning and
diagnostic capture. The service it talks to is defined in
[`../../docs/bluetooth_service_plan.md`](../../docs/bluetooth_service_plan.md).

## Expected files

| File | Planned content |
|---|---|
| `dashboard.py` or `app/` | Desktop application (Python with a cross-platform BLE library and a simple GUI/plotting framework) or a web/mobile app - decision TODO |
| `bhs_client.py` | Client-side model of the Bearing Health Service: UUIDs, decoding of characteristic values, notification handling |
| `views/` | Live status view (score, level, LED-equivalent colour), trend view (per-feature history), alerts view, configuration view |
| `storage.py` | Local history logging (CSV/SQLite) of received values for trend display and later analysis |
| `requirements.txt` | Pinned dependencies |
| `screenshots/` (reference) | Screenshots belong in [`../../media/photos/`](../../media/photos/README.md) |

## Planned functionality

| Function | Description |
|---|---|
| Discovery and connection | Scan for the device by advertised service UUID or name; connect; optionally pair and bond |
| Live monitoring | Subscribe to notifications; show health score, condition level, anomaly score, and current feature values |
| Trend monitoring | Plot received values over time; highlight condition-level changes |
| Alerts | Visual and optional audible alert on Orange/Red; alert history |
| Baseline learning control | Start, monitor progress, and reset baseline learning (authenticated writes) |
| Diagnostic capture | Request and display a short feature history for engineering analysis |
| Export | Save history as CSV for offline analysis |

## Rules

- The dashboard is a monitoring and configuration client; it must never provide any control of the
  test-rig motor.
- Decoding must follow the wire formats in the service plan exactly; add a test for each characteristic.

## Current status

- No code; platform decision open; UUIDs not allocated.

## TODO

- [ ] Choose desktop Python versus web/mobile implementation.
- [ ] Implement `bhs_client.py` with decoding tests once UUIDs and formats are fixed.
- [ ] Implement live, trend, and alert views.
- [ ] Verify end-to-end against the firmware service.
