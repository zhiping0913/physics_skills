---
skill_id: mathematics.noether_selection_rules
type: reasoning
summary_50t: >
  Noether's theorem: every continuous symmetry → conserved current → selection
  rule. 6-domain specialization: translation→momentum conservation (phase
  matching), rotation→OAM conservation (l_n=n·l_1), gauge→charge conservation,
  discrete translation→crystal momentum (umklapp, QPM). Symmetry breaking as
  selection rule relaxation — continuous→discrete introduces modulo-N allowances.
  Cross-domain template: selection rules = Noether charges in quantum transition
  amplitudes.
trigger:
  - deriving conservation / selection rules for nonlinear optical processes
  - understanding why crystal symmetry relaxes OAM or momentum conservation
  - unifying phase matching, OAM rules, atomic transitions, and QPM under one principle
reasoning_role: symmetry_selection_rules
parent: mathematics.distribution_limits
retrieval_cost: 1
---

# mathematics.noether_selection_rules — Symmetry → Conserved Current → Selection Rule

## Core Picture

Every continuous symmetry of the action corresponds to a conserved Noether
current ∂_μ j^μ = 0. The conserved charge Q = ∫ j⁰ d³x then imposes a
**selection rule**: quantum transition amplitudes ⟨f|O|i⟩ vanish unless the
conserved charge is equal in initial and final states. The same Noether
structure governs momentum conservation in phase matching, angular momentum
conservation in harmonic generation, crystal momentum in periodic lattices,
and charge conservation in gauge theories. When symmetry is **broken** from
continuous to discrete, the conservation rule relaxes — the conserved
quantity is only defined modulo the symmetry group order (umklapp paradigm).

## Derivation Sketch

### 1. Noether's theorem for classical fields

For a field theory with Lagrangian density L(φ_a, ∂_μ φ_a), an infinitesimal
symmetry transformation:
```
x^μ → x^μ + ε X^μ(x),    φ_a → φ_a + ε Φ_a(x,φ)
```
that leaves the action invariant (δS = 0) implies the conserved current:
```
j^μ = (∂L/∂(∂_μ φ_a)) Φ_a − T^μ_ν X^ν
```
with ∂_μ j^μ = 0 on-shell. The conserved charge Q = ∫ j⁰ d³x is time-independent.

### 2. Quantum selection rule from conserved charge

In quantum field theory, the conserved charge becomes an operator Q̂ that
commutes with the Hamiltonian: [Q̂, Ĥ] = 0. Eigenstates of Q̂ with eigenvalues q:
```
⟨q_f | O | q_i⟩ = 0    unless q_f = q_i (for Q̂-invariant operators O)
```
For a transition amplitude with n initial and m final particles:
```
Σ_f q_f = Σ_i q_i         (conserved charge selection rule)
```

### 3. Six-domain specialization

| Symmetry | Conserved Noether charge | Selection rule | Domain |
|----------|-------------------------|---------------|--------|
| **Time translation** (t → t + ε) | Energy E | E_f = E_i (energy conservation) | All physics |
| **Spatial translation** (x → x + ε) | Linear momentum P | **Σ k_f = Σ k_i** (phase matching Δk = 0) | Nonlinear optics, particle scattering |
| **Continuous rotation** (φ → φ + ε) | Angular momentum L_z | **l_out = Σ l_in** (OAM conservation in χ⁽ⁿ⁾) | Nonlinear optics with OAM beams |
| **U(1) gauge** (ψ → e^{iα}ψ) | Electric charge Q | Q_f = Q_i (charge conservation) | EM, particle physics |
| **Discrete translation** (x → x + a) | Crystal momentum ℏK mod G | **K_f = K_i + G** (umklapp, QPM) | Solid state, periodic structures |
| **Rotational SO(3)** | Total angular momentum J | **ΔJ = 0, ±1** (dipole selection) | Atomic transitions |

The first four are continuous (exact); the last two are discrete (modulo-N).

## Selection Rules by Domain

### A. Nonlinear Optics — Phase Matching as Momentum Conservation

Spatial translation invariance of the medium → linear momentum conserved:
```
Δk = Σ k_out − Σ k_in = 0    (perfect phase matching)
```
When violated (Δk ≠ 0): conversion efficiency η ∝ sinc²(Δk L/2). The finite
crystal length L limits momentum resolution by Δk ∼ 2π/L (uncertainty
principle: finite interaction region → momentum non-conservation within Δk).

**Quasi-phase matching (QPM)** as deliberate discrete symmetry:
```
Δk_QPM = Δk − k_G = 0,    k_G = 2π/Λ (grating vector)
```
Introducing a periodic domain inversion (Λ = 2L_coh) breaks continuous
translation to discrete translation. Momentum is conserved modulo k_G —
this IS the crystal-momentum paradigm applied to engineered nonlinear optics.

### B. Nonlinear Optics — OAM as Angular Momentum Conservation

Rotational invariance about the propagation axis → OAM conserved:
```
l_n = n × l_1          (nth-harmonic generation from l_1 input)
```
For SHG: l_SH = 2 l_fund. For SFG: l_sum = l_1 + l_2.

**Crystal point-group symmetry breaking**: Real crystals have discrete n-fold
rotational symmetry (C_n), not continuous C_∞. The selection rule relaxes:
```
l_out = Σ l_in ± n_crystal × m    (m = 0, ±1, ±2, ...)
```
This is the **angular-momentum umklapp** — the crystal can absorb/release
angular momentum in units of its rotational symmetry order. For BBO (3m):
l_out = Σ l_in ± 3m. For LiNbO₃ (3m): same. For KDP (4̄2m): multiples of 4.

### C. Atomic Transitions — Dipole Selection Rules

SO(3) rotational symmetry of the Coulomb potential + photon (J=1):
```
ΔL = 0, ±1    (not 0→0);    Δm_L = 0, ±1
ΔS = 0        (spin-forbidden, broken by spin-orbit)
ΔJ = 0, ±1    (not 0→0)
```
Parity (spatial inversion symmetry): Laporte rule Δl = ±1 for electric-dipole.
Higher multipoles (M1, E2) have different selection rules because the
interaction Hamiltonian carries different angular momentum.

### D. Solid State — Crystal Momentum and Umklapp

Discrete translation invariance → crystal momentum ℏk conserved modulo
reciprocal lattice vector G:
```
k_f = k_i + G
```
Normal processes (G = 0): "momentum conserved." Umklapp processes (G ≠ 0):
"momentum not conserved" in the naive sense, but crystal momentum IS conserved.
This is the same structure as QPM: grating k_G ↔ G.

### E. Plasma — Manley-Rowe as Photon Number Conservation

The Manley-Rowe relations (photon number conservation in lossless nonlinear
mixing) follow from the time-averaged Hamiltonian structure — an adiabatic
invariant, not an exact Noether charge for time-dependent Hamiltonians. But
in the rotating-wave approximation (time-averaged, stationary envelope), the
photon flux N_i/ω_i is the conserved quantity:
```
ΔN₁/ω₁ = ΔN₂/ω₂ = ΔN₃/ω₃ = ...
```
This bridges to `plasma: reasoning.plasma.instability_classification`
(parametric instabilities — L → L' + S follows same Manley-Rowe structure).

## Symmetry Breaking as Selection Rule Relaxation

The general template:

| Symmetry type | Conservation | Breaking mechanism | Relaxed rule |
|--------------|-------------|-------------------|-------------|
| Continuous translation C_∞^trans | Δk = 0 (exact) | Finite crystal length L | η ∝ sinc²(Δk L/2); Δk ∼ 2π/L allowed |
| Discrete translation (period Λ) | Δk = 0 mod 2π/Λ | — | Δk = k_G (QPM) |
| Continuous rotation C_∞^rot | Σ l_f = Σ l_i (exact) | Crystal point group C_n | Σ l_f = Σ l_i mod n |
| Continuous rotation SO(3) | ΔJ = 0, ±1 | Spin-orbit coupling | ΔS ≠ 0 allowed; intersystem crossing |
| Spatial inversion P | Parity conserved | Crystal without inversion center | Parity not a good quantum number |

**Unifying principle**: Continuous symmetry → exact conservation law.
Discrete symmetry → conservation modulo group order. Finite interaction
volume/time → conservation within uncertainty width.

## Algorithm — Given Process → Selection Rules

```
1. IDENTIFY the interaction Lagrangian/Hamiltonian: L_int, H_int.

2. LIST the symmetries of the TOTAL system:
   - Translation (continuous → momentum; discrete → crystal momentum)
   - Rotation (continuous → total J; discrete → modulo n_crystal)
   - Gauge / phase rotation → charge / photon number
   - Parity / time reversal → parity / Kramers degeneracy

3. For continuous symmetries:
   Compute Noether charges Q_i = q_i for each particle.
   Selection rule: Σ_f q_f = Σ_i q_i.

4. For discrete symmetries:
   Selection rule: Σ_f q_f = Σ_i q_i mod N (N = symmetry order).
   Identify which G vectors (umklapp) or n_crystal multiples are allowed.

5. For broken symmetries:
   - Finite size → conservation within Δk ∼ 2π/L.
   - Spin-orbit → ΔS ≠ 0 transitions with small amplitude (∼ (Zα)²).
   - Crystal field → point-group-determined angular momentum mixing.

6. WRITE the net selection rule as ⟨f|H_int|i⟩ ≠ 0 iff {rules satisfied}.

7. VERIFY: test with known cases (SHG OAM, phase matching, dipole ΔL=±1).
```

## Cross-Domain Unification Table

| Domain | Process | Symmetry | Conserved Charge | Selection Rule |
|--------|---------|----------|-----------------|---------------|
| Nonlinear optics (SHG) | ω+ω→2ω in bulk crystal | Continuous translation | k (momentum) | k_{2ω} = 2k_ω (phase matching) |
| Nonlinear optics (QPM) | SHG in PPLN | Discrete translation (Λ) | k mod 2π/Λ | k_{2ω} = 2k_ω + k_G |
| Nonlinear optics (OAM-SHG) | l_fund → l_SH in C_∞ | Continuous rotation | L_z (OAM) | l_SH = 2 l_fund |
| Nonlinear optics (OAM-crystal) | l_fund → l_SH in BBO (3m) | Discrete rotation C_3 | L_z mod 3 | l_SH = 2 l_fund ± 3m |
| Atomic transitions | |g⟩ → |e⟩ + photon | SO(3) rotation | J, m_J | ΔJ = 0, ±1; Δm_J = 0, ±1 |
| Solid state (electron) | k → k' + phonon | Discrete translation | k mod G | k' = k + q + G |
| Plasma parametric | L → L' + S (Langmuir decay) | Time-averaged Hamiltonian | N/ω (Manley-Rowe) | ΔN_L/ω_L = ΔN_{L'}/ω_{L'} = ΔN_S/ω_S |
| Particle physics | n → p + e⁻ + ν̄ | SU(2)×U(1) gauge | Q, B, L | Q_n = Q_p+Q_e; B,L conserved (approx) |

## Connection to geometric_phase

The conserved charge from continuous rotation symmetry is the same OAM that
appears in the geometric phase for twisted wavefronts. The PB phase 2α is
the holonomy from transporting polarization on the Poincaré sphere; the OAM
selection rules constrain which holonomies are compatible with which crystal
symmetries. Cross-reference: `mathematics.geometric_phase` §PB phase for
metasurface OAM generation.

## Edge Cases

- **Nonlinear crystals without inversion center**: χ⁽²⁾ ≠ 0, but parity broken
  → no parity selection rule. All χ⁽²⁾-allowed transitions possible within
  Δk and OAM rules.
- **Rotational symmetry < n_crystal in SHG**: If a BBO crystal is cut so the
  propagation axis is NOT along the 3-fold axis, the effective symmetry along
  k is lower → OAM mixing from off-axis propagation.
- **Gouy phase contributes to effective OAM**: The mode-dependent Gouy phase
  ψ_G = (2p+|l|+1)arctan(z/z_R) BREAKS the translational symmetry along z in
  focused beams → OAM is not exactly conserved across a focus unless the full
  modal decomposition is considered.
- **Time-dependent media**: When ε(t) or the Hamiltonian is explicitly
  time-dependent, energy is not a Noether charge. The system may still have
  adiabatic invariants.

## Cross-References

- Landau Vol.1 §6-7 (Noether's theorem in classical mechanics)
- Landau Vol.2 §2 (Noether for fields; energy-momentum tensor)
- Landau Vol.3 §29-31 (angular momentum selection rules for dipole radiation)
- mathematics-theorems: mathematics.distribution_limits (parent — delta functions
  enforce conservation in transition amplitudes)
- mathematics-theorems: mathematics.geometric_phase (PB holonomy from U(1)
  symmetry; OAM selection rules constrain compatible holonomies)
- electrodynamics: reasoning.em.nonlinear_optical_response (SHG, OAM conservation)
- electrodynamics: knowledge.em.oam_beams (OAM beam generation and detection)
- plasma: reasoning.plasma.instability_classification (Manley-Rowe for
  parametric instabilities)
