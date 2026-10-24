# Temperature Driver (`firmware/drivers/temperature`)

**Status: Placeholder** - no driver code exists yet.

## Purpose

This directory will contain the integration of the temperature sensing channel. Two temperature
measurements are planned:

1. **Bearing-housing temperature**, measured as close to the outer race as the housing allows.
2. **Ambient temperature**, measured away from the motor and bearing, used as the reference for the
   "temperature above ambient" and "temperature rise rate" features.

Both sensors may be digital (I2C) temperature sensors or NTC thermistors read through the SAADC. The
choice is **planned**, not decided.

## Expected files

| File | Planned content |
|---|---|
| `temp.h` | API: `temp_init()`, `temp_read_housing_c()`, `temp_read_ambient_c()`, `temp_get_rise_rate_c_per_min()` |
| `temp_digital.c` | Backend using the Zephyr sensor API for an I2C digital temperature sensor |
| `temp_ntc_adc.c` | Backend for NTC thermistors: SAADC read, voltage-divider conversion, beta or Steinhart-Hart equation, calibration offsets |
| `temp_filter.c` | Slow low-pass filtering and rise-rate estimation over a sliding window |
| `Kconfig` | Backend selection, sampling period, thermistor parameters (beta, nominal resistance, divider resistor) |
| `CMakeLists.txt` | Adds the selected backend to the build |

## Planned requirements

| Requirement | Preliminary target | Rationale |
|---|---|---|
| Sampling period | About 1 s (TODO) | Thermal time constants are long; low rate is sufficient |
| Resolution | Approximately 0.1 degC | Rise-rate estimation over minutes |
| Accuracy | Relative accuracy between housing and ambient sensors matters more than absolute accuracy | Features are differences and trends |
| Mounting | Good thermal contact with the housing (thermal paste or clamp), insulated from airflow | Reliable housing reading |

## Planned implementation notes

- The housekeeping thread samples both sensors periodically and publishes filtered values and the
  rise rate to the processing thread.
- Housing and ambient sensors should be the same type so that their offset can be calibrated by
  reading both at thermal equilibrium before a run.
- Implausible readings (open or shorted thermistor, I2C error) raise a sensor fault.

## Current status

- Sensor type not yet selected; no code written.

## TODO

- [ ] Select digital sensor or NTC approach; document the trade-off.
- [ ] Define the mounting method together with `mechanical/sensor_mounts/`.
- [ ] Define the rise-rate window and filtering.
- [ ] Implement the backend, calibration procedure, and fault detection.
