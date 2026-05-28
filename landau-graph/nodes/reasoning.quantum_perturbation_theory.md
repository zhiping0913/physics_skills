---
skill_id: reasoning.quantum_perturbation_theory
type: reasoning
summary_50t: >
  Ĥ = Ĥ₀ + V̂. E_n = E_n^(0) + V_nn + Σ'|V_mn|²/(E_n−E_m) + ...
  ψ_n = ψ_n^(0) + Σ' V_mn/(E_n−E_m) ψ_m^(0). Condition: |V_mn| ≪ |E_n−E_m|.
  Degenerate case: secular equation. Time-dependent: Fermi golden rule.
trigger:
  - small correction to known quantum system
  - transition rates (Fermi golden rule)
  - Zeeman/Stark effects, fine structure
reasoning_role: quantum_perturbation
parent: reasoning.classical_to_quantum_correspondence
retrieval_cost: 1
---

# reasoning.quantum_perturbation_theory — Small Term → Perturbative Expansion

## Core Picture

Exact solutions of Schrödinger's equation are rare. Perturbation theory
provides systematic corrections when Ĥ = Ĥ₀ + V̂ with V̂ "small."

The structure mirrors classical perturbation theory (Vol.1 §28, Vol.5 §32)
but with the crucial quantum feature: the denominator contains ENERGY
DIFFERENCES, requiring non-degenerate spectrum or special treatment.

## Stationary (time-independent) PT (§38-39)

```
1. Write Ĥ = Ĥ₀ + V̂, with Ĥ₀ψ_n^(0) = E_n^(0)ψ_n^(0) known
2. Expand: ψ_n = ψ_n^(0) + ψ_n^(1) + ... , E_n = E_n^(0) + E_n^(1) + ...
3. First order: E_n^(1) = V_nn = ⟨n|V̂|n⟩ (mean value of perturbation)
   ψ_n^(1) = Σ' V_mn/(E_n^(0)−E_m^(0)) ψ_m^(0)
   Set c_n^(1)=0 to keep ψ_n normalized to first order
4. Second order: E_n^(2) = Σ' |V_mn|²/(E_n^(0)−E_m^(0))
   For ground state (n=0): E_0 < E_m ∀m → denominator negative → E_0^(2) < 0
```

## Degenerate Case (§39)

When E_n^(0) = E_m^(0): diagonalize V̂ in the degenerate subspace.
Solve det|V_{αβ} − E^(1)δ_{αβ}| = 0 (secular equation). The eigenvalues
of this equation are the first-order energy corrections; the corresponding
eigenvectors are the correct zeroth-order wave functions. The perturbation
lifts the degeneracy.

## Time-dependent PT (§40-43)

Transition amplitude: c_f(t) = −(i/ℏ)∫₀^t V_fi(t')e^{iω_fi t'} dt'.
For constant V: P_if = (2π/ℏ)|V_fi|² δ(E_f−E_i) t.
Transition rate: w = (2π/ℏ)|V_fi|² ρ(E_f) (Fermi golden rule).

For periodic perturbation V(t) = F e^{−iωt} + F† e^{iωt}:
Resonance when ℏω = E_f − E_i (absorption) or ℏω = E_i − E_f (emission).

## Cross-References
- Landau Vol.3 §38-44
- Landau Vol.1 §28 (anharmonic oscillations — same pattern!)
- Landau Vol.5 §32 (thermodynamic perturbation theory — same pattern!)
