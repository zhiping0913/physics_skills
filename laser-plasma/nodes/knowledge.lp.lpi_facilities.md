---
skill_id: knowledge.lp.lpi_facilities
type: knowledge
summary_50t: >
  Major laser-plasma facilities worldwide: NIF (1.8 MJ, 192 beams, 3ω),
  LMJ (1.5 MJ, 176 beams, 3ω), Omega (30 kJ, 60 beams), Omega-EP
  (2.6 kJ, PW), ELI-Beamlines (10 PW, 1.5 kJ), ELI-NP (2×10 PW, 200 J),
  SULF (10 PW, 300 J), CoReLS (4 PW, 80 J), BELLA (PW, 40 J). ICF vs
  high-rep-rate vs high-intensity classification.
trigger:
  - looking up facility parameters for experiment design
  - comparing capabilities across laser facilities
parent: reasoning.lp.laser_wakefield_acceleration
retrieval_cost: 1
---

# knowledge.lp.lpi_facilities — Worldwide Laser-Plasma Facilities

## ICF Facilities (kJ–MJ, low rep-rate)

| Facility | Location | Energy (kJ) | λ (μm) | Beams | Pulse (ns) | Peak Power | Shots/day |
|----------|----------|------------|--------|-------|------------|------------|-----------|
| **NIF** | LLNL, USA | 1800 | 0.351 | 192 | 1–20 | 500 TW | 1–2 |
| **LMJ** | CEA, France | 1500 | 0.351 | 176 | 1–20 | 400 TW | 1 |
| **Omega** | LLE, USA | 30 | 0.351 | 60 | 1–3 | 30 TW | 10 |
| **SG-III** | China | 180 | 0.351 | 48 | 3 | 60 TW | 1 |
| **Gekko-XII** | ILE, Japan | 10 | 1.053/0.527 | 12 | 1 | 10 TW | 4 |

## PW-Class (high intensity, kJ/sub-kJ)

| Facility | Location | Power (PW) | Energy (J) | τ (fs) | λ (μm) | Rep-rate |
|----------|----------|------------|------------|--------|--------|----------|
| **ELI-Beamlines** | Czech Rep. | 10 | 1500 | 150 | 0.8 | 1/min |
| **ELI-NP** | Romania | 2×10 | 200×2 | 22 | 0.8 | 1/min |
| **SULF** | Shanghai | 10 | 300 | 30 | 0.8 | shot/hr |
| **Apollon** | France | 10 | 150 | 15 | 0.8 | 1/min |
| **CoReLS** | S. Korea | 4 | 80 | 20 | 0.8 | 0.1 Hz |
| **BELLA PW** | LBNL, USA | 1.3 | 40 | 30 | 0.8 | 1 Hz |
| **Omega-EP** | LLE, USA | 1 | 2600 | 1000 | 1.053 | shot/hr |
| **Titan** | LLNL, USA | 1 | 500 | 500 | 1.053 | 2/hr |
| **J-KAREN-P** | Japan | 0.5 | 15 | 30 | 0.8 | 0.1 Hz |
| **Astra-Gemini** | RAL, UK | 0.5 | 15 | 30 | 0.8 | 0.1 Hz |
| **DRACO** | HZDR, Germany | 0.15 | 4.5 | 30 | 0.8 | 10 Hz |

## High Repetition Rate (LWFA drivers)

| Facility | Power (TW) | Energy (J) | Rep-rate (Hz) | Notes |
|----------|------------|------------|---------------|-------|
| BELLA (kHz) | 0.01 | 0.01 | 1000 | LWFA staging R&D |
| CALA (Munich) | 0.06 | 1.5 | 1–5 | Medical protons |
| LPA (LOA) | 0.2 | 5 | 10 | LWFA injection |

## XFEL + Laser Combinations

| Facility | X-ray energy | Laser power | λ_laser | Notes |
|----------|-------------|-------------|---------|-------|
| LCLS + MEC | 1–25 keV | 0.2 TW | 0.8 μm | Warm dense matter |
| EuXFEL + HED | 3–25 keV | 0.1 TW | 0.8 μm | HED physics |
| SACLA | 4–20 keV | 0.5 TW | 0.8 μm | Japan |

## Facility Classification

| Class | Power/Energy | Example | Primary physics |
|-------|------------|---------|----------------|
| ICF ignition | 1–2 MJ, ns | NIF, LMJ | Fusion burn, HEDP |
| Multi-PW | 1–10 PW, fs | ELI, SULF | QED-plasma, ion accel |
| LWFA driver | 100 TW–PW, fs | BELLA, Astra | Electron acceleration |
| High rep-rate | 10–100 TW, kHz | BELLA-kHz | Applications, medical |
| HED probe | XFEL + laser | LCLS-MEC | WDM, EOS |
