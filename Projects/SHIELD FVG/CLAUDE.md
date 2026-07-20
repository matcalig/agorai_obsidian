# Project: SHIELD (FVG Flood/Hydrogeological Risk)

## Overview
SHIELD is a **territorial digital twin for hydraulic & hydrogeological (flood) risk management in Friuli Venezia Giulia**, built by Agorai with **Regione FVG (Direzione Centrale Ambiente), ARPA FVG, and Protezione Civile FVG**. One of Agorai's four use cases (alongside [[Projects/Fincantieri ARM|ARM]], [[Projects/xFarm AI-Gronomist|AI-Gronomist]], FVG C.A.R.E.).

**Core problem:** in small basins a catastrophic flood can develop in **~2 hours** — faster than the existing model chain (weather → runoff → flood propagation) can produce an actionable risk assessment. The bottleneck is compute time, not physics.

**The approach:** move the physics **offline** to pre-compute a scenario library; at runtime, an **AI pattern-matching / scenario-retrieval** layer matches live sensor readings (rain gauges, hydrometric levels, cameras) to the most similar pre-computed scenarios — no live model run. Essentially: *"what already-studied situation does this most resemble, and what happened next?"*

**Pilot territory:** the **Judrio–Versa–Corno basin** — chosen because it compresses FVG's full terrain spectrum (mountain→hill→plain→coast, rural→urban) into a tractable area. Scales to the Tagliamento basin (45% of FVG) and, in principle, similar EU regions.

## The IP split (same model as ARM)
- **Agorai owns the AI layer** — scenario-retrieval/inference + production architecture (the defensible IP).
- **SISSA owns the physical model** + data-validation methodology (publishable), via the **Fondazione Agorai** academic partnership.
- Physics runs offline to build the scenario library; AI queries it in real time.

## Status
- **Phase:** Pre-start / de-risking — pilot **not yet begun**. Higher structural risk than ARM.
- **Matteo's role:** PM / portfolio — currently building the **SHIELD budget model** (`SHIELD_Budget_Model_v0_1`) and portfolio budget levers.

> **⚠️ Update 2026-07-20 (from Alex's W30 prep — supersedes the June sources this file was built from):**
> - **SHIELD is now the most active use case in Alex's inbox** — not "pre-start." Regione has been waiting; Maurizio called it "molto urgente" (4 Jul).
> - **SISSA proposal superseded:** the June framing (~€15–20k, 4–5 months, 1 postdoc @50–60%/3mo) is replaced by a formal **SISSA proposal ~€94k for a 12-month post-doc** (arrived ~20 Jul, Prof. Rozza). Maurizio is asking where the **economic offer** is.
> - **art. 19 IP incongruence** flagged by both Sara Cremascoli and Sara Levi Sacerdotti; Maurizio delegated the IP + open-questions answer to Alex.
> - **De-facto driver: Sara Levi Sacerdotti (DS&AI Foundation ETS)** — not in the roster below. SISSA contacts: **Rozza, Dellapi**; **UniUD** now involved (Montanari, Policriti).
> - **FVG kickoff scheduling** is live and **collides with the ARM kickoff (Fri 24 Jul, 15–16 CET)** — coverage decision needed (likely Matteo).

## Key people
- **Regione FVG – Ambiente:** Massimo Canali (project owner), Massimo Zanetti (hydrology).
- **ARPA FVG (OSMER):** Fulvio Stel (meteo modeling & data validation; developing runoff/afflussi-deflussi models).
- **Protezione Civile FVG:** Claudio Garlatti; Amedeo Aristei (director) — the operational **end user**.
- **SISSA:** physical-modeling partner (Guido Sanguinetti on modeling) — **participation not guaranteed** (see risks).
- **Fondazione Agorai:** academic-partnership vehicle for SISSA/university research.
- **Agorai:** Alex Presani (STO/governance), Maurizio Cortese (CEO; sovereignty framing), Matteo (PM).
- **Generali Climate Hub** (potential design/data partner): Francesca Monti, Alessandro Barducci, Eloisa Gattaglio.

## What already exists (regional groundwork)
300+ meteo stations + rain/hydrometric gauges + cameras · high-res **DTM** (LASCAN, updated after the November flood) · ARPA validated meteo (OSMER) + runoff models in development · historical event record (Nov flood + 2–3 prior) · public portals (IGOL, IRDAT) · a **regional delibera (~Mar 2026)** that permits AI use of regional data via a formal compliance process.

## SISSA pilot (proposed, 4–5 months)
Three sequential-ish filoni:
- **A — Data consolidation:** unify/align the Judrio dataset (sensor series, DTM, ARPA meteo), versioned + documented. *(SISSA-led)*
- **B — Physics-informed base model:** calibrated hydrological model reproducing historical events, generating scenario outputs. *(SISSA-led)*
- **C — Retrieval/classification layer:** given current sensor state, return the most-similar scenario + outcome + confidence. *(Agorai-led)*
Resourcing: SISSA ~1 postdoc @50–60%/3mo; Agorai ~1 research engineer @30%. Direct-contract cost ~€15–20k (lower if via Fondazione).
**Long-term ladder:** Retrieval (pilot) → **Hazard** (2D hydraulic propagation) → **Impact** (exposure/vulnerability, location-by-location, real-time). Research track (SISSA, publishable) + production track (Agorai).

## Next Actions
- [ ] **Resolve delivery governance** — Deloitte is gone; the entire delivery side has no owner (Alex) — Supports: [[1. Yearly Goals]]
- [ ] **Lock down SISSA** (or line up a fallback for the physical-modeling layer) via Fondazione — open dependency
- [ ] Start **regional data-access procedures now** (delibera compliance review) — target: DTM + ≥1 historical event series in hand
- [ ] Finish the **SHIELD budget model** + portfolio budget levers (Matteo, in progress today)
- [ ] Plan the **OSMER / Protezione Civile / Ambiente site visit** (Alex, target July)
- [ ] Designate operational contacts for Ambiente, ARPA, Protezione Civile

## Blockers / risks
- **No delivery owner** — Deloitte's full exit **~9 Sep 2026** is a hard clock; Fondazione's operational role/staffing unclear.
- **Physical-modeling gap is Agorai's to solve** — someone must build & pre-compute the flood-propagation scenarios; currently unassigned.
- **SISSA not secured** — recent signals show SISSA pulling back; treat as an open dependency, prepare a fallback.
- **Data-access process** is the likeliest source of delay — the delibera's mandatory **compliance review** must clear before regional/ARPA data flows.
- **Data sovereignty** — largely mitigated (Agorai foundation is EU-region only: Frankfurt primary, Amsterdam DR, so residency is handled); remaining gate is the delibera review, not geography. Keep a single cross-use-case sovereignty position (shared with [[Projects/xFarm AI-Gronomist|illy/xFarm]]).
- **Generali Climate Hub** = design/data partner, **not** a delivery client — guard the IP boundary (their historical claims↔damage data is valuable ground truth; don't become a free fine-grained data source for their pricing models).

## Resources (Drive — shared "Agorai" folder & My Drive)
- `SHIELD — Territorial Digital Twin for Hydraulic Risk (FVG).md` (consolidated brief — read first)
- `SHIELD_SISSA_Proposta_Collaborazione_v2` · `SHIELD_use_case.pdf` · `Progetto Shield-Analisi-HPE.docx`
- `2026-06-09 Generali Climate Hub — Collaborazione SHIELD & illy` (meeting notes)
- `20260512_Agorai_Progetto SHIELD.pptx` · Verbale Incontro SHIELD (13 May) · `SHIELD_Budget_Model_v0_1`
- Critical User Journey / Product Discovery — Hydrogeological Risk (My Drive)

## Notes for Claude
Created 2026-07-20 from the shared **Agorai** Drive folder (digital-twin brief, SISSA proposal v2, Generali Climate Hub notes). Most content dates to **early–mid June 2026**; the pilot may have moved since — verify current status with Alex before acting. The pilot brief says "Judrio" basin; one Italian note says "Idro" — canonical is **Judrio–Versa–Corno**; confirm.
