---
name: landau-vol1-deep
description: "LEGACY — Superseded by LandauGraph node-per-skill format. Deep reasoning templates distilled from Landau Vol.1 Mechanics."
---

# Landau Vol.1 — Deep Reasoning Templates (LEGACY)

> **SUPERSEDED 2026-05-25.** This skill is retained for reference but the
> 5 templates below have been replaced by the LandauGraph format:
> - `/home/zhiping/.hermes/skills/landau-graph/` — 75 nodes, 125 typed edges across 7 volumes
> - `landau-course` skill — `references/extraction-methodology.md`
>
> The LandauGraph format adds: typed reasoning edges (prerequisite /
> reasoning-instance / abstraction / analogy), 50t+300t two-layer nodes,
> and GRAPH.json with retrieval weights.


Each template captures not just the derivation steps, but **when to apply it,
what inputs are needed, and where it breaks down**.

Load `landau-course` first for the chapter map and key equations.
Then load this skill when you need to **reason through** a mechanical problem
from first principles.

---

## T1 — Symmetry → Lagrangian Form

### Trigger
You are constructing a Lagrangian for an unfamiliar system and need to
constrain its functional form. The system possesses continuous symmetries.

### Inputs
- The symmetry group and its infinitesimal generators
- The degrees of freedom and their transformation rules
- Whether the Lagrangian is defined up to a total time derivative (always yes
  in classical mechanics: L and L + dF/dt give identical equations)

### Algorithm
```
1. Identify all symmetries of the physical setup
   → space homogeneity, time homogeneity, space isotropy, Galilean/Lorentz
     invariance, gauge invariance, etc.
2. For each symmetry, write the infinitesimal transformation of the
   generalized coordinates q and velocities q̇
3. Write the Lagrangian as an unknown function constrained by step 1:
   - If space is homogeneous → L cannot depend explicitly on r
   - If time is homogeneous → L cannot depend explicitly on t
   - If space is isotropic → L can depend on v² (scalar) but not direction of v
4. For symmetries linking reference frames (Galilean/Lorentz), apply the
   stronger condition: δL must equal dF/dt (total derivative), not necessarily zero
5. The constraint ∂L/∂(v²) = constant emerges from demanding that
   δL = ∂L/∂(v²) · 2v·ε is a total derivative
6. Fix the proportionality constant via additivity: for non-interacting
   system, L = Σ L_a
```

### Worked Example: Galilean Invariance → L = mv²/2
```
Step 1: Free particle in inertial frame. Symmetries: homogeneity (r,t),
         isotropy (v direction), Galilean relativity.
Step 2: r → r, v → v + ε (K' moves at infinitesimal velocity ε relative to K)
Step 3: L(r,v,t) → L(v²) — eliminates r,t and direction dependence
Step 4: L(v'²) = L(v² + 2v·ε + ε²) = L(v²) + ∂L/∂(v²) · 2v·ε
        δL = ∂L/∂(v²) · 2v·ε
        For δL to be dF/dt, ∂L/∂(v²) must be constant (since v·ε = d/dt(r·ε))
Step 5: ∴ L ∝ v²
Step 6: L = (m/2)v². Mass m > 0 (otherwise action has no minimum).
        For N particles: L = Σ m_a v_a²/2.
```

### Edge Cases & Failure Modes
- **Discrete symmetries** (parity, time reversal): do NOT constrain the
  functional form of L — they only restrict which terms can appear
- **Symmetry mixes space and time** (Lorentz): requires metric-based approach
  (see Vol.2). The pattern is: proper time ds is invariant → L = −mc²√(1−v²/c²)
- **Gauge theories**: δL = 0 (not just dF/dt) → stronger constraint
- **External fields break homogeneity**: U(r) appears, Lagrangian is
  L = mv²/2 − U(r,t), which is the most general form compatible with
  Galilean invariance when external forces are present

### Connections
- Noether's theorem (T2): this is the reverse direction
- Vol.2 §2: relativistic generalization L = −mc²√(1−v²/c²)
- Vol.3: Lagrangian for Schrödinger field uses same pattern

---

## T2 — Continuous Symmetry → Conserved Quantity

### Trigger
A system has a known continuous symmetry. Determine the corresponding
conserved quantity and its conditions of validity.

### Inputs
- The Lagrangian L(q,q̇,t) of the system
- The infinitesimal transformation: q → q + δq, t → t + δt (if applicable)

### Algorithm
```
1. Write δL under the infinitesimal transformation.
   If the symmetry involves time reparameterization, include δt.
2. Two cases:
   Case A: Exact symmetry of L → δL = 0 identically
   Case B: Symmetry up to total derivative → δL = dF/dt
3. Use the Euler-Lagrange equations to replace ∂L/∂q with d/dt(∂L/∂q̇)
4. Rearrange δL = d/dt(...) to extract a conserved quantity Q with dQ/dt = 0
5. Verify additivity: Q for non-interacting subsystems = Σ Q_a
```

### Worked Example A: Spatial Homogeneity → Momentum Conservation
```
Step 1: Infinitesimal translation r_a → r_a + ε
        δL = Σ ∂L/∂r_a · ε
Step 2: Homogeneity of space → δL = 0 (Case A)
Step 3: ∂L/∂r_a = d/dt(∂L/∂v_a) via Lagrange equations
Step 4: δL = ε · d/dt Σ ∂L/∂v_a = 0
        → d/dt Σ ∂L/∂v_a = 0
        → P = Σ p_a = Σ m_a v_a conserved
Step 5: Additivity obvious from definition
```

### Worked Example B: Time Homogeneity → Energy Conservation
```
Step 1: Time translation t → t + ε is not a coordinate transformation
        of the same type. Instead: for closed system ∂L/∂t = 0.
Step 2: dL/dt = Σ (∂L/∂q_i · q̇_i + ∂L/∂q̇_i · q̈_i) + ∂L/∂t
        With ∂L/∂t = 0 and Lagrange eqns:
        dL/dt = Σ d/dt(∂L/∂q̇_i · q̇_i)
Step 3: d/dt (Σ q̇_i ∂L/∂q̇_i − L) = 0
Step 4: E = Σ q̇_i p_i − L conserved
```

### Worked Example C: Space Isotropy → Angular Momentum Conservation
```
Step 1: Infinitesimal rotation: δr = δφ × r, δv = δφ × v
Step 2: δL = Σ (∂L/∂r_a · δr_a + ∂L/∂v_a · δv_a) = 0
Step 3: Replacing with Lagrange eqns and p_a = ∂L/∂v_a
Step 4: d/dt Σ r_a × p_a = 0 → M = Σ r_a × p_a conserved
```

### Edge Cases & Failure Modes
- **External fields break translation symmetry → P not conserved**
  Partial exception: if U is independent of a coordinate (e.g. homogeneous
  field along z), the corresponding momentum component is conserved
- **Reference frame dependence**: P and M transform between inertial frames
  (formulas 8.1, 9.5, 9.6). M depends on origin unless P = 0.
- **Non-inertial frames**: Noether derivation fails — need fictitious forces

### Connections
- Noether's theorem (general): continuous symmetry → conserved current
- Vol.2: Energy-momentum tensor from spacetime translation invariance
- Quantum: conserved quantities → good quantum numbers

---

## T3 — Homogeneous Potential → Scaling Relations

### Trigger
You need scaling relations between physical quantities (periods, velocities,
energies) without solving the equations of motion. The potential energy is
a homogeneous function of coordinates.

### Inputs
- The homogeneity degree k of U: U(αr₁,...,αr_N) = αᵏ U(r₁,...,r_N)
- The form of kinetic energy T ∝ v²

### Algorithm
```
1. Confirm U is homogeneous: U(αr) = αᵏ U(r). If not — the template fails.
2. Set up the scaling ansatz: r → αr, t → βt
3. T scales as α²/β² (since v = dr/dt scales as α/β)
4. U scales as αᵏ
5. Demand equations of motion invariant → L scales by constant factor.
   This requires T and U to scale identically: α²/β² = αᵏ
6. Solve: β = α^(1−k/2) → t'/t = (l'/l)^(1−k/2)
7. All other quantities follow:
   v'/v = (l'/l)^(k/2)
   E'/E = (l'/l)^k
   M'/M = (l'/l)^(1+k/2)
```

### Worked Examples
```
k = 2  (harmonic oscillator):  β = α⁰ → period independent of amplitude
       v'/v = l'/l → linear scaling
       Virial: 2⟨T⟩ = 2⟨U⟩ → ⟨T⟩ = ⟨U⟩,  ⟨U⟩ = E/2

k = 1  (uniform gravity):      β = α^(1/2) → t'/t = √(l'/l)
       Free fall: t² ∝ h

k = −1 (Coulomb/Newton):       β = α^(3/2) → T² ∝ a³ (Kepler's 3rd law)
       v'/v = (l'/l)^(−1/2) → v² ∝ 1/r
       Virial: 2⟨T⟩ = −⟨U⟩,  E = −⟨T⟩
```

### Virial Theorem (same template, time-averaged form)
```
For bounded motion:
  d/dt(Σ p_a·r_a) averages to zero over long times
  → 2⟨T⟩ = ⟨Σ r_a·∂U/∂r_a⟩
  If U is homogeneous of degree k: ⟨Σ r_a·∂U/∂r_a⟩ = k⟨U⟩
  → 2⟨T⟩ = k⟨U⟩  and  ⟨U⟩ = 2E/(k+2), ⟨T⟩ = kE/(k+2)
```

### Edge Cases & Failure Modes
- **U not homogeneous**: template fails entirely; no universal scaling exists
- **Multiple scales in U**: e.g. U = ar² + br⁴ — homogeneity broken,
  different regimes dominate at different scales
- **Unbounded motion**: virial theorem derivation requires that
  Σ p_a·r_a remains bounded. If the system escapes, the time average diverges
- **k = −2**: β → α², marginal case

### Connections
- Plasma physics: virial theorem for Vlasov-Poisson, MHD equilibrium
- Astrophysics: virial mass estimates for galaxies/clusters
- Vol.5: statistical virial theorem

---

## T4 — Lagrangian → Hamiltonian Transition

### Trigger
You have a Lagrangian system and need to convert to Hamiltonian form for:
- Canonical transformation theory
- Identifying adiabatic invariants
- Quantization (via Poisson bracket → commutator)

### Inputs
- L(q,q̇,t)
- The Hessian ∂²L/∂q̇_i∂q̇_j must be non-singular (system must be non-degenerate)

### Algorithm
```
1. Compute generalized momenta: p_i = ∂L/∂q̇_i
2. Invert to express q̇_i = q̇_i(q,p,t). This requires the Hessian condition.
3. Construct H(q,p,t) = Σ p_i q̇_i − L, expressed entirely in (q,p) variables
4. Hamilton's equations: q̇_i = ∂H/∂p_i,  ṗ_i = −∂H/∂q_i
5. For any function f(q,p,t): df/dt = {f,H} + ∂f/∂t
   where {f,g} = Σ (∂f/∂q_i ∂g/∂p_i − ∂f/∂p_i ∂g/∂q_i)
6. Phase space volume is conserved (Liouville's theorem):
   ∮ dp dq invariant under Hamiltonian flow
```

### Worked Example: Harmonic Oscillator
```
L = (m/2)q̇² − (k/2)q²
Step 1: p = mq̇
Step 2: q̇ = p/m
Step 3: H = p·(p/m) − [(m/2)(p/m)² − (k/2)q²]
        = p²/2m + kq²/2 = p²/2m + (mω²/2)q²
Step 4: q̇ = p/m,  ṗ = −mω²q
        → q̈ + ω²q = 0
Step 5: {q,p} = 1, {q,q} = {p,p} = 0
Step 6: Ellipse in (q,p) plane, area = π√(2mE)·√(2E/mω²) = 2πE/ω
        → I = E/ω conserved (adiabatic invariant, see T5)
```

### The Hessian Condition (when it fails)
```
If det(∂²L/∂q̇∂q̇) = 0, the system has constraints.
Example: L = (m/2)(ẋ²+ẏ²) + B(xẏ − yẋ)/2c  (charged particle in B)
  → p_x = mẋ − By/2c, p_y = mẏ + Bx/2c
  Constraints appear if some coordinates have no kinetic term.
  → Dirac-Bergmann constrained Hamiltonian theory needed
```

### Edge Cases & Failure Modes
- **Gauge theories**: L has redundant degrees of freedom → Hessian singular,
  need gauge fixing
- **Relativistic systems**: L = −mc²√(1−v²/c²) → p = mv/√(1−v²/c²),
  H = √(p²c² + m²c⁴)
- **Time-dependent L**: H is NOT the energy unless ∂L/∂t = 0
  (H = E only for conservative systems)

### Connections
- Quantum: { , } → (iħ)⁻¹[ , ], H → Ĥ
- Liouville: foundation of statistical mechanics (Vol.5)
- Canonical transformations (T5): preserving { , } structure

---

## T5 — Slow Parameter → Adiabatic Invariant

### Trigger
A bounded periodic system has a parameter λ(t) that changes slowly
compared to the system's natural period. Find the quantity that remains
(approximately) conserved.

### Inputs
- H(q,p;λ) — Hamiltonian with parameter λ
- The period T(E,λ) of the unperturbed motion (λ held constant)
- The slowness condition: T·|dλ/dt| ≪ |λ|

### Algorithm
```
1. Verify slowness: T·|λ̇| ≪ |λ|. If not satisfied, adiabatic
   approximation invalid.
2. For fixed λ, the system is integrable (1D bounded → periodic orbit).
   Energy E and λ parametrize the orbit.
3. Write dE/dt = (∂H/∂λ)λ̇. The RHS oscillates on fast timescale.
4. Average over one period (holding λ constant during average):
   ⟨dE/dt⟩ = λ̇ · ⟨∂H/∂λ⟩_period
5. Convert time integral to phase-space integral:
   dt = dq / (∂H/∂p) → ⟨∂H/∂λ⟩ = (∮ ∂H/∂λ · dq/(∂H/∂p)) / (∮ dq/(∂H/∂p))
6. Using H(q,p;λ) = E → ∂H/∂λ + ∂H/∂p · ∂p/∂λ = 0:
   ∂H/∂λ / (∂H/∂p) = −∂p/∂λ|_E
   and 1/(∂H/∂p) = ∂p/∂E|_λ
7. The averages combine to: d/dt (∮ p dq) = 0
8. The adiabatic invariant is:
   I = (1/2π) ∮ p dq    (action variable)
   For rotation (angle coordinate φ): I = (1/2π) ∫₀²π p_φ dφ
```

### Worked Example A: Harmonic Oscillator with Slowly Varying ω(t)
```
H = p²/2m + mω²(t)q²/2
Verify slowness: T = 2π/ω, so need ω̇/ω ≪ ω
For fixed ω: elliptic orbit in (q,p), area = 2πE/ω
→ I = E/ω
→ E(t) = I·ω(t) → energy tracks frequency proportionally
Physical meaning: oscillation amplitude decreases when frequency increases
  (E ∝ ω, but E ∝ ω²A² → A ∝ 1/√ω)
```

### Worked Example B: Magnetic Moment as Adiabatic Invariant
```
Charged particle in slowly varying B field (gyration):
  p_φ = mv_⊥r − eA_φ(r)/c (canonical angular momentum)
  I = (1/2π) ∮ p_φ dφ = ... = (mc/e) μ
  where μ = mv_⊥²/2B is the magnetic moment
→ μ is conserved when B changes slowly on gyroperiod scale
This is the basis of magnetic mirror confinement.
```

### Worked Example C: Kepler Problem — Adiabatic Change of Coupling
```
U = −α(t)/r, α changes slowly
I_φ = M = mvr × r (angular momentum — always conserved exactly)
I_r = −M + α√(m/2|E|) (radial action)
E = −mα²/[2(I_r + I_φ)²]
When α changes slowly: I_r, I_φ conserved
→ eccentricity e² = 1 − [I_φ/(I_r+I_φ)]² stays constant
→ orbit preserves shape, semi-major axis a ∝ 1/α
```

### Error Estimate (Section 51)
```
If λ(t) is analytic (all derivatives bounded), the change in I
over the entire transition λ(−∞) → λ(+∞) is exponentially small:
  ΔI ∝ exp(−C/|λ̇|)  for some constant C
This is much better than the naive T·|λ̇| estimate.
Key assumption: λ(t) varies smoothly — discontinuities in λ̇ or
higher derivatives degrade the invariance.
```

### Edge Cases & Failure Modes
- **Not slow enough**: T |λ̇|/|λ| not ≪ 1 → invariant drifts
- **Resonance crossing**: in multi-DOF systems (Vol.1 §52), if frequencies
  become commensurate during λ-change, adiabatic invariance can break
  (degeneracy enables large energy exchange between DOF)
- **Separatrix crossing**: if the orbit approaches a separatrix (where
  T → ∞), the slowness condition always fails near the separatrix
  → I can change dramatically
- **Non-analytic λ(t)**: if λ̈ is discontinuous, error goes from
  exponential to power-law in λ̇

### Connections
- Old quantum theory: Bohr-Sommerfeld quantization: I = nℏ
- Plasma physics: μ = mv_⊥²/2B is the fundamental adiabatic invariant
  for magnetized plasmas. The longitudinal invariant J = ∮ v_∥ ds
  and flux invariant Φ are the second and third invariants.
- Vol.5: adiabatic theorem in thermodynamics (entropy as adiabatic invariant)

---

## Quick Reference — Which Template When?

| Situation | Template |
|-----------|----------|
| Constructing L for unknown system | T1 |
| Finding conserved quantities from symmetries | T2 |
| Need scaling laws without solving EOM | T3 |
| Switching to Hamiltonian/p,q description | T4 |
| Slowly varying parameter, need invariant | T5 |
