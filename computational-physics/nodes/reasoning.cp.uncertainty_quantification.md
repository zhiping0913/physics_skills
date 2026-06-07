---
skill_id: reasoning.cp.uncertainty_quantification
type: reasoning
summary_50t: >
  4-step UQ framework: input UQ → uncertainty propagation → output UQ →
  sensitivity analysis. Three methods: MC (∝1/√N, dimension-robust),
  gPCE (Galerkin intrusive, best in multidim), stochastic collocation
  (non-intrusive, curse of dimensionality). Wiener-Askey: Gaussian→Hermite,
  Uniform→Legendre, Beta→Jacobi, Gamma→Laguerre. Galerkin-on-probability-space
  cross-template: same variational principle in 5+ Hilbert spaces.
trigger:
  - quantifying how input parameter uncertainty affects CEM simulation outputs
  - computing statistical moments and PDFs of EM quantities of interest
  - performing global sensitivity analysis for EM design/optimization
reasoning_role: uncertainty_quantification_cem
parent: reasoning.cp.galerkin_rayleigh_ritz
retrieval_cost: 1
---

# reasoning.cp.uncertainty_quantification — Input PDF → Propagation → Output Statistics → Sensitivity

## Core Picture

Uncertainty Quantification in CEM answers: given uncertain input parameters
(geometry, material properties, excitation) with known probability
distributions, what are the statistical properties of the outputs (S-parameters,
field values, resonance frequencies, RCS)? The fundamental insight: UQ via
generalized Polynomial Chaos Expansion (gPCE) is Galerkin projection in
**probability Hilbert space** — the same variational template that unifies
FEM, MoM, and modal expansion in physical Hilbert space.

## Derivation Sketch

From `computational-physics: reasoning.cp.galerkin_rayleigh_ritz` (abstract
Galerkin in any Hilbert space) and the Wiener-Askey polynomial chaos framework
(Xiu & Karniadakis 2002):

### 1. Four-step UQ framework (Poljak §9.1)

```
Step 1: UQ OF INPUTS — assign PDFs to uncertain parameters X = (X₁,...,X_d)
Step 2: UNCERTAINTY PROPAGATION — map input uncertainty to output via model M
Step 3: OUTPUT UQ — compute moments, PDF, confidence intervals of Y = M(X)
Step 4: SENSITIVITY ANALYSIS — rank input importance via Sobol indices
```

### 2. Three propagation approaches

| Method | Formula | Pros | Cons |
|--------|---------|------|------|
| Monte Carlo (MC) | μ̂ = (1/N) Σ Y^(n), convergence ∝ 1/√N | Dimension-robust, trivial to implement, embarrassingly parallel | Slow convergence, N = O(10⁶) for 1% error |
| Stochastic Collocation (SC) | Ŷ(ξ) = Σ L_i(ξ) Y^(i), moments = Σ Y^(i) w_i | Non-intrusive (black-box solver), reuses deterministic code | Curse of dimensionality: N^d nodes for tensor grid |
| gPCE (intrusive Galerkin) | Y ≈ Σ c_α ψ_α(ξ), solve for c_α via Galerkin projection | Best in multidim (spectral convergence), analytic moments | Intrusive — requires modifying solver code |

### 3. Wiener-Askey gPCE scheme

The generalized Polynomial Chaos expands the random output in orthogonal
polynomials of the input random variables:
```
Y(X) ≈ Σ_{|α|≤P} c_α ψ_α(ξ)
```
where ξ = (ξ₁,...,ξ_d) are independent standardized random variables, ψ_α
are multivariate orthogonal polynomials, and α is a multi-index.

**Wiener-Askey correspondence** (Poljak §9.2.3):

| Input ξ PDF | Polynomial Family | Orthogonality Weight |
|-------------|-------------------|---------------------|
| Gaussian N(0,1) | Hermite He_n(ξ) | e^{-ξ²/2} |
| Uniform U(-1,1) | Legendre P_n(ξ) | 1 |
| Beta B(α,β) | Jacobi P_n^{(α,β)}(ξ) | (1−ξ)^α(1+ξ)^β |
| Gamma Γ(k,θ) | Laguerre L_n^{(k-1)}(ξ) | ξ^{k-1}e^{-ξ} |
| Poisson Po(λ) | Charlier C_n(ξ;λ) | discrete |

**Orthogonality**: ⟨ψ_α, ψ_β⟩_p = ∫ ψ_α(ξ) ψ_β(ξ) p(ξ) dξ = γ_α δ_{αβ}

### 4. Galerkin projection in probability space

This is the key cross-template insight. For a linear operator L (e.g.,
Maxwell operator with random parameters):
```
L(ξ) u(ξ) = f(ξ)
```
Expand u ≈ Σ c_α ψ_α(ξ). Galerkin projection:
```
⟨ψ_β, L Σ c_α ψ_α⟩_p = ⟨ψ_β, f⟩_p
```
This yields a coupled deterministic system for {c_α}:
```
Σ_α ⟨ψ_β, L ψ_α⟩_p c_α = ⟨ψ_β, f⟩_p
```
**Same structure as FEM/MoM**: A c = b where A_{βα} = ⟨ψ_β, L ψ_α⟩_p.
The only difference is the inner product domain — probability space instead
of physical space.

**Coefficient computation** (three methods):
- **Galerkin projection** (intrusive): c_α = ⟨Y, ψ_α⟩_p / γ_α — requires
  modifying solver
- **Regression** (non-intrusive): least-squares fit to N_s simulation outputs
- **Pseudo-spectral collocation**: evaluate Y at quadrature nodes, compute
  c_α via quadrature

### 5. Analytic moments from PCE coefficients

Once the PCE coefficients {c_α} are known, all statistical moments follow
analytically — no additional sampling needed:
```
μ_Y = c_0                                           (mean)
σ²_Y = Σ_{|α|>0} c_α² γ_α                           (variance)
Skew = (1/σ³) Σ_{α,β,γ} c_α c_β c_γ ⟨ψ_α ψ_β ψ_γ⟩  (skewness)
```

### 6. Sensitivity analysis — Sobol indices from PCE

The **first-order Sobol index** quantifies the fraction of output variance
due to input X_i alone:
```
S_i = Var[E[Y|X_i]] / Var(Y)
```
From PCE coefficients, this is computed analytically (Poljak §9.3):
```
S_i = (Σ_{α: α_i≠0, α_j=0 for all j≠i} c_α² γ_α) / σ²_Y
```
The **total-order Sobol index** includes all interaction effects involving X_i:
```
S_T,i = 1 − Var[E[Y|X_{~i}]] / Var(Y)
      = (Σ_{α: α_i≠0} c_α² γ_α) / σ²_Y
```
**No additional MC sampling needed** — the PCE coefficients carry all
sensitivity information.

### 7. Curse of dimensionality and Smolyak sparse grids

Tensor-product quadrature requires N^d nodes — exponential in d.
Smolyak sparse grids reduce this to approximately N · log(N)^{d-1}:
```
Nodes: A(q,d) = ∪_{q−d+1 ≤ |i| ≤ q} (U^{i₁} × ... × U^{i_d})
```
For stochastic collocation: Smolyak grids enable up to d ≈ 10-20 dimensions.

## Hilbert-Space Unification (Highest-Value Cross-Template)

The Galerkin/Rayleigh-Ritz template specializes to 5+ Hilbert spaces:

| Hilbert Space | Galerkin Specialization | Node / Method |
|--------------|------------------------|---------------|
| **Physical 3D space** | FEM, MoM, modal expansion | `galerkin_rayleigh_ritz`, FEM, MoM |
| **Probability space** | PCE, stochastic collocation | **This node (UQ)** |
| **Time domain** | TDIE / MOT | `moment_method` §TD extension |
| **Fock space** | Quantum chemistry CI / coupled-cluster | Future skill |
| **Function space** | Optimal control variational | Future skill |

The basis functions change (Nédélec edge elements → Hermite polynomials →
time-domain basis → Slater determinants → control functions) but the
Galerkin projection algorithm — choose basis, project residual onto test
space, solve linear system — is **identical**. This is the deepest structural
unification across the entire physics skill graph.

## Algorithm — Given Solver → UQ Analysis

```
1. IDENTIFY uncertain inputs X = (X₁,...,X_d) and their joint PDF.
   If independent, factor p(X) = Π p_i(X_i).

2. CHOOSE METHOD based on dimension d and intrusiveness tolerance:
   - d ≤ 5: gPCE (spectral convergence, analytic moments)
   - 5 < d ≤ 20: Smolyak sparse-grid SC (non-intrusive, d-dimensional)
   - d > 20: MC or quasi-MC (Sobol sequences)

3. IF gPCE: select polynomial family via Wiener-Askey correspondence.
   Truncate to total order P: |α| = α₁+...+α_d ≤ P.
   Number of terms: K = (P+d)!/(P! d!).

4. COMPUTE COEFFICIENTS:
   - Intrusive: assemble A_{βα} = ⟨ψ_β, L ψ_α⟩_p, solve for c_α.
   - Non-intrusive: run solver at N quadrature nodes, least-squares fit c_α.

5. EXTRACT STATISTICS:
   μ = c₀, σ² = Σ c_α² γ_α, PDF via kernel density or sampling from PCE.

6. SOBOL SENSITIVITY:
   S_i = Σ_{only α_i≠0} c_α² γ_α / σ²_Y
   S_T,i = Σ_{α_i≠0} c_α² γ_α / σ²_Y

7. VALIDATE: compare PCE moments with Monte Carlo reference for a few
   parameter values. Check σ² convergence with P.
```

## Edge Cases

- **Gaussian inputs, non-Gaussian outputs**: gPCE converges spectrally
  regardless of output distribution — no Gaussian output assumption.
- **Correlated inputs**: Nataf or Rosenblatt transformation maps correlated
  inputs to independent standard variables before PCE.
- **Discontinuous outputs (bistability, bifurcation)**: global polynomial
  basis struggles. Use multi-element gPCE (ME-gPCE) — domain decomposition
  in probability space.
- **High-dimensional with low effective dimension**: Use ANOVA decomposition
  or active subspace methods to identify the important dimensions first.
- **Intrusive gPCE for Maxwell**: the coupled deterministic system is a
  tensor-product of spatial and stochastic DOFs — use block iterative solvers.

## Connection to Statistical EM

`reasoning.em.statistical_em_cavity` and this node both handle random EM
fields but from different angles:
- **UQ**: forward UQ of output given uncertain input parameters (parametric).
- **Statistical EM**: ensemble of realizations from mode stirring (intrinsic).
- **Ergodic connection**: for a stationary stirred chamber, time-average of
  reverberant field = spatial-average of UQ ensemble → same statistics
  emerge from different sources of randomness.

## Cross-References

- Poljak, D., Šušnjara, A., *Deterministic and Stochastic CEM Modeling* (2023) Ch.7, 9
- Xiu, D., Karniadakis, G.E., "The Wiener-Askey polynomial chaos for
  stochastic differential equations" SIAM J. Sci. Comput. 24:619 (2002)
- Le Maître, O.P., Knio, O.M., *Spectral Methods for Uncertainty
  Quantification* (2010) — comprehensive monograph
- Saltelli, A., et al., *Global Sensitivity Analysis: The Primer* (2008)
- computational-physics: reasoning.cp.galerkin_rayleigh_ritz (parent —
  UQ = probability-space specialization)
- electrodynamics: reasoning.em.statistical_em_cavity (sister — both random EM)
- computational-physics: reasoning.cp.regularization_ill_posed (Bayesian
  inverse problems → UQ on posterior)
