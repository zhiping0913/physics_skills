---
skill_id: reasoning.optics.gaussian_beam_optics
type: reasoning
summary_50t: >
  Paraxial beams: q-parameter 1/q=1/R−iλ/πw². ABCD law q₂=(Aq₁+B)/(Cq₁+D).
  Free space, lens, mirror are ABCD matrices. Resonator stability: |(A+D)/2|<1.
  Mode matching, M² factor, brightness B=P/(λ²M²)².
trigger:
  - designing laser resonators, computing beam propagation
  - mode matching between cavities/fibers
reasoning_role: gaussian_beam
parent: reasoning.normal_mode_decomposition
retrieval_cost: 1
sign_convention: >
  q-parameter: 1/q = 1/R − iλ/(πw²). Time convention e^{i(kz−ωt)}.
  R>0 for diverging wavefront (curvature center upstream). Gouy phase
  accumulated through focus: total π. M² ≥ 1 by definition (M²=1 ideal).
references:
  - landau-graph: reasoning.normal_mode_decomposition (resonator modes = eigenfunctions)
---

# reasoning.optics.gaussian_beam_optics — q-parameter → ABCD → Mode

## Core Picture

In the paraxial approximation (θ ≪ 1), a monochromatic beam propagating along z
is described by a complex q-parameter (Siegman §16-20, Marcuse §2):

```
1/q(z) = 1/R(z) − iλ/(π w²(z))
```

where R(z) is the wavefront radius of curvature and w(z) is the 1/e² beam radius.
The q-parameter propagates through any paraxial optical system via the ABCD law:
**q₂ = (A q₁ + B) / (C q₁ + D)**.

## Derivation Sketch

Starting from `landau-graph: reasoning.normal_mode_decomposition` (resonator
modes are eigenfunctions of the round-trip operator; each mode is a
self-consistent field distribution):

1. **Paraxial wave equation** (the key reduction):
   Insert ansatz E(x,y,z) = ψ(x,y,z) e^{i(kz−ωt)} into the Helmholtz equation
   (∇² + k²)E = 0. In the paraxial limit (∂²ψ/∂z² ≪ 2k ∂ψ/∂z), the
   second z-derivative drops out, yielding the paraxial wave equation:
   ```
   ∂²ψ/∂x² + ∂²ψ/∂y² + 2ik ∂ψ/∂z = 0
   ```
   This is the Schrödinger equation with z as "time" — the foundation for
   all Gaussian beam optics.

2. **Fundamental Gaussian solution**: The ansatz ψ(x,y,z) ∝ exp[ik(x²+y²)/2q(z)]
   with 1/q = 1/R − iλ/πw² satisfies the paraxial equation when:
   q(z) = q₀ + z  (free-space propagation), with q₀ = i z_R at the waist.
   This is the lowest-order eigenmode — analog to the ground state in
   a harmonic oscillator, consuming the parent's "modes as eigenfunctions"
   framework.

3. **ABCD law derivation** (the non-obvious step — Siegman §20):
   For an optical system described by a 2×2 ray matrix [A B; C D], the
   ray position and angle transform as [x₂; θ₂] = M [x₁; θ₁]. For a
   Gaussian beam, the complex radius q = x/θ (since θ = ∂ψ/∂x ∝ (ik/q)ψ·x).
   Then q₂ = (A q₁ + B)/(C q₁ + D) follows directly from the ray optics
   algebra applied to the complex beam parameter. This unification of ray
   and wave optics through a COMPLEX ray parameter is the insight that makes
   Gaussian beam design practical.

4. **Eigenmode condition for resonators** (consuming normal_mode_decomposition):
   Self-consistency after one round trip: q = (Aq+B)/(Cq+D). Solving the
   quadratic gives 1/q = (D−A)/(2B) ± i√[1−((A+D)/2)²]/|B|. The stability
   criterion |(A+D)/2| < 1 means the radicand is positive → finite spot size.
   When |(A+D)/2| = 1 (confocal, concentric, plane-parallel), spot size
   diverges and the mode is marginally stable — beam walk-off or finite
   aperture will select the surviving mode.

## Algorithm

```
1. Characterize the beam at a reference plane: w₀ (waist), z_R = πw₀²/λ.
2. Free-space propagation (distance L): q₂ = q₁ + L.
   Equivalent ABCD: [1 L; 0 1].
3. Thin lens (focal length f): 1/q₂ = 1/q₁ − 1/f.
   ABCD: [1 0; −1/f 1].
4. Spherical mirror (radius R, at incidence angle θ):
   Tangential: f = (R/2)cos θ. Sagittal: f = (R/2)/cos θ.
5. Complex system: multiply ABCD matrices in order.
6. Find eigenmode (resonator): self-consistent after round trip.
   q = (Aq+B)/(Cq+D) → 1/q = (D−A)/(2B) ± i√[1−((A+D)/2)²]/|B|.
   Stability: |(A+D)/2| < 1.
```

## Higher-Order Modes (Siegman §16-17)

Beyond the fundamental TEM₀₀ Gaussian, the paraxial wave equation supports
a complete family of orthogonal transverse modes:

- **Hermite-Gauss HG_mn** (rectangular symmetry, stable resonators with
  rectangular apertures):
  ```
  ψ_mn(x,y,z) ∝ H_m(√2 x/w) H_n(√2 y/w) exp[−(x²+y²)/w²]
                × exp[ik(x²+y²)/2R] exp[i(m+n+1)ψ_Gouy]
  ```
  where H_m are Hermite polynomials. The Gouy phase per mode is
  (m+n+1) arctan(z/z_R) — higher-order modes accumulate more Gouy phase,
  which shifts their resonance frequencies: ν_mnq = (q + (m+n+1)/π·arccos√g₁g₂)·c/2L.

- **Laguerre-Gauss LG_pl** (cylindrical symmetry, circular apertures):
  ```
  ψ_pl(r,φ,z) ∝ (r√2/w)^|l| L_p^{|l|}(2r²/w²) exp[−r²/w²]
                × exp(ilφ) exp[i(2p+|l|+1)ψ_Gouy]
  ```
  where L_p^{|l|} are associated Laguerre polynomials. p = radial index,
  l = azimuthal index. LG₀l modes carry ORBITAL ANGULAR MOMENTUM (OAM) of
  ℏl per photon (Allen et al., PRA 45, 8185, 1992). Applications: optical
  tweezers (trapping + rotation), STED microscopy (depletion beam = LG₀₁
  donut), quantum communication (OAM as high-dimensional encoding).

- **Mode conversion**: HG ↔ LG via astigmatic mode converter (π/2 converter:
  pair of cylindrical lenses). HG_mn → LG_pl with p = min(m,n),
  l = m−n.

## Key Parameters

- **Rayleigh range**: z_R = πw₀²/λ. Beam area doubles at z = z_R.
- **Gouy phase**: ψ(z) = arctan(z/z_R). Total π phase shift through focus.
- **Resonator stability**: g₁ = 1−L/R₁, g₂ = 1−L/R₂. Stable if 0 < g₁g₂ < 1.
- **M² factor**: M² = (π/λ) w₀ θ. M² = 1 for ideal Gaussian. M² ≥ 1.
  ISO 11146 standard: measure beam width via D4σ (second-moment method) at
  ≥10 positions through focus, fit hyperbolic w²(z) = w₀²[1+(z−z₀)²/z_R²],
  extract w₀ and θ → M² = (π/λ) w₀ θ. D4σ avoids ambiguity in non-Gaussian
  beam profiles (clipped, structured) where 1/e² width is undefined.
- **Brightness**: B = P/(λ² M_x² M_y²). Invariant in lossless optics.

## Beyond Gaussian: Non-Diffracting and Partially Coherent Beams

- **Bessel beams** (Durnin 1987): solution of Helmholtz with transverse profile
  J₀(k_⊥ r) — propagation-invariant intensity (ideal limit requires infinite
  energy). Produced by axicon (conical lens) or annular aperture + lens.
  Self-healing property: obstacles on axis do not cast a shadow downstream
  (the conical wavefront reconstructs the central spot). Applications:
  light-sheet microscopy, optical coherence tomography, laser machining
  of high-aspect-ratio channels.
  **Breaks down** at finite aperture — finite-energy Bessel-Gauss beams
  have a finite propagation range z_max = w₀ / tan(α) where α is the
  axicon angle. Use Gaussian beams with large z_R as a simpler alternative
  for moderate depth-of-field requirements.

- **Gaussian Schell-model beams** (partially coherent, Mandel & Wolf §5):
  Cross-spectral density W(r₁,r₂) = √[I(r₁)I(r₂)] μ(r₁−r₂) with Gaussian
  spectral degree of coherence μ. The beam still propagates with an ABCD
  law BUT with an effective q-parameter modified by the coherence length σ_μ:
  1/q_eff = 1/R − iλ/(πw²) − iλ/(πσ_μ²). Reduced spatial coherence acts as
  an effective source-size increase → larger divergence → degraded M².
  Relevant for multimode fiber output, LED-coupled systems, and propagation
  through random media (atmospheric turbulence).

## Edge Cases

- **Non-paraxial (NA > 0.5)**: scalar paraxial theory fails. Need vector
  diffraction theory (Richards-Wolf integral, Born & Wolf §8.8). The
  paraxial assumption ∂²ψ/∂z² ≪ 2k ∂ψ/∂z breaks — longitudinal field
  components (E_z) appear, the focal spot becomes asymmetric, and the
  spot size saturates (does not go to zero as predicted by paraxial theory).
  Use Richards-Wolf code (e.g., PSF Lab) for NA > 0.6.
- **High-power thermal lensing**: dn/dT > 0 → thermal gradient → effective lens.
  Changes resonator stability dynamically. Mitigation: active cavity control
  (piezo mirror repositioning based on output power monitor), or cryogenic
  cooling (Yb:YAG at 77K reduces dn/dT by ~10×).
- **M² measurement error**: knife-edge or slit scan gives different M² than D4σ
  for non-Gaussian beams. ISO 11146 mandates D4σ second-moment method. If
  the beam has significant diffraction ring structure, D4σ may overestimate
  M² — use beam propagation ratio from encircled power (86.5% criterion) as
  a practical alternative for multi-mode beams.

## Cross-References

- Siegman §16-21, Marcuse §2-4
- landau-graph: reasoning.normal_mode_decomposition (modes from eigenvalue problem;
  parent edge: actively consumed in Derivation Sketch — resonator eigenmode
  condition derives directly from this)
