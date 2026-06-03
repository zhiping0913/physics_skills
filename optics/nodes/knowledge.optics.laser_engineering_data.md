---
skill_id: knowledge.optics.laser_engineering_data
type: knowledge
summary_50t: >
  He-Ne 632.8nm, Nd:YAG 1064nm, Ti:Sapph 700-1100nm, CO₂ 10.6μm, diode.
  4-level: η_slope∝T/(T+L). Q-switch: P_peak∝ΔN_i/τ_c. Mode-lock: τ_p≈0.44/Δν.
  CPA: stretch→amp→compress. f_rep=c/2L. Comb: f_n=n f_rep+f_CEO.
trigger: selecting gain medium, computing laser output power, pulse energy
reasoning_role: laser_data
parent: reasoning.optics.laser_rate_equations
retrieval_cost: 1
---

# knowledge.optics.laser_engineering_data

**Gain media**: He-Ne (λ=632.8nm, Doppler Δν∼1.5GHz, P∼mW).
Nd:YAG (1064nm, τ=230μs, 4-level, P∼kW cw). Ti:Sapphire (700-1100nm, τ=3μs,
vibronic, tunable, fs pulses). Yb:YAG (1030nm, τ=1ms, low quantum defect ∼9%).
CO₂ (10.6μm, τ∼ms, P∼kW cw). Diode (GaAs 808nm, InGaAsP 1.3-1.55μm, η>50%).
Er:fiber (1.55μm, eye-safe, telecom). Excimer (ArF 193nm, KrF 248nm, UV).

**Slope efficiency** (4-level): η_slope = η_pump·(T/(T+L))·(hν_laser/hν_pump).
T=output coupling, L=round-trip loss. Threshold: P_th = hν_p·(T+L)·A/(2σ τ η_pump).

**Q-switch active**: AOM/EOM. P_peak ≈ (hν/τ_c)ΔN_i V. τ_pulse∼τ_c∼10ns.
Energy: E_out ≈ (ΔN_i−ΔN_f)hν V. Passive: Cr⁴⁺:YAG saturable absorber.

**Mode-locking**: transform limit τ_p=0.44/Δν (Gauss), 0.315/Δν (sech²).
Ti:Sapph: τ_p∼5fs (Δν∼100THz, octave-spanning). f_rep=80MHz (L≈1.9m).
P_avg∼1W → P_peak∼2.5MW (τ_p=5fs).

**CPA**: stretch to ∼ns → amplify in Ti:Sapph or fiber → recompress.
P_peak ∼ PW achieved. ELI (10PW), NIF-ARC (PW-class petawatt).

**Frequency comb**: f_n=n f_rep+f_CEO. f-2f self-referencing. Optical clock:
Δf/f∼10⁻¹⁸. Applications: precision spectroscopy, distance metrology, exoplanet detection.

- Siegman §6-7, §24, §27; Svelto §7-8
