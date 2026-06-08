---
name: ultrafast-optics
description: "Ultrafast optics skill — distills femtosecond/attosecond pulse generation, propagation, characterization, shaping, amplification, frequency combs, and ultrafast spectroscopy from 10 specialized textbooks. Extends optics with deep mode-locking theory, FROG/SPIDER/d-scan pulse measurement, CPA/OPCPA amplification, carrier-envelope phase control, optical frequency combs, attosecond pulse generation (HHG), and ultrafast spectroscopy methods."
unit_system: SI
unit_note: >
  All formulas in SI units. Consistent with optics, electrodynamics, and plasma skills.
  No edges into landau-graph (Gaussian units skill).
conventions: >
  See `physics-conventions` for all sign / normalization / naming defaults.
  Time convention: e^{-iωt}. Metric: (−+++).
  Pulse intensity: I(t) = |E(t)|². Chirp: positive = red leads blue (dω/dt > 0).
  GDD = d²φ/dω². β₂ = −GDD (waveguide convention). τ_p = FWHM intensity.
  Transform limit: Gaussian τ_p Δν = 0.44, sech² τ_p Δν = 0.315.
---

# Ultrafast Optics Skill Graph

Extends the physics foundations (optics, electrodynamics, plasma) with
deep ultrafast optics: how to GENERATE few-cycle pulses via mode-locking,
CHARACTERIZE them via FROG/SPIDER/d-scan, SHAPE them via Fourier synthesis,
AMPLIFY them via CPA/OPCPA, STABILIZE their carrier-envelope phase, and
use them as frequency combs and attosecond probes.

## Source Texts

- Weiner, *Ultrafast Optics* (2009) — primary textbook
- Diels & Rudolph, *Ultrashort Laser Pulse Phenomena* (2006, 2nd ed)
- Trebino, *Frequency-Resolved Optical Gating* (2000)
- Dantus, *Femtosecond Laser Shaping* (2017)
- Ye & Cundiff, *Femtosecond Optical Frequency Comb* (2005)
- Mukamel, *Principles of Nonlinear Optical Spectroscopy* (1995) — response functions, Liouville space, cumulant, Brownian oscillator
- Siegman, *Lasers* (1986) — mode-locking sections (§26-27)
- Svelto, *Principles of Lasers* (2010, 5th ed) — test set
- PUILS XIII, *Progress in Ultrafast Intense Laser Science* (2017) — test set
- Herrmann & Wilhelmi, *Laser für ultrakurze Lichtimpulse* (1986) — test set
- Akhmanov et al., *Оптика фемтосекундных лазерных импульсов* (1988) — test set

## Relation to optics skill

This skill REPLACES the following optics nodes with deeper treatments:
- `reasoning.optics.ultrashort_pulse_generation` → uo: mode_locking_active + mode_locking_passive + cpa + cep
- `reasoning.optics.pulse_characterization` → uo: pulse_characterization_frog + pulse_characterization_spider_dscan
- `reasoning.optics.dispersion_management_gdd` → uo: dispersion_compensation
- `knowledge.optics.pulse_measurement_data` → uo: pulse_measurement_techniques

The following optics nodes remain as general foundations:
- `reasoning.optics.pulse_propagation_nlse` (general NLSE)
- `reasoning.optics.laser_rate_equations` (general laser physics)

Edge protocol: ultrafast-optics ↔ all non-landau-graph skills (bidirectional).

## Distillation Plan

See `/home/zhiping/task/ultrafast-optics/distillation-plan.md`
