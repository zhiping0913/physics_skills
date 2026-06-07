---
skill_id: reasoning.em.t_matrix
type: reasoning
summary_50t: >
  T-matrix/Waterman scattering maps regular incident vector spherical wave
  coefficients a to outgoing scattered coefficients b: b = T a. Boundary
  conditions determine T once for a target, reusable for arbitrary illumination.
  Sphere limit is diagonal Mie theory; rotations use Wigner D matrices.
trigger:
  - scattering by a nonspherical finite object
  - reusing one scatterer solution for many incident beams or orientations
  - computing cross sections from vector spherical wave coefficients
reasoning_role: multipole_scattering_operator
parent: knowledge.em.vector_wave_functions
retrieval_cost: 1
sign_convention: time-harmonic e^{-iωt}; outgoing waves use spherical Hankel h_l^(1)
---

# reasoning.em.t_matrix — Incident Multipoles → Scattered Multipoles

## Core Picture

The T-matrix (extended boundary condition / Waterman method) is the linear
operator that turns an incident-field multipole expansion into the scattered
multipole expansion of the same object.

Use regular vector spherical wave functions (VSWFs) for the incident field and
outgoing VSWFs for the scattered field:

```
E_inc(r)  = Σ_n a_n Ψ_n^reg(k r)        regular at the origin, radial j_l(kr)
E_scat(r) = Σ_n b_n Ψ_n^out(k r)        outgoing at infinity, radial h_l^(1)(kr)

b = T a
```

Here n abbreviates the polarization/parity plus angular indices, for example
n = (p,l,m) with p = magnetic/electric or TE/TM. Maxwell boundary conditions on
the scatterer surface determine T. Once T is computed at a frequency and material
state, it can be reused for arbitrary incident beams by only changing a.

## Derivation Sketch

Starting from `knowledge.em.vector_wave_functions`, expand all source-free fields
outside the circumscribing sphere in VSWFs. Linearity of Maxwell's equations and
boundary conditions implies a linear map from incident coefficients to scattered
coefficients.

For a trial incident basis vector a = e_j:

```
1. E_inc = Ψ_j^reg.
2. Solve boundary conditions on the actual scatterer surface S.
3. Project the resulting outgoing field onto Ψ_i^out.
4. The projected coefficients form column j of T: T_ij = b_i.
```

Repeating for every retained incident multipole gives the truncated matrix T.
The Waterman/EBCM implementation avoids volume meshing: it uses surface integral
relations on S and the equivalence principle to assemble matrices connecting
regular and outgoing spherical-wave coefficients.

## Properties and Diagnostics

### 1. Reciprocity

For reciprocal materials (ε and μ symmetric tensors, no magneto-optic bias),
Lorentz reciprocity imposes a symmetry relation on T. In a real reciprocal VSWF
basis this is simply

```
T = T^T.
```

In the more common complex spherical basis, the same statement includes the
m ↔ −m partner transformation:

```
T_{p l m, p' l' m'} = (-1)^{m+m'} T_{p' l' -m', p l -m}
```

up to the phase and normalization convention used for the VSWFs. A violation is
a useful sign-convention, surface-normal, or material-model diagnostic.

### 2. Losslessness, unitarity, and optical theorem

For a passive lossless scatterer the full partial-wave S-matrix is unitary. With
one common convention S = I + 2T,

```
S† S = I    ⇒    T + T† + 2 T†T = 0.
```

Other phase conventions replace this by the equivalent anti-Hermitian-part
constraint for S = I + 2iT. Physically the constraint says that extinction equals
scattered power: no absorption channel is available.

For the common Mie-coefficient normalization this reduces mode-by-mode to

```
Re(t_n) = |t_n|^2        lossless single channel
Re(t_n) ≥ |t_n|^2        passive channel with possible absorption
```

and the equality is the multipole form of the optical theorem.

### 3. Rotation by Wigner D matrices

If T is known in the body frame of a particle, the laboratory-frame T for an
orientation R is obtained without recomputing surface integrals:

```
T_lab(R) = D(R) T_body D(R)^{-1}      (= D T_body D† for unitary D)
```

where D is block diagonal in l and polarization, with entries D^l_{m m'}(R).
This is the key computational advantage for orientation averaging and multiple
incident directions.

### 4. Sphere limit: Mie scattering

For a homogeneous isotropic sphere, spherical symmetry prevents mixing of l, m,
and polarization. The T-matrix is diagonal:

```
T_{p l m, p' l' m'} = δ_pp' δ_ll' δ_mm' t_{p l}
```

The two diagonal entries t_{electric,l} and t_{magnetic,l} are the standard Mie
coefficients (up to the chosen sign convention). Thus Mie theory is the diagonal,
maximally symmetric special case of the T-matrix method.

## Practical Algorithm

```
Input: wavelength/frequency k, material tensors, scatterer surface S,
       circumscribing radius a, incident expansion coefficients a_n.

1. Choose VSWF truncation.
   Size parameter x = k a. A common starting rule is
       L_max ≈ x + 4 x^(1/3)
   then increase L_max until cross sections and energy-balance checks converge.

2. Build the basis.
   Retain n = (p,l,m), with 1 ≤ l ≤ L_max and -l ≤ m ≤ l.
   Use regular waves for incident/internal expansions and outgoing waves for
   scattered fields.

3. Assemble Waterman/EBCM surface matrices.
   Evaluate surface integrals over S involving tangential traces of VSWFs and
   their curls. These matrices encode boundary continuity of tangential E and H
   (or PEC tangential E = 0).

4. Solve for T columns.
   For each incident basis vector, solve the linear system from the boundary
   conditions and store the outgoing coefficients as one column of T.
   Equivalently solve the matrix equation for all columns at once.

5. Reuse T.
   For any incident beam, compute its regular VSWF coefficients a and evaluate
       b = T a.
   For a rotated particle use T_lab(R) = D(R) T_body D(R)^{-1}.

6. Compute observables.
   Convert b to far-field amplitudes and integrate to get differential and total
   scattering. In a power-normalized basis,
       C_scat ∝ Σ_n |b_n|^2 / incident_flux,
       C_ext  is fixed by the forward interference term a†T a.
   For lossless targets verify C_ext = C_scat; for passive lossy targets verify
   C_ext ≥ C_scat.
```

## When to Use

- Many illuminations or orientations of the same particle: compute T once, reuse.
- Nonspherical but compact scatterers: spheroids, cylinders, aggregates,
  rough particles, coated particles.
- Multiple scattering: each particle has a T-matrix; translation-addition
  theorems move VSWF coefficients between particle centers.

## Failure Modes / Checks

- L_max too small: cross sections and near fields fail to converge.
- Bad origin/circumscribing radius: expansions converge slowly or not at all.
- Highly elongated, concave, or touching objects: surface-integral matrices can
  become ill-conditioned; extended precision or alternative solvers may be needed.
- Nonreciprocal media: do not enforce reciprocal symmetry.
- Absorbing media: S is not unitary; optical theorem becomes C_ext = C_scat +
  C_abs with C_abs ≥ 0.

## Cross-References

- electrodynamics: knowledge.em.vector_wave_functions (regular/outgoing VSWFs)
- electrodynamics: reasoning.em.scattering_cross_section (cross sections and
  optical theorem)
- electrodynamics: knowledge.em.born_approximation_scattering (weak-scattering
  alternative)
- Waterman, P.C., "Matrix formulation of electromagnetic scattering," Proc. IEEE
  53, 805-812 (1965)
- Mishchenko, Travis & Lacis, *Scattering, Absorption, and Emission of Light by
  Small Particles* (T-matrix implementation details)
