---
skill_id: knowledge.optics.advanced_nonlinear_optics
type: knowledge
summary_50t: >
  Soliton: i∂A/∂z=(β₂/2)∂²A/∂T²−γ|A|²A, N²=γP₀T₀²/|β₂|. N=1 fundamental.
  EIT: quantum interference→transparency, v_g∼c/10⁶. Comb: f_n=n f_rep+f_CEO,
  f-2f. Supercontinuum: SPM+soliton fission+DW. OPO: ω_p=ω_s+ω_i, tuning.
trigger: soliton propagation, EIT/slow light, frequency comb, supercontinuum
reasoning_role: adv_nonlinear
parent: reasoning.em.nonlinear_optical_response
retrieval_cost: 1
references:
  - electrodynamics: reasoning.em.nonlinear_optical_response
---

# knowledge.optics.advanced_nonlinear_optics

**Optical soliton** (Boyd §7): NLS i∂A/∂z=(β₂/2)∂²A/∂T²−γ|A|²A.
Soliton order N²=γ P₀ T₀²/|β₂|. N=1: fundamental, sech² shape, propagates
unchanged. N>1: periodic evolution (soliton period z₀=πT₀²/(2|β₂|)).
Anomalous dispersion (β₂<0) needed for bright soliton. Normal (β₂>0): dark soliton.

**EIT** (electromagnetically induced transparency, Boyd §6): three-level Λ system.
Coupling laser creates dressed states → destructive quantum interference → absorption
cancels at line center. Transparency window Δω∼Ω_c (Rabi frequency of coupling field).
Refractive index slope at transparency → v_g=c/(n+ω dn/dω)≈c/10⁶. Slow light:
light pulses delayed by ∼μs in mm. Storage: coupling field off→probe stored as
spin coherence→coupling on→retrieved. Quantum memory.

**Frequency comb** (Nobel 2005): f_n=n f_rep+f_CEO. f_rep=c/2L (MHz-GHz).
f_CEO from group/phase velocity difference. f-2f self-referencing: SHG of comb
near ν → beat with comb near 2ν → f_CEO. Carrier-envelope phase stabilized to
∼mrad. Optical atomic clocks: Sr (429 THz, Δf/f∼10⁻¹⁸).

**Supercontinuum**: Pulsed laser in PCF (photonic crystal fiber). SPM broadens
spectrum → soliton fission (higher-order dispersion) → dispersive wave generation
at phase-matched wavelengths → octave-spanning white light. Applications: OCT
(optical coherence tomography, resolution ∼μm), frequency comb generation, spectroscopy.

**OPO**: pump ω_p→ω_s+ω_i. Doubly resonant (DRO): lower threshold, complex tuning.
Singly resonant (SRO): higher threshold, smooth tuning. Tuning: temperature,
angle, or pump wavelength. MgO:PPLN: fan-out grating for wide tuning.

- Boyd §6-7, §12; Svelto §9
