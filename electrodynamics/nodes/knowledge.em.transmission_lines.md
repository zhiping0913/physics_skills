---
skill_id: knowledge.em.transmission_lines
type: knowledge
summary_50t: >
  TEM: Z₀=√(L/C). Coax: Z₀=(η₀/2π)ln(b/a)≈60ln(b/a)Ω. Γ=(Z_L−Z₀)/(Z_L+Z₀).
  VSWR=(1+|Γ|)/(1−|Γ|). λ/4 transformer: Z₁=√(Z₀ Z_L). Smith chart: Z→Γ plane.
trigger: impedance matching, power transfer in TEM transmission lines
reasoning_role: transmission_lines
parent: reasoning.em.waveguide_mode_decomposition
retrieval_cost: 1
---

# knowledge.em.transmission_lines

**TEM mode** (Ez=Hz=0): V,I satisfy telegrapher's equations. Propagation
constant γ=α+iβ=√((R+iωL)(G+iωC)). Lossless: β=ω√(LC), v_p=1/√(LC)=c/n.
Characteristic impedance Z₀=√(L/C). Coaxial: L=(μ/2π)ln(b/a), C=2πε/ln(b/a)
→ Z₀=(1/2π)√(μ/ε)ln(b/a)≈(60/√ε_r)ln(b/a) Ω. Microstrip: Z₀≈(87/√(ε_r+1.41))ln(5.98h/(0.8w+t)).

**Reflection**: Γ=(Z_L−Z₀)/(Z_L+Z₀). Matched Z_L=Z₀→Γ=0. Short Z_L=0→Γ=−1.
Open Z_L=∞→Γ=+1. VSWR=(1+|Γ|)/(1−|Γ|). Return loss RL=−20log₁₀|Γ| dB.

**Impedance matching**: λ/4 transformer: Z₁²=Z₀ Z_L (single frequency).
Stub tuning: shunt open/short stub at distance d from load. Smith chart:
normalized impedance z=r+jx mapped to Γ-plane → graphical design.

**Power**: P_avg=(|V₀⁺|²/2Z₀)(1−|Γ|²). Maximum available power (conjugate
match: Z_L=Z₀*). Attenuation: α=α_c+α_d (conductor + dielectric loss).

## Substrate-Integrated Waveguide (SIW)

SIW = rectangular waveguide synthesized using two rows of metallized vias in
a dielectric substrate. Bridges microstrip (low cost, high loss) and metal
waveguide (high cost, low loss). Only **TE modes** are supported — TM modes
leak between vias.

**Equivalent width** (Cassivi-Wu-Deslandes 2002):
```
a_eff = W − d²/(0.95 p)
```
where W = center-to-center via row spacing, d = via diameter, p = via period.

**Design rules**:
- p ≤ 2d (to prevent leakage between vias)
- p/λ₀ ≤ 0.05–0.1 (subwavelength period)
- Cutoff: same as rectangular waveguide with width a_eff:
  f_c(TE₁₀) = c/(2 a_eff √ε_r)

**SIW vs microstrip vs metal waveguide**:
| Property | SIW | Microstrip | Metal WG |
|----------|-----|-----------|----------|
| Loss | Medium | High | Low |
| Cost | Low | Low | High |
| Integration | PCB-compatible | PCB-native | Separate component |
| Modes | TE only | Quasi-TEM | TE/TM |
| mm-wave viable | Yes (up to ∼100 GHz) | Marginal (>60 GHz lossy) | Yes |

## EM-Transmission Line Coupling

External electromagnetic fields (lightning, HEMP, HIRF) induce currents
on transmission lines via three canonical coupling models:

**Taylor model** (distributed voltage sources):
dI/dz + Y V = −Y E_tan(z) — tangential E-field drives distributed current
sources along the line via the impedance Y.

**Agrawal model** (scattered voltage formulation):
dV_scat/dz + Z I = E_z_inc — incident axial E-field drives distributed
voltage sources. Scattered voltage V_scat plus incident voltage V_inc
reconstructs the total voltage.

**Rachidi model** (magnetic-field excitation):
V(z) = −∫_0^h ∂B_y/∂t dz — the time-derivative of the incident magnetic
flux drives voltage sources.

These models are equivalent for the same geometry (Štumpf 2019 §12). The
Agrawal form is preferred for numerical implementation because it handles
lossy grounds naturally. All three follow from the reciprocity theorem
applied to the transmission-line equations.

- Jackson §8.1
- Štumpf, *Time-Domain EM Reciprocity in Antenna Modeling* (2019) §12
- Chen et al., *Substrate-Integrated mm-Wave Antennas* (2021) §3
