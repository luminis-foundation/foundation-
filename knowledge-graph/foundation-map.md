# Luminis Foundation — Institutional Map

> Last updated: 2026-06-23
> Maintained by: Carlos Garcia (President) / Board of Directors
> Status legend: ✅ Complete | 🔄 In progress | 📋 Planned | ⬜ Future | ❓ Unknown | ⚠️ Gap

---

## 1. Legal Entity

| Field | Value | Source | Notes |
|---|---|---|---|
| Legal name | Luminis Foundation | NM SOS filings | |
| Entity type | Domestic Nonprofit Corporation | NM SOS | |
| State | New Mexico | NM SOS | |
| Entity ID | 0008089293 | `governance/mission.md`, NM SOS | Already public |
| Formation date | March 16, 2026 | `governance/milestones.md` | |
| Registered office | 133 Frontage Rd 2116, Rowe, NM 87562 | `governance/mission.md` | Public registered address |
| Mailing address | P.O. Box 86, Rowe, NM 87562 | `governance/mission.md` | Public mailing address |
| Governing law | Chapter 53, Article 8 NMSA 1978 (NM Nonprofit Corporation Act) | `governance/mission.md` | |
| EIN | Not included in public records | — | Keep private; do not commit |
| Banking | Not yet established | `governance/roadmap.md` (open item) | ⚠️ Gap |

---

## 2. Governance

| Document | Status | Source | Owner | Next Action |
|---|---|---|---|---|
| Certificate of Incorporation | ✅ Issued Mar 16, 2026 | `governance/milestones.md` | Carlos Garcia | Keep in private records |
| Bylaws | ✅ Adopted Mar 19, 2026 | `governance/milestones.md` | Board | Consider redacted public summary |
| Conflict-of-interest policy | ✅ Adopted Mar 19, 2026 | `governance/milestones.md` | Board | Consider committing redacted version |
| NM Initial Report | ✅ Filed May 7, 2026 | `governance/milestones.md` | Guillermo Martin | Annual report due each year |
| Form 1023-EZ | ✅ Filed Jun 9, 2026 | `governance/milestones.md` | Carlos Garcia | Await IRS determination letter |
| NM-COROS charitable registration | ⬜ Not yet filed | `governance/roadmap.md` (open) | Carlos Garcia | File after 501(c)(3) determination |
| Board minutes | ⚠️ Not in repo | `governance/board-minutes/` is empty | Board Secretary | Document organizational meeting; store privately |
| Annual reports | ⚠️ Not yet needed | `governance/annual-reports/` empty | Guillermo Martin | Required each year to NM SOS |
| Banking infrastructure | ⚠️ Not yet established | Open roadmap item | Adam Kimble | Establish checking + fiscal controls |
| 501(c)(3) determination letter | 📋 Pending IRS | Filed Jun 9, 2026 | IRS / Carlos | Await; do not claim exemption until received |

---

## 3. Board and Officers

| Name | Role | Contact | Status | Notes |
|---|---|---|---|---|
| Carlos Garcia | President, Founder, Research Director | carlos@luminisfoundationresearch.org | ✅ Active | Primary technical and research lead; single point of failure risk |
| Guillermo Martin | Secretary | — | ✅ Active | Board minutes and filing responsibilities |
| Adam Kimble | Treasurer | adam@luminisfoundationresearch.org | ✅ Active | Financial oversight; banking not yet established |
| Sterling VanKuijk | Vice President | sterling@luminisfoundationresearch.org | ✅ Active | ⚠️ Name spelled "VanKaujk" in some older documents — verify correct spelling |

**Board gap notes:**
- No succession plan documented for any officer
- No quorum or meeting cadence policy visible in public records
- Board size (4) is at lower end for sustained governance
- No independent director(s) on record

---

## 4. Public Websites

| Site | URL | Status | Owner | Notes |
|---|---|---|---|---|
| Foundation website | luminisfoundationresearch.org | ✅ Live | Carlos Garcia | Single-page HTML; good CSP headers; accurate status language |
| MycoSense demo | mycosense.vercel.app | ✅ Live | Carlos Garcia | Simulated/mock data; correctly labeled in UI and README |
| GitHub org | github.com/luminis-foundation | ✅ Live | Carlos Garcia | Public-facing org; 5 repos |

**Website audit notes:**
- 501(c)(3) language on website: "Filed — awaiting IRS determination" ✅ Correct
- MycoSense status on website: "Prototype planned" ✅ Correct
- Simulated data disclaimer: Present ✅
- No CSP issues noted; strict `default-src 'none'` base ✅

---

## 5. Repositories

| Repository | Purpose | Status | Key Files | Gaps |
|---|---|---|---|---|
| `luminis-foundation/foundation` | Institutional records (this repo) | ✅ Active | governance/, research/, knowledge-graph/, risk/, operations/ | Board minutes, annual reports, bylaws text absent |
| `luminis-foundation/mycosense` | MycoSense platform (dashboard + firmware + Pi) | ✅ Active | README.md, FIELD_STATUS.md, SECURITY.md, docs/ | Field protocols, calibration docs absent |
| `luminis-foundation/luminis-foundation-open` | Public research + community | ✅ Active | governance/, research/, field-deployment/ | field-deployment/protocols/, field-deployment/site-specs/ empty; publications/ empty |
| `luminis-foundation/luminis-foundation.github.io` | Foundation website source | ✅ Active | index.html, luminis-banner.jpg, luminis-logo.jpg | No privacy policy; no contact form |
| `luminis-foundation/security-hardening` | Security documentation | Unknown | — | Not yet inspected in this audit |

**Repo audit notes:**
- `luminis-foundation-open` README: "Field deployment (Pecos watershed) — ✅ Building" ⚠️ Potentially misleading; should be "in development / bench-tested; on-site prototype planned"
- `luminis-foundation-open` README: "organized under IRC §501(c)(3)" ⚠️ Could be misread as confirmed status; should clarify "applied for recognition"
- Name spelling inconsistency: "VanKuijk" (website) vs "VanKaujk" (milestones, open repo) — unresolved

---

## 6. Research Programs

| Program | Description | Status | Publication | Next Milestone |
|---|---|---|---|---|
| Fungal electrophysiology & mycelial biosensing | Electrode sensing of mycelial electrical signals; spike detection; EI/EC profiling | 🔄 Software built; no field data | DOI 10.5281/zenodo.20143391 | Step 3: on-site prototype deployment |
| Mycelium-inspired decentralized AI | Network topology research inspired by mycorrhizal architecture | 🔄 Theoretical framework published | DOI 10.5281/zenodo.20143391 | TinyML classifier design |
| TinyML and edge-deployed sensor networks | Quantized ML models for ESP32 deployment | 📋 Planned | — | Firmware v2 with TinyML |
| Privacy-preserving federated learning | Federated model-update protocol with biological threshold-gating | 📋 Planned | DOI 10.5281/zenodo.20143391 (Section 10.5 framework) | Protocol specification |
| Bio-hybrid plant–fungal–AI systems | Integration of living systems with AI decision-making | 📋 Theoretical | DOI 10.5281/zenodo.20143391 | First field trial |

---

## 7. MycoSense — Detailed Status

| Component | Description | Status | Location |
|---|---|---|---|
| React 18 dashboard | Browser-based biosensor visualization | ✅ Deployed (mock data) | mycosense.vercel.app |
| Mock data generator | Procedural simulated sensor data | ✅ Complete | `src/data/mockSensorData.js` |
| ESP32-C6/S3 firmware | Sensor node firmware (Arduino/C++) | ✅ Bench-tested | `esp32-firmware/` |
| Raspberry Pi gateway | FastAPI + SQLite data coordinator | ✅ Bench-tested | `pi-server/` |
| Full E2E stack (ESP32 → Pi → Dashboard) | Complete data pipeline | ✅ Bench-validated | — |
| Calibration system | CalibrationPanel.jsx; calibration hooks | ✅ Built (not field-calibrated) | `src/components/CalibrationPanel.jsx` |
| Data export + provenance hashing | SHA-256 provenance; CSV export | ✅ Built | `src/utils/provenanceHash.js` |
| Field map / zone layout | Spatial zone layout definitions | ✅ Built (mock zones) | `src/data/fieldLayout.js` |
| GPS coordinates | Node position recording | ⚠️ Not yet set — null values | `FIELD_STATUS.md` |
| Solar power + outdoor runtime | Continuous unattended operation | ⬜ Not validated | — |
| Weatherproofing | Outdoor enclosure validation | ⬜ Not validated | — |
| MQTT TLS (production) | Encrypted field MQTT | ⬜ Planned for Phase 2 | `docs/FIELD_DEPLOYMENT_SECURITY.md` |
| OTA firmware updates | Automated firmware delivery | ⬜ Planned | — |
| Data retention policy | Long-term log management | ⬜ Not defined | — |
| On-site prototype deployment (Step 3) | Rowe, NM Foundation office site | 📋 Planned | `FIELD_STATUS.md` |
| Validated local field dataset (Step 4) | First real sensor dataset | ⬜ Future | — |
| Pecos watershed deployment (Step 5) | Broader deployment + public data | ⬜ Future | — |

---

## 8. Legal / Compliance Records

| Record | Status | Date | Notes |
|---|---|---|---|
| NM Certificate of Incorporation | ✅ Issued | Mar 16, 2026 | Private — do not commit PDF |
| Bylaws | ✅ Adopted by Board | Mar 19, 2026 | Private — consider redacted summary |
| Conflict-of-interest policy | ✅ Adopted by Board | Mar 19, 2026 | Private — consider redacted version |
| NM Initial Report | ✅ Filed | May 7, 2026 | Adds Sterling VanKuijk as VP |
| Form 1023-EZ | ✅ Filed | Jun 9, 2026 | $275 user fee paid Jun 10; IRS determination pending |
| NM-COROS registration | ⬜ Not filed | — | Required if soliciting in NM; file after IRS determination |
| Federal EIN | ❓ Not in public records | — | Do not commit — keep private |
| Annual report (NM SOS) | ⬜ Not yet due | — | Required annually; first due 2027 |
| IRS 990 / 990-N | ⬜ Not yet filed | — | Required annually after tax year end |

---

## 9. Funding and Grant Status

| Funder | Program | Amount | Status | Submitted | Notes |
|---|---|---|---|---|---|
| Awesome Foundation | Conservation & Climate | $1,000 | Pending | Jun 10, 2026 | Microgrant; does not require 501(c)(3) |

**Funding gaps:**
- No operational budget documented
- No financial reserves
- Banking not yet established
- No major grant strategy documented
- No earned revenue model
- No donor acknowledgment process documented

---

## 10. Publications

| Title | Authors | Year | DOI | License | Status |
|---|---|---|---|---|---|
| Bridging Mycelium-Inspired Decentralized Computing and Symbiotic Plant–Fungal–AI Bio-Hybrid Systems in Northern New Mexico's High-Desert Ecosystems | Garcia, Kimble, Martin, VanKuijk | 2026 | [10.5281/zenodo.20143391](https://doi.org/10.5281/zenodo.20143391) | CC-BY-4.0 | Preprint (Zenodo) |

**Publication gaps:**
- No follow-on empirical publications
- No peer-reviewed journal placement recorded
- No conference presentations recorded
- `research/publications/` directory is empty (records not yet added)
- `luminis-foundation-open/research/publications/` directory also empty

---

## 11. Prototype Hardware

| Asset | Description | Status | Location | Notes |
|---|---|---|---|---|
| ESP32-C6/S3 nodes | Sensor node microcontrollers | ✅ Bench-tested | Foundation office / Rowe, NM | WiFi + MQTT; NVS credential storage |
| Raspberry Pi (gateway) | Local data coordinator | ✅ Bench-tested | Foundation office / Rowe, NM | FastAPI + SQLite; LAN-only |
| Electrode arrays | Soil/mycelial contact electrodes | ❓ Status unknown | — | Specific model/spec not in public docs |
| ADS1115/ADS1299 ADC | Signal acquisition boards | 📋 Specified in roadmap | — | Referenced in governance/roadmap.md |
| Solar power system | Off-grid outdoor power | ⬜ Not yet validated | — | Required for Step 3 |
| Outdoor enclosures | Weatherproofing for nodes | ⬜ Not yet validated | — | Required for Step 3 |

---

## 12. Data / Dataset Status

| Dataset | Status | Notes |
|---|---|---|
| Simulated dashboard data | ✅ Procedurally generated | `src/data/mockSensorData.js` — not real sensor data |
| Bench-test readings | ❓ Unknown | May exist locally; not in public repo |
| On-site prototype data | ⬜ Future | Requires Step 3 deployment |
| Validated local field dataset | ⬜ Future | Requires Step 3 + calibration + QC |
| Public Zenodo dataset | ⬜ Future | Requires Step 4 before release |

---

## 13. Open Questions

| Question | Category | Owner | Priority |
|---|---|---|---|
| Has an EIN been assigned by the IRS? | Legal/compliance | Carlos Garcia | P0 |
| Has banking been established? If not, what is blocking it? | Finance | Adam Kimble | P0 |
| Is "VanKuijk" or "VanKaujk" the correct spelling? Which is legal name? | Governance records | Guillermo Martin | P1 |
| When is the NM-COROS charitable registration required? | Legal/compliance | Carlos Garcia | P1 |
| Are there bench-test data logs from ESP32/Pi that should be preserved? | Research/data | Carlos Garcia | P1 |
| What is the specific electrode array model and part number? | Hardware | Carlos Garcia | P1 |
| Is there a fiscal sponsorship or umbrella arrangement in place? | Finance | Adam Kimble | P1 |
| What is the on-site deployment timeline for Step 3? | MycoSense | Carlos Garcia | P1 |
| Are board meeting minutes being recorded? Where are they stored? | Governance | Guillermo Martin | P1 |
| Is the Rowe, NM site owned/leased by the Foundation or a private party? | Legal/compliance | Carlos Garcia | P2 |

---

## 14. Missing Records

| Missing Record | Why It Matters | Recommended Action |
|---|---|---|
| Bylaws (even redacted text) | Governance transparency; grant reviewers expect it | Commit a public summary or redacted version |
| Conflict-of-interest policy | IRS and grant compliance | Commit a public version |
| Board meeting minutes | Governance continuity | Store privately; keep a log |
| Organizational meeting minutes | Confirms bylaws adoption, officer elections | Store privately |
| Financial controls policy | Required for grant accountability | Draft and adopt |
| Field protocol documents | Research credibility; needed before deployment | Draft in `research/protocols/` |
| Calibration protocol | Data quality for any future dataset | Draft before Step 3 |
| Data management plan | Required by many funders | Draft before first grant |
| Site agreements/permits | Required before field deployment | Confirm land access |
| Research ethics review | May be required for ecological sensing | Determine if IRB/IEC needed |

---

## 15. Dependencies

| Dependency | Type | Risk if Lost | Mitigation Status |
|---|---|---|---|
| Carlos Garcia | Human — founder, researcher, primary technical contact | Critical — research stalls | No succession plan ⚠️ |
| Vercel hosting (MycoSense) | Infrastructure | Demo goes offline | Free tier; switch to GitHub Pages if needed |
| Zenodo (publication host) | Research infrastructure | Preprint inaccessible | DOI persists; Zenodo has high uptime |
| GitHub (repositories) | Infrastructure | Codebase inaccessible | Mirror/backup not documented |
| ESP32 supply chain | Hardware | Prototype can't be scaled | Common chip; multiple suppliers |
| Rowe, NM site access | Physical | Step 3 deployment blocked | Site ownership/access unclear |
| IRS 501(c)(3) determination | Legal/financial | Grant eligibility restricted | Form 1023-EZ filed; no controls on IRS timing |

---

## 16. Near-Term Decisions

| Decision | Deadline | Owner | Stakes |
|---|---|---|---|
| Establish banking | ASAP — blocks financial operations | Adam Kimble | Cannot receive grants, manage expenses, or pay fees |
| Determine NM-COROS registration requirement | After 501(c)(3) determination | Carlos Garcia | Legal compliance for NM charitable solicitation |
| Correct VanKuijk/VanKaujk name across all repos | P1 | Guillermo Martin | Consistency in legal and public records |
| Revise luminis-foundation-open README field deployment status language | P1 | Carlos Garcia | Risk of overclaiming to funders/public |
| Set Step 3 deployment date | P1 | Carlos Garcia | Unlocks research program, grant eligibility |
| Draft and adopt financial controls policy | P1 | Adam Kimble | Required for IRS compliance and grant accountability |
| Draft field and calibration protocols | Before Step 3 | Carlos Garcia | Research credibility; data quality |
| Decide board expansion strategy | P2 | Board | Governance resilience; diverse expertise |
