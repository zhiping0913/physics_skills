---
skill_id: reasoning.wkb_quasiclassical
type: reasoning
summary_50t: >
  Ψ = exp(iσ/ℏ), σ = σ₀ + (ℏ/i)σ₁ + ... → σ₀ = ±∫p dx.
  Condition: |dλ/dx| ≪ 1. Connects quantum to classical trajectory.
  Bohr-Sommerfeld: ∮p dq = (n+γ)2πℏ. Tunneling: Ψ ∝ exp(−∫|p|dx/ℏ).
trigger:
  - λ ≪ L (wavelength small compared to system size)
  - semiclassical quantization
  - tunneling through barrier
reasoning_role: semiclassical_approximation
parent: reasoning.classical_to_quantum_correspondence
children:
  - knowledge.quantum.wkb_approximation
retrieval_cost: 1
---

# reasoning.wkb_quasiclassical — Small Wavelength → Semiclassical Approximation

## Core Picture

When the de Broglie wavelength λ = 2πℏ/p is small compared to the scale L
over which the potential varies, the wave function takes the form:
Ψ ∝ (1/√p) exp(±i∫p dx/ℏ) — a wave whose amplitude varies slowly (1/√p)
and whose phase is the classical action divided by ℏ.

This is the quantum analog of geometric optics: wave mechanics →
ray optics as λ → 0.

## Algorithm

```
1. Ansatz: Ψ = exp(iσ/ℏ), expand σ = σ₀ + (ℏ/i)σ₁ + (ℏ/i)²σ₂ + ...
2. O(ℏ⁰): (1/2m)σ₀'² = E − U(x) → σ₀ = ±∫p(x)dx, p=√[2m(E−U)]
3. O(ℏ): σ₁ = −½ln p → Ψ ∝ (1/√p)exp(±i∫p dx/ℏ)
4. Validity: |dλ/dx| ≪ 1, equivalently mℏ|F|/p³ ≪ 1
   FAILS at turning points (p=0) — need connection formulas
```

## Bohr-Sommerfeld Quantization (§48)

For bound states: ∮p dq = (n + γ)·2πℏ, γ = 1/2 for smooth turning points.
Connects directly to adiabatic invariant I = ∮p dq / 2π → I = (n+γ)ℏ.
This is the bridge from Vol.1 §49 to old quantum theory.

## Tunneling (§50)

Through classically forbidden region (E < U): p = i|p|, Ψ ∝ exp(−∫|p|dx/ℏ).
Transmission coefficient: D ∝ exp(−2∫√[2m(U−E)] dx/ℏ).

## Cross-References
- Landau Vol.3 §46-53 (WKB method, Bohr-Sommerfeld, tunneling)
- Landau Vol.1 §49 (adiabatic invariant → I = ∮p dq / 2π)
- Landau Vol.2 §53 (geometric optics — same mathematics: λ→0 limit)
