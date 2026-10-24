# Board Configuration (`firmware/boards`)

**Status: Placeholder** - no devicetree overlays or Kconfig fragments exist yet.

## Purpose

This directory will hold board-specific configuration for the Nordic nRF54LM20 DK: devicetree overlays
that describe how the sensors, RPM input, and RGB LED are wired to the development kit, and Kconfig
fragments that enable the corresponding Zephyr drivers.

Keeping wiring in overlays (rather than in application code) follows Zephyr conventions and makes it
possible to support alternative sensor choices or a future custom sensor carrier board without
changing the application.

## Expected files

| File | Planned content |
|---|---|
| `nrf54lm20dk_nrf54lm20a_cpuapp.overlay` | Pin assignments and device nodes: SPI (or I2C) accelerometer with interrupt line, PDM microphone (or SAADC channel for a piezo sensor), I2C digital temperature sensor(s) or SAADC channels for NTC thermistors, GPIO input for the RPM sensor, PWM channels for the RGB LED |
| `nrf54lm20dk_nrf54lm20a_cpuapp.conf` | Kconfig fragment enabling SPI/I2C/PDM/ADC/PWM/GPIO drivers and the Zephyr sensor subsystem for this board |
| `pinctrl.dtsi` (optional) | Pin control groups for the peripherals used by the sensors |
| `README.md` | This file, updated with a pin-assignment table once wiring is final |

The board target name must be confirmed against the pinned nRF Connect SDK release; the file names
above assume `nrf54lm20dk/nrf54lm20a/cpuapp`.

## Planned pin assignment table

The table will be completed after the sensors are selected and the DK pinout has been checked against
the official DK documentation. Pin numbers must not be guessed.

| Function | Interface | DK header / pin | Notes |
|---|---|---|---|
| Accelerometer data | SPI (preferred) or I2C | TODO | SPI preferred for high output data rates and FIFO reads |
| Accelerometer interrupt | GPIO | TODO | FIFO watermark / data-ready |
| MEMS microphone | PDM (CLK, DIN) | TODO | Alternative: piezo contact sensor on a SAADC channel |
| Housing temperature | I2C or SAADC | TODO | Digital sensor or NTC thermistor |
| Ambient temperature | I2C or SAADC | TODO | Reference for temperature-above-ambient feature |
| RPM sensor | GPIO (interrupt / timer capture) | TODO | Hall or optical; open-collector output may need a pull-up |
| RGB LED | PWM x3 or GPIO x3 | TODO | Could use DK on-board LEDs for early bring-up |
| Emergency stop status (optional) | GPIO input | TODO | Read-only monitoring of E-stop state; never used for control |

## Planned implementation notes

- Use devicetree `compatible` bindings provided by Zephyr for the chosen sensors where available;
  otherwise write a minimal out-of-tree driver (see [`../drivers/`](../drivers/)).
- Place board-level electrical details (pull-ups, level shifting, decoupling) in
  [`../../hardware/wiring/README.md`](../../hardware/wiring/README.md), and keep this directory focused on
  the software view of the wiring.
- Keep a single overlay per board target; alternative sensor options should use separate, clearly named
  overlays (for example `*_piezo.overlay`) selected with `-DEXTRA_DTC_OVERLAY_FILE`.

## Current status

- Sensors have not been selected; no pin has been assigned.
- The DK has not been acquired, so no pinout has been verified.

## TODO

- [ ] Select sensors and confirm interface types (SPI/I2C/PDM/ADC).
- [ ] Verify the nRF54LM20 DK pinout and peripheral availability in the pinned SDK release.
- [ ] Write the overlay and Kconfig fragment; fill in the pin-assignment table.
- [ ] Cross-check the overlay against the wiring documentation in `hardware/wiring/`.
