---
skill_id: reasoning.plasma.strongly_coupled_thermodynamics
type: reasoning
summary_50t: >
  OCP: Γ = (Ze)²/(a kT), a = (3/4πn)^{1/3}. F_ex/(NkT) = aΓ + bΓ^{1/4}
  + cΓ^{-1/4} + d lnΓ + e. Wigner crystallisation at Γ_m ≈ 165 (bcc).
  HNC: g = exp(−V/kT + h − c), c(k) = h(k)/[1 + n h(k)]. From Debye (∝ −Γ^{3/2})
  to Madelung (∝ −0.8975Γ). Quantum: r_s = a/a_B, Thomas-Fermi λ_TF.
trigger:
  - plasma nonideality parameter Γ > 1
  - liquid-like ion structure, Wigner crystallisation
  - astrophysical dense matter (white dwarf interior, giant planet core)
reasoning_role: strongly_coupled_thermodynamics
parent: reasoning.plasma.generalized_fluid_equations
retrieval_cost: 1
---

# reasoning.plasma.strongly_coupled_thermodynamics — Coulomb Fluid → Crystal

## Core Picture

When the Coulomb coupling parameter Γ = (Ze)²/(a k_B T) exceeds ~1
(a = (3/4πn)^{1/3} is the Wigner-Seitz radius, or ion-sphere radius),
the ion subsystem behaves as a strongly-coupled liquid. The Debye-Hückel
theory (perturbative in Γ ≪ 1) fails. The system is described by the
One-Component Plasma (OCP) model: point ions in a uniform neutralizing
electron background (Fortov, Iakubov & Khrapak 2006, Ch.5).

## Derivation Sketch

### 1. The coupling parameter and the OCP limit

The breakdown of weak-coupling theory is signalled by Γ ∼ 1, where the
average Coulomb energy equals thermal energy:

```
Γ = (Ze)² / (a k_B T),    a = (3/4πn_i)^{1/3}
Γ ≪ 1: Debye-Hückel (gas-like),  1 < Γ < 165: Coulomb fluid (liquid-like)
Γ > 165: Wigner crystal (bcc ordered solid)
```

In terms of the Debye screening parameter: N_D = (4π/3)n λ_D³. The
relationship: Γ = (2γ³)^{1/2} = 1/(3N_D), where γ = e²/(λ_D k_B T).
The ideality condition N_D ≫ 1 coincides with Γ ≪ 1 — both express
the requirement that many particles inhabit a Debye sphere.

When electrons are degenerate (n_e λ_e³ ≳ 1, λ_e = ℏ/√(2m_kT)): the
relevant coupling parameter becomes the QUANTUM coupling parameter
γ_q = (r_s/a₀) where r_s = a/a_B. The electron subsystem is then an
ideal Fermi gas, but the ion subsystem remains strongly coupled.

### 2. OCP equation of state from Monte Carlo (Slattery et al. 1980)

The excess internal energy (beyond ideal gas) of the classical OCP,
obtained from Monte Carlo simulations with 32–500 particles per cell
over 0.05 < Γ < 300, is fitted by:

```
u_ex/(NkT) = a Γ + b Γ^{1/4} + c Γ^{-1/4} + d ln Γ + e
```

where a = −0.89752, b = 0.94544, c = 0.17954, d = −0.80049, e = ... (fitted).

The free energy follows by thermodynamic integration:
```
F_ex/(NkT) = ∫₀^Γ u_ex(Γ') d(ln Γ')
```

The dominant term at large Γ (∝ −0.8975 Γ) is the Madelung energy of a
bcc lattice embedded in a uniform negative background — the ions arrange
into the bcc structure, which has the lowest Coulomb energy among all
Bravais lattices. The correction terms (∝ Γ^{1/4} and ∝ ln Γ) represent
harmonic and anharmonic thermal vibrations about the lattice sites.

The virial theorem for Coulomb systems gives: pV = u/3. For Γ > 10,
the ionic pressure becomes NEGATIVE — the total pressure is maintained
positive by the degenerate electron pressure (≈ (3π²)^{2/3} ℏ² n_e^{5/3}/(5m)).

### 3. Wigner crystallisation

The free energy curves of liquid and solid OCP intersect at the melting
temperature Γ_m. Monte Carlo calculations (Slattery et al. 1980; Stringfellow
et al. 1990) place the transition at:

```
Γ_m ≈ 165 ± 6    [bcc lattice crystallisation]
```

The solid has bcc structure (confirmed as the lowest-energy lattice by
direct comparison of fcc, bcc, and hcp). The Lindemann melting criterion
gives a consistent estimate: the rms ion displacement ⟨δr²⟩^{1/2}/a ≈ 0.19
at melting — a universal value across Coulomb systems.

Key: the crystallisation is into a CLASSICAL Wigner crystal of ions.
Electron Wigner crystallisation (r_s > 100, as in 2D electron systems on
liquid helium) requires much lower density and is a distinct phenomenon.

For white dwarf interiors (Γ ∼ 100–200, depending on the cooling model),
the ion plasma may be partially crystalline, affecting the specific heat
and cooling rate.

### 4. HNC integral-equation closure

The hypernetted-chain (HNC) approximation is the most accurate integral-
equation closure for Coulomb systems. Starting from the Ornstein-Zernike
relation between the total correlation function h(r) = g(r) − 1 and the
direct correlation function c(r):

```
h(r) = c(r) + n ∫ c(|r − r'|) h(r') d³r'     [OZ equation]
```

Fourier transforming: h(k) = c(k) + n c(k) h(k) → c(k) = h(k)/[1 + n h(k)].

The HNC closure relation is:

```
g(r) = exp[−V(r)/k_B T + h(r) − c(r)]       [HNC closure]
```

where V(r) = (Ze)²/r is the bare Coulomb potential.

**Solution procedure**:
1. Start from an initial guess for h(r) (e.g., h(r) = −V(r)/k_B T).
2. Fourier transform → h(k).
3. Compute c(k) = h(k)/[1 + n h(k)], inverse transform → c(r).
4. Compute new g(r) via HNC closure.
5. h_new(r) = g(r) − 1. Iterate to convergence (typically 10–50 iterations).

The HNC reproduces Monte Carlo OCP data within ~1% for all Γ up to ~100.
At very strong coupling (Γ > 100), the bridge function B(r) must be added:
g(r) = exp[−V/kT + h − c + B(r)], with B(r) from hard-sphere or reference
system models.

The Mean Spherical Approximation (MSA) is a simpler alternative:
```
g(r) = 0    for r < σ (hard core)
c(r) = −V(r)/k_B T    for r > σ
```
MSA has an analytic solution for charged hard spheres and captures the
Coulomb hole (g(r) = 0 at small r) but misses the oscillatory structure
of g(r) at intermediate Γ.

### 5. Electrical conductivity regimes

The electrical conductivity of Coulomb systems crosses three regimes
as Γ increases (Fortov 2006, Ch.6–7):

| Regime | Γ range | σ scaling | Theory |
|--------|---------|-----------|--------|
| Spitzer (weakly coupled) | Γ < 0.1 | σ ∝ T^{3/2} / (Z lnΛ) | Landau collision integral, Chapman-Enskog |
| Intermediate | 0.1 < Γ < 10 | σ ∝ T^{1/2} ... ? | Ziman theory (ion structure factor) |
| Ziman (liquid metal) | Γ > 10 | σ ∝ 1/ρ(T) S(2k_F) | Ion-ion correlation enters via S(k) |

In the Ziman regime, the resistivity is:
```
ρ = (3π m_e² / (2ℏ³ e² n_e)) ∫₀^{2k_F} S(k) |v_ps(k)|² (k/2k_F)³ dk/k_F
```
where S(k) is the ion-ion static structure factor (from HNC or MC) and
v_ps(k) is the electron-ion pseudopotential. The resistivity increases
with increasing ion-ion correlation (larger S(k) at k ∼ 2k_F) — the
opposite trend from the Spitzer regime where stronger coupling INCREASES
conductivity by reducing the Coulomb logarithm.

## Algorithm — Given (n_i, Z, T) → regime and key properties

```
1. Compute Wigner-Seitz radius: a = (3/4πn_i)^{1/3}
2. Compute coupling: Γ = (Ze)²/(a k_B T)
3. Compute quantum parameter: r_s = a/a_B, θ = k_B T/E_F
4. Γ < 0.1 → Debye-Hückel perturbation theory (gas)
5. 0.1 < Γ < 1 → weak nonideality, Debye-Hückel + O(Γ³) corrections
6. 1 < Γ < 165 → Coulomb fluid: use HNC or fitted MC formula
7. Γ > 165 → bcc Wigner crystal: Madelung + harmonic phonon term
8. For conductivity: Ziman formula when Γ > 10
9. Check: is θ < 1? → include electron degeneracy separately
```

## Edge Cases

- **Quantum corrections at high density**: when r_s < 1 and θ < 1,
  the classical OCP must be replaced by the quantum OCP. The Wigner
  crystallisation criterion changes: for r_s > 100 (electron Wigner
  crystal, 2D systems on helium), and for ion systems the quantum
  melting boundary lies at lower Γ_m (∼ 100–120 depending on r_s).
- **Phase separation in ion mixtures**: for binary ionic mixtures (e.g.,
  H⁺/He²⁺ in Jupiter interior), the excess free energy is linear in
  concentration (ΔF_ex ≈ x₁ΔF₁ + x₂ΔF₂) only approximately. At low T,
  the mixture can separate into two immiscible Coulomb fluids (Stevenson
  1975), with critical temperature T_c ∼ 6300 K at 6 TPa for H-He.
- **Dusty plasma extension**: when dust grains (μm-sized, charged to
  Z_d ∼ 10³–10⁴) are embedded in plasma, the dust-dust coupling parameter
  Γ_d ∝ Z_d² n_d^{1/3}/T_d can exceed 10⁴ at moderate density — the dust
  subsystem crystallises independently of the electron-ion background.

## Cross-References

- Fortov, Iakubov & Khrapak, *Physics of Strongly Coupled Plasma* (2006) Ch.5-7
- Ichimaru, *Rev. Mod. Phys.* 54, 1017 (1982) — canonical review
- Slattery, Doolen & DeWitt, *Phys. Rev. A* 21, 2087 (1980) — OCP EOS fit
- plasma: reasoning.plasma.generalized_fluid_equations (parent — moment hierarchy, strongly coupled corrections)
- plasma: reasoning.plasma.transport_coefficients (Spitzer ↔ Ziman conductivity bridge)
- plasma: reasoning.plasma.atomic_transition_rates (IPD from strongly coupled plasma)
