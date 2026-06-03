---
skill_id: knowledge.em.kirchhoff_diffraction_detail
type: knowledge
summary_50t: >
  Kirchhoff integral: U(P)=−(ikU₀/4π)∬(e^{ikr}/r)(1+cosθ)dS. Fresnel
  N_F=a²/λz. Fresnel zone: Cornu spiral C(w),S(w). Fraunhofer: FT of aperture.
  Rectangle: I∝sinc²(πa sinθ_x/λ)sinc²(πb sinθ_y/λ). Circle: Airy [2J₁(x)/x]².
trigger: computing diffraction patterns from apertures of known shape
reasoning_role: kirchhoff_data
parent: reasoning.em.scalar_diffraction_kirchhoff
retrieval_cost: 1
---

# knowledge.em.kirchhoff_diffraction_detail

**Kirchhoff integral**: U(P)=−(ik/4π)∬ U₀(e^{ikr}/r)(cosθ₁+cosθ₂)dS.
Obliquity factor: (cosθ₁+cosθ₂)≈(1+cosθ) for normal incidence.

**Fresnel zones**: annular zones where path length increases by λ/2.
Zone plate radius r_n=√(nλf+n²λ²/4)≈√(nλf). Focuses like lens with f_n=r₁²/nλ.

**Cornu spiral**: complex Fresnel integrals C(w)=∫₀^w cos(πu²/2)du,
S(w)=∫₀^w sin(πu²/2)du. w=z√(2/λ)(1/d₁+1/d₂)^{1/2}. Straight edge:
I/I₀ behind edge oscillates, first maximum I≈1.37I₀.

**Rectangular aperture** a×b: I(x,y)=I₀ sinc²(πax/λz)sinc²(πby/λz).
**Circular aperture** D: I(θ)=I₀[2J₁(kD sinθ/2)/(kD sinθ/2)]².
Airy disk radius: θ_min=1.22λ/D. Central maximum contains 84% of energy.
**N-slit grating** (d=period): I=I₀[sin(Nπd sinθ/λ)/sin(πd sinθ/λ)]².

**Babinet**: A+B complementary → diffraction patterns identical outside
direct beam. Wire = slit of same width (diffraction only).

- Born & Wolf §8.3-8.6, Goodman §3-4
