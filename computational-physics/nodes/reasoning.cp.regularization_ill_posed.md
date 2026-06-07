---
skill_id: reasoning.cp.regularization_ill_posed
type: reasoning
summary_50t: >
  First-kind integral equations Ku=f are ill-posed when K is compact:
  singular values σ_n→0, so noisy data components along small singular
  vectors are amplified by 1/σ_n. Stabilize with Tikhonov
  u_α=(K^*K+α²I)^{-1}K^*f, filter σ²/(σ²+α²), or early-stopped
  CG/LSQR before semi-convergence. Choose α/iteration by Morozov
  discrepancy ||Ku−f||≈δ or L-curve corner.
trigger:
  - solving noisy first-kind integral equations from MoM or inverse problems
  - stabilizing compact-operator inversions with decaying singular values
  - choosing Tikhonov regularization parameter or iterative stopping point
reasoning_role: inverse_problem_regularization
parent: reasoning.cp.moment_method
retrieval_cost: 1
---

# reasoning.cp.regularization_ill_posed — Compact Ku=f Needs Controlled Inversion

## Core Picture

First-kind integral equations

```
(Ku)(x) = ∫_Ω k(x,y) u(y) dy = f(x)
```

are often smoothing maps: fine-scale structure in `u` is blurred in `f`.
Mathematically, many such operators `K` are compact. Their singular values
`σ_n` accumulate at zero, so the formal inverse is unbounded. If measured data
are `f^δ = f + η` with `||η|| ≈ δ`, then solving `Ku=f^δ` naively divides noise
components by tiny `σ_n` and produces oscillatory, nonphysical `u`.

For a discrete MoM or inverse-problem matrix `K = UΣV*`, the least-squares
solution is

```
u_LS = Σ_n (u_n^* f^δ / σ_n) v_n.
```

Small `σ_n` modes behave like high-gain noise amplifiers. Regularization means:
keep data-supported modes, damp unsupported modes, and verify that the residual
is consistent with the known noise level rather than fitting noise.

## Why Compact First-Kind Equations Are Ill-Posed

Hadamard well-posedness requires existence, uniqueness, and continuous
dependence on data. Compact first-kind equations typically fail continuous
dependence:

1. `K` maps bounded sets to relatively compact sets, suppressing fine scales.
2. Singular values satisfy `σ_1 ≥ σ_2 ≥ ... → 0`.
3. The inverse gain along right singular vector `v_n` is `1/σ_n`.
4. Even small noise coefficients `u_n^* η` dominate when `σ_n ≲ δ`.

Thus the practical inverse is not “solve harder,” but “solve only to the
information content of the data.”

## Tikhonov Regularization

Classical zero-order Tikhonov solves

```
u_α = argmin_u ||Ku − f^δ||² + α² ||u||²
    = (K^*K + α² I)^{-1} K^* f^δ.
```

In SVD coordinates,

```
u_α = Σ_n [ σ_n / (σ_n² + α²) ] (u_n^* f^δ) v_n
     = Σ_n [ σ_n² / (σ_n² + α²) ] (u_n^* f^δ / σ_n) v_n.
```

The quantity

```
φ_n(α) = σ_n² / (σ_n² + α²)
```

is the filter factor. For `σ_n >> α`, `φ_n ≈ 1` and the mode is retained. For
`σ_n << α`, `φ_n ≈ σ_n²/α²` and the noise-sensitive mode is suppressed.

Generalized Tikhonov replaces `||u||²` by `||L u||²`, where `L` encodes smoothness,
minimum curvature, divergence constraints, or physically admissible source
structure:

```
u_α = argmin_u ||Ku − f^δ||² + α² ||L u||².
```

Use `L=I` for minimal-energy solutions; use derivative or physics-based `L` when
roughness, charge nonconservation, or unphysical source oscillation is the danger.

## Early-Stopped CG / LSQR and Semi-Convergence

Iterative solvers for least-squares systems, such as CG on normal equations
(CGLS) or LSQR, also act as regularizers when stopped early.

Typical behavior:

1. Early iterations reconstruct dominant large-`σ` components.
2. Later iterations reach smaller-`σ` components and begin fitting noise.
3. The solution error decreases, reaches a minimum, then increases: this is
   semi-convergence.

Therefore the iteration count `m` is itself a regularization parameter. In large
MoM or tomography problems where a full SVD is impossible, prefer LSQR/CGLS with
a discrepancy stop, cross-validation, or L-curve monitoring.

## Choosing α or the Iteration Count

### Morozov Discrepancy Principle

If the data noise norm is known or estimated as `δ`, choose `α` or stop the
iteration when

```
||K u_α − f^δ|| ≈ τ δ,     τ ≈ 1 to 1.5.
```

Do not drive the residual far below `δ`; doing so fits noise. If the residual is
far above `δ`, the solution is over-regularized or the forward model is wrong.

### L-Curve

When `δ` is unknown, plot

```
x(α) = log ||K u_α − f^δ||,
y(α) = log ||L u_α||        or log ||u_α||.
```

Choose the corner of the L-curve: the point of largest curvature where residual
reduction begins to require a disproportionate increase in solution norm. For
iterative methods, plot the same curve versus iteration number.

L-curve is useful diagnostically, but it can be ambiguous for smooth spectra,
correlated noise, or model error. Morozov is preferred when a trustworthy `δ` is
available.

## Jones Insight: Singular Kernels Can Help Conditioning

In radiation and scattering integral equations, “singular kernel” does not always
mean “worse numerics.” Jones emphasized that, for certain radiation problems,
more singular kernels can improve first-kind conditioning because the operator is
less smoothing: it preserves more local information about the source. A very
smooth kernel strongly damps high spatial frequencies, causing rapid singular
value decay; a kernel with physical near-field singularity may retain near-source
information and slow the decay of `σ_n`.

Practical implication: do not automatically regularize away or oversmooth the
kernel singularity in MoM radiation formulations. Treat singular quadrature
accurately. Replacing a physically singular kernel by an overly smoothed kernel
can make the inverse problem more ill-conditioned, even if the matrix looks more
benign locally.

## Concrete Algorithm — Noisy Ku=f

```
INPUT:
    K        forward operator or matrix from discretized first-kind equation
    fδ       measured data
    δ        estimate of ||noise|| in the same norm as residual
    L        optional regularization operator; default L = I
    method   "svd" for small/medium dense problems, "iterative" for large ones

1. SCALE / WHITEN
    If data errors have covariance Cη, solve with weighted residual
        ||Cη^{-1/2}(K u − fδ)||.
    Otherwise scale rows/columns so residual components have comparable units.

2. DIAGNOSE ILL-POSEDNESS
    If feasible, compute singular values σ_n of K or of weighted K.
    Look for σ_n → 0 and a Picard plot: |u_n^* fδ| should decay faster than σ_n
    for stable inversion; flattening indicates the noise floor.

3A. SVD / TIKHONOV PATH
    For candidate α values:
        u_α = (K^*K + α² L^*L)^{-1} K^* fδ
        r_α = ||K u_α − fδ||
        s_α = ||L u_α||
    If L = I and SVD is available, apply filter factors
        φ_n = σ_n²/(σ_n²+α²).

3B. ITERATIVE PATH
    Run LSQR/CGLS on min ||K u − fδ||.
    At iteration m:
        compute r_m = ||K u_m − fδ||
        store s_m = ||L u_m|| or ||u_m||
    Stop before semi-convergence, not at machine residual.

4. CHOOSE REGULARIZATION
    If δ is known:
        choose α or m such that r ≈ τ δ, with τ≈1–1.5.
    If δ is unknown:
        choose the L-curve corner in (log r, log s), or use validation data.

5. VERIFY
    Confirm ||K u − fδ|| ≈ δ.
    Inspect u for physical plausibility: support, smoothness, sign/positivity,
    conservation laws, boundary conditions, and absence of grid-scale ringing.
    Perturb fδ by plausible noise and verify u is stable at the chosen α/m.

OUTPUT:
    regularized solution u, chosen α or iteration m, residual norm, diagnostic plot/data
```

## Cross-Domain Use Cases

| Domain | K maps | Ill-posed symptom | Regularization cue |
|--------|--------|-------------------|--------------------|
| EM inverse scattering | currents/contrast → fields | evanescent and multiple-scattering information lost | Tikhonov, total variation, truncated SVD, distorted Born iterations |
| Antenna synthesis | aperture/current distribution → far-field pattern | many current distributions produce nearly same pattern | minimum-norm or smooth current; stop when pattern error ≈ measurement error |
| CT/MRI | attenuation/spin density → projections/k-space samples | incomplete angles, limited bandwidth, noise | filtered/penalized reconstruction; discrepancy or validation stopping |
| Seismic tomography | velocity/slowness perturbation → travel times/waveforms | poor ray coverage, null spaces | damping + smoothing; L-curve or resolution tests |
| Atmospheric retrievals | temperature/composition profile → radiances | vertical smoothing kernels, correlated instrument noise | optimal estimation/Tikhonov with covariance-weighted residual |

## MoM Connection

The Method of Moments often produces second-kind equations for well-posed forward
scattering, but inverse source, inverse radiation, and many synthesis problems are
first-kind or effectively compact. Refining the mesh can expose smaller singular
values rather than improve the inverse. The right question is not only “is the
linear system solved?” but “which singular subspace is supported by the data?”

For radiation problems, preserve accurate singular-kernel physics during matrix
fill, then regularize the inverse solve. Kernel smoothing is not a substitute for
regularization.

## Edge Cases

- **Wrong δ**: Underestimated noise causes overfitting; overestimated noise causes
  oversmoothing. Check residual statistics, not just residual norm.
- **Model error**: If `min_u ||Ku−fδ|| >> δ`, the forward model, calibration, or
  boundary conditions are inconsistent with the data.
- **Correlated noise**: Use covariance weighting; otherwise Morozov can choose a
  misleading α.
- **Nonlinear inverse problems**: Apply the same ideas to each linearized step,
  but include trust-region or line-search control.
- **Null spaces**: Regularization selects one solution among many; ensure the
  selected null-space component is physically meaningful.

## Cross-References

- computational-physics: reasoning.cp.moment_method (parent — discretizes integral equations into Ku=f or Zα=V)
- computational-physics: reasoning.cp.multigrid_solver (iterative solvers and stopping for large systems)
- Harrington, *Field Computation by Moment Methods* — integral-equation discretization context
- Hansen, *Rank-Deficient and Discrete Ill-Posed Problems* — SVD filters, L-curve, semi-convergence
- Tikhonov & Arsenin, *Solutions of Ill-Posed Problems* — classical regularization
