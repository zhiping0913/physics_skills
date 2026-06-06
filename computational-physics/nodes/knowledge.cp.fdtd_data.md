---
skill_id: knowledge.cp.fdtd_data
type: knowledge
summary_50t: >
  FDTD reference: Yee grid staggering patterns, CFL limits for 1D/2D/3D,
  numerical dispersion curves, PML reflection vs thickness/order, TF/SF
  injection formulas, grid resolution vs accuracy (λ/Δ cells).
retrieval_cost: 1
---

# knowledge.cp.fdtd_data — FDTD Reference

## Yee Grid Layout (3D)

| Component | Index | Location |
|-----------|-------|----------|
| E_x | (i+½, j, k) | Mid-edge along x |
| E_y | (i, j+½, k) | Mid-edge along y |
| E_z | (i, j, k+½) | Mid-edge along z |
| H_x | (i, j+½, k+½) | Face center (yz-plane) |
| H_y | (i+½, j, k+½) | Face center (xz-plane) |
| H_z | (i+½, j+½, k) | Face center (xy-plane) |

Each E component is surrounded by 4 H components in the orthogonal plane.

## CFL Stability Limits

| Dimension | Δt_max | Example (Δ=1mm) |
|-----------|--------|-----------------|
| 1D | Δ/c | 3.33 ps |
| 2D (square) | Δ/(c√2) | 2.36 ps |
| 3D (cube) | Δ/(c√3) | 1.92 ps |
| 3D (Δx≠Δy≠Δz) | 1/[c√(1/Δx²+1/Δy²+1/Δz²)] | — |

Safety factor: use 0.95-0.99 × CFL limit.

## Numerical Dispersion (3D, Δx=Δy=Δz=Δ)

For a plane wave at angle (θ,φ), the numerical wavenumber k̃ satisfies:
```
sin²(ωΔt/2) = (cΔt/Δ)² [sin²(k̃_x Δ/2) + sin²(k̃_y Δ/2) + sin²(k̃_z Δ/2)]
```
Worst case: diagonal propagation (θ=45°, φ=45°).
Relative velocity error: (v_p/c − 1) ≈ −(π²/12)(Δ/λ)² + O(Δ/λ)⁴.

| Δ/λ | v_p/c error |
|-----|------------|
| 1/5 | −3.3% |
| 1/10 | −0.8% |
| 1/20 | −0.2% |
| 1/40 | −0.05% |

## PML Performance (10-cell CPML, m=4)

| σ_max/σ_opt | Normal reflection | Grazing (θ=85°) |
|-------------|-------------------|-----------------|
| 0.5 | −40 dB | −25 dB |
| 1.0 (opt) | −65 dB | −35 dB |
| 2.0 | −55 dB | −30 dB |

CPML with α_max=0.05 improves grazing absorption by ~10 dB.

## TF/SF Source Types

| Source | Time-domain | Frequency-domain |
|--------|------------|-----------------|
| Gaussian pulse | e^{−(t−t₀)²/τ²} | Broadband |
| Modulated Gaussian | sin(ω₀t) e^{−(t−t₀)²/τ²} | Band-limited at ω₀ |
| Differentiated Gaussian | −2(t−t₀)/τ² e^{−(t−t₀)²/τ²} | No DC component |
| Sine wave (CW) | sin(ω₀t) | Single frequency |

3D TF/SF box: 6 planar surfaces surrounding scatterer. Add E_inc on
TF side, subtract H_inc on SF side at each interface.

## Common Pitfalls

- **Δt > CFL**: Instant exponential blowup within ~10 time steps.
- **PML touching scatterer**: Near-field evanescent coupling → enhanced reflection.
  Keep scatterer at least 5 cells from PML.
- **Material dispersion without ADE**: Simple ε(ω) ≠ ε_const violates causality
  → unstable or wrong results.
