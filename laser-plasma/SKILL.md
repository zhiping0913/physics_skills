---
name: laser-plasma
description: "Laser-plasma physics skill — distills intense laser propagation, absorption mechanisms, parametric instabilities, electron/ion acceleration, relativistic plasma effects, strong-field QED, high energy density physics, inertial confinement fusion, and computational methods from ~20 specialized textbooks. Extends plasma and ultrafast-optics with deep laser-plasma coupling theory."
unit_system: SI
unit_note: >
  All formulas in SI units. Consistent with plasma, electrodynamics, and ultrafast-optics.
  No edges into landau-graph (Gaussian units skill).
conventions: >
  See `physics-conventions` for all sign / naming defaults.
  Time convention: e^{-iωt}. Metric: (−+++).
  Critical density: n_c = ε₀ m_e ω²/e². Normalized vector potential: a₀ = eE₀/(m_e ω c).
  Relativistic regime: a₀ > 1. Collisionless: ν_ei ≪ ω.
---

# Laser-Plasma Physics Skill Graph

Extends the physics foundations (plasma, electrodynamics, ultrafast-optics)
with deep laser-plasma interaction physics: how intense laser light PROPAGATES
in plasma, how energy is ABSORBED, how parametric INSTABILITIES grow, how
electrons and ions are ACCELERATED, how relativistic EFFECTS modify the plasma
response, and how strong-field QED ENTERS at extreme intensities.

## Source Texts

**Tier 1 — Distill (12 books)**:
- Kruer, *The Interaction of High-Power Lasers with Plasmas* (2002)
- Gibbon, *Short Pulse Laser Interactions with Matter* (2005)
- Macchi, *A Superintense Laser-Plasma Interaction Theory Primer* (2013)
- Brabec (ed), *Strong Field Laser Physics* (2009)
- Avetissian, *Relativistic Nonlinear Electrodynamics* (2006)
- Strong Field Physics (2025)
- Handbook of Plasma Physics Vol.3 (1991)
- Friedberg, *Ideal Magnetohydrodynamics* (1987)
- Drake, *High-Energy-Density Physics* (2006)
- Zel'dovich & Raizer, *Physics of Shock Waves* (1966/2002)
- Atzeni & Meyer-ter-Vehn, *The Physics of Inertial Fusion* (2004)
- Birdsall & Langdon, *Plasma Physics via Computer Simulation* (2018)

**Tier 2 — Test (7 books)**: see distillation plan.

## Relation to plasma skill

`plasma.laser_plasma_interaction` is DELETED from the plasma skill and fully
migrated into this skill as its foundation. All laser-plasma queries route
directly to `laser-plasma`. The `plasma` skill retains general plasma physics
(MHD, waves, transport, diagnostics).

Edge protocol: laser-plasma ↔ all non-landau-graph skills (bidirectional).

## Distillation Plan

See `/home/zhiping/task/laser-plasma/distillation-plan.md`
