---
skill_id: reasoning.plasma.atomic_transition_rates
type: reasoning
summary_50t: >
  Spontaneous: A_{21} = (ω³|d_{12}|²)/(3πε₀ℏc³). Collisional excitation
  rate: ⟨σv⟩ = (8k_BT_e/πm_e)^{1/2} (ℏ²/m_e²) Υ(T_e) exp(−ΔE/k_BT_e).
  Collisional-radiative balance: n_e n_z C_{i→j} = rate matrix. Saha
  equation: n_{z+1} n_e/n_z = (2g_{z+1}/g_z)(m k_BT/2πℏ²)^{3/2} exp(−I_z/k_BT).
trigger:
  - computing ionization balance or level populations in laser plasma
  - evaluating line emission from HHG plasma medium
reasoning_role: atomic_transition_rates
parent: reasoning.plasma.wave_particle_resonance
retrieval_cost: 1
---

# reasoning.plasma.atomic_transition_rates — Level Populations in Plasma

## Core Picture

In laser-produced plasmas, the ionization balance and excited-state populations
determine EVERYTHING about radiation: line emission, opacity, gain for X-ray
lasers, and ionization-induced refraction. The three fundamental rates are:

| Process | Rate coefficient | Scaling |
|---------|-----------------|---------|
| Spontaneous emission | A_{21} [s⁻¹] | ∝ ω³ |d₁₂|² |
| Collisional excitation | ⟨σv⟩_{1→2} [cm³/s] | ∝ exp(−ΔE/kT) |
| Radiative recombination | α_r [cm³/s] | ∝ Z² T^{-1/2} |
| Three-body recombination | α_{3b} = n_e C [cm³/s] | ∝ n_e Z³ T^{-9/2} |

## Derivation Sketch

### 1. Einstein A and B coefficients (from electrodynamics)

From Fermi's golden rule with quantized EM field (`landau-graph: knowledge.em.dipole_radiation`):

```
A_{21} = (ω_{21}³ |⟨2|er|1⟩|²) / (3π ε₀ ℏ c³)    [spontaneous emission]
B_{12} = (π |⟨2|er|1⟩|²) / (3 ε₀ ℏ²)            [absorption]
B_{21} = B_{12}                                   [stimulated emission]
```

These are the foundation: ALL radiative rates derive from the dipole matrix
element d_{12} = ⟨2|er|1⟩ which comes from atomic structure calculations.

### 2. Collisional excitation (Van Regemorter formula)

For electron-impact excitation 1→2 with threshold ΔE = E₂−E₁:

```
⟨σv⟩_{1→2} = (8k_B T_e / π m_e)^{1/2} π a₀² (E_H/ΔE) f_{12} Υ(T_e) exp(−ΔE/k_B T_e)
```

where f_{12} is the absorption oscillator strength, Υ(T_e) is the thermally
averaged Gaunt factor (Υ ∼ 0.2 at T_e ∼ ΔE, Υ ∼ 1 at T_e ≫ ΔE),
a₀ is the Bohr radius, and E_H = 13.6 eV. The exponential factor means
that ONLY electrons in the high-energy tail of the Maxwellian contribute
to excitation — this is the critical bottleneck for X-ray laser gain.

### 3. Collisional-radiative (CR) balance

For each ionization stage z and level i, the steady-state rate equation:

```
n_e Σ_{j≠i} n_z^j C_{j→i} − n_e n_z^i Σ_{j≠i} C_{i→j}
  + Σ_{j>i} n_z^j A_{ji} − n_z^i Σ_{j<i} A_{ij}
  + n_e² n_{z+1} α_r(i) − n_e n_z^i S_i = 0
```

Each line: collisional in, collisional out, radiative in, radiative out,
recombination in, ionization out. This is an N_levels × N_ions matrix equation
that determines ALL level populations in the plasma.

### 4. Saha ionization equilibrium

When collisional processes dominate over radiative (LTE — local thermodynamic
equilibrium), the ionization balance is given by the Saha equation:

```
n_{z+1} n_e / n_z = (2 g_{z+1} / g_z) (m_e k_B T / 2π ℏ²)^{3/2} exp(−I_z/k_B T)
```

where I_z is the ionization potential. This connects to `reasoning.statistical.saha_equation`.

## Algorithm — Given (n_e, T_e, Z, ion species) → charge state distribution

```
1. Compute ionization potentials I_z for each charge state.
2. Saha check: if n_e > n_crit (Griem criterion), LTE → Saha equation.
3. If not LTE: set up CR matrix including all relevant levels.
4. Use approximate Gaunt factors Υ(T_e) for excitation rates.
5. Solve the linear system for n_z^i → ionization balance + level populations.
6. From level populations: compute emissivity, opacity, gain coefficient.
```

## Edge Cases

- **Ionization potential depression (IPD)**: at high density (n_e > 10²¹ cm⁻³),
  neighboring ions screen the nuclear potential → I_z_eff < I_z_isolated.
  Stewart-Pyatt or Ecker-Kröll models: ΔI ∼ (Ze²/4πε₀)(3/4πn_i)^{1/3}.
- **Coronal equilibrium**: at low density (n_e < 10¹⁶ cm⁻³), radiative decay
  dominates over collisional → excited states are empty; only ground state
  ionization/recombination matters.

## Cross-References

- Joachain, *Atoms in Intense Laser Fields* (2011) Ch.6
- Griem, *Principles of Plasma Spectroscopy* (1997)
- landau-graph: knowledge.em.dipole_radiation (Einstein coefficients)
- landau-graph: reasoning.statistical.gibbs_ensemble (Saha equation from partition function)
