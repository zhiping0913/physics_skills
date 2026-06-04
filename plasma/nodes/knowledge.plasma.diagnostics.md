---
skill_id: knowledge.plasma.diagnostics
type: knowledge
summary_50t: >
  Thomson: σ_T=6.65×10⁻²⁹m², T_e from Doppler, n_e from intensity. Collective:
  α=1/kλ_D>1→ion feature+electron satellites. Interferometry: Δφ∝∫n_edl.
  Faraday: Δψ∝∫n_eB_∥dl. ECE: T_e(r) from optically thick harmonics. Probe:
  I-V→T_e,n_e. Spectroscopy: Stark broadening→n_e, Zeeman→B, Doppler→T_i.
trigger: selecting diagnostic for plasma parameter measurement
reasoning_role: diagnostics
parent: reasoning.plasma.dispersion_relation_method
retrieval_cost: 1
---

# knowledge.plasma.diagnostics

**Thomson scattering** (Hutchinson §5-7): σ_T=(8π/3)r_e²=6.65×10⁻²⁹ m².
Incoherent (α≪1): scattered spectrum = Doppler-broadened Gaussian,
Δλ/λ∝√(T_e/m_e c²). T_e[eV]≈(Δλ_1/e/λ·1.05×10⁻⁴)². n_e from absolute
intensity calibration. Collective (α=1/kλ_D>1): Salpeter parameter α.
Ion feature (narrow, λ_D scale) + electron satellites (broad, ω=±ω_p).

**Interferometry** (Hutchinson §3): Δφ=(e²/2ε₀m_e c ω)∫n_e dl.
For λ=1.06μm: Δφ=3.8×10⁻²⁰ rad·m²·n̅_e·L. Fringe counting: N_f=Δφ/2π.
Two-color for vibration compensation. Heterodyne for higher sensitivity.

**Faraday rotation** (Hutchinson §3): Δψ=(e³λ²/8π²ε₀m_e²c³)∫n_eB_∥dl.
For λ=1mm, ITER: Δψ∼10° → I_p measurement. Cotton-Mouton (⊥B): Δφ∝∫n_eB_⊥²dl.

**ECE** (Hutchinson §4): optically thick harmonics (τ≫1)→blackbody I(ω)∝T_e.
τ=1 layer at ω=nω_ce→T_e(r). nth harmonic: optically thick at n_e high enough.
ECE imaging: 2D array of detectors → T_e(r,t) movies.

**Langmuir probe** (Hutchinson §2): I-V characteristic: ion saturation at
V≪V_f, electron retarding at V_f<V<V_p. T_e from ln(I_e) slope. n_e from
I_sat=(1/2)en₀c_s A_probe. RF compensation needed in RF plasmas.

**Spectroscopy**: Stark broadening (H_β): Δλ_1/2∝n_e^{2/3}. n_e>10²⁰m⁻³.
Doppler: Δλ/λ=√(8kT_i ln2/m_i c²). Zeeman: Δλ∝B. Line ratios: coronal
equilibrium→T_e. CXRS: fully stripped impurity + neutral beam→line emission→T_i(r).

- Hutchinson (entire book)
