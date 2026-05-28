---
skill_id: knowledge.kinetic.plasma_instabilities
type: knowledge
summary_50t: >
  Beam-plasma (bump-on-tail → δf/∂v > 0 → inverse Landau damping).
  Two-stream (counter-propagating beams → ω² = ω_p² + k²v₀² unstable branch).
  Weibel (anisotropic T → B grows from current filamentation).
trigger:
  - plasma stability analysis
  - identifying unstable modes
  - kinetic vs fluid instabilities
reasoning_role: plasma_instability
parent: reasoning.plasma_dielectric_response
retrieval_cost: 1
---

# knowledge.kinetic.plasma_instabilities

**General mechanism**: Instability occurs when the dielectric function
ε_l(k,ω) = 0 has solutions with Im ω > 0 (growing modes).

**Key instabilities in Vol.10**:

**Beam-plasma (bump-on-tail) instability** (§30):
- Equilibrium f₀(v) has positive slope ∂f₀/∂v > 0 somewhere
- This is INVERSE Landau damping: waves GROW instead of damping
- Growth rate: γ ∼ ω_p (n_b/n_p)^{1/3} for weak beam

**Two-stream instability** (§30):
- Two counter-propagating electron beams with velocities ±v₀
- Dielectric: ε_l = 1 − ω_p²/(ω−kv₀)² − ω_p²/(ω+kv₀)²
- Unstable for k < ω_p/v₀, maximum growth at k ∼ ω_p/v₀

**Weibel instability** (§31):
- Temperature anisotropy T_⊥ ≠ T_∥ → free energy
- Purely growing (Re ω = 0), produces magnetic fields
- Mechanism: current filamentation from anisotropic pressure

**Ion-acoustic instability** (§33):
- Current-driven when v_d > c_s (electron drift exceeds ion sound speed)
- Ion Landau damping competes with electron inverse Landau damping

**General stability criterion** (Penrose):
- ∫ dv ∂f₀/∂v / (v − ω/k) with analytic continuation determines stability
- f₀ must be a monotonically decreasing function of v² for stability

- Landau Vol.10 §30-35 (beam, two-stream, Weibel, ion-acoustic)
