---
skill_id: reasoning.plasma.surface_waves_plasmonics
type: reasoning
summary_50t: >
  At plasma-dielectric interface: SPP with k=(ω/c)√[ε_d ε_p/(ε_d+ε_p)].
  Condition: ε_p(ω) < −ε_d → ω < ω_p/√(1+ε_d). Sub-wavelength confinement.
  Excitation: prism (Kretschmann/Otto), grating. LSPR for nanoparticles.
  Interfaces reserved: quantum plasmonics, strong-field plasmonics.
trigger:
  - EM waves at plasma/metal-dielectric interfaces
  - sub-wavelength light confinement, plasmonic sensing
reasoning_role: surface_plasmon
parent: reasoning.spatial_dispersion
retrieval_cost: 1
references:
  - landau-graph: reasoning.spatial_dispersion (nonlocal ε)
  - electrodynamics: reasoning.em.waveguide_mode_decomposition (guided waves)
---

# reasoning.plasma.surface_waves_plasmonics — Interface → SPP

## Core Picture

At a flat interface between a dielectric (ε_d > 0) and a plasma/metal
(ε_p(ω) < 0 for ω < ω_p), a surface plasmon polariton (SPP) exists:
a coupled EM wave + plasma oscillation that propagates ALONG the interface
and decays exponentially PERPENDICULAR to it.

## SPP Dispersion (Shah §2-3, Raether §2)

For a single flat interface (dielectric | Drude metal):

```
k_SPP = (ω/c) √[ε_d ε_p(ω) / (ε_d + ε_p(ω))]
ε_p(ω) = 1 − ω_p²/ω²    (Drude model, no damping)
```

**Existence condition**: ε_d + ε_p(ω) < 0 → ω < ω_p/√(1+ε_d).
For metal/vacuum: ω < ω_p/√2. For metal/dielectric: cutoff reduced.

**Confinement** (1/e decay lengths):
- Into dielectric: δ_d = (1/k) √[1 − ε_d/ε_p] (longer)
- Into plasma/metal: δ_p = (1/k) √[1 − ε_p/ε_d] (shorter, ∼10-50 nm)

**Dispersion character**: at low k, SPP ≈ light line (ω≈ck/√ε_d).
At high k, SPP → ω_p/√(1+ε_d) (asymptotic surface plasmon frequency).
Momentum mismatch with free-space light → needs grating or prism coupling.

## Excitation Methods

- **Kretschmann** (prism coupling): thin metal film on prism, ATR dip.
- **Otto**: prism separated by gap from metal surface, evanescent coupling.
- **Grating coupling**: periodic surface provides Δk = 2πn/Λ matching.
- **Near-field** (SNOM): sub-wavelength probe excitation.

## Localized Surface Plasmons (LSPR)

**Nanoparticles** (sub-wavelength): no propagating SPP, instead localized
oscillation. For spherical NP in uniform field:
α = 4πa³ (ε_p−ε_d)/(ε_p+2ε_d). Resonance at Re[ε_p] = −2ε_d.
Field enhancement: |E_loc|/|E₀| ∼ |3ε_d/(ε_p+2ε_d)|. LSPR frequency depends
on size, shape, material, environment. Used in: SERS (enhancement ∼10⁶-10⁸),
biosensing (shift with binding), color engineering (stained glass).

## Reserved Interfaces

- **Quantum plasmonics**: nonlocal response (k_∥ ∼ k_F → δ ∼ λ_F), electron
  spill-out, tunneling across sub-nm gaps, quantum-size effects in NP.
- **Strong-field plasmonics**: field emission at sharp tips, tunnel ionization,
  optical-field electron emission, attosecond nanoplasmonics.

## Edge Cases

- **Interband transitions**: Noble metals (Ag, Au, Cu) have d→sp transitions
  at visible frequencies (Ag: ∼3.8 eV, Au: ∼2.4 eV). The Drude model fails —
  ε_p(ω) becomes complex with Re[ε_p] > −ε_d, suppressing SPP. Use measured
  optical constants (Johnson & Christy).
- **Nonlocal response**: For gaps < 1 nm or features < λ_F (∼0.5 nm in Au),
  the local ε approximation fails — requires quantum treatment.
- **Gain media**: ε_p'(ω) > 0 (pumped) → loss-compensated or amplifying SPP.
- **Ultra-strong coupling**: Rabi splitting > 10% ω₀ → SPP dispersion
  bifurcates into upper/lower polariton branches.

## Cross-References

- Shah §2-4, Raether (1988), Maier (2007)
- landau-graph: reasoning.spatial_dispersion (nonlocal ε at interfaces)
- electrodynamics: reasoning.em.waveguide_mode_decomposition (guided wave analog)
