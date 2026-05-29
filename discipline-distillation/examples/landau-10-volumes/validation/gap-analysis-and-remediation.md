# Landau-Graph: Complete Gap Analysis and Remediation Plan

**Based on**: 10-volume closed-book reasoning experiment (DeepSeek V4 Flash)
**Scope**: All 37 existing reasoning nodes across all volumes
**Goal**: Identify missing reasoning nodes and cross-volume bridges

---

## Part I: Missing Universal Reasoning Nodes

These patterns appear in ≥3 volumes but have NO dedicated node.

### U-1. Noether's Theorem (General Form)

**Appears in**: Vol.1, Vol.2, Vol.3, Vol.5, Vol.6, Vol.8, Vol.10

**What exists**: `reasoning.symmetry_to_conservation` (Vol.1) — only covers
point mechanics in Lagrangian form (E, P, M).

**What's missing**: A general Noether theorem covering:
- Classical fields: ∂_j(∂L/∂(∂_jψ)·δψ) − L·δx^j = conserved current
- Quantum: probability current j^μ from U(1) symmetry
- Statistical: ensemble classification by conserved quantities
- Gauge symmetries → constraints, charge conservation

**Why this is a gap**: Without it, the T^{ik} construction in Vol.2 requires
external knowledge. The probability current in Vol.3 appears as a formula
without derivation. The charge conservation in Vol.8 has no foundation.

**Suggested node**: `reasoning.noether_general`

---

### U-2. Legendre Transform (in All Contexts)

**Appears in**: Vol.1, Vol.5, Vol.7, Vol.8

**What exists**: `reasoning.canonical_transformation` (Vol.1) — covers generating
functions for canonical transformations, but presented as a mechanics tool.

**What's missing**: A unified Legendre transform node:
- Thermodynamics: F↔Ω↔G↔H (Vol.5)
- Elasticity: Helmholtz ↔ elastic potential (Vol.7)
- Dielectrics: F(E) ↔ F(D) (Vol.8)
- Lagrangian ↔ Hamiltonian (Vol.1)

The MATHEMATICS is identical in all cases: given F(x), define G(y) = F − xy
with y = dF/dx. But no single node captures this universality.

**Suggested node**: `reasoning.legendre_transform_universal`

---

### U-3. Matched Asymptotic Expansions / Multiple Scales

**Appears in**: Vol.1, Vol.3, Vol.5, Vol.6, Vol.10

**What exists**: `reasoning.small_parameter_expansion` (Vol.1) — covers
Taylor expansion near equilibrium. `reasoning.adiabatic_invariance` (Vol.1) —
covers two-timescale separation.

**What's missing**: A general multiple-scales/matched-asymptotics node:
- Boundary layers (Vol.6): inner/outer expansion, matching
- WKB (Vol.3): short-wavelength expansion, connection formulas
- Adiabatic (Vol.1): fast/slow timescale separation
- Chapman-Enskog (Vol.10): Knudsen number expansion
- Regular vs singular perturbations

The `small_parameter_expansion` node covers REGULAR perturbations
(Taylor series). SINGULAR perturbations (boundary layers, WKB turning
points) need a DIFFERENT method — matched asymptotics.

**Suggested node**: `reasoning.matched_asymptotics`

---

### U-4. Linear Response Theory

**Appears in**: Vol.5, Vol.8, Vol.9, Vol.10

**What exists**: `reasoning.causality_to_analyticity` (Vol.8) — only covers
the Kramers-Kronig aspect. `reasoning.fluctuation_dissipation_quantum` (Vol.9) —
covers the FDT but at the quantum level.

**What's missing**: A general linear response theory node:
- Definition: χ_{AB}(t) = iθ(t)⟨[A(t), B(0)]⟩ for any two observables
- Response: ⟨ΔA⟩(ω) = χ_{AB}(ω) · F_B(ω)
- Causality → Kramers-Kronig
- Fluctuation-dissipation theorem
- Onsager reciprocal relations
- Applications: dielectric (Vol.8), susceptibility (Vol.5), conductivity

**Suggested node**: `reasoning.linear_response_general`

---

### U-5. The Exponential / Logarithm Trick (Cumulant Expansion)

**Appears in**: Vol.3, Vol.5, Vol.9

**What exists**: `reasoning.thermodynamic_perturbation_theory` (Vol.5)
contains the key insight: "F = −T ln Z, and Z involves Σ exp(...).
The logarithm cancels extensive terms."

**What's missing**: This trick extends beyond thermodynamics:
- Generating functions in statistics: ln⟨e^{tX}⟩ = Σ κ_n t^n/n!
- Connected diagrams in QFT: W = ln Z, Feynman rules for connected graphs
- Correlation functions: cumulants = connected moments

This is a universal mathematical pattern: the logarithm turns a sum of
exponentials into an extensive quantity.

**Suggested node**: `reasoning.cumulant_expansion`

---

### U-6. Scale Invariance and Conformal Symmetry

**Appears in**: Vol.1, Vol.2, Vol.5, Vol.6

**What exists**: `reasoning.homogeneity_to_scaling` (Vol.1) — covers
homogeneous potentials and mechanical similarity. `reasoning.dimensional_analysis_to_similarity` (Vol.6) — covers Π-theorem and dimensionless numbers.

**What's missing**: The connection between scale-invariant actions and
traceless energy-momentum tensors. Specifically:
- Scale invariance → T^μ_μ = 0 (Vol.2)
- EM field F² is scale-invariant → T^{ik} of EM is traceless
- Conformal invariance in 2D → infinite-dimensional symmetry

**Suggested node**: `reasoning.scale_invariance_traceless_t`

---

## Part II: Missing Volume-Specific Reasoning Nodes

### V1-1. Galilean Invariance → Lagrangian Construction

**Volume**: Vol.1 (Mechanics)
**Gap identified in**: Vol.1 report (Confusion 1-3)

**What's missing**: The derivation of L = ½mv² from Galilean invariance:
1. Free particle L = f(v²) by homogeneity + isotropy
2. L' = L + dF/dt allows ambiguity
3. Transform between inertial frames → L = const·v² + const
4. Additivity across subsystems → const = m/2
5. For interacting particles: L = T(v²) − U(r)

**Without this**: The momentum formula P = Σ mv and the energy
E = T + U appear as assumptions, not consequences.

---

### V1-2. Hidden / Dynamical Symmetries

**Volume**: Vol.1 (Mechanics)
**Gap identified in**: Vol.1 report (Confusion 7)

**What's missing**: Symmetries that are NOT obvious from the Lagrangian:
- Runge-Lenz vector in 1/r potential (extra conservation law)
- Laplace-Runge-Lenz → orbit closure without Bertrand
- Fradkin symmetry of harmonic oscillator (SO(4) or SU(3))
- How to FIND hidden symmetries: check if orbit closes for all bound states

**Without this**: Runge-Lenz is a "surprise" — no reasoning template
predicts it.

---

### V1-3. Bertrand's Theorem (Full Proof)

**Volume**: Vol.1 (Mechanics)
**Gap identified in**: Vol.1 report (Confusion 5)

**What's missing**: Complete proof that only U∝−1/r and U∝r² give
closed orbits for all bound states. Requires:
1. Circular orbit: perturbation analysis of Δφ
2. Expand Δφ around circular orbit to second order
3. Show that Δφ = 2π requires specific U(r) form

**Current coverage**: `reasoning.conservation_to_effective_reduction`
note: "Only U∝−1/r and U∝r² give strictly closed orbits (Bertrand)."
— This is an assertion, not a derivation.

---

### V2-1. Noether Current for Fields

**Volume**: Vol.2 (Fields)
**Gap identified in**: Vol.2 report (Confusion 14), revised Vol.2

**What's missing**: The field-theoretic Noether procedure:
1. For translation x^i → x^i + ε^i: δL = ∂_k(ε^k L)
2. Using equations of motion → ∂_k T^{kl} = 0
3. T^{kl} = (∂L/∂(∂_k A_i))·∂^l A_i − g^{kl}L
4. Belinfante symmetrization for gauge-invariant T^{ik}

**Without this**: The EM energy-momentum tensor T^{ik} is a memorized
formula rather than a derived consequence of translation invariance.

---

### V2-2. Liénard-Wiechert Fields (from potentials)

**Volume**: Vol.2 (Fields)
**Gap identified in**: Vol.2 report (Confusion 11)

**What's missing**: The computation from LW potentials to fields:
1. φ = e/[R − v·R/c], A = ev/[c(R − v·R/c)]
2. E = −∇φ − (1/c)∂A/∂t
3. The retarded-time derivatives produce κ = 1 − n·v/c
4. Velocity field (1/R²) and acceleration field (1/R)
5. The full: E = e[(n−v/c)(1−v²/c²)/(κ³R²)]_ret + e[n×[(n−v/c)×v̇]]/(c²κ³R)_ret

**Without this**: There's a large algebraic gap between the LW potential
and the LW field formulas in the knowledge node.

---

### V2-3. Relativistic Radiation (General)

**Volume**: Vol.2 (Fields)
**Gap identified in**: Vol.2 report (Confusion 12, 13)

**What's missing**: When the multipole condition a ≪ λ FAILS (γ ≫ 1):
1. Return to LW acceleration field as starting point
2. Fourier transform for spectral distribution
3. Relativistic beaming: κ³ denominator → Δθ ~ 1/γ
4. Synchrotron: Airy function → K_{5/3} Bessel function
5. Undulator/wiggler: periodic motion, harmonic structure

**Without this**: Synchrotron radiation is only covered by the knowledge
node (formula given) with no derivation path.

---

### V3-1. Spin from Rotation Group

**Volume**: Vol.3 (QM)
**Gap identified in**: Vol.3 report (Confusion 14)

**What's missing**: The quantum theory of angular momentum:
1. Ladder operators: L_± = L_x ± iL_y
2. [L_+, L_-] = 2ℏL_z, [L_z, L_±] = ±ℏL_±
3. Eigenvalues: L²|l,m⟩ = ℏ²l(l+1)|l,m⟩
4. Half-integer l allowed by algebra but NOT by orbital L = r×p
5. Spin = intrinsic angular momentum with no orbital representation
6. Pauli matrices and spin-½

**Current coverage**: `knowledge.quantum.angular_momentum` exists as a
knowledge leaf with NO reasoning parent for the ladder operator derivation.
The half-integer case is stated, not derived.

---

### V3-2. Identical Particles / Exchange Symmetry

**Volume**: Vol.3 (QM)
**Gap identified in**: Vol.3 report (multiple)

**What's missing**: The quantum statistics of identical particles:
1. Ψ(1,2) = ±Ψ(2,1) for bosons/fermions from indistinguishability
2. Slater determinant for fermions, permanent for bosons
3. Pauli exclusion principle: no two fermions in same state
4. Exchange interaction: E_ex = ±⟨ψ₁ψ₂|V|ψ₂ψ₁⟩
5. Spin-statistics theorem (connection to Vol.4)

**Without this**: The entire theory of multi-electron atoms, the periodic
table, and the Bose/Fermi distributions in Vol.5 have no foundation
in the reasoning graph.

---

### V3-3. WKB Connection Formulas

**Volume**: Vol.3 (QM)
**Gap identified in**: Vol.3 report (Confusion 9, 11)

**What's missing**: The Airy function matching at turning points:
1. Near x = a where E = U(a): linearize U(x) ≈ E + F(x−a)
2. Schrödinger → Airy equation: ψ''(ξ) − ξψ(ξ) = 0
3. Asymptotic matching of Airy functions
4. Connection formulas:
   - 2/√p cos(∫_x^a p dx'/ℏ − π/4) ↔ 1/√|p| exp(−∫_a^x |p|dx'/ℏ)
   - Maslov index γ = ½ (from π/4 phase shift per turning point)

**Current coverage**: `reasoning.wkb_quasiclassical` gives the WKB
wave function and validity condition, but the connection formulas
are only in the knowledge node, not derivable from the reasoning.

---

### V4-1. Feynman Diagram Construction

**Volume**: Vol.4 (QED)
**Gap identified in**: Vol.4 report (Confusion 6)

**What's missing**: The systematic construction of Feynman rules:
1. Dyson expansion: S = T exp(−i∫H_int d⁴x)
2. Wick contractions: T(ψ̄ψA ψ̄ψA ...) = Σ (all pairings) × G₀
3. Feynman rules from S-matrix expansion
4. Momentum-space rules: vertices, propagators, loops
5. Cross-section formula from |M|²

**Current coverage**: `reasoning.quantum_perturbation_theory` (Vol.3)
gives the non-relativistic PT structure. `reasoning.retarded_green_function`
(Vol.2) gives the propagator concept. But the leap from these to
Feynman diagrams requires a dedicated node.

---

### V4-2. Renormalization

**Volume**: Vol.4 (QED)
**Gap identified in**: Vol.4 report (biggest single gap)

**What's missing**: The complete renormalization program:
1. UV divergences in loop diagrams
2. Regularization (Pauli-Villars, dimensional)
3. Counterterms: mass, charge, wave function
4. Renormalization conditions
5. Running coupling: β(e) = μ de/dμ
6. Asymptotic freedom vs QED infrared behavior

**Without this**: The most important technical achievement of QED
(the finite predictions for Lamb shift, g−2) cannot be understood.
This is arguably the largest single gap in the entire graph.

---

### V4-3. Covariant Quantization of Gauge Fields

**Volume**: Vol.4 (QED)
**Gap identified in**: Vol.4 report (Confusion 3)

**What's missing**: How to quantize A^μ covariantly:
1. Problem: A^μ has 4 components but only 2 physical polarizations
2. Gupta-Bleuler formalism: k·a|phys⟩ = 0
3. Faddeev-Popov ghosts for non-Abelian gauge theories
4. Relation to gauge fixing and the photon propagator

---

### V5-1. Landau Theory of Phase Transitions

**Volume**: Vol.5 (Stat Phys I)
**Gap identified in**: Vol.5 report (major omission)

**What's missing**: The complete Landau theory:
1. Order parameter: η (magnetization, polarization, etc.)
2. Free energy expansion: F(η) = F₀ + aη² + bη⁴ + ...
3. Second-order transition: a = a₀(T−T_c), b > 0
4. Critical exponents: β = ½, γ = 1, ν = ½ (mean field)
5. Fluctuation corrections → Ginzburg criterion
6. First-order transitions: b < 0 or cubic term

**Without this**: A major part of Vol.5 (§83-88, §143-156) has no
reasoning coverage.

---

### V5-2. Grand Canonical Ensemble

**Volume**: Vol.5 (Stat Phys I)
**Gap identified in**: Vol.5 report (partial coverage)

**What's missing**: The grand ensemble in detail:
1. Grand partition function: Ξ = Σ exp[(μN − E_n)/T]
2. Grand potential: Ω = −T ln Ξ = −PV
3. Number: N = −∂Ω/∂μ
4. Fluctuations: ⟨(ΔN)²⟩ = T∂²Ω/∂μ²
5. Connection to canonical via fugacity expansion

**Current coverage**: `reasoning.partition_to_thermodynamics` mentions
the grand canonical in its edge cases but doesn't develop it fully.
The knowledge node `free_energy` gives Ω = −PV.

---

### V6-1. Kolmogorov Turbulence Theory

**Volume**: Vol.6 (Fluid)
**Gap identified in**: Vol.6 report (biggest single gap)

**What's missing**: The turbulence cascade:
1. Richardson cascade: energy flows from large to small scales
2. Kolmogorov 1941: E(k) = C ε^{2/3} k^{−5/3} (inertial range)
3. Kolmogorov scale: η_K = (ν³/ε)^{1/4}
4. Energy dissipation: ε = ν⟨(∇v)²⟩
5. Intermittency corrections
6. Two-point correlation functions

**Without this**: ~30% of Vol.6 (turbulence chapters) has no reasoning
foundation. `reasoning.dimensional_analysis_to_similarity` gives the
tool (Re, Π-theorem) but the specific turbulence phenomenology
requires a dedicated node.

---

### V6-2. Boundary Layer Theory

**Volume**: Vol.6 (Fluid)
**Gap identified in**: Vol.6 report (Confusion 3)

**What's missing**: The Prandtl boundary layer:
1. Prandtl's 1/√Re scaling: δ/x ~ 1/√Re
2. Boundary layer equations (parabolic, not elliptic)
3. Blasius solution: f''' + ff'' = 0
4. Displacement thickness, momentum thickness
5. Separation: ∂p/∂x > 0 → adverse pressure gradient → separation

**Without this**: Chapter IV of Vol.6 has no reasoning coverage.

---

### V7-1. 3D→1D/2D Elastic Reduction

**Volume**: Vol.7 (Elasticity)
**Gap identified in**: Vol.7 report (Confusion 1)

**What's missing**: How to reduce 3D elasticity to beam/plate equations:
1. Euler-Bernoulli beam: assume plane sections remain plane
2. Kirchhoff plate: midsurface approximation
3. Timoshenko beam: include shear deformation
4. St. Venant's principle
5. Buckling: Euler load P_cr = π²EI/L²

**Without this**: Chapter II of Vol.7 has no reasoning coverage.

---

### V7-2. Defect Mechanics

**Volume**: Vol.7 (Elasticity)
**Gap identified in**: Vol.7 report (Confusion 2)

**What's missing**: Dislocations and fracture:
1. Burgers vector b and dislocation types (edge, screw, mixed)
2. Stress field of a dislocation: σ_θz = μb/2πr
3. Dislocation energy: E = (μb²/4π)ln(R/r₀)
4. Peierls stress, Frank-Read sources
5. Griffith fracture criterion: σ_f = √(2Eγ/πa)

**Without this**: Chapters III-IV of Vol.7 have no reasoning coverage.

---

### V8-1. Nonlinear Optics

**Volume**: Vol.8 (Continuous Media)
**Gap identified in**: Vol.8 report (Confusion 3)

**What's missing**: The nonlinear response:
1. P = χ⁽¹⁾E + χ⁽²⁾E² + χ⁽³⁾E³ + ...
2. Second harmonic generation: ω + ω → 2ω
3. Phase matching: Δk = 0 condition
4. Manley-Rowe relations (energy conservation in nonlinear processes)
5. Pockels effect (linear electro-optic)
6. Kerr effect (quadratic electro-optic)
7. Parametric processes: SPDC, OPO

---

### V8-2. Magnetohydrodynamics (MHD)

**Volume**: Vol.8 (hybrid Vol.6+Vol.8)
**Gap identified in**: Vol.8 report

**What's missing**: The coupling of fluid flow and EM fields:
1. Induction equation: ∂B/∂t = ∇×(v×B) + η_m∇²B
2. Frozen-in flux: B is "frozen" into the plasma at high Rm
3. Alfvén waves: ω = k·v_A, v_A = B/√(4πρ)
4. Magnetic pressure: p_B = B²/8π
5. Pinch effect: J×B confinement

MHD is a CROSS-VOLUME subject requiring BOTH Vol.6 (fluid) and
Vol.2/Vol.8 (EM). A dedicated synthesis node is needed.

---

### V9-1. BCS Superconductivity

**Volume**: Vol.9 (Condensed Matter)
**Gap identified in**: Vol.9 report

**What's missing**: The microscopic theory of superconductivity:
1. Cooper instability: bound state from attractive interaction at T_c
2. BCS gap equation: Δ_k = −½ Σ V_{kk'} Δ_{k'}/E_{k'}
3. T_c: from gap equation at Δ → 0
4. Meissner effect: perfect diamagnetism
5. Flux quantization: Φ₀ = hc/2e
6. Josephson effect

**Without this**: The most important application of the Green's function
method in condensed matter (BCS) has no reasoning coverage.

---

### V9-2. Strongly Correlated Systems

**Volume**: Vol.9 (Condensed Matter)
**Gap identified in**: Vol.9 report

**What's missing**: When Fermi liquid theory breaks down:
1. Hubbard model: H = −t Σ⟨ij⟩ c_i†c_j + U Σ n_i↑n_i↓
2. Mott insulator: at U ≫ t, electrons localize
3. Kondo effect: magnetic impurity in metal
4. Luttinger liquid: 1D systems (TL model)
5. Non-Fermi liquid behavior near quantum critical points

---

## Part III: Missing Cross-Volume Bridges

These connect EXISTING reasoning nodes across volumes.

### B-1. δS=0 → Lagrangian Construction Bridge

**Connects**: `reasoning.variational_principle` (Vol.1)
          → `reasoning.lorentz_invariance_to_action` (Vol.2)
          → `reasoning.classical_to_quantum_correspondence` (Vol.3)

**Purpose**: Shows the SAME template (δS=0 → find L → derive EOM)
in three different contexts:
- Classical: find L from symmetries → E-L equations
- Relativistic: find L from Lorentz invariance → Dirac/EM action
- Quantum: find L as operator → Schrödinger equation

**Gap**: The student knows "δS=0" but doesn't know HOW to find L.
The bridge should give the method: "determine L from symmetry principles."

---

### B-2. Poisson Bracket → Commutator Bridge

**Connects**: `reasoning.canonical_transformation` (Vol.1)
          → `reasoning.classical_to_quantum_correspondence` (Vol.3)

**Purpose**: Shows that {f,g} → [f̂,ĝ]/iℏ is not an analogy but
the SAME mathematical structure:
- {q,p} = 1 → [q̂,p̂] = iℏ
- {f,H} = df/dt → [f̂,Ĥ] = iℏ df̂/dt
- Invariant under canonical/unitary transformations

**Gap**: Without this bridge, quantization appears as an arbitrary
rule ("replace p by −iℏ∇") rather than the natural generalization
of the symplectic structure.

---

### B-3. Propagator Family Bridge

**Connects**: `reasoning.retarded_green_function` (Vol.2)
          → `reasoning.wkb_quasiclassical` (Vol.3)
          → `reasoning.green_function_method` (Vol.9)
          → `reasoning.second_quantization` (Vol.4)

**Purpose**: Shows the UNIFIED concept of propagators across all physics:
- Classical: retarded Green's function G_ret = δ(t−R/c)/R
- Quantum: Feynman propagator K(x,t;x',t') = ⟨x|e^{−iĤt/ℏ}|x'⟩
- Many-body: G(x,x') = −i⟨T ψ(x)ψ†(x')⟩
- Path integral: K = ∫ D[x] exp(iS/ℏ)

**Gap**: Each appears in a different volume with different notation.
The bridge should make explicit they're the SAME concept.

---

### B-4. Causality → Analyticity Universal Bridge

**Connects**: `reasoning.causality_to_analyticity` (Vol.8)
          → `reasoning.fluctuation_dissipation_quantum` (Vol.9)
          → `reasoning.landau_damping` (Vol.10)
          → `reasoning.partition_to_thermodynamics` (Vol.5)

**Purpose**: Shows the universal pattern:
"Causality → response analytic in upper half-plane → Kramers-Kronig"
appearing in:
- Dielectric function ε(ω) (Vol.8)
- Landau damping i0 prescription (Vol.10)
- Fluctuation-dissipation theorem (Vol.9)
- Generalized susceptibility (Vol.5)

---

### B-5. WKB → Eikonal → Geometric Optics Bridge

**Connects**: `reasoning.wkb_quasiclassical` (Vol.3)
          → `reasoning.multipole_expansion_radiation` (Vol.2)
          → (Vol.6 geometric acoustics, currently no node)

**Purpose**: Shows the same λ→0 (short wavelength) limit in:
- Quantum: WKB wave function, H-J equation (Vol.3)
- EM: geometric optics, eikonal equation (Vol.2)
- Sound: geometric acoustics (Vol.6)
- Elastic: ray theory for seismic waves (Vol.7)

**Existing reference**: The WKB node explicitly cross-references
Vol.2 §53 (geometric optics). But no node captures the general
principle.

---

### B-6. Equilibrium → Kinetic Bridge

**Connects**: `reasoning.ensemble_logic` (Vol.5)
          → `reasoning.kinetic_equation_closure` (Vol.10)
          → `reasoning.microcanonical_to_canonical` (Vol.5)

**Purpose**: Shows how equilibrium emerges from kinetics:
- Boltzmann equation → H-theorem → equilibrium distribution
- St f = 0 → Maxwell-Boltzmann = canonical ensemble
- Detailed balance = microreversibility
- Gibbs vs Boltzmann: two formulations of the SAME equilibrium

---

### B-7. Perturbation Theory Quadruple Bridge

**Connects**: `reasoning.small_parameter_expansion` (Vol.1)
          → `reasoning.quantum_perturbation_theory` (Vol.3)
          → `reasoning.thermodynamic_perturbation_theory` (Vol.5)
          → `reasoning.green_function_method` (Vol.9, Dyson equation)

**Purpose**: The SINGLE most cross-referenced pattern in the graph.
Explicitly show the parallel structure:

| | Classical (V1) | Quantum (V3) | Statistical (V5) | Many-body (V9) |
|---|---|---|---|---|
| Bare | x₀(t) | ψ⁽⁰⁾, E⁽⁰⁾ | F₀, Z₀ | G₀ |
| Correction | x₁(t) | E⁽¹⁾=⟨V⟩ | F₁=⟨V⟩ | Σ |
| Small param | amplitude | ΔE splitting | V/T | V/g(ε_F) |

---

### B-8. Constitutive Relation Trinity Bridge

**Connects**: `reasoning.constitutive_relation_from_symmetry` (Vol.6)
          → (Vol.7 Hooke's law, currently inferred)
          → (Vol.8 dielectric tensor, currently inferred)
          → (Vol.10 transport coefficients, currently inferred)

**Purpose**: The SINGLE most powerful cross-volume transfer.
Show that ONE method (linearity + symmetry → unique tensor form)
gives THREE constitutive relations:
- Viscous stress σ'_ik = η(∂_i v_k + ∂_k v_i − ⅔δ_ik div v) + ζδ_ik div v
- Hooke's law σ_ik = 2μ u_ik + λδ_ik u_ll
- Dielectric D_i = ε_ik E_k (classified by crystal symmetry)
- Conductivity j_i = σ_ik E_k

---

### B-9. Adiabatic Invariant Triple Bridge

**Connects**: `reasoning.adiabatic_invariance` (Vol.1)
          → `reasoning.wkb_quasiclassical` (Vol.3)
          → (quantum adiabatic theorem, currently missing)

**Purpose**: Show the three manifestations of the SAME principle:
- Classical: I = (1/2π)∮p dq is conserved for slow λ(t)
- Quantum: Bohr-Sommerfeld I = (n+½)ℏ from WKB
- Quantum: adiabatic theorem — system stays in instantaneous eigenstate
- Modern: Berry phase γ = i∮⟨n|∇_R n⟩·dR

**Existing reference**: The WKB node says "Connects directly to
adiabatic invariant I = ∮p dq / 2π → I = (n+γ)ℏ." But neither
has a bridge to the quantum adiabatic theorem.

---

### B-10. Energetic Convexity / Stability Bridge

**Connects**: `reasoning.small_parameter_expansion` (Vol.1, stability)
          → `reasoning.partition_to_thermodynamics` (Vol.5, F minimum)
          → `reasoning.variational_principle` (Vol.1, δ²S > 0)

**Purpose**: Show that stability = convexity of an energy functional:
- Mechanics: δ²U > 0 at equilibrium (positive definite Hessian)
- Thermodynamics: F minimum at fixed T,V; G minimum at fixed T,P
- Elasticity: elastic energy positive definite
- QM: Ĥψ = Eψ, ground state minimizes ⟨ψ|Ĥ|ψ⟩

---

## Part IV: Implementation Priority

| Priority | Node | Reason | Affected Volumes |
|----------|------|--------|-----------------|
| P0 | B-8 Constitutive trinity | Single biggest cross-volume pattern | 6, 7, 8, 10 |
| P0 | V4-2 Renormalization | Biggest single gap in QED | 4 |
| P0 | V3-2 Identical particles | Missing foundation for Vol.5 Fermi/Bose | 3, 5 |
| P1 | U-1 Noether general | Appears in 7 volumes | 1, 2, 3, 5, 6, 8, 10 |
| P1 | V6-1 Kolmogorov turbulence | 30% of Vol.6 uncovered | 6 |
| P1 | V5-1 Phase transitions | Major Vol.5 topic | 5 |
| P1 | V3-1 Spin/ladder operators | Needed for Vol.3 + Vol.5 magnetism | 3, 5 |
| P2 | U-2 Legendre transform | 4 volumes | 1, 5, 7, 8 |
| P2 | B-7 PT quadruple bridge | Most cross-referenced pattern | 1, 3, 5, 9 |
| P2 | V4-1 Feynman diagrams | Needed for Vol.4 core | 4 |
| P2 | B-9 Adiabatic triple bridge | Connects V1→V3 | 1, 3 |
| P3 | U-3 Matched asymptotics | 4 volumes | 1, 3, 5, 6 |
| P3 | V1-1 Galilean→Lagrangian | Foundation gap in V1 | 1 |
| P3 | V2-3 Relativistic radiation | Synchrotron gap | 2 |
| P3 | V6-2 Boundary layers | Vol.6 Chapter IV | 6 |
| P3 | V7-1 Elastic reduction | Vol.7 Chapter II | 7 |
| P4 | U-4 Linear response general | Unifies 4 volumes | 5, 8, 9, 10 |
| P4 | V1-2 Hidden symmetries | Runge-Lenz | 1 |
| P4 | V2-2 LW fields | Algebraic gap | 2 |
| P4 | V8-1 Nonlinear optics | Vol.8 Chapter XI | 8 |
| P4 | V8-2 MHD | Cross-volume gap | 6+8 |
| P4 | V9-1 BCS | Important application | 9 |
| P5 | U-5 Cumulant expansion | Niche but useful | 3, 5, 9 |
| P5 | U-6 Scale invariance | Elegant but specialized | 1, 2, 5 |
| P5 | V1-3 Bertrand theorem | Specific proof | 1 |
| P5 | V3-3 Connection formulas | WKB completion | 3 |
| P5 | V4-3 Gauge quantization | Technical QED gap | 4 |
| P5 | V5-2 Grand canonical detail | Enhancement | 5 |
| P5 | V7-2 Defect mechanics | Vol.7 Chapters III-IV | 7 |
| P5 | V9-2 Strongly correlated | Beyond Fermi liquid | 9 |

---

## Part V: Summary Statistics

**Total nodes recommended**: 10 universal (U) + 22 volume-specific (V) + 10 bridges (B) = **42 new reasoning nodes**
**Total existing**: 37 reasoning nodes
**Increase**: ~114%

**By implementation effort**:
- P0 (critical): 3 nodes
- P1 (high): 7 nodes
- P2 (medium): 6 nodes
- P3 (lower): 9 nodes
- P4 (selective): 9 nodes
- P5 (completion): 8 nodes

**Key insight**: Just the P0 nodes (B-8, V4-2, V3-2) would fill the
three largest gaps in the graph. The top 10 priority nodes (P0+P1)
would address ~70% of all identified gaps.

---

*End of analysis.*
