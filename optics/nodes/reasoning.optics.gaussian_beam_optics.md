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

## Key Parameters

- **Rayleigh range**: z_R = πw₀²/λ. Beam area doubles at z = z_R.
- **Gouy phase**: ψ(z) = arctan(z/z_R). Total π phase shift through focus.
- **Resonator stability**: g₁ = 1−L/R₁, g₂ = 1−L/R₂. Stable if 0 < g₁g₂ < 1.
- **M² factor**: M² = (π/λ) w₀ θ. M² = 1 for ideal Gaussian. M² ≥ 1.
- **Brightness**: B = P/(λ² M_x² M_y²). Invariant in lossless optics.

## Edge Cases

- **Non-paraxial** (NA > 0.5): scalar paraxial theory fails. Need vector
  diffraction theory (Richards-Wolf).
- **High-power thermal lensing**: dn/dT > 0 → thermal gradient → effective lens.
  Changes resonator stability dynamically.
- **Higher-order modes**: Hermite-Gauss HG_mn (rectangular symmetry) and
  Laguerre-Gauss LG_pl (cylindrical symmetry, p=radial, l=azimuthal).
  LG₀l carries orbital angular momentum (OAM) ℏl per photon. Applications:
  optical tweezers, quantum communication, STED microscopy.

## Cross-References

- Siegman §16-21, Marcuse §2-4
- landau-graph: reasoning.normal_mode_decomposition (modes from eigenvalue problem)
