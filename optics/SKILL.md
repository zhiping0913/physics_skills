---
name: optics
description: "Optics engineering skill — extends landau-graph, electrodynamics, and plasma with Fourier optics, laser engineering, ultrashort pulse generation/measurement, acousto/electro-optics, stimulated scattering, and wave propagation in real media from 11 specialized textbooks."

unit_system: SI
unit_note: >
  All formulas in SI units. landau-graph uses Gaussian — conversion via
  `physics-conventions` (which absorbed `si-gaussian-conversion` and adds all
  project-wide conventions). Bidirectional with electrodynamics and plasma OK.
  No edges into landau-graph.
conventions: >
  See `physics-conventions` for all sign / normalization / naming defaults.
  Defaults are used silently; deviations declared in node `sign_convention` field.
---

# Optics Skill Graph

Extends the physics foundations (31 nodes across landau-graph, electrodynamics,
plasma) with the engineering optics layer: how to DESIGN lasers, ANALYZE imaging
systems, MEASURE ultrashort pulses, and SIMULATE optical propagation in real media.

## Source Texts

- Goodman, *Introduction to Fourier Optics* (2017) — lens as FT, CTF/OTF, holography
- Siegman, *Lasers* (1986) — rate equations, resonators, mode locking, amplifiers
- Svelto, *Principles of Lasers* (2010) — laser physics, Q-switching, ultra-short pulses
- Trebino, *FROG* (2000) — ultrashort pulse measurement
- Boyd, *Nonlinear Optics* (2020) — SBS/SRS, EIT, frequency combs, damage
- Yariv & Yeh, *Optical Waves in Crystals* (1984) — AO/EO modulators, devices
- Marcuse, *Light Transmission Optics* (1982) — Gaussian beams, fibers
- Iizuka, *Engineering Optics* (1987) — aberrations, holography, speckle
- Jarem & Banerjee, *Computational Methods* (2011) — RCWA, BPM, FDTD
- Carcione, *Wave Fields in Real Media* (2022) — attenuation, anisotropy, Biot

## Distillation Plan

See `/home/zhiping/task/optics/distillation-plan.md`
