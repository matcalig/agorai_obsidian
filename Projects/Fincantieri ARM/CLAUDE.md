# Project: Fincantieri ARM (Robotics)

## Overview
Agorai robotics use case for **Fincantieri** (shipyard automation), delivered with partner **DGS** and built on GCP by technical partner **ACT BI**. Internally referred to as the "ARM" project.

## Status
- **Phase:** Active — kickoff Fri 2026-07-24
- **Progress:** ~15% (environment setup underway, yard visit done)
- **Started:** ~2026-07-02 (Matteo's first week)
- **Target:** 2-month delivery plan (~end Sept 2026) — *confirm from plan doc*

## Goals
Stand up a GCP environment and a robotics/vision use case for Fincantieri, with DGS as delivery partner. End deliverable to Fincantieri still to be pinned down (flagged as an open question in the plan doc).

## Key People
- **Agorai:** Matteo Caligaris (PM), Alex Presani (Head of Tech & R&D)
- **Fincantieri:** Carlo Dentesano, Michele Tornielli, Giacomo Rodeghiero
- **DGS:** Fabrizio Bottarel, Ermanno Santin, Francesco Di Bianco
- **ACT BI (GCP build):** Nicolas Bossi, Nikos, Murtaza

## Current Focus
GCP setup: GPU VM provisioning and first commits to the infra repo. Preparing for the Jul 24 kickoff.

## Key Decisions
- **GPU VM:** `g2-standard-16` (Belgium region — nearest to Trieste with the needed VM types). Earlier "g4" reference was a typo. VM renamed `case-01` → `armfin-01`; new `3-armfin-dev` stage.
- **Infra repo:** github.com/Agorai-TS/Agorai-GCP
- **Docs/materials:** Fincantieri SharePoint folder (shared by Carlo) + a "2 Months Plan Proposal" Google Doc (2026-07-02).

## Next Actions
- [ ] Attend progress call "Discussione progresso Robotica Fincantieri" — **today, Mon 2026-07-20 13:00**
- [ ] Prep for **kickoff Fri 2026-07-24 15:00** (agenda, attendees, deliverable framing)
- [ ] Define the **end product delivered to Fincantieri** (open question in the plan doc) — Supports: [[1. Yearly Goals]]
- [ ] Resolve GPU VM firewall/rename follow-ups with Murtaza (`armfin-01`, `3-armfin-dev`)
- [ ] Confirm first commits landed on `Agorai-GCP` repo (Nicolas)
- [ ] Get remaining data/materials from Fincantieri (via SharePoint)

## Blockers
- ARM-Fincantieri GPU VM work flagged as blocked in Murtaza's 2026-07-20 note — *needs reading in full to confirm exact blocker.*

## Resources
- Infra repo: https://github.com/Agorai-TS/Agorai-GCP
- "2 Months Plan Proposal — Agorai GCP setup / DGS Robotics Use Case" (Google Doc, 2026-07-02)
- Fincantieri SharePoint (yard materials/videos)
- Gemini notes: "Progetti di ricerca - Caso Fincantieri" (Jun 30), "ARM Weekly Standup" (Jun 30, Jul 15)

## Notes for Claude
Source: reconstructed from Gmail (last 3 weeks) on 2026-07-20 — snippet-level, not full threads. Dates/decisions marked *confirm* need verification against the plan doc or full threads before relying on them.
