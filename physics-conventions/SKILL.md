---
name: physics-conventions
description: "Canonical sign / Fourier / unit / normalization / handedness / naming conventions for all downstream physics skills (electrodynamics, plasma, optics). Contains the full SI↔Gaussian unit conversion (absorbed from si-gaussian-conversion). landau-graph keeps Landau conventions; the boundary is handled by exceptions.landau_graph_bridge."
unit_system: SI
unit_note: >
  Downstream skills (electrodynamics, plasma, optics) use SI and the conventions
  in this skill. landau-graph retains Landau-Lifshitz conventions (Gaussian,
  metric (+−−−), Landau's R/L naming). When a downstream node cites landau-graph,
  apply the bridge rules in exceptions.landau_graph_bridge.
---

# Physics Conventions — Single Source of Truth

When any non-landau skill writes a formula whose sign, normalization, factor,
or naming could differ between standard textbooks, the choice is fixed here.
Nodes following these defaults need not repeat them. Nodes that deviate MUST
declare the deviation in their `sign_convention` frontmatter field.

## Master Convention Table

| # | Topic | **Project Convention** | Landau Exception | Reference |
|---|-------|------------------------|------------------|-----------|
| 1 | Plane-wave phase | **e^{i(k·r − ωt)}** | same | Jackson, Landau, Stix |
| 2 | Fourier pair | **f(t)=∫(dω/2π)F̃(ω)e^{−iωt}, F̃=∫f e^{+iωt}dt** | same | physics FT |
| 3 | Metric signature | **(−+++)** | (+−−−) | MTW / Weinberg |
| 4 | Units | **SI** | Gaussian | Jackson, Griffiths |
| 5 | Right circular pol. | **E CCW in xy from +z (looking back along −k) = CW from source = helicity +1 = (x̂+iŷ)/√2** | Landau optical | IEEE / quantum |
| 6 | Helmholtz Green | **(∇²+k²)G = −δ → G = e^{ikr}/(4πr)** | −4πδ → G = e^{ikr}/r | SI |
| 7 | Charge | **e > 0; q_s = z_s·e (z_e=−1, z_i=+Z)** | same | physics |
| 8 | Cyclotron frequency | **ω_c = qB/m (SIGNED): ω_ce < 0** | same | Stix |
| 9 | Plasma R/L waves | **Stix: R = pos-charge gyration sense** | same | Stix |
| 10 | Fresnel r_p | **Verdet (H-tangential)** | n/a | Verdet / Stratton |
| 11 | χ⁽n⁾ definition | **Boyd Butcher-Cotter: P^(n)=ε₀ ΣK χ⁽n⁾ E₁…Eₙ** | n/a | Boyd §1.5 |
| 12 | n₂ from χ⁽³⁾ | **n₂ = (3/4n₀²ε₀c) Re[χ⁽³⁾₁₁₁₁]** | n/a | Boyd |
| 13 | Z(ζ) plasma disp. | **Fried-Conte: Z(ζ)=π^{−½}∫e^{−x²}/(x−ζ)dx** | same | Fried-Conte / Stix |
| 14 | δW MHD stability | **δW > 0 = stable** | n/a | Friedberg |
| 15 | β plasma | **β = 2μ₀p/B² (SI)** | 8πp/B² (Gaussian) | MHD |
| 16 | a₀ (LPI) | **a₀ = eE_peak/(m_e ω₀ c)** (linear pol.) | n/a | LPI standard |
| 17 | Critical density | **n_c = ε₀ m_e ω²/e²** (SI) | m_e ω²/(4πe²) | SI |
| 18 | Complex ñ | **ñ = n + iκ, κ ≥ 0 absorbing** | same | physics |
| 19 | Spitzer η | **Spitzer-Härm (0.51 e-e correction for Z=1)** | same | Spitzer-Härm |
| 20 | Chirp parameter | **C > 0 = up-chirp** | n/a | NLSE community |
| 21 | β₂ / GDD sign | **β₂ > 0 = normal** (red leads blue) | n/a | NLSE community |
| 22 | ABCD matrix order | **M_total = M_last · … · M_first** | n/a | Siegman |
| 23 | Adiabatic action | **J = ∮p dq** (full action) | same | Landau Vol 1 |
| 24 | TE/TM in waveguide | **TE = E_z = 0** (transverse to k̂) | n/a | Jackson |
| 25 | Stokes parameters | **(s_0,s_1,s_2,s_3), s_3 > 0 = right circ.** | n/a | Born & Wolf |

## Per-Topic Detail Nodes

| Topic | Node ID |
|-------|---------|
| Time / Fourier convention | [[convention.time_fourier]] |
| Metric signature | [[convention.metric_signature]] |
| Units systems + SI↔Gaussian conversion (absorbed from si-gaussian-conversion) | [[convention.units_systems]] |
| Charge & cyclotron sign | [[convention.charge_cyclotron]] |
| Polarization handedness | [[convention.polarization_handedness]] |
| Green's functions normalization | [[convention.green_functions]] |
| Fresnel r_p sign | [[convention.fresnel_rp]] |
| Nonlinear susceptibility χ⁽n⁾ | [[convention.nonlinear_susceptibility]] |
| Plasma dispersion function Z(ζ) | [[convention.plasma_dispersion_function]] |
| Plasma parameters (β, a₀, n_c) | [[convention.plasma_parameters]] |
| MHD energy principle δW | [[convention.mhd_energy_principle]] |
| Transport / resistivity | [[convention.transport_resistivity]] |
| Pulse phase, chirp, β₂, ABCD | [[convention.pulse_phase_chirp]] |
| Action variables J | [[convention.action_mechanics]] |
| Scattering amplitude f | [[convention.scattering_amplitude]] |
| TE/TM in waveguides | [[convention.waveguide_te_tm]] |
| Landau-graph bridge (exceptions) | [[exceptions.landau_graph_bridge]] |

## How Downstream Skills Cite This Skill

Each non-landau skill's `SKILL.md` shall contain:

> Conventions: see `physics-conventions`. Defaults used silently;
> deviations declared in node `sign_convention` frontmatter.

Each reasoning node:
- **Default convention** → no `sign_convention` field needed.
- **Deviation** → `sign_convention: > <one line + justification>`.
- **Two conventions in same node** (e.g., quoting Stix and converting to standard)
  → name both explicitly inline.

## How landau-graph Relates

`landau-graph` retains Landau-Lifshitz conventions (Gaussian, metric (+−−−),
Landau's circular-polarization naming, J = ∮p dq full action). When a downstream
node consumes a landau-graph result, the citing node applies the bridge rules
from [[exceptions.landau_graph_bridge]]. This is asymmetric: downstream → landau
bridges are explicit; landau → downstream does not exist (landau-graph never
references downstream skills).
