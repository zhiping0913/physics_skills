---
skill_id: knowledge.lp.pic_parameters
type: knowledge
summary_50t: >
  PIC simulation parameters: grid resolution Δx ≲ 0.5 λ_D, CFL Δt <
  Δx/c√d, particles per cell N_pc > 10. Typical 2D/3D costs: LWFA
  (10⁷–10⁹ cells, 10⁸–10¹⁰ particles). Boosted frame speedup γ_b².
  Common codes: EPOCH, OSIRIS, PIConGPU, SMILEI, WarpX. GPU acceleration
  (PIConGPU ~10× speedup). QED Monte Carlo overhead.
trigger:
  - estimating computational cost for PIC simulation
  - choosing code and resolution for specific problem
parent: reasoning.lp.pic_methods_laser_plasma
retrieval_cost: 1
---

# knowledge.lp.pic_parameters — PIC Codes & Computational Costs

## Resolution Requirements

| Physics constraint | Condition | Typical value at 0.8 μm |
|-------------------|----------|------------------------|
| Laser wavelength | Δx < λ₀/20 | 40 nm |
| Debye length | Δx < λ_D | 10–100 nm |
| Skin depth | Δx < c/ω_p | 5–100 nm |
| CFL (3D cubic) | Δt < Δx/(c√3) | 0.08 fs (Δx=40 nm) |
| Plasma period | Δt < 0.2 × 2π/ω_p | 0.1–1 fs |
| Particle resolution | N_pcell > 10 | Per species |

**Governing resolution**: typically λ_D for collisionless, non-relativistic;
λ₀/N for laser-resolved PIC.

## Computational Cost Estimates

### 2D Cartesian (laser plane)

| Problem | L_x×L_y | Δx | Cells | N_p | Timesteps | CPU-hours |
|---------|---------|-----|-------|-----|-----------|-----------|
| LWFA (mm) | 100×50 μm² | 20 nm | 12.5M | 250M | 10⁵ | ~100–1000 |
| TNSA (μm) | 20×10 μm² | 5 nm | 8M | 160M | 10⁴ | ~10–100 |
| Foil interaction | 20×10 μm² | 5 nm | 8M | 160M | 10⁴ | ~10–100 |

### 3D Cartesian

| Problem | L_x×L_y×L_z | Δx | Cells | N_p | CPU-hours |
|---------|------------|-----|-------|-----|-----------|
| LWFA (mm) | 100×50×50 μm³ | 40 nm | 40M | 800M | 10³–10⁵ |
| TNSA (μm) | 20×20×10 μm³ | 10 nm | 80M | 1.6B | 10⁴–10⁶ |
| QED cascade | 5×5×5 μm³ | 5 nm | 125M | 2.5B | 10⁵–10⁷ |

**Scaling**: cost ∝ N_cells × N_p × N_timesteps ∝ Δx⁻⁴ (3D).

## PIC Codes — Comparison

| Code | Type | GPU | Boosted frame | QED | Ionization | Language |
|------|------|-----|---------------|-----|-----------|----------|
| **EPOCH** | Open-source | ✗ | ✗ | ✓ | ✓ | Fortran |
| **OSIRIS** | Academic | ✓* | ✓ | ✓ | ✓ | Fortran |
| **PIConGPU** | Open-source | ✓✓ | ✓ | ✓ | ✓ | C++/CUDA |
| **SMILEI** | Open-source | ✗ | ✓ | ✓ | ✓ | C++/Python |
| **WarpX** | Open-source | ✓✓ | ✓ | Planned | ✓ | C++/AMReX |
| **VLPL** | Academic | ✓ | ✗ | ✓ | ✓ | Fortran |
| **VPIC** | Open-source | ✓✓ | ✗ | ✗ | ✗ | C++/CUDA |
| **LSP** | Commercial | ✗ | ✗ | ✗ | ✓ | — |
| **CALDER** | Academic | ✓ | ✗ | ✓ | ✓ | C++ |

*OSIRIS GPU version in development.

## Boosted Frame Speedup

| n_e (cm⁻³) | λ₀ (μm) | γ_b_opt | Speedup (γ_b²) | Feasibility |
|------------|---------|---------|---------------|-------------|
| 10¹⁷ | 0.8 | 135 | ~18000 | 3D feasible |
| 10¹⁸ | 0.8 | 43 | ~1800 | 3D feasible |
| 10¹⁹ | 0.8 | 13 | ~170 | 3D marginal |
| 10²⁰ | 0.8 | 4 | ~16 | Limited benefit |

**Overhead**: boosted frame requires FFT-based (PSATD) solver to mitigate
NCI, which adds ~2-3× cost per cell. Net speedup ~γ_b² / 2-3.

## PIC Performance Rules of Thumb

| Metric | 2D | 3D |
|--------|-----|-----|
| Memory per cell | ~1 KB | ~2 KB |
| Particles per cell | 20 | 10 |
| Memory per particle | ~200 B | ~200 B |
| GPU speedup | 5–10× | 10–30× |
| Core-hours per 10⁶ cells per 10⁴ steps | 0.1–1 | 1–10 |

**Typical simulation time**:
- 2D LWFA: hours on workstation (GPU) or small cluster.
- 3D LWFA: days on 1000–10000 cores.
- 3D QED cascade: weeks on largest GPU clusters.

## Common Pitfalls

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| Insufficient λ_D resolution | Grid heating, T_e rising | Δx < λ_D/2 |
| Poor particle statistics | Noisy fields, spurious diffusion | N_pcell > 10 |
| CFL violation | Instability, NaN | Reduce Δt |
| Missing ionization | Wrong n_e, wrong absorption | Enable ADK/BSI |
| NCI (boosted frame) | Exponential noise growth | PSATD + digital filter |
| Reflected EM from boundaries | Spurious fields | PML or large buffer |

## Cross-References

- laser-plasma: reasoning.lp.pic_methods_laser_plasma (parent — method details)
- computational-physics: reasoning.cp.fdtd_yee_algorithm (Yee solver)
- laser-plasma: knowledge.lp.plasma_parameters_laser (n_c, λ_D, ω_p)
