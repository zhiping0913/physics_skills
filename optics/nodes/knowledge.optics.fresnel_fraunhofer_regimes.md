---
skill_id: knowledge.optics.fresnel_fraunhofer_regimes
type: knowledge
summary_50t: >
  N_F=a²/λz ≫1: geometric. ∼1: Fresnel, Cornu spiral, Talbot z_T=2a²/λ.
  ≪1: Fraunhofer (FT). Fresnel integrals C(w),S(w). Zone plate f_n=r_n²/nλ.
  Gaussian beam: N_F=z_R/z → far-field at z≫z_R. Talbot: self-image at z_T.
trigger: determining diffraction regime, computing Fresnel/Fraunhofer patterns
reasoning_role: fresnel_regimes
parent: reasoning.optics.fourier_optics_transfer_function
retrieval_cost: 1
---

# knowledge.optics.fresnel_fraunhofer_regimes

**Fresnel number**: N_F=a²/(λz). N_F≫1: geometric optics (ray tracing valid,
negligible diffraction). N_F∼1: Fresnel diffraction (near field, spherical
wavefront curvature matters). N_F≪1: Fraunhofer diffraction (far field or
lens focal plane, field = Fourier transform of aperture).

**Fresnel diffraction**: convolution with quadratic phase kernel.
Rectangular aperture: 2D separable Fresnel integrals. Straight edge:
C(w), S(w) → Cornu spiral. First bright fringe at w≈1.22, I/I₀≈1.37.

**Fresnel integrals**: C(w)=∫₀^w cos(πu²/2)du. S(w)=∫₀^w sin(πu²/2)du.
w=√(2/λz)·x (distance from geometric shadow edge).

**Talbot effect**: periodic object (period a) self-images at z_T=2a²/λ
(Talbot length). At z_T/2: image shifted by a/2. At z_T/4: period halved
(a/2). Used in: array illuminators, displacement sensors.

**Fresnel zone plate**: alternating transparent/opaque annular zones.
r_n²=nλf+n²λ²/4≈nλf (n≪f/λ). f_n=r₁²/(nλ). Multiple foci: f, f/3, f/5...
Resolution: Δ≈1.22Δr (outermost zone width). Efficiency: 10% (amplitude),
40% (phase-reversal).

**Gaussian beam transition**: Fresnel number N_F=z_R/z (z_R=Rayleigh range).
N_F≫1: near field (waist region). N_F∼1: Fresnel region. N_F≪1: Fraunhofer
(far-field divergence θ=λ/(πw₀)).

- Goodman §4-5, Born & Wolf §8
