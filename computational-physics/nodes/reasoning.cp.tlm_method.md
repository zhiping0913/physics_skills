---
skill_id: reasoning.cp.tlm_method
type: reasoning
summary_50t: >
  Space discretized as transmission-line network. Voltage/current pulses
  scatter at nodes. Two-step cycle: scatter (Huygens principle at nodes)
  → connect (pulses propagate to neighbors). Equivalence to Maxwell via
  Huygens' principle. Shunt (2D TM) and series (2D TE) nodes. SCN (3D).
trigger:
  - time-domain EM simulation via circuit-network analogy
  - modeling complex boundaries, thin wires, diffusion, acoustics
reasoning_role: tlm_network_solver
parent: reasoning.em.waveguide_mode_decomposition
retrieval_cost: 1
---

# reasoning.cp.tlm_method — Space → Transmission-Line Network

## Core Picture

TLM replaces continuous space with a network of interconnected transmission
lines. Voltage pulses propagate along lines, scatter at junctions (nodes),
and reconnect — exactly analogous to Huygens' principle for EM waves. The
result is an explicit, unconditionally stable time-domain scheme.

## Derivation Sketch

From `electrodynamics: reasoning.em.waveguide_mode_decomposition`
(TE/TM modes in waveguides → a 2D cross-section supports wave propagation
modeled as voltage/current on equivalent transmission lines):

1. A 2D plane (x,y) is replaced by a mesh of interconnected TL segments.
   Each segment has inductance L (∝ μ) and capacitance C (∝ ε).
2. Voltage pulses incident on a node from four directions scatter according
   to a scattering matrix S (determined by impedance continuity).
3. The scattered pulses propagate to neighboring nodes in one time step Δt.

Equivalence condition: Δt = Δℓ/c where Δℓ is the mesh spacing and c = 1/√(LC).

## Algorithm — 2D Shunt Node (TM_z, E_z, H_x, H_y)

```
1. BUILD MESH: Rectangular grid, spacing Δℓ. Each node labeled (i,j).

2. INITIALIZE: At t=0, incident voltage pulses V^i_k = 0 on all 4 branches
   (k = 1,2,3,4 for −x, +x, −y, +y).

3. TIME LOOP (n = 1 to N):
   a. SCATTER at every node:
      V^s = S · V^i   where S_ij = ½ if i≠j, S_ii = −½
      (Total voltage at node: V_z = ½ Σ V^i_k → E_z ∝ V_z)
   b. CONNECT: scattered pulses become incident on neighbors at next time step:
      V^i_{1}(i,j) = V^s_{2}(i−1,j)    (outgoing right → incoming from left)
      V^i_{2}(i,j) = V^s_{1}(i+1,j)    (outgoing left → incoming from right)
      V^i_{3}(i,j) = V^s_{4}(i,j−1)    (outgoing top → incoming from bottom)
      V^i_{4}(i,j) = V^s_{3}(i,j+1)    (outgoing bottom → incoming from top)
   c. EXCITATION: Soft source — add source pulse V_src(t) to all incident pulses V^i_k at the source node at each time step. For z-polarized E-field in 2D shunt TLM: add V_src equally to all 4 ports. Pulse shape: Gaussian derivative V_src(t) = (t−t₀)/τ exp(−(t−t₀)²/(2τ²)) for zero-DC broadband excitation. Hard source (overwrite total voltage) reflects outgoing waves — avoid unless modeling an ideal voltage generator.
   d. BOUNDARY: at PEC: reflect with −1. At PMC: reflect with +1.
      At absorbing (Absorbing Boundary): At mesh boundaries, terminate the exterior half-links with matched impedance Z_L = Z₀ (characteristic impedance of the link). Reflection coefficient Γ = (Z_L−Z₀)/(Z_L+Z₀) = 0 at matched boundary. For normal incidence this gives ~−20 dB reflection. For improved absorption, add 8-10 PML layers of TLM cells with graded loss (conductivity stubs).
   e. OUTPUT: record E_z(i,j) = ½ Σ V^i_k(i,j) at observation points.
```

## 3D: Symmetrical Condensed Node (SCN)

The 2D node generalizes to 12 transmission lines per 3D node (Johns 1987).
SCN is the standard 3D TLM cell. It models full vector Maxwell with all 6
field components in one cell, no staggering needed.

SCN scattering (Johns 1987): 12 incident pulses V^i labeled by port (direction + polarization). The scattered pulses V^s = S·V^i where S = ½ I − ... The key coupling: voltage pulses on links in the same coordinate plane are coupled through the node center. For lossless isotropic media: all reflected pulses receive ½ sum of co-planar incident pulses minus the incident pulse itself.

## Key Properties

- **Unconditional stability** (unlike FDTD): the scheme is stable for any
  Δt because it preserves passivity — the scattering matrix S is unitary
  for lossless media.
- **Memory**: stores pulse histories (typically 12 floats per cell for 3D
  SCN). Higher than FDTD's 6 field components.
- **Boundaries**: PEC/PMC/absorbing handled by pulse reflection coefficients.
  Curved boundaries via conformal mapping of TL segment lengths.

## Edge Cases

- **Fine features (≪ Δℓ)**: Use graded mesh or multigrid TLM.
- **Dispersive materials**: Frequency-dependent L, C or Z_termination
  implemented via digital filter networks (Z-transform).
- **Thin wires/slots**: Subcell models: modify node scattering to incorporate
  wire inductance or slot capacitance.

## Cross-References

- Christopoulos, *The Transmission-Line Modeling Method* (1995) Ch.1-10
- Johns & Beurle, Proc. IEE 118, 1203 (1971)
- electrodynamics: reasoning.em.waveguide_mode_decomposition (parent)
- computational-physics: reasoning.cp.fdtd_yee_algorithm (alternative time-domain solver)
