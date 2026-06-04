---
skill_id: reasoning.em.cherenkov_radiation
type: reasoning
summary_50t: >
  v > c/n(ω) → Cherenkov cone at cosθ_c=c/[vn(ω)]. Frank-Tamm:
  d²E/dx dω=(q²/4πε₀c²) ω[1−1/(β²n²(ω))]. Threshold βn(ω)>1.
  Polarization in (v,k) plane. PID via Cherenkov detectors (RICH).
trigger:
  - charged particle moving faster than light in a dielectric medium
  - computing Cherenkov angle, spectrum, and energy loss
reasoning_role: cherenkov_radiation
parent: knowledge.continuous.dielectric_dispersion
retrieval_cost: 1
---

# reasoning.em.cherenkov_radiation — v > c/n → Coherent Shock Wave

## Core Picture

When a charged particle traverses a dielectric medium with speed v > c/n(ω),
it outruns its own electromagnetic field. The resulting electromagnetic
shock wave — the Cherenkov effect — produces coherent radiation at a fixed
angle cos θ_c = c/[v n(ω)], analogous to the Mach cone in supersonic flow
(Jackson §13.4-13.5, Cao §6.6).

## Derivation Sketch (from dielectric dispersion → Frank-Tamm)

Starting from `landau-graph: knowledge.continuous.dielectric_dispersion`
(the medium response ε(ω) sets the phase velocity c/n(ω)):

### 1. Fourier-domain field from a moving point charge

A point charge q moving with velocity v = βc along z:
ρ(r,t) = q δ(x)δ(y)δ(z−vt),   J(r,t) = qv δ(x)δ(y)δ(z−vt)

Fourier transform (in x,y,t → k_x,k_y,ω):
ρ̃(k_⊥,ω,z) = (q/v) δ(ω − k_z v) e^{ik_z z}    with k_z = ω/v

The δ(ω−k_z v) is the Cherenkov phase-matching condition: the particle's
motion selects a specific k_z for each ω — this is what makes the radiation
coherent (not just transition radiation).

### 2. Wave equation in dispersive medium

In frequency domain with ε(ω): ∇²E + (ω²/c²)ε(ω) E = iωμ₀ J̃ − ∇(∇·E)

Decompose into transverse coordinates:
(∇_⊥² + k_⊥²) E_⊥ = source,   k_⊥² = (ω²/c²)n²(ω) − k_z² = (ω²/c²)[n²(ω) − 1/β²]

### 3. The Cherenkov condition

k_⊥ is REAL (propagating cylindrical wave) when: n²(ω) − 1/β² > 0
→ β n(ω) > 1 → v > c/n(ω)

When satisfied: outgoing cylindrical wave ∝ H₀^(1)(k_⊥ ρ) → energy flows
away from the particle trajectory. When NOT satisfied: k_⊥ imaginary →
field exponentially localized around particle (no radiation).

### 4. Cone angle from phase matching (geometric construction)

In time Δt, particle travels vΔt; light travels (c/n)Δt. The condition
that successive wavefronts interfere constructively gives:
cos θ_c(ω) = (c/n(ω))/v = 1/[β n(ω)]

### 5. Frank-Tamm formula (energy loss via Poynting flux)

Compute Poynting vector S_ρ through a cylinder of radius ρ around the
particle trajectory, integrate over ρ → ∞. The radiated energy emerges
from the imaginary part of the Hankel function as k_⊥ becomes real:
```
d²E/(dx dω) = (q²/4πε₀c²) ω [1 − 1/(β² n²(ω))]        for β n(ω) > 1
            = 0                                          otherwise
```

## Algorithm

```
1. Check Cherenkov condition: β n(ω) > 1 ? If no → no radiation.

2. Cherenkov angle: cos θ_c(ω) = 1/[β n(ω)].

3. Frank-Tamm energy spectrum (per unit length, per angular frequency):
   d²E/(dx dω) = (q²/4πε₀c²) ω [1 − 1/(β² n²(ω))]   [β n(ω) > 1]

4. Total energy loss per unit length:
   dE/dx = (q²/4πε₀c²) ∫_{ω: βn(ω)>1} ω [1 − 1/(β² n²(ω))] dω

5. Photon number spectrum (α = q²/(4πε₀ℏc)):
   d²N/(dx dω) = (α/πc) [1 − 1/(β² n²(ω))]           [β n(ω) > 1]

6. Polarization: linear, in the plane containing v̂ and k̂ (radially polarized
   on the Cherenkov cone). The E-field is azimuthal around the cone's axis.
```

## Key Features

- **Threshold**: For water (n≈1.33): β_th≈0.75, proton E_th≈480 MeV.
  For gas (n≈1.001): β_th≈0.999, much higher threshold.
- **Spectrum**: d²E/dx dω ∝ ω → energy rises with frequency (blue-biased).
  In wavelength: d²E/dx dλ ∝ 1/λ³ — strongly UV/blue. Saturation at
  frequencies where n(ω)→1 (X-ray region, no Cherenkov in hard X-rays).
- **Detectors**: Measure θ_c → determine β → particle ID (PID). Ring-imaging
  Cherenkov (RICH) detectors use gas radiators for relativistic particle
  identification (pion/kaon/proton separation at GeV energies).
- **Dispersion smearing**: n(ω) variation broadens the ring; Δθ_c ≈ Δn/(n²β sin θ_c).

## Edge Cases

- **Below threshold** (β n < 1): No Cherenkov. All field energy stays bound.
  Still have energy loss via ionization (Bethe-Bloch), which is distinct.
- **Strong-field / nonlinear**: χ⁽³⁾ modifies ε → Cherenkov angle shifts;
  nonlinear Cherenkov generates harmonics of the fundamental. Cross-ref:
  `electrodynamics: knowledge.em.strong_field_electrodynamics` and
  Avetissian §2 (induced/nonlinear Cherenkov).
- **Transition radiation** (particle crosses boundary): accompanies Cherenkov
  near interfaces. Distinguish: transition radiation ∝ γ (forward-peaked
  at high energy), Cherenkov ∝ fixed θ_c.

## Cross-References

- Jackson §13.4-13.5, Cao §6.6
- landau-graph: knowledge.continuous.dielectric_dispersion (parent:
  ε(ω) determines threshold and spectrum)
- landau-graph: knowledge.continuous.moving_media_electrodynamics
  (field in moving media; prerequisite for frequency-domain treatment)
- electrodynamics: knowledge.em.strong_field_electrodynamics
  (nonlinear Cherenkov, strong-field modifications)
- electrodynamics: reasoning.em.lienard_wiechert_radiation (point charge
  radiation in vacuum; Cherenkov is the MEDIUM generalization)
