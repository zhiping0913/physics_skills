---
skill_id: reasoning.em.waveguide_mode_decomposition
type: reasoning
summary_50t: >
  Boundary conditions on waveguide walls quantize k_⊥ → discrete modes.
  Propagation: β_n = √(ω²/c²−k_⊥(n)²). Below cutoff ω<ω_c: evanescent.
  TE/TM/TEM classification from axial field components. Same math as
  normal modes but with CONTINUOUS ω and discrete k_⊥.
trigger:
  - electromagnetic fields in hollow or dielectric waveguides
  - need to find propagating modes and cutoff frequencies
  - designing microwave/optical transmission structures
reasoning_role: waveguide_modes
parent: landau-graph:reasoning.normal_mode_decomposition
sign_convention: propagation e^{i(βz−ωt)}; β = k_z is the propagation constant
retrieval_cost: 1
references:
  - landau-graph: reasoning.normal_mode_decomposition (analogy)
---

# reasoning.em.waveguide_mode_decomposition — Boundary → Discrete Modes

## Core Picture

In free space, EM waves are TEM (E⊥k, B⊥k) with continuous k. In a waveguide,
conducting walls impose boundary conditions (E_tangential = 0 on walls) that
QUANTIZE the transverse wave number → DISCRETE propagation modes.

The mathematical structure is identical to `reasoning.normal_mode_decomposition`,
but with a twist: ω is continuous (driving frequency) while k_⊥ is discrete
(from BCs). This produces the characteristic CUTOFF behavior.

## Derivation Sketch

Starting from `landau-graph: reasoning.normal_mode_decomposition` we have the
pattern: coupled degrees of freedom → eigenvalue problem → discrete spectrum
of normal modes. In mechanics, the eigenvalue is ω_n (oscillation frequency).
In waveguides, the roles invert: ω is a continuous parameter (the driving
frequency) and the eigenvalue is k_⊥(n) (transverse wavenumber from BCs), with
β_n = √(k²−k_⊥(n)²) as the propagation constant.

**Key non-obvious step — the Helmholtz eigenproblem structure**:
Maxwell's equations reduce to (∇_⊥² + γ²)ψ = 0 on the cross-section, where
γ² = k² − β². The boundary condition ψ=0 (Dirichlet for TM, Neumann ∂ψ/∂n=0
for TE) turns this into a Sturm-Liouville eigenproblem on the 2D cross-section.
The eigenvalues γ_n² form a discrete, positive, increasing sequence. The
dispersion relation β_n(ω) = √(k²−γ_n²) implies:

- **Cutoff**: below k = γ_n, β becomes imaginary → EVANESCENT decay.
- **Phase velocity**: v_p = ω/β_n = c/√(1−ω_c²/ω²) > c (always superluminal).
- **Group velocity**: v_g = dω/dβ_n = c√(1−ω_c²/ω²) < c, and crucially:
  v_g·v_p = c²  (a universal waveguide relation).

**Energy velocity = group velocity**: The time-averaged Poynting power P =
(1/2)Re ∫(E×H*)·n̂ dS and stored energy per unit length W' satisfy v_g =
P/W' — energy propagates at the group velocity (Jackson §8.5).

## Algorithm (Jackson §8.1-8.6)

```
1. Assume propagation along z: E,B ∝ e^{i(k_z z − ωt)}.
   Transverse Laplacian: (∇_⊥² + k² − k_z²) ψ = 0 where k=ω/c.

2. Classify modes by which field component is AXIAL:
   TE (Transverse Electric): E_z = 0, solve ∇_⊥²H_z + γ²H_z = 0, H_z=0→BC
   TM (Transverse Magnetic): H_z = 0, solve ∇_⊥²E_z + γ²E_z = 0, E_z=0→BC
   TEM: E_z = H_z = 0, requires 2+ conductors (coax, stripline)

3. BCs → discrete eigenvalues γ_n² = k² − k_z² = k_⊥(n)²:
   Rectangular (a×b): k_⊥(mn)² = (mπ/a)² + (nπ/b)²
   Circular (radius R): k_⊥ = x_mn/R or x'_mn/R (zeros of Bessel J_m or J'_m)

4. Propagation constant: k_z(n) = √(k² − k_⊥(n)²)
   Above cutoff (k > k_⊥(n)): propagating wave with phase velocity v_p = ω/k_z > c
   Below cutoff (k < k_⊥(n)): EVANESCENT (exponential decay ∝ e^{−|k_z|z})
   Cutoff frequency: ω_c(n) = c·k_⊥(n)

5. Transverse fields from axial: E_⊥, H_⊥ expressed as derivatives of E_z, H_z.
```

## Key Results

**Rectangular waveguide (TE₁₀ mode)** — the dominant mode:
Cutoff: f_c = c/(2a) for a > b. Operating band: f_c < f < 2f_c (single mode).
Power: P = (ab/4Z_TE)|E₀|², attenuation α ∝ R_s (surface resistance).

**Circular waveguide (TE₁₁ mode)** — lowest loss:
TE₁₁: k_⊥R ≈ 1.841. TM₀₁: k_⊥R ≈ 2.405.

**Coaxial cable (TEM mode)**: No cutoff! Propagates down to DC.
Impedance Z₀ = (1/2π)√(μ/ε) ln(b/a). Loss minimum at optimal b/a ratio.

## Dielectric Waveguides (Optical Fiber)

**Slab waveguide** (n_core > n_clad): TE/TM guided modes. Dispersion:
tan(κd) = κ(α+γ)/(κ²−αγ) where κ=k₀√(n_core²−n_eff²), γ=k₀√(n_eff²−n_clad²).
Number of modes ∝ V = k₀d√(n_core²−n_clad²). V<π→single mode.

**Step-index circular fiber**: V = (2πa/λ)NA. Single-mode: V<2.405.
LP_lm modes: l=angular, m=radial order. LP₀₁ is fundamental (near-Gaussian).
Dispersion: material (dn/dλ) + waveguide (geometry). Zero-dispersion point:
λ₀≈1.31μm (standard fiber), shifted to 1.55μm in DSF. Mode field diameter
MFD≈2a for V∼2. Polarization-maintaining fiber (PMF): stress-induced
birefringence (PANDA, bow-tie). Photonic crystal fiber (PCF): endlessly
single-mode, high nonlinearity, anomalous dispersion at visible.

## Cavity Resonators — Q, Mode Density, Purcell Factor

For a closed cavity (or ring resonator), resonances occur when βL = mπ
(longitudinal quantization on top of transverse).

**Eigenmode BVP caveat:** for a conducting-wall cavity, the vector eigenproblem
is not defined by n̂×E = 0 alone. One must also impose ∇·E = 0 in the source-free
volume (or an equivalent compatible gauge/constraint). Otherwise irrotational
gradient fields satisfy the curl-curl equation spuriously and contaminate the
mode set. This is the continuum version of the L/M/N split in
`electrodynamics: knowledge.em.vector_wave_functions`; in FEM, edge elements
and the discrete de Rham complex in
`computational-physics: reasoning.cp.finite_element_method` remove the same
spurious gradient modes.

Key figures of merit:

- **Quality factor**: Q = ω₀ W_stored / P_loss. For a cavity with volume V
  and surface resistance R_s: Q ∼ (V/S)(1/δ_skin). Superconducting cavities
  reach Q > 10¹⁰.
- **Mode density** (free space): ρ(ω) = ω²/π²c³ per polarization. In a cavity,
  this becomes a sum of Lorentzians centered at ω_n with width ω_n/Q.
- **Purcell factor**: F_P = (3/4π²)(λ/n)³(Q/V). For a single-mode cavity
  resonant with a dipole emitter, F_P > 1 → ENHANCED spontaneous emission
  rate. This is the basis of cavity QED (Purcell, Phys. Rev. 1946).

## Analogy to Normal Modes

Same mathematical structure as `reasoning.normal_mode_decomposition`:
Coupled DOFs → eigenproblem → discrete spectrum. The difference: in
mechanics, ω is the eigenvalue (discrete); here, k_⊥ is the eigenvalue
(discrete) while ω is a continuous parameter.

## Cross-References

- Jackson §8.1-8.6
- Griffiths §9.5
- landau-graph: reasoning.normal_mode_decomposition (same mathematical structure)
- electrodynamics: knowledge.em.vector_wave_functions (L/M/N vector mode basis;
  separates solenoidal modes from gradient fields)
- computational-physics: reasoning.cp.finite_element_method (FEM edge elements
  and discrete de Rham complex suppress spurious modes)
- electrodynamics: reasoning.em.fresnel_interface_reflection_refraction
  (waveguide conducting walls = TIR boundary; dielectric interface is the
  planar counterpart — Fresnel coefficients from the same boundary-condition
  matching framework; bidirectional: Fresnel derives from waveguide decomposition)
