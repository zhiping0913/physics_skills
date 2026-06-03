---
skill_id: knowledge.optics.wave_propagation_real_media
type: knowledge
summary_50t: >
  Attenuation α=ω/(2cQ), Q⁻¹∝ω⁰ (constant-Q). Christoffel: |c_ijkl n_j n_l−ρv²δ_ik|=0
  → qP, qS1, qS2. Biot slow P-wave: fluid+frame coupling. Thomsen ε,δ,γ for VTI.
  K-K demands dispersion with attenuation. Fracture: anisotropy from aligned cracks.
trigger: wave propagation in attenuating, anisotropic, or porous media
reasoning_role: real_media
parent: knowledge.continuous.dielectric_dispersion
retrieval_cost: 1
references:
  - landau-graph: knowledge.continuous.dielectric_dispersion (ideal ε(ω))
---

# knowledge.optics.wave_propagation_real_media

**Attenuation** (Carcione §2-3): Q=2π E_stored/E_lost per cycle. Q≫1 in most
rocks/solids (Q∼10²−10³). Q_p > Q_s (P-waves less attenuated than S-waves).
α(ω)=ω/(2cQ). Constant-Q model: α∝ω (linear with f). Kramers-Kronig: attenuation
→ dispersion n(ω)=n(ω₀)[1+(1/πQ)ln(ω/ω₀)].

**Anisotropy** (Carcione §4): Christoffel eq |c_ijkl n_j n_l − ρv²δ_ik|=0.
Three eigenvalues → three wave types. Direction-dependent velocity.
Phase velocity v (⊥ to wavefront) ≠ group velocity (energy propagation).
Slowness surfaces (1/v vs direction): spherical (isotropic), ellipsoidal (VTI).
Cusps in group-velocity surfaces at triplication points.

**Biot theory** (§7): Fluid-saturated porous solid. Frame moduli (dry rock) +
fluid moduli + porosity φ. Two P-waves: fast (frame+fluid in phase) and
slow (frame+fluid out of phase, diffusive at low f). Slow P-wave discovered
by Plona (1980) — confirmed Biot prediction.
Viscodynamic operator: frequency-dependent tortuosity α(ω)→∞ at high f.
Transition frequency f_c=ηφ/(2πκρ_f α_∞). Below f_c: viscous (Darcy). Above:
inertial (Biot slow wave propagates).

**Fractures** (§4): Aligned cracks → HTI (horizontal transverse isotropy).
Thomsen parameters for VTI: ε=(c₁₁−c₃₃)/2c₃₃, γ=(c₆₆−c₄₄)/2c₄₄,
δ=[(c₁₃+c₄₄)²−(c₃₃−c₄₄)²]/[2c₃₃(c₃₃−c₄₄)].
Anellipticity η=(ε−δ)/(1+2δ). η=0: elliptical (SH-wavefronts are ellipses).
η≠0: anelliptic.

**Applications**: Seismic (AVO/AVAZ for reservoir characterization), medical
ultrasound (shear-wave elastography, Q-imaging), NDE (composite delamination
detection, porosity mapping).

- Carcione §1-8
