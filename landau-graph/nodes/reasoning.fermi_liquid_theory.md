---
skill_id: reasoning.fermi_liquid_theory
type: reasoning
summary_50t: >
  Interacting fermions → quasiparticles with same quantum numbers as
  free fermions. Adiabatic continuity from ideal gas. Landau f-function
  parametrizes residual interactions. Effective mass m*, specific heat ∝ T.
trigger:
  - interacting fermion system at low T
  - liquid He-3, electrons in metals, neutron matter
  - need to understand why Fermi gas picture works despite strong interactions
reasoning_role: quasiparticle_paradigm
parent: reasoning.green_function_method
retrieval_cost: 1
---

# reasoning.fermi_liquid_theory — Strong Interactions → Quasiparticle Picture

## Core Picture

**Universal foundation** (§1): Every weakly excited state of a macroscopic body
can be treated in QM as a collection of individual elementary excitations
(quasiparticles). This principle underlies ALL quantum liquid theory, not just FLT.

How can a strongly interacting fermion system (e.g., liquid He-3) behave
like a gas of nearly free particles? Landau's answer (1956-58): the
low-lying excitations are QUASIPARTICLES — dressed fermions that are in
1-to-1 correspondence with the states of the non-interacting Fermi gas.

The key is ADIABATIC CONTINUITY: if you turn on interactions slowly,
each eigenstate of the non-interacting system evolves continuously into
an eigenstate of the interacting system, keeping its quantum numbers.

**Crucial caveat (§1)**: The total energy E of the liquid is NOT the sum of
quasiparticle energies: E ≠ ∫nε dτ. E is a functional of the distribution n,
but ε = δE/δn is defined as the VARIATIONAL DERIVATIVE — the change in total
energy when ONE quasiparticle is added. The self-consistency is deeper than
Hartree: the interaction changes not just the potential energy but the very
dependence of the KINETIC energy operator on momentum (§1). This is WHY m* ≠ m.

**Context**: Only TWO quantum liquids exist in nature (³He, ⁴He). All other
substances freeze before quantum effects matter. Helium is special due to
weak interatomic interaction. For ³He: |ε_F| ≈ 2.5K but quantitative FLT
applicability limited to T ≲ 0.1K.

## Landau's Construction

```
1. Ground state = filled Fermi sea up to p_F. The relation p_F³ = 3π²ℏ³(N/V)
   (1.1) is preserved by interactions (Luttinger theorem, proved in §20).
2. Low excitations = adding/removing quasiparticles near p_F.
   ε = δE/δn — variational derivative, not independent particle energy.
3. Quasiparticle energy near Fermi surface: ε(p) − ε_F ≈ v_F(p−p_F)
   Effective mass m* = p_F/v_F (1.14). 
   At T=P=0: ε_F = μ is NEGATIVE (§1) — −μ = heat of vaporization per particle.
4. Quasiparticle spin is ALWAYS 1/2 regardless of real particle spin (§1).
   For s>1/2, (ŝ·p)² splits (2s+1)-fold degeneracy into (2s+1)/2 branches.
5. Interaction energy between quasiparticles: f̂ = F(ϑ) + σ·σ' G(ϑ)
   (§2, 2.4). F and G expanded in Legendre polynomials: F_l, G_l.
6. Galilean invariance → m*/m = 1 + ⟨F(ϑ)cosϑ⟩ (2.12) — DERIVED, not empirical.
7. Stability conditions (§2): F_l + 1 > 0, G_l + 1 > 0.
   l=1 → m* > 0. l=0 → positive compressibility.
8. Measurable quantities through F and G:
   Specific heat: C_V = (m*/m)C_V^(0) (same form, m→m*)
   Compressibility: u² = (p_F²/3mm*)(1 + ⟨F⟩) (2.17)
   Spin susceptibility: χ = (m*/m)χ^(0)/(1 + G_0)
```

## Key Results

- Specific heat: C_V = (m*/m) C_V^(0) — just replaces m with m*
- Zero sound: collective density oscillation at T=0, distinct from
  ordinary (first) sound. Exists because quasiparticles restore
  local equilibrium faster than density can relax.
- Quasiparticle lifetime: τ ∝ 1/T² (long-lived at low T!)

## Alternative "Hole" Picture (§1)

Landau also gives an equivalent formulation where ε ≥ 0 always:
- Quasiparticles outside Fermi sphere: ε = v_F(p−p_F), particles
- "Holes" inside Fermi sphere: ε = v_F(p_F−p), positive energy
- Both obey Fermi distribution with μ=0: n = [e^{ε/T}+1]^{-1}
- Excitations appear/disappear in pairs; no "filled sea" needed
- Eliminates the unobservable filled Fermi sphere of quasiparticles

## When Fermi Liquid Theory Fails

- 1D systems (Luttinger liquid — completely different!)
- Near quantum critical points (non-Fermi liquid behavior)
- Superconducting/superfluid ground states
- When the quasiparticle weight Z → 0

## Cross-References
- Landau Vol.9 §1-6 (Fermi liquid), §7-21 (Green's function formulation)
- Landau Vol.5 §57-61 (degenerate electron gas — non-interacting limit)
- Landau Vol.10 §41 (Landau collision integral — kinetics of quasiparticles)
