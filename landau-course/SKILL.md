---
name: landau-course
description: "Landau-Lifshitz 10巻 physics navigation layer. KB paths, key equations, chapter maps. \nLandauGraph (84 nodes, 144 edges, 9 vols complete) at /home/zhiping/.hermes/skills/landau-graph/.\nFull methodology: references/landaugraph-status.md."
---

# Landau & Lifshitz — Course of Theoretical Physics

> **STATUS: 9/10 volumes distilled. LandauGraph: 84 nodes, 144 edges.**
> This skill is the **navigation layer**. For the full reasoning graph, see
> `references/landaugraph-status.md` and `/home/zhiping/.hermes/skills/landau-graph/`.

Distilled reference for the 10-volume Russian edition (ФИЗМАТЛИТ, 2001–2005).
All 10 volumes in `/home/zhiping/knowledge_base/book/`.

## §0 — How to use this skill

This is a **physics navigation and equation index**, not a replacement for the original.
For each volume:

| Section | What it gives you |
|---------|-------------------|
| Core idea | One-paragraph physical essence |
| Chapter map | What each chapter covers, in physical terms |
| Key equations | Selected equations with physical interpretation |
| KB reference | Path to full `.md` in knowledge base |

When you need to go deeper: read the referenced `.md` file from the knowledge base.

---

## §1 — Volume 1: Mechanics (Механика, 2004, 5th ed.)

KB: `/home/zhiping/knowledge_base/book/2004/2004--Механика/book.md`

### Core idea

Mechanics is not a collection of problem-solving recipes — it is the first systematic application of the **principle of least action** to physical systems. Landau opens with generalized coordinates (§1), arrives at the Lagrangian within four sections, and never touches Newton's laws until §5 — and even then only as a derived consequence. The entire structure is deductive: spacetime symmetries → conservation laws (§6–9), homogeneity of potential → mechanical similarity and the virial theorem (§10). The second half of the book builds the canonical formalism (§40–48) and culminates in **adiabatic invariants** (§49–52), a distinctly Landau contribution that connects classical mechanics to the old quantum theory and, later, to plasma physics.

### Chapter map

**Ch I — Equations of Motion (§1–§5)**
- §1 Generalized coordinates: configuration space, degrees of freedom s
- §2 Principle of least action: action S = ∫L dt, δS = 0 → Euler-Lagrange equations. Lagrangian defined up to total time derivative.
- §3 Galileo's relativity: inertial frames, homogeneity/isotropy of space and time
- §4 Lagrangian of a free particle: from Galilean invariance alone → L = mv²/2. Mass defined via additivity.
- §5 Lagrangian of a system: L = T − U, Newton's equations as consequence. External fields → U(r,t). Constraints and degrees of freedom.

**Ch II — Conservation Laws (§6–§10)**
- §6 Energy: time homogeneity → ∂L/∂t = 0 → E = Σ q̇ᵢ ∂L/∂q̇ᵢ − L = T + U
- §7 Momentum: space homogeneity → P = Σ ∂L/∂vₐ conserved. Generalized momenta pᵢ = ∂L/∂q̇ᵢ.
- §8 Center of mass: R = Σ mₐrₐ / Σ mₐ, moves uniformly for closed system. Internal energy E_int.
- §9 Angular momentum: space isotropy → M = Σ [rₐ × pₐ] conserved. Transformation between frames.
- §10 Mechanical similarity: if U is homogeneous of degree k, geometrically similar trajectories exist with t'/t = (l'/l)^(1−k/2). *Virial theorem*: 2⟨T⟩ = k⟨U⟩. For Newtonian/Coulomb (k=−1): 2⟨T⟩ = −⟨U⟩; for small oscillations (k=2): ⟨T⟩ = ⟨U⟩.

**Ch III — Integration of Equations of Motion (§11–§16)**
- §11 One-dimensional motion: energy integral suffices, quadrature dt = dx/√(2[E−U(x)]/m)
- §12 Period from potential: T(E) = √(2m) ∮ dx/√[E−U(x)]
- §13 Reduced mass: two-body problem → one-body with μ = m₁m₂/(m₁+m₂)
- §14 Central field: angular momentum conservation → effective 1D radial motion with U_eff = U(r) + M²/2mr²
- §15 Kepler problem: U = −α/r. Closed elliptical orbits. E < 0 → bound. Third law: T² ∝ a³.

**Ch IV — Collisions (§17–§20)**
- §17 Disintegration of particles
- §18 Elastic collisions: conservation of P and E in lab and CM frames
- §19 Scattering: cross-section, impact parameter, scattering angle
- §20 Rutherford formula: dσ/dΩ ∝ 1/sin⁴(θ/2) for Coulomb scattering

**Ch V — Small Oscillations (§22–§29)**
- §22 Free 1D oscillations: ω = √(k/m)
- §23 Forced oscillations: resonance when ω ≈ ω₀
- §24 Systems with many degrees of freedom: normal modes, secular equation
- §26 Damped oscillations: e^{−λt} decay, aperiodic damping threshold
- §27 Parametric resonance: Mathieu equation, instability zones

**Ch VI — Rigid Body Motion (§31–§39)**
- §31–33 Angular velocity, inertia tensor, principal axes
- §34–36 Euler's equations: I₁ω̇₁ = (I₂−I₃)ω₂ω₃ + M₁
- §37 Asymmetric top: integrable case, Poinsot construction
- §39 Motion in non-inertial frames: Coriolis, centrifugal forces

**Ch VII — Canonical Equations (§40–§52)**
- §40 Hamilton's equations: q̇ = ∂H/∂p, ṗ = −∂H/∂q. H = Σ pᵢq̇ᵢ − L.
- §42 Poisson brackets: {f,g} = Σ (∂f/∂qᵢ ∂g/∂pᵢ − ∂f/∂pᵢ ∂g/∂qᵢ). {f,H} = df/dt.
- §43 Action as function of coordinates: S(q,t) satisfies p = ∂S/∂q, ∂S/∂t = −H.
- §44 Maupertuis principle: δ∫ p dq = 0 for fixed energy.
- §45 Canonical transformations: preserving Hamilton equations form. Generating functions.
- §47 Hamilton-Jacobi equation: ∂S/∂t + H(q, ∂S/∂q, t) = 0. Separability.
- §48 Separation of variables: when H-J separates, each coordinate yields constant of motion.
- §49 Adiabatic invariants: for slowly varying parameter λ (T |dλ/dt| ≪ |λ|), I = (1/2π)∮p dq is conserved. For harmonic oscillator: I = E/ω.
- §50 Action-angle variables: ẇ = dE/dI = ω(I), İ = 0. Every single-valued function periodic in w with period 2π.
- §51 Accuracy of adiabatic invariance: ΔI is exponentially small in 1/λ̇ for analytic λ(t).
- §52 Conditionally-periodic motion: s action variables Iᵢ (one per degree of freedom) when H-J separates. Degeneracy when frequencies commensurate. Kepler problem: I_φ = M, I_r = −M + α√(m/2|E|).

### Key equations

```
δS = δ∫ L dt = 0,  L = L(q, q̇, t)
    →  d/dt (∂L/∂q̇ᵢ) − ∂L/∂qᵢ = 0
```
_Euler-Lagrange equations. The entire mechanical formalism follows from this variational principle._

```
E = Σ q̇ᵢ ∂L/∂q̇ᵢ − L = T + U
```
_Energy conservation from time homogeneity. For closed systems, ∂L/∂t = 0 → E = const._

```
P = Σ ∂L/∂vₐ = Σ mₐvₐ     (conserved from space homogeneity)
M = Σ [rₐ × pₐ]            (conserved from space isotropy)
```
_The seven additive integrals of a closed system._

```
2⟨T⟩ = k⟨U⟩    (virial theorem)
```
_For homogeneous potential U ∝ rᵏ. k=−1 (Coulomb): 2⟨T⟩ = −⟨U⟩. k=2 (harmonic): ⟨T⟩ = ⟨U⟩._

```
t'/t = (l'/l)^(1−k/2)    (mechanical similarity)
```
_Geometrically similar trajectories for homogeneous potentials. Kepler's 3rd law: k=−1 → T² ∝ a³._

```
H = Σ pᵢq̇ᵢ − L,   q̇ᵢ = ∂H/∂pᵢ,   ṗᵢ = −∂H/∂qᵢ
```
_Hamilton's canonical equations. Phase space (q,p) flow preserves volume (Liouville)._

```
∂S/∂t + H(q, ∂S/∂q, t) = 0    (Hamilton-Jacobi)
```
_The central equation for canonical transformation theory. When separable, s conserved quantities emerge._

```
I = (1/2π) ∮ p dq,   dI/dt = 0 for adiabatic λ(t)
```
_Adiabatic invariant. For harmonic oscillator: I = E/ω. For Kepler: I_φ = M, I_r = −M + α√(m/2|E|)._

```
ẇ = ω(I) = dE/dI,   İ = 0,   Δw = 2π per period
```
_Action-angle variables. I is the adiabatically invariant action, w is the phase._

### Distillation notes

- Landau's approach is deductive, not inductive. He starts from the most general principle (least action) and derives everything downward. This is the opposite of how mechanics is usually taught.
- The Lagrangian is not defined — it is *discovered* from symmetry requirements (Galilean invariance, homogeneity, isotropy). This is the deepest lesson of the volume.
- Adiabatic invariants (§49–§52) are the bridge from classical to quantum mechanics. The Bohr-Sommerfeld quantization condition is I = nℏ. In plasma physics, the magnetic moment μ = mv⊥²/2B is an adiabatic invariant.
- The virial theorem (§10) is used throughout astrophysics and plasma physics.
- Poisson brackets (§42) are the classical precursor to quantum commutators.
- The book uses s degrees of freedom and writes "for brevity we denote by q the set of all q₁,...,qₛ" — this compressed notation is Landau's trademark.

---

## §2–§10 — Remaining Volumes

_Vol.1, 2, 5, 10 have been fully distilled into the LandauGraph format (see references/landaugraph-methodology.md)._

Volume 2: Classical Theory of Fields (2003) — **DISTILLED** (14 nodes)
Volume 3: Quantum Mechanics (2002) — pending
Volume 4: Quantum Electrodynamics (2005) — pending
Volume 5: Statistical Physics Part 1 (2002) — **DISTILLED** (11 nodes)
Volume 6: Fluid Mechanics (2001) — pending
Volume 7: Theory of Elasticity (2003) — pending
Volume 8: Electrodynamics of Continuous Media (2005) — pending
Volume 9: Statistical Physics Part 2 (2001) — pending
Volume 10: Physical Kinetics (2002) — **DISTILLED** (10 nodes)

---

## §CROSS — Cross-Volume Concept Index

_To be populated as volumes are distilled._

| Concept | Volumes |
|---------|---------|
| Action principle | 1§2, 2§8 |
| Conservation laws | 1§6–9 |
| Symmetry → Lagrangian form | 1§4 (Galilean), 2§8 (Lorentz) |
| Virial theorem | 1§10, 2§34 |
| Adiabatic invariants | 1§49–52 |
| Poisson brackets → commutators | 1§42, 3 |
| Hamilton-Jacobi | 1§47 |
| Canonical transformations | 1§45 |
| Central field / Kepler | 1§14–15 |
| Lorentz transformation | 2§4 |
| Mass-energy equivalence | 2§9 |
| EM field tensor / Maxwell eqns | 2§23, §26-31 |
| Gauge invariance | 2§18 |
| Retarded potentials | 2§62 |
| Liénard-Wiechert potentials | 2§63 |
| Dipole radiation | 2§67 |
| Synchrotron radiation | 2§74 |
| EM energy-momentum tensor | 2§32-33 |
| Scale separation (multipole) | 2§67 ↔ 1§10, §21-22 |
| Action decomposition S = S_f+S_m+S_mf | 2§27 |
| Entropy S = ln ΔΓ = −Σ w_n ln w_n | 5§7 |
| Gibbs (canonical) distribution | 5§28-29 |
| Partition function → thermodynamics | 5§31 |
| Thermodynamic perturbation theory | 5§32 |
| Equipartition theorem | 5§44 |
| Fermi-Dirac statistics | 5§53-61 |
| Bose-Einstein statistics / BEC | 5§53-55, §62-63 |
| Fluctuations / fluctuation-dissipation | 5§110-123 |

---

## §KB — Knowledge Base Path Table

All paths relative to `/home/zhiping/knowledge_base/book/`.

| Vol | Title | Year | Nodes | Status |
|-----|-------|------|-------|--------|
| 1 | Механика | 2004 | 21 | ✓ |
| 2 | Классическая теория поля | 2003 | 14 | ✓ |
| 3 | Квантовая механика | 2002 | 7 | ✓ |
| 4 | Квантовая электродинамика | 2005 | 4 | ✓ |
| 5 | Статистическая физика. Часть 1 | 2002 | 11 | ✓ |
| 6 | Гидродинамика | 2001 | 7 | ✓ |
| 7 | Теория упругости | 2003 | — | pending |
| 8 | Электродинамика сплошных сред | 2005 | 6 | ✓ |
| 9 | Статистическая физика. Часть 2 | 2001 | 5 | ✓ |
| 10 | Физическая кинетика | 2002 | 10 | ✓ |
| **Total** | | | **84** | 9/10 done |

## LandauGraph (Reasoning-Constrained Physics Skill Graph)

A deeper, graph-structured distillation of the Landau course exists at
`/home/zhiping/.hermes/skills/landau-graph/`. It contains:

- **75 individual SKILL.md nodes** (per-concept, not per-chapter)
- **GRAPH.json** with 125 typed edges (prerequisite, reasoning-instance, analogy, abstraction)
- Each node: 50-token fast-load header + 300-token full body + KB path reference

The extraction methodology is documented in `references/extraction-methodology.md`.
