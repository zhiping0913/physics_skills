---
skill_id: knowledge.qed.feynman_rules
type: knowledge
summary_50t: >
  Electron propagator: i(γp+m)/(p²−m²+i0). Photon propagator:
  −ig_{μν}/k². Vertex: −ieγ^μ. S-matrix: Feynman diagrams.
  Ward identity: k_μ M^μ = 0 (gauge invariance).
trigger:
  - computing scattering amplitudes in QED
  - Feynman diagrams for electrons and photons
  - cross sections, decay rates
reasoning_role: qed_calculational_rules
parent: reasoning.dirac_equation_antiparticles
retrieval_cost: 1
---

# knowledge.qed.feynman_rules

**Propagators** (momentum space):
```
Electron:  i(γ·p + m)/(p² − m² + i0)
Photon:    −ig_{μν}/k² (Feynman gauge)
```

**Vertex**: −ieγ^μ. e²/ℏc ≈ 1/137 (fine structure constant).

**S-matrix expansion**:
S = T exp(−i∫ d⁴x H_int). H_int = e ψ̄γ^μψ A_μ.

**Feynman rules for scattering**:
1. External lines: u(p) (in-electron), ū(p) (out-electron),
   v(p) (in-positron), v̄(p) (out-positron), ε_μ (photon)
2. Internal lines = propagators
3. Vertices = −ieγ^μ. Conserve 4-momentum.
4. Closed fermion loop → (−1) factor + trace over γ-matrices
5. Integrate over unconstrained momenta: ∫ d⁴k/(2π)⁴

**Ward identity**: k_μ M^μ = 0 where k is photon momentum.
Consequence: gauge invariance is preserved order by order in PT.
Longitudinal photon polarization decouples.

**Cross section** (2→2):
dσ = |M|²/(4I) · dΦ_2 where I = √[(p₁·p₂)²−m₁²m₂²], dΦ_2 = phase space.

- Landau Vol.4 §72-78
