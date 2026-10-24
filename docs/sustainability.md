# Sustainability

**Status: Draft.** This document describes the **expected** sustainability impact of the BearingGuard AI
concept and how it could be assessed. No impact has been measured or demonstrated.

## 1. Why predictive maintenance matters for sustainability

Rotating machinery - motors, pumps, fans, compressors, conveyors - consumes a large share of industrial
electricity, and bearings are among its most frequent failure points. Maintenance strategy determines
how much material, energy, and production is wasted around those failures:

| Strategy | Typical waste |
|---|---|
| Run-to-failure | Collateral damage (shafts, housings, motors), unplanned downtime, scrap production, emergency logistics |
| Fixed-interval replacement | Healthy bearings discarded early; unnecessary labour and parts; failures between intervals still occur |
| Condition-based (predictive) | Replacement when degradation actually begins; planned downtime; reduced collateral damage |

## 2. Expected contributions of BearingGuard AI

| Area | Expected effect | Mechanism |
|---|---|---|
| Material use | Fewer bearings replaced prematurely; fewer shafts, housings, and motors damaged by bearing failure | Early deviation detection and trend monitoring |
| Energy use | Degraded bearings increase friction losses; earlier intervention keeps drive trains efficient | Detection of friction-related temperature and acoustic changes |
| Production waste | Fewer unplanned stoppages that spoil in-process material | Planned maintenance windows triggered by Orange/Red levels |
| Accessibility | Wireless, self-learning, low-cost monitoring for machines that are not instrumented today | BLE node without infrastructure, baseline learning instead of expert setup |
| Data minimisation | Raw signals stay on the device; only compact features and scores are transmitted | On-device Edge AI |

These are **expected** benefits of the approach in general; the demonstrator will not quantify them for
a real installation.

## 3. Footprint of the demonstrator itself

- **Small electronics**: one development kit, a handful of sensors, an LED.
- **Low power**: Edge AI inference at a slow evaluation period on a low-power SoC; BLE instead of
  continuous streaming. Power will be measured for information using the DK's current-measurement
  pins (planned).
- **Reusable test rig**: bearings are the only consumable; the rig and sensors are reused for all
  campaigns.
- **Responsible test specimens**: pre-worn bearings are created by documented, bounded procedures or
  sourced from already-worn stock; bearings are recycled as metal scrap after use.
- **No cloud dependency**: no servers are required to run the device.

## 4. How impact could be assessed later

| Indicator | Method (planned, optional) |
|---|---|
| Device energy consumption | Current measurement on the DK during monitoring and notification |
| Potential bearing-life extension | Literature comparison of fixed-interval vs. condition-based replacement for the chosen bearing class |
| Detection lead time | Detection delay measured on the rig for each controlled condition (from the evaluation protocol) |
| Avoided collateral damage | Qualitative: which secondary failures the detected conditions would precede in field equipment |

## 5. Limits of the sustainability claim

- Benefits depend on operators acting on the recommendations.
- Transfer from a laboratory rig to real machinery is unproven in this project.
- Manufacturing footprint of sensors and electronics is not accounted for.
- The project will report expected benefits as expectations, not as achieved results.

## TODO

- [ ] Measure device power consumption once firmware runs on the DK.
- [ ] Add references to published studies on predictive-maintenance benefits (with citations).
- [ ] Decide which optional assessments are within scope.
