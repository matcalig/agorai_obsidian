# Project: Fincantieri ARM (Advanced Robots Mobility)

## Overview
ARM is **Agorai's first Physical AI proof point and highest-conviction product bet** — an autonomous navigation system for robots operating in dynamic, GPS-denied industrial environments, specifically the interior of **Fincantieri ship hulls under active construction**. Fincantieri is both **sponsor and first customer**.

**The IP thesis:** DGS (Trieste robotics division) delivers the robotic stack; **Agorai owns the reasoning/AI layer (Layer 3) — the defensible, non-negotiable IP** (Knowledge Graph + agentic AI, auditable/deterministic at the decision boundary → the precondition for safety certification). The product is deliberately a **form-agnostic autonomy payload** (self-contained sensor+compute unit mountable on any robot), because Fincantieri runs ~20 heterogeneous robots and the payload is independently sellable to other industrial operators.

## Status
- **Phase:** POC / simulation — **18 May → 20 Sep 2026**
- **Next phases:** MVP 21 Sep 2026 → 10 Jan 2027 (first supervised hull deployment) · MVP delivery to Fincantieri **~Jun 2027** · commercialisation 2028
- **DGS contract:** signed; kickoff held. Shipyard visit done (Monfalcone, 16 Jul).
- **Matteo's role:** PM, **day-to-day single point of contact for ARM**.

> **⚠️ Update 2026-07-20 (from Alex's W30 weekly prep — reconciles against the mid-July report below):**
> - **ARM reclassified to Research / moonshot** (16 Jul): no commercial version within ~5 years. Alex sent Maurizio a "Caso Fincantieri" expectation-reset letter (19 Jul) after the shipyard visit. **This supersedes the "MVP Jun 2027 / commercialisation 2028" framing for CdA purposes** — treat those as retired commercial dates, not plan-of-record. ⚠️ The business plan being built may still carry ARM revenue that's been privately retired — reconcile before the ~16 Sep CdA.
> - **AI Architect hire is now an executive search** (head-hunter, under Generali HR): the previously-named candidate declined 13 Jul, so the "starts 1 Sep" assumption is void; the L3-capacity date is now uncertain.
> - **Alessandra Chiuderi left** (contract ended 15 Jul) — was the data-governance / IP-coordination contact; ownership now open.
> - **Kickoff Fri 24 Jul:** Agorai's docs to Dentesano still outstanding as of 14 Jul (DGS delivered theirs).
> - **Live ops blockers (20 Jul):** `case-01→armfin-01` rename blocked; GitHub org permissions unclear (Nicolas lacks write access / unclear who administers the org); a DGS user needs a GCP group add — all "who owns the platform" questions.

## Governance & key people
- **STO (full product authority): Alex Presani** — Head of Tech & R&D, Agorai. All architecture/IP/partner-scope decisions flow through him.
- **CEO: Maurizio Cortese** — owns the Fincantieri executive relationship & commercial framing.
- **Fincantieri:** Carlo Dentesano (Head of Robotics, Digital Lab — technical sponsor & discovery counterpart), Michele Tornielli (innovation/sponsor channel), Giacomo Rodeghiero, Paolo Cerioli.
- **DGS (robotic stack):** Francesco di Bianco (Robotic Stack lead), Fabrizio Bottarel, Ermanno Santin, Diego Marussi, Michele Balbi (leads DGS Trieste), Luca Scopelliti (cloud/DevOps, BID).
- **ACT BI (GCP build):** Nicolas Bossi, Nikos, Murtaza.
- **Google:** Maurizio Colleluori (Cloud PSO, infra track).
- **Research:** IIT (Lorenzo Natale, Piero Gamarra, Claudio Semini), SISSA, Domyn (Pasquali — exploratory, edge reasoning; diagnose Fincantieri–Domyn friction before pitching).

## The two POC research questions
1. **Sensor/hardware:** minimum sensor + compute config, as a form-agnostic payload, for reliable semantic navigation in a hull?
2. **Reasoning:** is a Knowledge-Graph semantic map the right L3 architecture (vs. the VLMaps baseline), and what ontology/data does it need?

A well-evidenced **negative result is a valid POC outcome.**

## Use cases (confirmed on July shipyard visit)
- **UC1 — Autonomous on-board navigation** (core enabling capability): move in-ship, self-localize, ~1 m precision; geometric on approach → semantic near target. **No premapping** (ship changes daily; builds/updates its own map, "Waze"-style).
- **UC2 — Work-progress monitoring** (the initial application Fincantieri wants): daily round detecting progress by area (ceiling grids, cable-tray density, insulation extent, paint status).
- **UC3 — Tool/material transport** (~30 kg, future; depends on UC1).
- **UC4 — Tank/void inspection** — *out of ARM scope* (separate Fincantieri project); possible future extension.

Initial sim scope: upper decks, mid-ship, public areas & cabins, rough-construction phase. **Excluded:** engine room, decks 2–3.

## Safety architecture (Fincantieri's buying criterion)
Safety Arbiter (validates every AI proposal vs. KG constraints before any motor command) · Navigation Primitive API (AI acts only through a bounded, validated action set — no direct motor control) · hardware E-stop (physical relay) · FULL→DEGRADED→MINIMAL SAFE operating modes · **navigation only, the robot touches nothing.**

## GCP / infrastructure build (actBI 2-month plan)
Two people (Nicolas, Murtaza), ~2 months + optional month-3 buffer.
- **Step 0 — Access & Roles:** GCP IAM, **L4 GPU quota** (long lead), GitHub admin, KMS/secret store, Tailscale admin, named DGS counterpart, agreed **RACI** (Agorai = Accountable on delivery; correct the pattern of the Google contact brokering/gating). **+ Define the end product delivered to Fincantieri** (gates env sizing, release targets).
- **Milestone A — VPN & GCP validation:** validate Agorai GCP account; stand up **Tailscale** VPN.
- **Milestone B — Isaac Sim dev env:** private Ubuntu 22.04 VM, NICE DCV, NVIDIA Isaac Sim; **g2-standard-16 (16 vCPU, 64 GB, 1× L4)**; Terraform/Digger; golden image; auto-stop-on-idle.
- **Milestone C — CICD & release (DGS-facing, parallel):** GitHub + Artifact Registry, **Cosign** image signing (KMS-backed) with `cosign verify` gate, release process defined *with* DGS. Fincantieri verifies authenticity with the public key only.
- **Repo:** github.com/Agorai-TS/Agorai-GCP · **VM naming:** `armfin-01`, `3-armfin-dev`.

## Key decisions
- DGS proposal chosen over Deloitte/IIT (platform-agnostic, offline-first, safer AI architecture, clean IP boundary).
- Layer 3 = Agorai IP, non-negotiable; DGS is **Consulted, not Responsible** on L3.
- Offline-first / edge-only (steel hull = Faraday cage).
- **Sept POC runs on an off-the-shelf placeholder model, not Agorai L3** (AI Architect starts 1 Sep) — hold the date, cut scope, use placeholder to discover L3 requirements.
- GPU: **g2-standard-16** (Belgium; earlier "g4" was a typo).
- Vendor-agnostic cloud (start GCP, keep portable; Agorai owns Terraform, not Google).

## Next Actions
- [ ] Attend **progress call "Discussione progresso Robotica Fincantieri" — today, Mon 2026-07-20, 19:00 Rome** (Google Meet; Matteo optional attendee)
- [ ] Prep & deliver the **kickoff — Fri 2026-07-24, 15:00 Rome** (deck structure drafted: 13 slides; pre-wire asks with Carlo/Michele; pre-wire architecture Q&A split with Alex) — Supports: [[1. Yearly Goals]]
- [ ] Push to **define the end product delivered to Fincantieri** (open in the actBI plan; blocks env sizing/release targets)
- [ ] Drive the **Fincantieri data agreement** to signature (gates KG work on real shipyard data) — WS4 (Sara Cremascoli)
- [ ] Resolve GPU VM firewall/rename follow-ups with Murtaza; confirm first commits on `Agorai-GCP` (Nicolas)
- [ ] Get remaining Fincantieri materials (3D drawings/DWG/point clouds, BOM) via SharePoint — blocks the DGS sim-env start
- [ ] Push Fincantieri to **structure its phase/work ontology** (doesn't exist yet; use the **BOM as the starting point**)
- [ ] Run ≥1 **structured operator discovery session** (WS5) — the shipyard visit does *not* substitute for it

## Blockers / top risks
- **Ceding architecture to DGS** (most acute) — insert decisively on the next 1–2 architecture decisions; keep an open-decisions list for the incoming AI Architect.
- **Hiring timeline** — AI Architect starts **1 Sep** (+2 Research Engineers ~Sep); all L3 capacity lands *on* the POC deadline, not before.
- **Ontology critical path** — no Fincantieri phase ontology exists (UC2 depends on it).
- **Timeline signal to verify** — informal "mid-2027 availability" comment at the visit; likely just restates the Jun-2027 MVP date — confirm who/what scope.
- **Repeatability** — a one-off demo is easy; reliable repetition is the hard part (frame expectations accordingly).

## Resources
- **Full project report** (comprehensive, regenerated 2026-07-17): Drive doc `ARM-Fincantieri-Project-Report.md` — the authoritative source; read it before major decisions.
- 2-Month Plan Proposal (actBI, Nicolas) · ARM Kickoff Structure & speaker notes · ARM Casi d'uso (shipyard-visit notes) · ARM cost sheets (G2/G4, budget model) · Use Case Canvas / POC Research Protocol v0.3 (Drive).
- Standing cadence: **ARM weekly standup ("Scrum of Scrums"), Tuesdays ~17:00 CEST.**

## Notes for Claude
Enriched 2026-07-20 from Gmail + Drive docs (ARM project report, 2-month plan, kickoff structure, shipyard-visit notes). **Strictly confidential** — defence-adjacent context. Verify action items with Alex before acting. Data discrepancies (ARM name, "AI Architect" vs "System Architect", POC start 18 vs 25 May) are tracked in the full report §13.
