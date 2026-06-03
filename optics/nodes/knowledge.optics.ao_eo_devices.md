---
skill_id: knowledge.optics.ao_eo_devices
type: knowledge
summary_50t: >
  AOM: θ_B=λf_a/2nv_s, η=sin²(πL/λ√(M₂I_a/2)), N=τΔf spots. EOM:
  V_π=λd/(2n³rL), Δφ=π V/V_π. Pockels: LiNbO₃ r₃₃≈30pm/V. Kerr: Δn=λK E².
  AO tunable filter: λ(nm)∝v_s/f_a. AOFS: ω_out=ω_in±Ω. Q-switch driver.
trigger: designing AO/EO modulators, deflectors, frequency shifters, Q-switches
reasoning_role: ao_eo_data
parent: reasoning.optics.acousto_optic_interaction
retrieval_cost: 1
---

# knowledge.optics.ao_eo_devices

**AOM (acousto-optic modulator)**:
Bragg angle θ_B=λf_a/(2nv_s). Rise time τ=d/v_s (d=beam diameter).
Bandwidth Δf≈0.35/τ. N_resolvable=τ Δf (time-bandwidth product ∼Δf·d/v_s).
RF drive power P_RF≈(λ²H/(2M₂L))·η/sin²(√η) for efficiency η.
TeO₂ slow-shear: v_s=617m/s, M₂=1200×10⁻¹⁵ s³/kg, Δf∼50MHz at 633nm.

**AO deflector**: scan angle Δθ=(λ/nv_s)Δf. Random access time τ.
AO tunable filter (AOTF): λ selected by f_a. TeO₂ non-collinear: λ=Δn·v_s/f_a.
Resolution R=λ/Δλ∝L/Λ. Tuning range: visible to IR.

**EOM (electro-optic modulator)**:
Pockels effect: Δ(1/n²)_i=r_ij E_j. Phase retardation Γ=πV/V_π.
V_π=λd/(2n³r L) (transverse), V_π=λ/(2n³r) (longitudinal).
LiNbO₃: n_o≈2.29, r₃₃≈30.8 pm/V → V_π≈2kV·(d/L) at 633nm (transverse).
KDP: n_o≈1.51, r₆₃≈10.6 pm/V. Amplitude modulator: EOM between crossed polarizers
at 45° → I_out=I_in sin²(Γ/2). Phase modulator: single polarization.

**Kerr effect**: Δn=λK E². K_CS₂≈3.3×10⁻¹⁴ m/V². K_nitrobenzene≈3×10⁻¹².
Response time: electronic (fs), molecular reorientation (ps-ns).

**Applications**:
- AOM: Q-switch driver (hold RF off→store→RF on→dump), pulse picker, frequency shifter.
- EOM: Q-switch (fast, ∼ns), pulse slicer, cavity dumper, phase modulator for
  frequency comb stabilization, Pockels cell for regenerative amplifier injection/extraction.
- AOFS (acousto-optic frequency shifter): +1 order shifted by +f_a. Used in heterodyne
  interferometry, laser Doppler velocimetry.

- Yariv §9-11, Iizuka §14
