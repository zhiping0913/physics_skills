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
parent: reasoning.normal_mode_decomposition
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

## Analogy to Normal Modes

Same mathematical structure as `reasoning.normal_mode_decomposition`:
Coupled DOFs → eigenproblem → discrete spectrum. The difference: in
mechanics, ω is the eigenvalue (discrete); here, k_⊥ is the eigenvalue
(discrete) while ω is a continuous parameter.

## Cross-References

- Jackson §8.1-8.6
- Griffiths §9.5
- landau-graph: reasoning.normal_mode_decomposition (same mathematical structure)
