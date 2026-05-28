---
skill_id: knowledge.statistical.fluctuations
type: knowledge
summary_50t: >
  ⟨(ΔN)²⟩ = N (Boltzmann), n(1∓n) (Fermi/Bose). Poisson: w_N = N̄^N e^{−N̄}/N!.
  Fluctuation-dissipation: response function = fluctuation spectrum / T.
trigger:
  - computing statistical fluctuations
  - noise, uncertainty in thermodynamic quantities
  - fluctuation-dissipation relations
reasoning_role: statistical_fluctuations
parent: reasoning.ensemble_logic
retrieval_cost: 1
---

# knowledge.statistical.fluctuations

**Number fluctuations** (ideal gas): ⟨(ΔN)²⟩ = N, relative = 1/√N.

**Occupation number fluctuations**:
```
Boltzmann:  ⟨(Δn_k)²⟩ = n̄_k
Fermi:      ⟨(Δn_k)²⟩ = n̄_k(1 − n̄_k)   → 0 at T=0 (Pauli)
Bose:       ⟨(Δn_k)²⟩ = n̄_k(1 + n̄_k)   → enhanced (bunching)
```

**Poisson distribution**: w_N = N̄^N e^{−N̄}/N! (valid for arbitrary N).

**Gaussian limit**: For small relative fluctuations (|N−N̄| ≪ N̄):
w(N) ∝ exp[−(N−N̄)²/(2N̄)].

**Black-body radiation** (Einstein 1909):
⟨(ΔE_Δω)²⟩ = ℏω·E_Δω + (π²c³/Vω²Δω)(E_Δω)².
First term: particle-like (shot noise). Second term: wave-like (interference).

**Fluctuation-dissipation theorem** (§122-123):
Generalized susceptibility α(ω) determines both response AND fluctuations.
⟨x²⟩_ω = (ℏ/2)coth(ℏω/2T)·Im α(ω). Classical limit: ⟨x²⟩_ω = (2T/ω)Im α(ω).

- Landau Vol.5 §110-123
