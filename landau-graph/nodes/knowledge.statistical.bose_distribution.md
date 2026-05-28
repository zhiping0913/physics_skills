---
skill_id: knowledge.statistical.bose_distribution
type: knowledge
summary_50t: >
  n̄_k = 1/[exp((ε_k−μ)/T)−1]. μ ≤ 0 for free bosons.
  Bose-Einstein condensation at T < T_c: macroscopic occupation of ε=0.
  Black-body radiation: μ=0, Planck spectrum.
trigger:
  - photons, phonons, ultracold atoms
  - Bose-Einstein condensation
  - black-body radiation spectrum
reasoning_role: quantum_statistics_bose
parent: reasoning.partition_to_thermodynamics
retrieval_cost: 1
---

# knowledge.statistical.bose_distribution

**Bose-Einstein**: n̄_k = 1/[exp((ε_k−μ)/T) − 1].
μ ≤ 0 required for n̄_k ≥ 0.

**BEC**: T_c = (2πℏ²/m)(n/ζ(3/2))^{2/3}.
For T < T_c: N_0 = N[1−(T/T_c)^{3/2}] (macroscopic ground state occupation).

**Black-body** (μ=0): n̄_ω = 1/[exp(ℏω/T)−1].
Energy density: u(ω) = (ℏω³/π²c³)/(exp(ℏω/T)−1).
Stefan-Boltzmann: I = σT⁴, σ = π²k⁴/60ℏ³c².

**Phonons** (Debye): ω_D = c(6π²n)^{1/3}. C_V ∝ T³ at low T.

- Landau Vol.5 §53-55, §62-63
