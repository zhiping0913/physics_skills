---
skill_id: reasoning.em.statistical_em_cavity
type: reasoning
summary_50t: >
  Plane-wave-spectrum representation in electrically large cavity. CLT →
  Gaussian field components → PDF hierarchy: Rayleigh, Exponential, Chi-6,
  Chi²-6. Equipartition, spatial correlation ρ(R)∝j₀(kR), coherence length
  λ/2. Cross-domain template: EM reverberation, optical speckle, acoustic
  reverberation, quantum chaos/RMT.
trigger:
  - statistically modeling fields in large overmoded cavities or chambers
  - deriving field PDFs from random superposition of many independent modes
  - connecting EM reverberation to optical speckle and wave chaos
reasoning_role: statistical_em_cavity_fields
parent: reasoning.em.dyadic_green_function
retrieval_cost: 1
---

# reasoning.em.statistical_em_cavity — Random Plane Waves → PDF Hierarchy

## Core Picture

In an electrically large cavity (kL ≫ 1), the field at any interior point is
a superposition of many independent, statistically equivalent modes with
random phases. The Central Limit Theorem (CLT) transforms this into a
predictable hierarchy of probability distributions for field components,
magnitudes, and total energy density. The same Gaussian complex amplitude →
Rayleigh intensity → exponential energy density structure appears in optical
speckle, acoustic reverberation rooms, and quantum chaos (Berry conjecture).

## Derivation Sketch

From `electrodynamics: reasoning.em.dyadic_green_function` (cavity Green's
function dyadic as eigenfunction expansion) and `mathematics-theorems:
mathematics.plane_wave_spectrum` (plane-wave integral representation):

### 1. Plane-wave-spectrum representation

For an electrically large cavity with many modes excited well above cutoff:
```
E(r) = ∫_{4π} F(Ω) e^{ik·r} dΩ
```
where F(Ω) is the angular plane-wave spectrum. Each direction Ω contributes
an independent plane wave. With incoherent excitation (stirring, mode
stirring, or source decorrelation), the F(Ω) components become statistically
independent random variables.

### 2. CLT → Gaussian field components

Each Cartesian field component receives contributions from many independent
plane waves. By the CLT, as the number of contributing modes N → ∞:
```
E_x(r), E_y(r), E_z(r) are jointly Gaussian complex RVs
Real/imag parts: E_xr, E_xi ~ N(0, σ²),   σ² = E₀²/6
```
The factor 1/6 comes from equipartition: 3 spatial components × 2 (real +
imag) = 6 degrees of freedom sharing the total mean-square field E₀².
This relies on spatial uniformity and isotropy of the cavity field (Hill §7.2,
eq 7.15-7.17).

### 3. PDF hierarchy (Hill §7.2-7.3)

From Gaussian field components, the distributions of derived quantities
follow from standard probability transformations:

| Quantity | Distribution | Parameters | Hill Eq |
|----------|-------------|-----------|---------|
| Real/imag part E_xr | Gaussian N(0,σ²) | σ²=E₀²/6 | 7.31 |
| Magnitude |E_x| | Rayleigh (chi-2 DoF) | Scale σ | 7.36 |
| Squared mag |E_x|² | Exponential (chi²-2) | Mean=E₀²/3 | 7.37 |
| Total magnitude |E| | Chi-6 | Scale σ | 7.38 |
| Total squared |E|² | Chi²-6 | Mean=E₀² | 7.39 |

The transformation chain is:
```
Gaussian components → Rayleigh magnitude (= √(X²+Y²) for X,Y~N(0,σ²))
                   → Exponential squared magnitude
                   → Chi-6 total (= √(Σ₆ X_i²) for 6 independent Gaussians)
```

### 4. Spatial correlation and coherence

The spatial autocorrelation function has tensor structure (Hill §7.4):
```
ρ_ij(R) = ⟨E_i(r)E_j*(r+R)⟩ / ⟨|E|²⟩
        ∝ [δ_ij − R̂_i R̂_j] j₀(kR) + [3R̂_i R̂_j − δ_ij] j₂(kR)
```
where j₀, j₂ are spherical Bessel functions. The dominant term decays as
sinc(kR) with coherence length ~λ/2 — the half-wavelength correlation
characteristic of random isotropic fields.

### 5. Equipartition and energy balance

The electric and magnetic energy densities are equal on average (Hill eq 7.20):
```
⟨ε|E|²⟩ = ⟨μ|H|²⟩
```
This holds for any statistically isotropic random field satisfying Maxwell's
equations in free space.

### 6. Limits of validity

- Electrical size: kL ≫ 1 (overmoded condition)
- Sufficient mode density: the number of modes within the bandwidth must be
  large enough that CLT applies (typically > 100 modes)
- Mechanical / frequency stirring: ensures statistical independence of modes
- Fails near walls (coherent boundary condition breaks isotropy within ~λ/4)

## Cross-Domain Unification Table

The Gaussian complex amplitude → Rayleigh intensity → exponential energy
pattern recurs across four wave-physics domains:

| Domain | Phenomenon | Same Gaussian+Chi Statistics | Key Reference |
|--------|-----------|------------------------------|---------------|
| EM reverberation chamber | Field statistics inside electrically large cavity | Hill §7.2-7.4 | Hill 2009 |
| Optical speckle | Intensity fluctuations from rough-surface scattering | Same Gaussian complex amplitude → Rayleigh intensity PDF | Goodman, *Statistical Optics* |
| Acoustic reverberation | Sound field in large rooms | Same Gaussian pressure → exponential energy density | Sabine 1900 |
| Quantum chaos / RMT | Wavefunction statistics in classically chaotic billiards | Wigner-Dyson level statistics; Berry conjecture for eigenfunctions | Berry 1977; BGS 1984 |

The unifying principle: any wave system where the field is a superposition
of many independent, incommensurate modes with random phases produces the
same Gaussian statistics, independent of the specific wave equation.

## Algorithm — Given Cavity → Statistical Field Model

```
1. Verify overmoded condition: k_min L ≫ 1. Count modes within bandwidth
   Δf: N_modes ≈ 8π V f² Δf / c³ (Weyl formula).

2. If stirring is present (mechanical or frequency), assume statistical
   uniformity and isotropy for the stirred field.

3. Gaussian field model:
   - Each Cartesian component ~ complex Gaussian N(0,σ²) with σ² = E₀²/6.
   - E₀² = Q P_tx / (ω ε₀ V) from power balance (Q = quality factor,
     P_tx = transmit power, V = cavity volume).

4. Derived distributions:
   - |E_x| ~ Rayleigh(σ) for single-component magnitude
   - |E| ~ Chi(6,σ) for total magnitude
   - |E|² ~ Gamma(3, 2σ²) for total squared magnitude

5. Threshold exceedance: P(|E| > E_th) = 1 − F_Chi6(E_th/σ).
   For high thresholds, use the chi-6 CDF or extreme-value asymptotics.

6. Spatial correlation: ⟨E_i(r)E_j*(r+R)⟩ decays as sinc(kR) with
   tensor structure above. Independent samples require spacing > λ/2.
```

## Connection to Uncertainty Quantification

Statistical EM (this node) and UQ (`reasoning.cp.uncertainty_quantification`)
both deal with random electromagnetic fields but from complementary angles:
- **UQ**: forward propagation of input parameter uncertainty → output field
  uncertainty (intrusive gPCE or non-intrusive stochastic collocation).
- **Statistical EM**: ensemble of field realizations inside a chaotic cavity;
  the ensemble is produced by mode stirring, not input parameter variation.
- **Ergodicity connection**: For a stationary stirred chamber, the time
  average of the reverberant field equals the spatial average of UQ ensemble
  outputs → ergodic equivalence bridges the two frameworks.

## Edge Cases

- **Unstirred / undermoded cavity**: CLT fails below a minimum mode count.
  The field statistics are not Gaussian — individual modes dominate.
- **Near conducting walls**: Boundary conditions impose correlations that
  break isotropy within ~λ/4 of walls. The field enhancement near a
  conducting surface follows a different (non-Rayleigh) distribution.
- **Anisotropic cavity**: If one dimension is much smaller (e.g., thin
  parallel-plate chamber), the field cannot be isotropic. Separate the
  statistics into parallel and perpendicular components.
- **Source directivity**: A highly directional source breaks isotropy unless
  stirring is applied.

## Cross-References

- Hill, D.A., *Electromagnetic Fields in Cavities* (2009) §7.2-7.4
- Goodman, J.W., *Statistical Optics* (2nd ed, 2015) — optical speckle theory
- Sabine, W.C., "Reverberation" (1900/1922) — acoustic reverberation
- Berry, M.V., "Regular and irregular semiclassical wavefunctions" J. Phys. A (1977)
- Bohigas, O., Giannoni, M.J., Schmit, C., "Characterization of chaotic quantum
  spectra" Phys. Rev. Lett. 52:1 (1984) [BGS conjecture]
- electrodynamics: reasoning.em.dyadic_green_function (parent — cavity G̿ eigenfunction expansion)
- mathematics-theorems: mathematics.plane_wave_spectrum (plane-wave integral representation)
- computational-physics: reasoning.cp.uncertainty_quantification (UQ framework — ergodic connection)
