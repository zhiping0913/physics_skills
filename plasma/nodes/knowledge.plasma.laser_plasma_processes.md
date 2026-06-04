---
skill_id: knowledge.plasma.laser_plasma_processes
type: knowledge
summary_50t: >
  n_c[cm⁻³]=1.1×10²¹/λ_μm². IB: α∝Zn_e²T_e^{−3/2}. SRS/SBS/TPD thresholds
  and growth. Ponderomotive: f_p=−(e²/4mω²)∇|E|². Wakefield: E∼100GV/m.
  Brunel: vacuum heating. Hole boring: v_hb/c=√(I/ρc³)/(1+√...).
trigger: computing laser absorption, parametric thresholds, acceleration
reasoning_role: lpi_knowledge
parent: reasoning.plasma.laser_plasma_interaction
retrieval_cost: 1
---

# knowledge.plasma.laser_plasma_processes

**Critical density**: n_c = ε₀m_e ω²/e² ≈ 1.1×10²¹/λ_μm² cm⁻³.
Below n_c: laser propagates. At n_c: reflected.

**Inverse bremsstrahlung**: α_IB[cm⁻¹] = 3.1×10⁻⁷ Z n_e² lnΛ / T_e[eV]^{3/2} √(1−n_e/n_c).

**Resonance absorption**: fraction absorbed ≈ ½φ²(τ), τ=(k₀L)^{1/3} sin θ.
Optimal angle: sin θ≈0.8/(k₀L)^{1/3}. Hot electron temperature T_hot ∝ (Iλ²)^{1/3−1/2}.

**SRS** (ω₀=ω_s+ω_epw): γ/ω₀ ≈ (k_epw v_osc/4)√(ω_p/ω₀). Backscatter at k_epw≈2k₀.
**SBS** (ω₀=ω_s+ω_iaw): γ/ω₀ ≈ (k_iaw v_osc/4)√(Zn_c/n_0 m_e/m_i).
**TPD** (ω₀=ω_1+ω_2): threshold I₁₄λ_μm² T_keV/L_μm > 10 at n_c/4.

**Ponderomotive**: Φ_p = e²|E|²/4mω² ≈ 9.3×10⁻¹⁴ I[W/cm²]λ_μm² eV.
Hole boring: v_hb/c = √(I/ρc³)/(1+√(I/ρc³)).

**Wakefield**: E_max [GV/m] ≈ 96 √(n_e/10¹⁸ cm⁻³) for a₀∼1.
Bubble regime (a₀>2): spherical cavity, self-injection, quasi-monoenergetic.
LWFA: E∼1GeV over ∼cm. PWFA: E∼50GeV over ∼m (proton-driven).

- Handbook PP-3, Kruer, Gibbon
