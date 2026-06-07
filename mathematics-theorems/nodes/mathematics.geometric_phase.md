---
skill_id: mathematics.geometric_phase
type: reasoning
summary_50t: >
  Geometric phase = phase acquired by a system transported along a closed
  loop in parameter space: γ = ∮ A · dλ. Unifies Berry phase (adiabatic
  quantum), Pancharatnam-Berry phase (polarization optics), Aharonov-Bohm
  phase (gauge potential), Foucault pendulum (parallel transport on sphere).
  Core structure: connection 1-form integrated along parameter path.
trigger:
  - understanding phase accumulation beyond dynamical phase (e^{−iEt/ℏ})
  - recognizing when PB, Berry, AB, or Foucault are the SAME geometric structure
  - designing geometric-phase metasurfaces or topological photonic devices
reasoning_role: geometric_phase_unifier
parent: mathematics.complex_analysis
retrieval_cost: 1
---

# mathematics.geometric_phase — γ = ∮ A · dλ

## Core Picture

A geometric phase is a phase shift that depends only on the **path in parameter
space**, not on time elapsed or dynamical evolution. In all four canonical
examples — Berry, PB, AB, Foucault — the phase is given by the line integral
of a **connection 1-form** (gauge potential) along a closed parameter-space
loop. The phenomenon is fundamentally topological: it survives even when the
dynamical phase vanishes.

## Derivation Sketch — Universal Structure

### 1. The connection 1-form A

In each domain, there exists a parameter-dependent quantity (Hamiltonian
eigenstate, polarization state, gauge field) with a natural inner product
that defines parallel transport:

| Domain | Parameter space | Connection 1-form A | Phase γ = ∮ A · dλ |
|--------|----------------|--------------------|--------------------|
| Berry phase (quantum adiabatic) | Hamiltonian parameter space {R} | A_n(R) = i⟨n(R)|∇_R|n(R)⟩ | γ_n = ∮ A_n · dR |
| Pancharatnam-Berry (polarization) | Poincaré sphere S² of polarization | A_σ = −σ · (k × dk)/(2k²) | γ_PB = −½ Ω (solid angle) |
| Aharonov-Bohm (gauge) | Real space around solenoid | A_μ = (q/ℏ) A_μ^EM | γ_AB = (q/ℏ) ∮ A · dl = (q/ℏ) Φ |
| Foucault pendulum (classical) | Tangent sphere of Earth rotation | A = −cos θ dφ | γ_F = −2π cos θ (per 24h) |

### 2. Berry phase (quantum adiabatic theorem, Berry 1984)

A quantum system with Hamiltonian H(R(t)) that varies slowly and returns to
its initial parameter values after time T acquires:
```
|ψ(T)⟩ = exp(iγ_n) exp(−(i/ℏ)∫₀ᵀ E_n(t) dt) |n(0)⟩
         └─ geometric ─┘ └───── dynamical ─────┘
```
where:
```
γ_n = i ∮ ⟨n(R)|∇_R|n(R)⟩ · dR
```
For a spin-½ in a slowly rotating magnetic field B(t) that traces a closed
curve on the parameter sphere: γ = −½ Ω, where Ω is the solid angle subtended
by the curve at the origin.

### 3. Pancharatnam-Berry (PB) phase in optics

When the polarization state of light is transported along a closed loop on
the Poincaré sphere, the beam acquires a geometric phase equal to **minus
half the solid angle** subtended by the loop:
```
γ_PB = −½ Ω
```

For a circularly polarized input beam passing through a half-wave plate
rotated by angle α, the output is:
```
|L⟩ → e^{+2iα} |R⟩,    |R⟩ → e^{−2iα} |L⟩
```
The factor e^{±2iα} is the PB phase. This is the basis of geometric-phase
metasurfaces: element orientation α(r,φ) = lφ/2 → PB phase = lφ → OAM beam
of charge l. This also enables **spin-orbit conversion**: SAM (handedness
flip L↔R) ↔ OAM gain (±l).

### 4. Aharonov-Bohm (AB) effect

An electron wave passing around a magnetic solenoid acquires a phase:
```
γ_AB = (q/ℏ) ∮ A · dl = (q/ℏ) Φ = 2π (Φ/Φ₀)
```
where Φ₀ = h/q is the flux quantum. The phase is non-zero even though B = 0
everywhere along the electron path. The connection 1-form is the EM gauge
potential A_μ itself.

**Connection to Berry**: the AB phase can be reformulated as a Berry phase
where the parameter is the magnetic flux Φ and the eigenstates are the
Aharonov-Bohm scattering states (not the usual energy eigenstates).

### 5. Foucault pendulum — geometric phase as parallel transport

A Foucault pendulum at latitude θ precesses by:
```
Δφ = −2π cos θ    per 24 hours
```
This is the holonomy (geometric phase) from parallel-transporting the
pendulum's swing plane vector along the latitude circle on the rotating
Earth. The connection is the Levi-Civita connection on the sphere:
```
A = −cos θ dφ,    γ = ∮ A = −2π cos θ
```

### 6. The unifying gauge-theoretic structure

All four instances obey the same pattern:
```
γ = ∮_C A_i dλ^i
```
where A is a gauge connection in a fiber bundle. The curvature 2-form
F = dA gives the phase as the surface integral (Stokes):
```
γ = ∮_C A = ∬_S F
```
For the sphere (Berry, PB, Foucault): F = (1/2) sin θ dθ ∧ dφ →
γ = −½ × (area enclosed) = −½ Ω.

## Algorithm — Recognize and Compute a Geometric Phase

```
1. IDENTIFY the parameter space M (sphere, torus, R³\{solenoid}, ...).

2. IDENTIFY the fiber: what is being parallel-transported?
   - Quantum eigenstate |n(R)⟩
   - Polarization state on Poincaré sphere
   - Electron wavefunction in gauge potential
   - Pendulum swing plane on rotating sphere

3. FIND the connection 1-form A:
   - Berry: A_n = i⟨n|d|n⟩
   - PB: A = −½(1 − cos θ) dφ on Poincaré sphere
   - AB: A = (q/ℏ) A_μ dx^μ
   - Foucault: A = −cos θ dφ

4. INTEGRATE along the closed path C:
   γ = ∮_C A

5. CHECK the sign convention (solid angle → γ = −½Ω for most cases).

6. VERIFY gauge invariance: γ mod 2π is independent of gauge choice.
```

## Cross-Domain Table

| Domain | Physical System | Parameter Space | Connection | Phase | Topological Invariant |
|--------|---------------|----------------|-----------|-------|---------------------|
| Quantum adiabatic | Spin in B-field, molecular Born-Oppenheimer | H-parameter manifold | Berry connection | γ = −½Ω | Chern number (integer) |
| Polarization optics | Waveplate, metasurface, bent fiber | Poincaré sphere S² | PB connection | γ = −½Ω | Spin-orbit conversion |
| Gauge theory | Electron near solenoid | Real space − solenoid | EM vector potential A_μ | γ = (q/ℏ)Φ | Flux quantum Φ₀ = h/q |
| Classical mechanics | Foucault pendulum | Rotating Earth S² | Levi-Civita connection | γ = −2π cos θ | Parallel transport holonomy |
| General relativity | Gyroscope in orbit | Curved spacetime | Christoffel symbols Γ^λ_{μν} | Precession angle | Curvature → geodesic deviation |
| Topological photonics | Light in photonic crystal | k-space Brillouin zone | Berry curvature of bands F_n(k) | γ = ∬ F_n d²k | Chern number → edge states |

## Application to Metasurface Design

For a PB-phase metasurface generating an OAM beam of charge l:
1. Incident beam: circular polarization (|L⟩ or |R⟩)
2. Element orientation: α(φ) = lφ/2
3. PB phase: γ(φ) = ±2α(φ) = ±lφ (sign from input handedness)
4. Output: opposite handedness + OAM = lℏ

Practical requirement: elements must function as local half-wave plates
(π phase retardation between fast/slow axes) for 100% conversion efficiency.

## Edge Cases

- **Non-adiabatic (Aharonov-Anandan) phase**: For cyclic but non-adiabatic
  evolution, the geometric phase generalizes to the Aharonov-Anandan phase
  γ = ∮ ⟨ψ|i d/dt − H/ℏ|ψ⟩ dt (subtract dynamical part).
- **Non-closed paths**: Geometric phase for open curves is gauge-dependent.
  Only closed-path holonomies are gauge-invariant.
- **Degenerate subspaces (Wilczek-Zee)**: When the eigenspace is degenerate,
  the geometric phase becomes a unitary matrix (non-Abelian holonomy).
  Foundation of topological quantum computing.

## Cross-References

- Berry, M.V., "Quantal phase factors accompanying adiabatic changes,"
  Proc. R. Soc. Lond. A 392:45 (1984) — the original paper
- Pancharatnam, S., "Generalized theory of interference," Proc. Ind. Acad.
  Sci. A 44:247 (1956) — PB phase precedes Berry by 28 years
- Aharonov, Y., Bohm, D., "Significance of electromagnetic potentials in the
  quantum theory," Phys. Rev. 115:485 (1959)
- mathematics-theorems: mathematics.complex_analysis (parent — contour
  integrals, holonomy structure)
- electrodynamics: knowledge.em.oam_beams (PB phase for OAM generation)
- electrodynamics: knowledge.em.vector_wave_functions (Hansen m = OAM l)
