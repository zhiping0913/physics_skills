---
skill_id: reasoning.second_quantization
type: reasoning
summary_50t: >
  Classical field → quantized oscillators → particles. [â,â†] = 1 → 
  photons are bosons. Large occupation numbers → classical field.
  The bridge from wave to particle description of fields.
trigger:
  - quantizing EM field, phonons, any classical field
  - understanding classical limit of quantum fields
  - need creation/annihilation formalism for many-body systems
reasoning_role: field_quantization
parent: reasoning.classical_to_quantum_correspondence
children:
retrieval_cost: 1
---

# reasoning.second_quantization — Classical Field → Quantum Particles

## Core Picture

The photon picture is NOT an alternative to the classical field description —
it is the ONLY description adequate to the physical meaning of the EM field
in quantum theory (Landau §5). A classical field is a continuous system with
infinitely many degrees of freedom. Quantizing each Fourier mode as a
harmonic oscillator yields quantized field excitations — PHOTONS.

**Classical limit**: NOT simply "N_k ≫ 1." If ALL modes had large occupation
numbers, the total energy would be infinite. The correct condition involves
TIME-AVERAGING over an interval Δt: only Fourier components with ωΔt ≤ 1
contribute. For a finite measurement time, only finitely many modes need
large N_k. For static fields (Δt→∞), the condition is always satisfied —
static fields are always classical.

**Vacuum fluctuations are ineliminable**: The zero-point energy can be
subtracted (normal ordering). But ⟨Ê²⟩ cannot — you would have to modify
the operators Ê, Ĥ themselves, which is impossible. This is the physical
origin of the Lamb shift, Casimir effect, and spontaneous emission.

## Algorithm

```
1. Write classical field as sum of normal modes: A(r,t) = Σ c_k e^{i(kr−ωt)}
2. Identify each mode as independent harmonic oscillator
3. Quantize: c_k → √(2πℏc²/ω) â_k, c_k* → same with â_k†
4. Commutation relations: [â_k, â_k'†] = δ_{kk'} (bosons)
5. Field operators: Â(r,t) = Σ √(2πℏc²/ω)(â_k e^{ikr} + h.c.)
   Ê = −(1/c)∂Â/∂t,  Ĥ = rot Â
6. Hamiltonian: Ĥ = Σ ℏω_k (â_k†â_k + ½)
7. States: |N_k₁, N_k₂,...⟩, N_k = 0,1,2,... (Bose statistics)
```

## Cross-References
- Landau Vol.4 §1-5 (EM field quantization)
- Landau Vol.3 §65 (second quantization for fermions: {â,â†} = 1)
- Landau Vol.9 §7 (field operators in condensed matter — same formalism)
