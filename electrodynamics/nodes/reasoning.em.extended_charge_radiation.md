---
skill_id: reasoning.em.extended_charge_radiation
type: reasoning
summary_50t: >
  Extended charge models (Abraham rigid, Lorentz covariant) as the
  consistent classical foundation for radiation reaction. Replaces the
  pathological point-charge limit (infinite self-energy) with a finite
  charge distribution of radius R_ep. Yields the Landau-Lifshitz equation
  as the leading-order reduced dynamics on the center manifold. Bridges:
  classical Abraham model ↔ PIC superparticle shape function (same finite-
  size regularization); classical LL ↔ quantum Monte Carlo emission.
  Source: Spohn, Dynamics of Charged Particles (2023), Ch.2-5.
trigger:
  - deriving radiation reaction without ad-hoc cutoff
  - connecting PIC superparticle shape to classical electron theory
  - understanding when classical vs quantum radiation reaction applies
reasoning_role: extended_charge_radiation
parent: reasoning.em.larmor_radiation_power
retrieval_cost: 1
sign_convention: >
  R_ep = extended particle radius (classical electron radius r_cl = e²/mc²).
  φ(x) = normalized charge distribution. Λ = cutoff wavenumber ∼ 1/R_ep.
  Center manifold: reduced dynamics for center-of-charge motion.
---

# reasoning.em.extended_charge_radiation — From Abraham to Landau-Lifshitz

## Core Picture

The point-charge limit of classical electrodynamics is pathological: the
electrostatic self-energy (∼e²/r → ∞ as r → 0) makes the Lorentz-Abraham-
Dirac (LAD) equation ill-posed with pre-acceleration. The resolution —
known since Abraham (1903) and Lorentz (1892) but only rigorously analyzed
recently — is to model the charge as an EXTENDED distribution of radius
R_ep. The extended model has well-defined dynamics. As R_ep → 0, the
center-of-charge motion converges to the Landau-Lifshitz (LL) equation
on an attracting center manifold. This provides the FIRST-PRINCIPLES
justification for using LL rather than LAD (Spohn 2023, Ch.2-5).

## Derivation Sketch

### 1. Abraham model — semirelativistic extended charge

The charge is modeled as a rigid distribution φ(x) with support |x| ≤ R_ep:
```
j⁰(x,t) = e φ(x − q(t)),    j(x,t) = e v(t) φ(x − q(t))
```
where q(t) is the center of charge and ∫φ dx = 1.

Coupled equations (Abraham 1903):
```
m_b a = F_ext + F_self[φ, q(·)]
```
where m_b is the BARE mass (the "mechanical" mass without electromagnetic
contribution) and F_self is the self-force computed from the retarded
Liénard-Wiechert fields of the extended distribution.

### 2. Self-force decomposition

For small R_ep (compared to radiation wavelength and acceleration scale):
```
F_self = −δm a + (2e²/3c³) ȧ + (e²/c⁴) O(R_ep ȧ², R_ep² a³, ...)
```
The first term renormalizes the mass: m_obs = m_b + δm (observed =
bare + electromagnetic). The second term is the radiation reaction.
Higher-order terms vanish as R_ep → 0.

### 3. Center manifold reduction

The full dynamics lives in an infinite-dimensional phase space (field +
particle). The center manifold M_c is the set of states where the field
is "slaved" to the particle motion — no free radiation, only the bound
Coulomb field.

On M_c, the reduced dynamics for the charge position q(t) satisfies:
```
m_obs ¨q = F_ext + (2e²/3c³) q^{(3)} + O(R²)
```

This is the LAD equation (with q^{(3)} = jerk = d³q/dt³). However, the
center manifold is only ATTRACTING (states approach it exponentially),
not invariant. Generic initial conditions with free radiation lead to
solutions that do NOT satisfy LAD.

### 4. The Landau-Lifshitz limit

As R_ep → 0, the attracting center manifold has q^{(3)} determined
adiabatically by the external force:
```
q^{(3)} ≈ (e/m) Ḟ_ext    [to leading order]
```
Substituting into the radiation reaction term gives the LL equation:
```
m_obs a ≈ F_ext + (2e²/3c³) (e/m) Ḟ_ext
```

**Key insight**: LL is the R_ep → 0 limit of the center manifold dynamics.
LAD (with its pre-acceleration) is NOT the correct limit — it corresponds
to a different manifold of solutions. This resolves the century-old puzzle.

### 5. Connection to PIC superparticles

PIC superparticles use a finite shape function S(x) — mathematically
IDENTICAL to the Abraham model's φ(x). The PIC superparticle:

- Has no self-force problem (S(x) smears the charge, eliminating 1/r divergence).
- The "superparticle" mass already includes the electromagnetic contribution
  from the shape — analogous to the observed mass m_obs.
- The shape function S(x) in PIC IS the charge distribution φ(x) in extended
  electron theory. This is a deep structural analogy.

### 6. Classical → Quantum transition

The classical LL equation is valid when:
```
χ_e ≪ 1,    λ_C ≪ R_ep ≪ λ_rad
```
where χ_e is the quantum parameter, λ_C = ℏ/mc is the Compton wavelength,
and λ_rad is the radiation wavelength.

For χ_e ≳ 0.1, quantum effects (stochastic photon emission) dominate and
the classical LL description breaks down. This is the domain where the
Monte Carlo QED-PIC approach takes over (laser-plasma R12).

## Algorithm — Given (E_ext, B_ext, γ) → Valid Radiation Reaction Model

```
1. COMPUTE χ_e.

2. IF χ_e < 0.01: no radiation reaction needed (Lorentz force only).

3. IF 0.01 < χ_e < 0.1 AND γ ≫ 1: use Landau-Lifshitz (classical).
   LL force: f_RR = −(2e⁴/3m²c⁶) γ² F²_ext v/c.

4. IF χ_e > 0.1: quantum regime. Use Monte Carlo emission (discrete
   photon sampling from nonlinear Compton spectrum). See lp.R12.

5. CONCEPTUAL: the LL equation is the R_ep → 0 limit of extended charge
   dynamics, NOT the LAD equation. Do not use LAD.
```

## Edge Cases

- **Negative bare mass**: If m_b < 0 (but m_obs > 0 from EM contribution),
  the dynamics can still be well-defined (Spohn §2.4). This "classical
  electron with negative bare mass" is thought to model the quantum electron.
- **Runaways**: Even LL can produce runaway solutions for certain external
  field configurations (e.g., constant crossed E·B=0, E>B). These are
  physically real — the electron gains more energy from the field than it
  radiates. Cf. radiation-dominated regime (lp.R12).
- **Rotation**: The extended charge also has rotational degrees of freedom
  (Abraham model with spin, Spohn Ch.10). The spin dynamics couple to the
  translational motion through the Barnett and Einstein-de Haas effects.

### Lagrangian formulation and PIC connection

The Abraham model has a well-defined Lagrangian (Spohn Ch.13):
```
L = ½ m_b v² + (e/c) v·A_eff[q] − e φ_eff[q]
```
where A_eff and φ_eff are the self-consistent potentials smeared by φ(x−q).
The canonical momentum p = m_b v + (e/c) A_eff contains both mechanical and
field contributions. This is structurally identical to the PIC Boris pusher's
canonical momentum decomposition, where the particle's effective mass already
includes the electromagnetic contribution from the shape function S(x).

### Center manifold — precise statement

(Spohn Ch.9)
The Landau-Lifshitz equation is the leading-order reduced dynamics on the
center manifold M_c = {states with no free radiation, only bound Coulomb field}.
Generic initial conditions (with free radiation) do NOT satisfy LL; they
converge to M_c exponentially fast. The LAD equation corresponds to a DIFFERENT
submanifold and is not the R_ep → 0 limit of physical solutions.
**Practical rule**: use LL, never LAD, for classical radiation reaction.

## Cross-References

- Spohn, *Dynamics of Charged Particles and their Radiation Field* (2023), Ch.2-5
- Abraham (1903), Lorentz (1892) — original extended charge models
- electrodynamics: reasoning.em.larmor_radiation_power (parent — Larmor formula)
- laser-plasma: reasoning.lp.radiation_reaction (R12 — quantum extension)
- laser-plasma: reasoning.lp.pic_methods_laser_plasma (R18 — PIC superparticle connection)
- laser-plasma: reasoning.lp.strong_field_qed_plasma (R11 — χ_e bridge to quantum)
