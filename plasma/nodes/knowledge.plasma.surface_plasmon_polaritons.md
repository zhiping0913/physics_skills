---
skill_id: knowledge.plasma.surface_plasmon_polaritons
type: knowledge
summary_50t: >
  k_SPP=(ω/c)√(ε_dε_p/(ε_d+ε_p)). Drude ε_p=1−ω_p²/ω²→ω<ω_p/√(1+ε_d).
  Kretschmann: R_min at θ_SPR gives k_SPP. LSPR: ε_p=−2ε_d (sphere), |E_loc/E₀|∝Q.
  SERS enhancement∼|E|⁴. Purcell F_p∝Q/V. Propagation length L_SPP=1/(2Im[k_SPP]).
trigger: designing plasmonic sensors, computing SPP dispersion and confinement
reasoning_role: spp_data
parent: reasoning.plasma.surface_waves_plasmonics
retrieval_cost: 1
---

# knowledge.plasma.surface_plasmon_polaritons

**SPP dispersion**: k_SPP=(ω/c)√(ε_dε_p/(ε_d+ε_p)). Drude: ε_p=1−ω_p²/ω².
Asymptote ω→ω_p/√(1+ε_d). Momentum mismatch with free-space: k_SPP>k₀→needs
grating or prism coupling. Confinement: δ_d=1/(k₀√(ε'_p+ε_d)/(ε_d)²),
δ_p=1/(k₀√(ε'_p+ε_d)/ε'_p²). Ag at 633nm: δ_p≈25nm, δ_d≈300nm.

**Kretschmann**: prism(n_p)+thin metal(d∼50nm)+dielectric. ATR dip at
θ where k_x=(ω/c)n_p sinθ=k_SPP. R(θ) fit→ε_p(ω). Otto: prism+gap+metal.

**LSPR** (nanoparticle): Fröhlich condition Re[ε_p]=−2ε_d (sphere in
uniform field). Resonance λ depends on size (<50nm: quasi-static), shape
(rod: two peaks, longitudinal red-shifted), and environment (RI sensing:
Δλ/RIU∼100-1000 nm/RIU). Field enhancement |E_loc/E₀|∝Q (∼10² for Ag,
Q≈10-50). SERS: enhancement ∝|E(ω_L)|²|E(ω_R)|²∼10⁶-10¹⁰.

**Purcell**: F_p=(3/4π²)(λ/n)³(Q/V_mode). V_mode small for plasmonic cavities
→F_p≫1. L_SPP=1/(2Im[k_SPP])=v_g τ_SPP. Ag: L_SPP∼10-100μm (visible).

**Near-field coupling**: sub-nm gap→tunneling→quantum plasmonics (reserved).

- Shah §2-4, Maier §2-7
