# MycoSense Data Management and Security — Brainstorm Document

> Status: Brainstorming / design document — not a final policy
> Last updated: 2026-06-23
> For: Carlos Garcia review and Board decision-making
> File: research/data-management-security-brainstorm.md

This document is a design brainstorm to inform a future airtight data security and data management policy for Luminis Foundation / MycoSense. It is not a policy. All items marked **[Carlos decision]** require explicit founder or Board confirmation before being committed to policy.

---

## Data Categories

### Raw vs Processed Data

| Type | Description | Examples |
|---|---|---|
| Raw sensor data | Direct ADC readings from ESP32 to Pi gateway | SQLite rows: timestamp, node_id, channel, raw_value |
| Calibrated data | Raw readings converted using calibration coefficients | Voltage or resistance units |
| Annotated data | Calibrated data with quality flags and metadata attached | quality_flag, artifact_note |
| Processed / analyzed data | Spike detection results, event classifications, derived metrics | spike_events.csv, daily_means.csv |
| Published dataset | Curated, quality-reviewed subset released publicly | Zenodo release |

**Design question:** Should raw and processed data be stored in the same SQLite database or separate stores? **[Carlos decision]**

---

### Public Data vs Private Operational Data

| Data Type | Public? | Notes |
|---|---|---|
| Published sensor dataset (Zenodo) | Yes — after quality review and Carlos approval | |
| Dashboard visualization data | Yes — simulated/mock only currently | Real sensor data not publicly live yet |
| Calibration records | No — private operational | Contain hardware-specific coefficients |
| Field session notes | No — private | May contain sensitive site observations |
| Raw Pi SQLite database | No — private operational | Unreviewed; too large for direct public release |
| Node firmware configs / NVS | No — private | Contain WiFi credentials and bearer tokens |
| Provenance hashes (SHA-256) | Yes — public | Hash verifiable without revealing underlying data |

---

### Sensitive Site-Location Data

- GPS coordinates of deployed nodes should be treated as operationally sensitive until the Foundation determines its disclosure policy
- Exact electrode burial locations within a site may be ecologically or legally sensitive depending on land access agreements
- Published datasets may use approximate geographic descriptions (e.g., county name or site name) rather than precise GPS coordinates until a disclosure decision is made
- **[Carlos decision]** What level of geographic precision is acceptable in public data releases?

---

### Device Logs

- The Pi SQLite database accumulates all raw session data; log rotation is required (see `docs/FIELD_DEPLOYMENT_SECURITY.md`)
- Raw logs should not be committed to any public repository
- **[Carlos decision]** Target raw data retention period? Proposed: retain all raw logs for a minimum of 2 years after collection date

---

### Metadata

- Metadata schema must be defined before first data collection (see `research/protocols/field-data-quality-sop-framework.md`)
- Metadata should be stored alongside data in SQLite and exported with each published dataset
- Field notes may contain sensitive site observations — review for sensitive content before including in public releases

---

## Access Roles

| Role | Proposed Access Level | Data Access |
|---|---|---|
| Carlos Garcia (President / Research Director) | Full | All data categories |
| Adam Kimble (Treasurer) | Financial records only | No sensor or field data |
| Guillermo Martin (Secretary) | Board records only | No sensor or field data |
| Sterling VanKaujk (VP) | **[Carlos decision]** | **[Carlos decision]** |
| AI agents (Claude / Lumen) | Read-only for analysis on public repo content | No raw private data; no private records |
| Future collaborators / researchers | **[Carlos decision]** | Define in contributor data access agreement |

**Design recommendation:** Apply the principle of least privilege — each role accesses only what is needed for their function.

---

## Storage Locations

| Data Type | Proposed Primary Location | Proposed Backup |
|---|---|---|
| Raw Pi SQLite database | Pi local storage (on-site, Rowe NM) | External drive at Foundation office |
| Calibration records | Private officer-controlled file store | Encrypted cloud backup |
| Field notes | Private officer-controlled file store | Physical printed copy retained by Carlos |
| Published dataset | Zenodo (DOI-anchored, immutable) | GitHub Releases or Foundation website mirror |
| Analysis scripts | GitHub (public or private repo — **[Carlos decision]**) | Local copy |
| Provenance hashes | GitHub public repo (already implemented) | Zenodo metadata |

**[Carlos decision]** What cloud backup service should the Foundation use? (Options: encrypted Dropbox Business, Backblaze B2, AWS S3 with server-side encryption, or similar. The Foundation must control the account.)

---

## Backup Strategy

| Data Type | Proposed Frequency | Proposed Method |
|---|---|---|
| Pi SQLite (raw) | After each deployment session | Manual rsync to external drive; verify SHA-256 |
| Calibration records | After each calibration session | Same |
| Processed / analyzed data | After each analysis run | Same |
| Published dataset | Permanent — Zenodo DOI is immutable | No further backup needed |

**Proposed process:**
1. End of each field session: rsync Pi SQLite to designated external drive
2. Verify backup integrity by comparing SHA-256 hashes of source and copy
3. Log backup event in field session notes (session ID, hash, date)
4. Monthly: copy external drive backup to encrypted cloud backup location

---

## Encryption Recommendations

### Data in Transit

| Channel | Current State | Recommendation |
|---|---|---|
| ESP32 → Pi (MQTT) | Cleartext over LAN | Add TLS in Phase 2 (see `docs/FIELD_DEPLOYMENT_SECURITY.md`) |
| Pi → external drive (backup) | Unencrypted | Encrypt drive before backup |
| Pi → researcher laptop | SSH | Already secure |
| Cloud backup | — | Client-side encryption before upload |

### Data at Rest

| Location | Recommendation |
|---|---|
| Pi SQLite database | Encrypt the storage partition (LUKS) or use SQLCipher — **[Carlos decision]** |
| External drive backup | Encrypt drive (LUKS on Linux, BitLocker on Windows, FileVault on macOS) |
| Cloud backup | Client-side AES-256 encryption before upload |
| Field notes (digital) | Encrypted folder or encrypted cloud storage |

---

## Data Integrity and Hashes

- SHA-256 provenance hashing is already implemented in `src/utils/provenanceHash.js`
- Each published dataset should have a SHA-256 hash recorded in the Zenodo release and in the public repo
- **[Carlos decision]** Should interim processed datasets also be hashed before archiving?
- Recommendation: maintain a `CHECKSUMS.md` file per data release listing file name, size, and SHA-256 hash

---

## Audit Trail

- Every data modification should be logged with: timestamp, operator ID, action taken, and brief description
- Pi SQLite raw data should be append-only — do not edit raw records in place; add corrected records with reason codes and links to originals
- Calibration record edits should be logged with reason
- Published dataset versions on Zenodo are immutable; corrections should be new DOI versions with clear versioning notes
- **[Carlos decision]** Should the Foundation maintain a separate offline audit log beyond Git commit history?

---

## Public Release Criteria

Before any dataset is published to Zenodo or any public platform:

- [ ] Quality review complete per final `research/protocols/field-data-quality-sop.md`
- [ ] Calibration records confirm sensor validity for the period covered
- [ ] All required metadata fields populated
- [ ] GPS / location disclosure reviewed and explicitly approved by Carlos Garcia
- [ ] SHA-256 hash computed and recorded
- [ ] Carlos Garcia approves release in writing (email retained in private records)
- [ ] Zenodo submission uses correct author names
- [ ] License confirmed as CC-BY-4.0 (or Foundation's chosen open data license)
- [ ] No device credentials, node tokens, or operational logs included in release files

---

## Zenodo Release Process

1. Prepare dataset in agreed format (CSV + JSON metadata minimum)
2. Compute and record SHA-256 hash
3. Review dataset for sensitive location data; apply approved precision level
4. Review author list for correct name spellings
5. Prepare Zenodo metadata (title, authors, description, keywords, license, related identifiers)
6. Carlos Garcia reviews and approves full submission package
7. Upload to Zenodo; record resulting DOI in `governance/milestones.md` and `research/publications/`
8. Announce through public-facing channels (website, GitHub README) after DOI is confirmed stable

---

## What Must Stay Private

Do not commit, publish, or share publicly:

- Pi bearer token, WiFi SSID/password, or NVS stored credentials
- Raw unreviewed SQLite database dumps
- GPS coordinates before explicit location disclosure decision
- Field session notes containing sensitive site observations
- Calibration records (operational; not public data)
- Any financial records (banking details, EIN, Pay.gov receipts, receipts)
- Private correspondence or legal documents
- Personal home addresses beyond the already-public registered office

---

## Open Questions for Carlos

1. What cloud backup service should the Foundation use for raw field data?
2. What level of GPS coordinate precision is acceptable in public dataset releases?
3. Should Sterling VanKaujk have access to raw sensor data for research purposes?
4. Should future collaborators/researchers sign a data access agreement before accessing unpublished datasets?
5. What is the target raw data retention period? (Proposed minimum: 2 years)
6. Should the Pi SQLite database be encrypted at rest (LUKS or SQLCipher)?
7. Should there be a named data steward role separate from the Research Director?
8. Should analysis scripts be in a public or private GitHub repository?
9. Should interim processed datasets be hashed and logged before archiving?
10. Should the Foundation maintain a separate offline audit log beyond Git commit history?

---

## Recommended Final Policy Structure

When this brainstorm is ready to be converted to a formal policy, the final document should include:

1. **Data governance roles** — who owns, who can access, who can approve public release
2. **Data classification** — public / private / sensitive site / operational
3. **Storage and backup requirements** — locations, frequencies, verification process
4. **Encryption requirements** — at rest and in transit for each data type
5. **Integrity verification** — SHA-256 hashing process and checksum records
6. **Audit trail requirements** — logging requirements, append-only raw records
7. **Public release process** — checklist, approval workflow, Zenodo submission steps
8. **Retention and deletion** — retention periods, secure deletion process
9. **Breach response** — actions if data is accidentally exposed
10. **Annual review** — who reviews, when, what triggers a policy revision
