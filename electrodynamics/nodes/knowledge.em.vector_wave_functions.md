---
node_type: knowledge
domain: electrodynamics
topic: vector_wave_functions
tags: [Hansen vectors, TE, TM, vector spherical harmonics, Mie theory, Green's function, wave functions]
citations:
  - "Stratton, J.A., Electromagnetic Theory, §§7.1, 7.11"
  - "Chew, W.C., Waves and Fields in Inhomogeneous Media, §§7.2–7.3"
  - "Hansen, W.W., 'A New Type of Expansion in Radiation Problems,' Phys. Rev., 47:139–143, 1935"
---

# Hansen Vector Wave Functions

## The Three Hansen Vectors

Given a scalar Helmholtz solution \(\psi\) (satisfying \(\nabla^2\psi + k^2\psi = 0\)) and a
constant "pilot vector" \(\mathbf{a}\), the three independent vector wave functions are:

\[
\begin{aligned}
\mathbf{L} &= \nabla\psi
&&\text{(Longitudinal / irrotational)}
\\[4pt]
\mathbf{M} &= \nabla \times (\mathbf{a}\psi)
&&\text{(TE — transverse electric)}
\\[4pt]
\mathbf{N} &= \frac{1}{k}\,\nabla \times \mathbf{M}
&&\text{(TM — transverse magnetic)}
\end{aligned}
\]

## Action of \(\nabla\times\nabla\times\)

These vectors form an eigen-system under the double-curl operator:

\[
\begin{aligned}
\nabla \times \nabla \times \mathbf{L} &= 0
&&\text{(L is irrotational)}
\\[4pt]
\nabla \times \nabla \times \mathbf{M} &= k^2 \mathbf{M}
&&\text{(M is solenoidal TE)}
\\[4pt]
\nabla \times \nabla \times \mathbf{N} &= k^2 \mathbf{N}
&&\text{(N is solenoidal TM)}
\end{aligned}
\]

Also: \(\nabla\cdot\mathbf{M} = 0\), \(\nabla\cdot\mathbf{N} = 0\), \(\nabla\times\mathbf{L} = 0\).

These properties make \(\{\mathbf{L}, \mathbf{M}, \mathbf{N}\}\) a complete basis for
representing any vector field satisfying the vector Helmholtz equation.

## Explicit Forms by Coordinate System

### Cartesian (\(a = \hat{z}\))

\[
\begin{aligned}
\psi_{mn} &= e^{i(k_x x + k_y y \pm k_z z)},
\quad k_z = \sqrt{k^2 - k_x^2 - k_y^2}
\\[4pt]
\mathbf{M} &= \nabla \times (\hat{z}\psi) = (ik_y, -ik_x, 0)\,\psi
\\[4pt]
\mathbf{N} &= \frac{1}{k}\nabla \times \mathbf{M}
= \frac{1}{k}(\pm i k_x k_z,\; \pm i k_y k_z,\; k_x^2 + k_y^2)\,\psi
\end{aligned}
\]

M and N give TE and TM plane-wave decompositions.

### Cylindrical (\(a = \hat{z}\), \(\psi = Z_n(k_\rho\rho) e^{i n\phi} e^{i k_z z}\))

\[
\begin{aligned}
\mathbf{M} &= \nabla \times (\hat{z}\psi)
= \left(\frac{i n}{\rho}Z_n,\; -\frac{\partial Z_n}{\partial\rho},\; 0\right) e^{i n\phi} e^{i k_z z}
\\[4pt]
\mathbf{N} &= \frac{1}{k}\nabla \times \mathbf{M}
= \frac{1}{k}\left(
i k_z\frac{\partial Z_n}{\partial\rho},\;
-\frac{n k_z}{\rho}Z_n,\;
k_\rho^2 Z_n
\right) e^{i n\phi} e^{i k_z z}
\end{aligned}
\]

Used in waveguide and fiber mode analysis.

### Spherical (\(a = \mathbf{r}\), radial pilot vector)

With \(\psi_{nm} = z_n(kr) P_n^m(\cos\theta) e^{i m\phi}\) where \(z_n\) is a spherical Bessel function:

\[
\begin{aligned}
\mathbf{M}_{nm} &= \nabla \times (\mathbf{r}\psi_{nm})
= z_n(kr)\,\left(
0,\;
\frac{im}{\sin\theta}P_n^m,\;
-\frac{\partial P_n^m}{\partial\theta}
\right) e^{i m\phi}
\\[4pt]
\mathbf{N}_{nm} &= \frac{1}{k}\nabla \times \mathbf{M}_{nm}
\end{aligned}
\]

These are the **vector spherical harmonics**, the foundation of Mie theory. The radial
components are:

\[
\begin{aligned}
\hat{r}\cdot\mathbf{M}_{nm} &= 0
\quad\text{(M is purely transverse to }\hat{r}\text{)}
\\[4pt]
\hat{r}\cdot\mathbf{N}_{nm} &= \frac{n(n+1)}{kr}z_n(kr) P_n^m(\cos\theta) e^{i m\phi}
\end{aligned}
\]

## Why \(\mathbf{L}\) Matters

Though \(\mathbf{L} = \nabla\psi\) is irrotational and does not represent propagating
waves in free space, it is **essential** for:

1. **Singular term in \(\bar{\bar{G}}\).** The dyadic Green's function expansion in
   eigenfunctions requires all three vector wave functions. The \(\mathbf{L}\mathbf{L}\)
   dyadic provides the longitudinal (non-solenoidal) part that captures the delta-function
   singularity at the source.

2. **Completeness.** Any vector field can be decomposed into solenoidal (M, N) and
   irrotational (L) parts via Helmholtz decomposition. In source regions, L is
   indispensable.

3. **Source representation.** When expanding current sources \(\mathbf{J}\), the L
   component handles \(\nabla\cdot\mathbf{J} \neq 0\) (non-solenoidal sources).

## Cross-Domain Connections

| Domain | Use of Hansen Vectors |
|---|---|
| **Mie theory** | Partial-wave expansion of scattered field: \(\mathbf{E}_s = \sum_n (a_n \mathbf{N}_n + b_n \mathbf{M}_n)\). M gives TE (no radial E), N gives TM (no radial H). |
| **TE/TM mode decomposition** | In waveguides and cavities, M ≡ TE modes (\(E_z = 0\)), N ≡ TM modes (\(H_z = 0\)). |
| **Dyadic Green's function** | \(\bar{\bar{G}}(\mathbf{r},\mathbf{r}') = \sum_\lambda \frac{\mathbf{M}_\lambda\mathbf{M}_\lambda + \mathbf{N}_\lambda\mathbf{N}_\lambda + \mathbf{L}_\lambda\mathbf{L}_\lambda}{k_\lambda^2 - k^2}\) — the eigenfunction expansion uses all three. |
| **Antenna radiation** | Spherical M and N functions expand the fields of any antenna in its far field and near field. |
| **Multiple scattering** | Translation-addition theorems for vector spherical harmonics use M and N. |
| **Computational EM** | FEM/MoM basis functions often built from M, N for divergence-free subspaces. |

## Historical Note

Hansen (1935) introduced these vectors while developing a systematic expansion for
electromagnetic radiation problems. Stratton (1941) popularized them in his textbook,
establishing the notation \(\mathbf{L}, \mathbf{M}, \mathbf{N}\) still used today.
Independently, the spherical versions are often called "vector spherical harmonics"
or "vector spherical wave functions" in the physics literature.

## Hilbert-Space Cross-Template

The Hansen triad {L, M, N} is the **physical-space orthogonal basis** for
vector Helmholtz fields. The same orthogonal-expansion Hilbert-space
template appears in:

| Hilbert Space | Orthogonal Basis | Inner Product | Application Node |
|--------------|-----------------|---------------|------------------|
| Physical 3D space | L, M, N (Hansen vectors) | ∫ E·E'* dV | `dyadic_green_function`, this node |
| Probability space | ψ_α(ξ) (Wiener-Askey polynomials) | ∫ ψ_α ψ_β p(ξ) dξ | `reasoning.cp.uncertainty_quantification` |
| Time domain | T_j(t) (temporal basis) | ∫ f(t) g(t) dt | `moment_method` §TD extension |
| Fock space | Slater determinants | ⟨Ψ|O|Ψ'⟩ | Quantum chemistry CI (future) |

In each case: expand unknown in orthogonal basis → project residual onto test
basis → solve linear system for coefficients. The only change is which Hilbert
space hosts the inner product.

## Key Takeaways

1. \(\mathbf{L}, \mathbf{M}, \mathbf{N}\) form a complete basis for the vector Helmholtz
   equation: L = irrotational, M = TE (solenoidal), N = TM (solenoidal).
2. M and N are eigenvectors of \(\nabla\times\nabla\times\) with eigenvalue \(k^2\);
   L is in the nullspace.
3. L is indispensable for the singular (source-region) term in the dyadic Green's function.
4. The spherical form gives the vector spherical harmonics — the mathematical engine
   behind Mie scattering and all spherical near/far-field expansions.
5. The choice of pilot vector \(\mathbf{a}\) determines the coordinate system and the
   physical interpretation (TE/TM with respect to a preferred direction).
