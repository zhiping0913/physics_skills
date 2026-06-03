---
skill_id: knowledge.optics.aberrations_polarization
type: knowledge
summary_50t: >
  Seidel: spherical, coma, astigmatism, field curv, distortion. Zernike:
  Z₁ piston, Z₂₃ tip/tilt, Z₄ defocus, Z₅₆ astig, Z₇₈ coma, Z₁₁ spherical.
  Strehl S≈exp(−(2πσ/λ)²). Maréchal: S>0.8→diffraction-limited.
  Jones (2×2, fully polarized). Mueller (4×4, partial/depolarized).
trigger: analyzing wavefront error, designing optical systems, polarization optics
reasoning_role: aberrations
parent: knowledge.em.crystal_optics
retrieval_cost: 1
references:
  - electrodynamics: knowledge.em.crystal_optics (polarization optics)
---

# knowledge.optics.aberrations_polarization

**Seidel aberrations** (3rd order, rotationally symmetric):
Spherical: σ_sph∝NA⁴, on-axis only. Coma: ∝NA³·y_field, asymmetric blur.
Astigmatism: ∝NA²·y_field², tangential/sagittal foci differ.
Field curvature: ∝NA²·y_field², image on curved surface.
Distortion: ∝y_field³, pincushion (+)/barrel (−), sharp but displaced.

**Zernike polynomials**: Z_n^m(ρ,θ) orthogonal on unit circle.
Z₁=1 (piston). Z₂=ρ cos θ, Z₃=ρ sin θ (tip/tilt). Z₄=2ρ²−1 (defocus).
Z₅=ρ² sin 2θ, Z₆=ρ² cos 2θ (astigmatism). Z₇=(3ρ³−2ρ)sin θ, Z₈=(3ρ³−2ρ)cos θ (coma).
Z₁₁=6ρ⁴−6ρ²+1 (spherical). RMS wavefront σ_W=√(Σ|c_n|²) for n≥2.

**Strehl ratio**: S=I_aberrated(0)/I_perfect(0). S≈exp(−(2πσ_W/λ)²) (small σ_W).
Maréchal: S>0.8 → effectively diffraction-limited → σ_W<λ/14.

**Jones calculus**: [E_x';E_y']=J[E_x;E_y]. Polarizer: diag(1,0). Waveplate:
diag(1,e^{iφ}). Rotator: [cos θ sin θ;−sin θ cos θ].

**Mueller calculus**: [S']=M[S], 4×4. Stokes: S₀=I, S₁=I_x−I_y, S₂=I_45−I_−45, S₃=I_R−I_L.
DOP=√(S₁²+S₂²+S₃²)/S₀. Depolarization: reduces DOP. Diattenuation: transmission
depends on polarization. Retardance: phase shift between eigenpolarizations.

- Iizuka §4-5, §9; Born & Wolf §9
