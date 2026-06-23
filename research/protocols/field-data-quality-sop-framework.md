# MycoSense Field Data Quality SOP — Planning Framework

> Status: Draft framework — final thresholds are funding-dependent and cannot be set until pilot data is available
> Last updated: 2026-06-23
> Requires: Carlos Garcia review before first deployment session
> File: research/protocols/field-data-quality-sop-framework.md

---

## Purpose

This document establishes a planning framework for defining what constitutes valid MycoSense sensor data during and after field deployment. It is **not a final validated SOP.** Final quality thresholds and acceptance criteria cannot be determined until:

- Step 3 (on-site prototype deployment, Rowe, NM) is complete
- Calibration has been performed (see `research/protocols/calibration-protocol-framework.md`)
- Initial pilot sensor data is available for review
- Environmental baseline for the Rowe, NM site is established

This framework ensures data collection is structured correctly from the first deployment session so that quality review can begin immediately once pilot data exists.

---

## What "Valid Data" Should Eventually Mean

A valid MycoSense data record should eventually be defined as a reading that:

- Has a verified timestamp within acceptable drift of NTP reference
- Has associated metadata meeting all required fields (see Metadata Requirements below)
- Was collected during a period when calibration was confirmed valid for that node
- Falls within the calibrated signal range for the relevant electrode channel
- Has no flagged artifact or noise event at that timestamp
- Has an associated field notes record for the session

Final numeric definitions for each criterion require pilot data analysis and Carlos Garcia approval.

---

## Why Final Thresholds Cannot Be Set Yet

| Reason | Explanation |
|---|---|
| No real field data exists | Thresholds must be empirically derived, not estimated from bench tests |
| Calibration not yet complete | Signal range limits depend on calibration output from actual hardware |
| Environmental baseline unknown | Rowe, NM soil and mycelium conditions affect what constitutes a normal reading |
| Electrode model not yet confirmed | Different electrode designs have different noise and impedance characteristics |
| Deployment experience not yet available | Artifact patterns and drift rates require real deployment to characterize |

---

## Timestamp and NTP Requirements

- All sensor nodes must synchronize via NTP before each deployment session
- Maximum acceptable NTP drift: [TBD — placeholder: ≤ 1 second relative to NTP reference]
- If NTP sync fails at session start: flag all data from that session as `timestamp_quality: UNVERIFIED`; do not delete
- Timestamp format: ISO 8601 UTC (e.g., `2026-07-01T14:32:00Z`)
- Timestamp must be recorded in SQLite database on Pi and included in provenance hash

---

## Metadata Requirements

Each deployment session must capture the following fields before data is considered complete:

| Field | Required | Notes |
|---|---|---|
| Session ID | Yes | UUID generated at session start |
| Node ID | Yes | ESP32 MAC address or assigned node name |
| GPS coordinates | Yes (after Step 3) | Null values not acceptable for published data |
| Site name | Yes | Canonical site name from site registry |
| Deployment start (UTC) | Yes | ISO 8601 |
| Deployment end (UTC) | Yes | ISO 8601 |
| Researcher initials | Yes | Person who started/ended session |
| Calibration record ID | Yes | Links session to pre-deployment calibration record |
| Ambient temperature at start | Recommended | °C if available |
| Weather conditions | Recommended | Brief text note |
| Electrode contact resistance at start | Recommended | Per channel |
| Anomalies observed | Recommended | Field notes on any unusual conditions |

Sessions with missing required fields are not eligible for public data release until fields are completed.

---

## Missing Data Concepts

- **Short gaps (< [TBD duration]):** Flag in database with `data_quality: FLAGGED`; retain in dataset
- **Long gaps (> [TBD duration]):** Investigate cause; if cause unknown, mark session invalid and document reason
- **Complete session failure:** Document in field notes; do not publish data from that session
- **NTP sync failure:** Flag all data from that session as `timestamp_quality: UNVERIFIED`
- **Incomplete metadata:** Session data is held from publication until all required fields are complete

Gap duration thresholds are placeholders and will be set after pilot data review.

---

## Noise and Artifact Review Concepts

- **Spike detection:** Readings exceeding [TBD — calibration-derived ceiling] are flagged as suspect
- **Flat-line detection:** Extended periods with no signal variation suggest electrode contact failure or data pipeline issue
- **60 Hz interference:** May appear in electrode signals near AC power sources; document and flag; do not silently discard
- **Cross-channel artifact:** Simultaneous identical readings across multiple independent channels suggest a wiring, grounding, or firmware artifact
- **Artifact disposition:** Artifacts are flagged, not deleted — retain in raw dataset with quality flags; do not alter raw records

All specific thresholds are placeholders until derived from pilot data.

---

## Field Notes Template

For each deployment session, the researcher records:

```
Session ID:        [UUID]
Date:              [YYYY-MM-DD]
Location:          [Site name — e.g., Rowe NM Foundation site]
Nodes deployed:    [List node IDs]
Start time (UTC):  [ISO 8601]
End time (UTC):    [ISO 8601]
NTP sync status:   [Confirmed / Failed / Not checked]
Calibration check: [Completed — record ID: XXXX / Not completed — reason: ]
Electrode contact resistance: [Per channel, or N/A]
Weather at start:  [Brief description]
Weather at end:    [Brief description]
Anomalies:         [Description or None]
Hardware issues:   [Description or None]
Researcher:        [Initials]
Notes:             [Free text]
```

---

## Pilot Data Review Process

After Step 3 deployment generates the first real data:

1. Export raw SQLite data and inspect for timestamp continuity and completeness
2. Review all flagged values and artifact annotations
3. Check metadata completeness across all sessions
4. Calculate baseline signal statistics per channel (mean, variance, noise floor)
5. Identify data that clearly cannot be salvaged; document reason in session record
6. Derive initial threshold candidates from pilot data distribution
7. Propose threshold values to Carlos Garcia for review
8. Carlos Garcia approves initial thresholds; update this document with approved values
9. No data from Step 3 pilot is published until quality review is complete and Carlos Garcia approves release

---

## Future Threshold-Setting Process

1. Collect minimum [TBD — proposed: 2 weeks] of pilot deployment data
2. Analyze noise floor distribution per channel
3. Analyze signal event amplitude and duration distribution
4. Propose thresholds based on distribution analysis (e.g., 99th percentile noise ceiling)
5. Review proposed thresholds against published literature on electrode biosensor data quality where available
6. Carlos Garcia approves final thresholds
7. Final thresholds added to this document and to `research/protocols/calibration-protocol-framework.md`
8. This framework is superseded by the finalized `research/protocols/field-data-quality-sop.md` once thresholds are confirmed

---

## What Cannot Be Finalized Yet

- Any specific numeric quality threshold
- Acceptable NTP drift tolerance in field conditions
- Maximum acceptable gap duration
- Spike and noise ceiling values
- Final artifact disposition rules beyond the conceptual guidance above
- Data publication readiness criteria (beyond structural requirements)

---

## Carlos Review Required

This framework requires review and approval by Carlos Garcia before the first deployment session. All placeholder values must be replaced with empirically derived values after pilot data is collected.

**Review status:** ⬜ Pending Carlos Garcia review
