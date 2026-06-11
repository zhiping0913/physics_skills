---
skill_id: reasoning.cp.fdtd_advanced_techniques
type: reasoning
summary_50t: >
  TF/SF plane-wave injection: Huygens surface separates total-field and
  scattered-field regions via 1D auxiliary propagation. CPML: complex-frequency-
  shifted PML with κ_max ~ 7-20, α_max ~ 0.05-0.3, m = 3-4 polynomial grading.
  ADE-FDTD: auxiliary differential equation for Drude/Lorentz/Debye dispersive
  media, updating polarization current J_p alongside E,H.
trigger:
  - plane-wave scattering from finite objects in FDTD
  - absorbing boundaries for dispersive or evanescent waves
  - modelling Drude metals, Lorentz dielectrics in time-domain
reasoning_role: fdtd_advanced
parent: reasoning.cp.fdtd_yee_algorithm
retrieval_cost: 1
---

# reasoning.cp.fdtd_advanced_techniques — TF/SF, CPML, ADE

## Core Picture

The Yee algorithm (`reasoning.cp.fdtd_yee_algorithm`) is the core engine.
Three advanced techniques make it usable for real problems:
- **TF/SF**: inject an arbitrary plane wave into a finite computational domain
- **CPML**: absorb outgoing waves without reflection (including evanescent modes)
- **ADE**: include dispersive materials (Drude metals, Lorentz resonances)

## Derivation Sketch

### 1. TF/SF plane-wave injection (Taflove 2005, Ch.5)

The Total-Field/Scattered-Field formulation separates the computational
domain by a virtual Huygens surface. Inside the surface: total fields
(E_tot = E_inc + E_scat). Outside: scattered fields only (E_scat, H_scat).

The incident field is computed on a 1D auxiliary grid and projected onto
the TF/SF boundary via the equivalence principle:

```
On TF/SF boundary, in total-field region:
  E_y^{n+1}(i_sf+1/2) = E_y|_{FDTD} + (Δt/ε₀ Δx) H_z_inc^{n+1/2}(i_sf)
  H_z^{n+1/2}(i_sf) = H_z|_{FDTD} + (Δt/μ₀ Δx) E_y_inc^{n}(i_sf+1/2)
```

The correction terms (±Δt/εΔx × H_inc and ±Δt/μΔx × E_inc) add the incident
field on the total-field side and subtract it on the scattered-field side.
ANY incident waveform (plane wave, Gaussian pulse, modulated) can be injected
— the 1D propagation merely advances the waveform in time along k̂.

### 2. Convolutional PML (CPML)

The original Berenger split-field PML (1994) is mathematically exact for
continuous fields but has two limitations: (i) it fails for evanescent waves,
(ii) the split-field formulation complicates implementation in inhomogeneous
and dispersive media. The CPML (Roden & Gedney 2000) resolves both by
introducing stretched-coordinate Maxwell's equations with complex
frequency-shifted (CFS) stretching:

```
∂/∂x̃ = (1/κ_x + σ_x/(α_x + iωε₀))⁻¹ ∂/∂x
```

where κ_x > 1 shifts the pole from ω = −iσ/ε₀, and α_x > 0 provides
absorption at low frequencies and for evanescent waves. The CFS stretching
is implemented via recursive convolution (no additional storage arrays
beyond 2 per field component):

```
Ψ_E^{n+1} = b Ψ_E^n + c (∇×H)^{n+1/2}
E^{n+1} = E^n + Δt (∇×H)^{n+1/2} + Σ Ψ_E
```

where b = exp(−(σ/κ + α) Δt/ε₀), c = (σ/(σ κ + α κ²)) (b−1). Typical
parameters: κ_max = 7–20 (polynomial grading), σ_max chosen for R(0) ~ 10⁻⁶,
α_max = 0.05–0.3, with m = 3–4 for polynomial grading of σ. Layer count:
N_PML = 10–15 cells.

### 3. ADE-FDTD for dispersive media

For a material with frequency-dependent permittivity, Maxwell-Ampère becomes:

```
ε₀ ε_∞ ∂E/∂t + ∂P/∂t = ∇×H    [P from material polarization]
```

For a Drude metal: ∂J_p/∂t + γ J_p = ε₀ ω_p² E (auxiliary ODE for current).
For a Lorentz resonance: ∂²P/∂t² + γ ∂P/∂t + ω₀² P = ε₀ Δε ω₀² E.

The Auxiliary Differential Equation (ADE) method discretises these ODEs
concurrently with Maxwell's equations on the Yee grid — J_p and P share the
E-field spatial location. The update is explicit: no matrix inversion needed.

**Drude ADE example** (Taflove §9.4):
```
J_p^{n+1/2} = (1−γΔt/2)/(1+γΔt/2) J_p^{n−1/2} + (ε₀ ω_p² Δt)/(1+γΔt/2) E^n
E^{n+1} = E^n + (Δt/ε₀ ε_∞)(∇×H^{n+1/2} − J_p^{n+1/2})
```

## Cross-References

- Taflove & Hagness, *Computational Electrodynamics* 3rd ed. (2005) Ch.5,7,9
- Roden & Gedney, *Microwave Opt. Tech. Lett.* 27, 334 (2000) — CPML
- computational-physics: reasoning.cp.fdtd_yee_algorithm (parent — core Yee)
- computational-physics: reasoning.cp.absorbing_boundary_conditions (PML → CPML bridge)
