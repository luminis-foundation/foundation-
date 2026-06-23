# MycoSense Calibration Protocol — Planning Framework

> Status: Draft framework — final methods and thresholds are funding-dependent
> Last updated: 2026-06-23
> Requires: Carlos Garcia review before any calibration work begins
> File: research/protocols/calibration-protocol-framework.md

---

## Purpose

This document establishes a planning framework for calibrating MycoSense sensor nodes (ESP32-C6/S3 + ADS1115/ADS1299 electrode arrays) before and during field deployment. It is **not a final validated calibration protocol.** Final calibration methods, thresholds, and acceptance criteria cannot be determined until:

- Hardware procurement is complete and specific electrode/ADC models are confirmed
- Reference calibration equipment is acquired
- Field deployment begins (Step 3, Rowe, NM)
- Initial pilot sensor data is available for analysis

This framework guides procurement planning and pre-deployment preparation so calibration work can begin promptly once funding is secured.

---

## Why Funding Is Required

Final calibration protocols depend on resources that are not yet secured:

| Dependency | Reason |
|---|---|
| Reference signal source (e.g., precision signal generator) | Required to inject known signals and verify ADC response |
| Reference electrodes with known electrochemical potential | Required to establish baseline signal accuracy |
| Professional-grade ADC calibration equipment | Required to verify ADS1115/ADS1299 gain, offset, and linearity |
| Environmental monitoring equipment (temperature/humidity logger) | Required for temperature compensation characterization |
| Field deployment (Step 3) | Real-world soil and mycelium conditions cannot be fully simulated on a bench |
| Pilot sensor data | Threshold values must be derived from real data, not estimates |

Without these, all threshold values in this document are placeholders only.

---

## Hardware and Equipment Dependencies

| Component | Status | Calibration Role |
|---|---|---|
| ESP32-C6/S3 sensor nodes | ✅ Bench-tested | ADC timing, sampling rate |
| ADS1115 / ADS1299 ADC board | 📋 Model to be confirmed by Carlos | Gain, offset, noise floor |
| Electrode arrays | ❓ Model/spec not yet documented | Contact resistance, signal amplitude |
| Raspberry Pi gateway | ✅ Bench-tested | Signal aggregation, timestamp integrity |
| Precision reference signal source | ⬜ Not yet acquired | Required for ADC linearity verification |
| Reference electrode | ⬜ Not yet acquired | Required for electrochemical baseline |
| Multimeter / LCR meter | ⬜ Not yet acquired | Resistance and capacitance measurement |
| Temperature / humidity logger | ⬜ Not yet acquired | Environmental compensation data |

---

## Pre-Deployment Calibration Concept

The following steps represent the intended pre-deployment calibration approach. All thresholds are placeholders.

### Step 1 — ADC linearity verification
- Apply known reference voltages to ADC input channels across the expected input range
- Record output values; verify linearity within [TBD — placeholder: ±X% of full scale]
- Document gain and offset coefficients per channel per board

### Step 2 — Electrode contact resistance check
- Measure contact resistance between electrode pairs in a known substrate
- Record baseline resistance per channel
- Flag any electrode showing resistance above [TBD threshold] as suspect

### Step 3 — Noise floor measurement
- Record sensor output with no signal applied (shielded bench environment)
- Measure peak-to-peak noise amplitude per channel
- Establish noise baseline for future spike detection threshold derivation

### Step 4 — Reference signal injection test
- Apply a known periodic signal (sine or square wave, known amplitude and frequency)
- Verify recorded data matches applied signal within [TBD tolerance]
- Document per-channel deviation from expected

### Step 5 — Temperature sensitivity characterization
- If feasible pre-deployment: record sensor output at multiple ambient temperatures
- Document any temperature-dependent drift per channel
- Placeholder for temperature compensation coefficients if required

---

## Post-Deployment Drift-Check Concept

After sensors are deployed at the Rowe, NM site:

1. **Periodic drift checks** — Re-apply reference signal to at least one node per session; compare to pre-deployment baseline. Frequency: [TBD — proposed: weekly or per session]
2. **Electrode re-seating check** — Inspect physical contact and re-measure contact resistance after any site disturbance
3. **Cross-node consistency check** — Compare simultaneous readings across co-located nodes; flag divergence above [TBD threshold]
4. **Data continuity audit** — Review timestamp continuity after each session; flag gaps above [TBD duration]

---

## Placeholder Thresholds

All values below are placeholders to be replaced with empirically derived values after pilot data analysis and calibration equipment testing:

| Parameter | Placeholder | Source of Final Value |
|---|---|---|
| ADC linearity tolerance | TBD | Bench calibration with reference signal |
| Electrode contact resistance ceiling | TBD | Electrode procurement and testing |
| Noise floor ceiling | TBD | Bench noise floor measurement |
| Reference signal match tolerance | TBD | Signal injection test |
| Drift check interval | TBD | Step 3 deployment experience |
| Cross-node divergence threshold | TBD | Pilot data analysis |

---

## What Cannot Be Finalized Yet

- Any specific numeric calibration threshold
- Temperature compensation coefficients (require environmental data from the Rowe, NM site)
- Electrode-specific calibration curves (require electrode procurement and hands-on testing)
- Final calibration session frequency (requires pilot deployment experience)
- Calibration acceptance and rejection criteria for data quality decisions

---

## Validation Steps After Funding

Once funding is secured and equipment is procured:

1. Confirm electrode model and ADC board model with Carlos Garcia
2. Procure reference signal equipment, reference electrodes, and environmental logger
3. Complete pre-deployment calibration steps 1–5 with all nodes
4. Record all calibration data in private operational records controlled by authorized Foundation officers/researchers. A public-safe summary may be committed later if appropriate, but raw calibration records should not be committed to the public repository.
5. Replace all placeholder thresholds with empirically derived values
6. Conduct field calibration check during Step 3 deployment
7. Review pilot dataset against calibration baseline
8. Update this document with final validated thresholds
9. Carlos Garcia signs off on finalized protocol before Step 3 data is treated as valid

---

## Future Acceptance Criteria

A calibration session will be considered complete when:

- [ ] All ADC channels verified against reference signal within confirmed tolerance
- [ ] All electrodes pass contact resistance check
- [ ] Noise floor measurement recorded and within confirmed ceiling
- [ ] Calibration records retained privately with session ID and timestamp
- [ ] Carlos Garcia or designated researcher has reviewed and approved the calibration record

---

## Carlos Review Required

This framework requires review by Carlos Garcia before any calibration work begins. Specific thresholds, equipment models, and acceptance criteria are subject to change based on hardware procurement and bench testing results.

**Review status:** ⬜ Pending Carlos Garcia review
