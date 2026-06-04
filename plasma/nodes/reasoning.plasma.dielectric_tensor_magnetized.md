---
skill_id: reasoning.plasma.dielectric_tensor_magnetized
type: reasoning
summary_50t: >
  Magnetized cold plasma has anisotropic ε(ω): S (sum), D (difference), P (plasma).
  CMA diagram classifies all cold-plasma waves by ω_p²/ω² vs ω_c/ω.
  Cutoffs (k→0), resonances (k→∞), R/L/O/X wave taxonomy.
trigger:
  - EM wave propagation in magnetized plasma
  - need to classify wave modes and find accessibility windows
reasoning_role: magnetized_dielectric
parent: knowledge.kinetic.plasma_dielectric
sign_convention: >
  Cyclotron frequency: ω_cα = q_α B₀/m_α (SIGNED — negative for electrons,
  positive for ions). This signed convention handles multi-species sums
  compactly in the Stix parameters R, L, S, D. For cold-plasma dielectric,
  the sign of ω_cα determines whether R or L has a resonance for a given
  species. When texts use |ω_c| > 0 (unsigned, e.g., Chen), R and L swap
  definitions; both are equivalent. The signed convention is used here to
  match Stix and Ginzburg. See plasma: reasoning.plasma.single_particle_drifts
  for drift formulas (also uses signed convention — the two nodes are now consistent).
retrieval_cost: 1
references:
  - landau-graph: knowledge.kinetic.plasma_dielectric
  - electrodynamics: knowledge.em.crystal_optics (analogy: anisotropic ε from B₀)
---

# reasoning.plasma.dielectric_tensor_magnetized — B₀ → Anisotropic ε(ω)

## Core Picture

A magnetic field B₀ breaks isotropy. In a COLD magnetized plasma with
B₀ = B₀ ẑ, the dielectric tensor is (Stix Ch.1-2, Ginzburg Ch.3):

```
        [ S   −iD   0  ]
ε(ω) =  [ iD    S   0  ]
        [ 0     0   P  ]
```

where the Stix parameters are:

```
S = ½(R+L)    R = 1 − Σ ω_pα²/[ω(ω+ω_cα)]    (right-hand cutoff)
D = ½(R−L)    L = 1 − Σ ω_pα²/[ω(ω−ω_cα)]    (left-hand cutoff)
P = 1 − Σ ω_pα²/ω²                             (plasma cutoff)
```

Sum over species α (electrons, ions). **ω_cα = q_α B₀/m_α (SIGNED)** — ω_ce < 0
for electrons. In texts using |ω_c| > 0 (Chen), R/L have opposite sign conventions.
Both forms are equivalent; the signed version handles multi-species sums compactly.

## Derivation Sketch (from kinetic ε → cold-fluid limit)

Starting from `landau-graph: knowledge.kinetic.plasma_dielectric` (which gives
the Vlasov-based conductivity tensor for a magnetized plasma with arbitrary
f₀(v)), the cold-plasma ε(ω) is obtained by the DRIFT FLUID REDUCTION:

1. **Kinetic linear response** → conductivity σ_ij(k,ω) from perturbed Vlasov
   equation: the general result involves integrals over f₀(v) with resonant
   denominators ω − k_∥v_∥ − nω_c. This is the starting point for warm/hot
   plasma but not yet the cold limit.

2. **Cold limit (T→0, f₀→δ(v))** — the velocity-space integrals collapse, and
   the resonant denominators become ω − nω_c. The trace over species α gives
   the Stix sums. KEY NON-OBVIOUS STEP: the off-diagonal ±iD terms come from
   the n=±1 cyclotron-harmonic contributions to the conductivity — the sign
   (±iD) reflects the response of electrons vs ions gyrating in opposite
   directions around B₀.

3. **Energy dissipation and the anti-Hermitian part**: the cold-plasma ε is
   purely real (Hermitian, no dissipation). When T>0, the resonant denominators
   acquire an imaginary part via the Landau prescription (ω → ω+i0⁺), producing
   the anti-Hermitian part ε_A = (ε−ε†)/2i, which encodes Landau damping,
   cyclotron damping, and collisional absorption. The Kramers-Kronig relations
   then link Re[ε(ω)] to an integral over Im[ε(ω)], ensuring causality.

4. **Bessel-function expansion** (warm correction): for finite k_⊥ρ_L, the
   orbit integral exp(ik_⊥·r_L) expands as Σ J_m(k_⊥ρ_L) e^{imθ}. Each m
   couples to the n=m cyclotron harmonic → thermal corrections to S, D, P
   scale as k_⊥²ρ_L² (Stix §10-11). This is the bridge to Bernstein waves
   and thermal cyclotron damping.

## Algorithm: From ε to Wave Modes

```
1. Write wave equation: N×(N×E) + ε·E = 0, where N = ck/ω.

2. For angle θ between k and B₀, the dispersion determinant is:
   | S−N²cos²θ   −iD       N²sinθ cosθ |
   |    iD      S−N²        0          | = 0
   | N²sinθ cosθ  0      P−N²sin²θ    |

3. Expand → AN⁴ − BN² + C = 0, where:
   A = S sin²θ + P cos²θ
   B = RL sin²θ + PS(1+cos²θ)
   C = PRL

4. For each (ω,θ): solve quadratic for N² → two propagating modes.
```

## Wave Taxonomy (CMA Diagram)

**Parallel propagation (θ=0, k∥B₀):**
- R-wave (whistler/helicon): N² = R, RH circular, resonance at ω=ω_ce
- L-wave (ion cyclotron): N² = L, LH circular, resonance at ω=ω_ci

**Perpendicular propagation (θ=π/2, k⊥B₀):**
- O-mode (ordinary): N² = P, E∥B₀, unaffected by B₀, cutoff at ω=ω_p
- X-mode (extraordinary): N² = RL/S, E⊥B₀, cutoffs at R=0 (ω_R) and L=0 (ω_L),
  resonances at S=0 (upper/lower hybrid)

**CMA diagram**: Parameter space (ω_p²/ω², ω_c/ω) → each region has
different wave topology (number of propagating modes, resonance cones).

## Key Frequencies

| Frequency | Formula | Significance |
|-----------|---------|-------------|
| ω_p | √(n₀e²/ε₀m_e) | Plasma frequency — EM cutoff |
| ω_ce | |e|B₀/m_e (magnitude) | Electron cyclotron — R-wave resonance |
| ω_UH | √(ω_p²+ω_ce²) | Upper hybrid — X-mode resonance |
| ω_LH | √(ω_ci ω_ce) (approx) | Lower hybrid — ion dynamics |

## Warm Plasma Corrections (Stix §10-11)

When T_e>0, the cold-plasma S,D,P acquire thermal corrections from finite
Larmor radius (k_⊥ρ_L). Key effects:

- **Electrostatic ε_l(k,ω)** = 1+Σ(ω_pα²/k²v_thα²)[1+ζ_α Z(ζ_α)] where
  Z(ζ) is the plasma dispersion function, ζ_α=(ω−nω_cα)/k_∥v_thα.
- **Landau damping** (n=0 resonance) and **cyclotron damping** (n≠0) appear
  as Im[Z(ζ)]. These are ABSENT in cold plasma.
- **Bernstein waves**: purely perpendicular (k_∥=0), undamped modes at
  ω≈nω_ce. Propagate in bands between cyclotron harmonics.
- **Bessel-function expansion** (warm tensor): the dielectric tensor elements
  generalize to S = 1 + Σ (ω_pα²/ω) Σ_n [n²/(k_⊥²ρ_Lα²)] e^{−λ} I_n(λ) / (ω−nω_cα),
  with λ = k_⊥²ρ_Lα²/2, I_n the modified Bessel function. For k_⊥ρ_L ≪ 1,
  I_n(λ) → (λ/2)^n/n! → recovers cold limit.
- **Anti-Hermitian part & Kramers-Kronig**: Im[ε_ij] from resonant particles
  ↔ energy dissipation. Causality demands Re[ε(ω)] = (1/π) P ∫ Im[ε(ω')]/(ω'−ω) dω'.
  This constrains any model ε(ω) — a fitted Drude-Lorentz plasma ε must satisfy KK
  or it's unphysical.
- Cold plasma is valid when k_⊥ρ_L ≪ 1 AND |ω−nω_c| ≫ k_∥v_th for all n.

## Edge Cases

- **B₀ → 0 (isotropic limit)**: cold-plasma ε reduces to isotropic ε(ω)=1−ω_p²/ω².
  R, L, S → 1−ω_p²/ω², D → 0, P → 1−ω_p²/ω². CMA diagram collapses to single
  cutoff at ω=ω_p. The cold-plasma approximation itself breaks down when ω~ω_p
  and T>0 — use `landau-graph: knowledge.kinetic.plasma_dielectric` for warm ε.
- **ω → 0 (static limit)**: S → 1 + ω_pi²/ω_ci², D → 0, P → −∞. The MHD regime
  kicks in; the dielectric tensor description transitions to the MHD Ohm's law
  E + v×B = ηJ. Use `landau-graph: reasoning.mhd_closure` instead.
- **ω ∼ ω_cα (cyclotron resonance)**: cold ε_diverges (N² → ∞). In reality,
  thermal effects smear the resonance — use the warm Bessel expansion above.
  The cold model predicts infinite k (zero wavelength), which breaks down
  when kρ_L ∼ 1 — use kinetic theory.
- **High density (ω_p ≫ ω)**: P → −∞, wave is evanescent. The cold model
  remains formally valid for ω≪ω_p but the evanescent skin depth λ_skin ∼ c/ω_p
  may be smaller than the Debye length λ_D for hot plasmas — use kinetic
  (nonlocal) dielectric when λ_skin < λ_D.

## Cross-References

- Stix §1-2, Ginzburg §3-5, Chen §4
- landau-graph: knowledge.kinetic.plasma_dielectric (warm plasma ε)
- electrodynamics: knowledge.em.crystal_optics (same math, different physics)
- plasma: reasoning.plasma.single_particle_drifts (both now use signed ω_c
  per `physics-conventions`; the E×B drift and ∇B/curvature drifts determine
  how particles respond to the wave fields described by this ε; bidirectional)
