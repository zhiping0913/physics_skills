---
skill_id: reasoning.plasma.nonlinear_wave_dynamics
type: reasoning
summary_50t: >
  Finite-amplitude waves in Vlasov plasmas. Sagdeev pseudopotential:
  (1/2)(dφ/dx)² + V(φ) = 0 with V(φ) from Poisson. Solitary/soliton when
  V(φ) has local max at origin + zero crossing. BGK modes: arbitrary f(ε)
  in trapped region. Wave breaking when fluid element overtakes neighbor
  (∂v/∂x → −∞). Bridges to mt.soliton_formation and lp.wakefield.
trigger:
  - finite-amplitude plasma wave beyond linear theory
  - soliton formation or wave breaking in laser-plasma
reasoning_role: nonlinear_wave_dynamics
parent: reasoning.plasma.wave_particle_resonance
retrieval_cost: 1
references:
  - plasma: reasoning.plasma.wave_particle_resonance (linear to nonlinear bridge)
  - mathematics-theorems: mt.soliton_formation (soliton from NLS/KdV)
---

# reasoning.plasma.nonlinear_wave_dynamics — Sagdeev → Soliton → Breaking

## Core Picture

When a plasma wave amplitude exceeds the linear regime (eφ/k_B T_e ∼ 1),
the wave modifies its own propagation medium. Three universal nonlinear
phenomena emerge from the same Vlasov-Poisson system:

1. **Sagdeev pseudopotential** — solitary waves (ion acoustic, magnetosonic)
2. **BGK modes** — arbitrary-amplitude trapped-particle equilibria
3. **Wave breaking** — fluid-velocity gradient singularity → trapping → dissipation

## Derivation Sketch

### 1. Sagdeev pseudopotential method (Sagdeev 1966)

For stationary 1D waves (∂/∂t = 0 in wave frame ξ = x − Mt):

**Step 1 — Ion fluid (cold)**: n_i v_i = n₀ M (continuity), (1/2)v_i² + eφ/m_i = (1/2)M² (energy conservation).

**Step 2 — Electrons (Boltzmann equilibrium)**: n_e = n₀ exp(eφ/k_B T_e).

**Step 3 — Poisson equation**: d²φ/dξ² = (e/ε₀)(n_e − n_i).

**Step 4 — "Energy integral"**: multiply by dφ/dξ, integrate, giving:

```
(1/2)(dφ/dξ)² + V(φ; M) = 0
```

where the Sagdeev pseudopotential is:

```
V(φ) = n₀ k_B T_e [1 − exp(eφ/k_B T_e)] + n₀ M² [1 − √(1 + 2eφ/m_i M²)]
```

**Step 5 — Solitary wave condition**: V(0) = V'(0) = 0 (always satisfied),
V''(0) < 0 (origin is a local maximum → wave can depart from equilibrium),
and V(φ₀) = 0 for some φ₀ ≠ 0 (wave returns to equilibrium → pulse shape).

The name "pseudopotential" reflects the analogy with a particle of unit mass
moving in potential V(φ) with "coordinate" φ and "time" ξ. This is the EXACT
same mathematical structure as central-field reduction in classical mechanics
(`landau-graph: knowledge.mechanics.central_field_effective`): the effective
potential U_eff(r) plays the role of V(φ), and the radial coordinate r plays
the role of φ. The pseudopotential bridge between plasma physics and analytical
mechanics is one of the deepest unifying structures in theoretical physics.

The Mach number M must satisfy: 1 < M < 1.6 for ion acoustic solitons
(the lower bound from V''(0) < 0, the upper bound from the existence of
a root φ₀ where V(φ₀) = 0 before the ion fluid becomes multivalued).

### 2. BGK modes (Bernstein-Greene-Kruskal 1957)

Any distribution f(ε) depending only on the total energy ε = (1/2)mv² + qφ
(in the wave frame) is an EXACT stationary solution of the Vlasov-Poisson
system. The crucial insight: trapped particles (ε < 0 in the wave potential
well) can have ANY distribution — the Vlasov equation imposes zero constraint
on the trapped population. This generates an infinite family of nonlinear
wave equilibria parameterized by the arbitrary function f_trapped(ε).

**Construction procedure**:
1. Choose f_trapped(ε) arbitrarily for ε < 0 (the "free function").
2. Match f_passing(ε) for ε > 0 to the boundary conditions at |x| → ∞.
3. Compute the density n(φ) = ∫ f(ε=v²/2+qφ) dv.
4. Solve Poisson d²φ/dx² = −(e/ε₀)(n_i − n_e(φ)) → φ(x) by quadrature.

BGK modes are the fully nonlinear generalization of Landau-damped linear
waves. The resonant particles that CAUSE Landau damping in linear theory
become permanently TRAPPED in the wave troughs, forming a phase-space island
(vortex in (x,v) phase space) whose width is Δv_trap = 2√(eφ₀/m).

### 3. Wave breaking

A fluid wave breaks when the velocity field overtakes itself — identically
to ocean waves. The fluid trajectory x(X, t) with Lagrangian coordinate X
becomes multi-valued when ∂x/∂X = 0. Equivalently, the Eulerian velocity
gradient diverges: ∂v/∂x → −∞.

For cold unmagnetized plasma oscillations:
```
v(φ) = √(2eφ/m),    t_break ∼ (ω_p)⁻¹ (λ/L_φ) (k_B T_e/eφ₀)^{1/2}
```

After breaking, the fluid description fails. The Vlasov equation with full
phase-space evolution is required. Wave breaking is the primary collisionless
dissipation mechanism in laser-plasma accelerators — it injects background
electrons into the wakefield, providing the electron source for LWFA.

## Algorithm — Given (n₀, T_e, wave parameters) → nonlinear regime

```
1. Linear check: is eφ/k_B T_e << 1? → linear theory (dispersion method)
2. If not: identify wave type (ion acoustic, Langmuir, magnetosonic)
3. For stationary 1D: write fluid equations in wave frame → V(φ)
4. V(φ) has zero-crossing at φ₀ ≠ 0? → solitary wave, amplitude φ₀
5. No zero-crossing? → wave is periodic (cnoidal) or breaks
6. For time-dependent: estimate ∂v/∂x → t_break
7. Breaking → Vlasov evolution, trapped particles (BGK regime)
```

## Edge Cases

- **Relativistic regime** (v ∼ c): replace v²/2 → (γ−1)c² in energy equation.
  The critical Mach number increases; new branch of relativistic solitons appears.
- **Magnetized solitons**: for perpendicular propagation, magnetic pressure
  enters V(φ) → fast magnetosonic solitons (admit both compressive and
  rarefactive branches, unlike unmagnetized ion acoustic which is compressive-only).
- **3D collapse**: Sagdeev 1D reduction fails. In 2D/3D, ponderomotive force
  excavates density cavity → Langmuir collapse (Zakharov 1972), analogous to
  optical Kerr self-focusing (`reasoning.em.positive_feedback_instability`).

## Cross-References

- Sagdeev, *Reviews of Plasma Physics* Vol.4 (1966)
- B. B. Kadomtsev, *Plasma Turbulence* (1965)
- plasma: reasoning.plasma.wave_particle_resonance (linear → nonlinear bridge)
- mathematics-theorems: mt.soliton_formation (soliton from integrable PDEs)
- laser-plasma: reasoning.lp.wakefield_acceleration (wave breaking injection)
- landau-graph: knowledge.mechanics.central_field_effective (same pseudopotential math)
