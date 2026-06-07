---
node_type: knowledge
domain: mathematics-theorems
topic: depolarization_dyadic
tags: [depolarization, dyadic, ellipsoid, dielectric, singularity, Clausius-Mossotti, plasma]
citations:
  - "Stratton, J.A., Electromagnetic Theory, §§3.27–3.28"
  - "Chew, W.C., Waves and Fields in Inhomogeneous Media, §7.1.2"
  - "Yaghjian, A.D., 'Electric dyadic Green's functions in the source region,' Proc. IEEE, 68(2):248–263, 1980"
---

# Ellipsoid Depolarization Dyadic

## Definition

For a homogeneous ellipsoid with semi-axes \(a, b, c\) aligned along coordinate directions
\(\hat{x}_1, \hat{x}_2, \hat{x}_3\), the depolarization dyadic \(\bar{\bar{L}}\) is diagonal:

\[
\bar{\bar{L}} = L_1 \hat{x}_1\hat{x}_1 + L_2 \hat{x}_2\hat{x}_2 + L_3 \hat{x}_3\hat{x}_3
\]

## Integral Formula

Each principal value \(L_i\) is given by the elliptic integral:

\[
L_i = \frac{abc}{2} \int_0^\infty \frac{ds}{(x_i^2 + s)\, R(s)},
\qquad
R(s) = \sqrt{(a^2 + s)(b^2 + s)(c^2 + s)}
\]

with \(x_1 = a\), \(x_2 = b\), \(x_3 = c\).

## Sum Rule

The depolarization factors always sum to unity:

\[
L_1 + L_2 + L_3 = 1
\]

This follows from \(\nabla \cdot \bar{\bar{G}}_0 \propto \bar{\bar{L}}\) and the trace of the
singular term in the dyadic Green's function.

## Special Cases

| Geometry | Axes | Depolarization Dyadic |
|---|---|---|
| Sphere | \(a = b = c\) | \(\bar{\bar{L}} = \frac{1}{3}\bar{\bar{I}}\) |
| Thin disk (⊥ \(\hat{z}\)) | \(a = b \gg c\) | \(\bar{\bar{L}} \approx \hat{z}\hat{z}\) |
| Thin needle (∥ \(\hat{z}\)) | \(a \ll b = c\) | \(\bar{\bar{L}} \approx \frac{1}{2}(\hat{x}\hat{x} + \hat{y}\hat{y})\) |
| Prolate spheroid | \(a > b = c\) | \(L_1 = (1-e^2)/e^2 \, [\tfrac{1}{2e}\ln\frac{1+e}{1-e} - 1]\) |
| Oblate spheroid | \(a = b > c\) | \(L_3 = (1+e^2)/e^3\,(e - \arctan e)\) |

where \(e\) is eccentricity: prolate \(e = \sqrt{1 - b^2/a^2}\), oblate \(e = \sqrt{a^2/c^2 - 1}\).

## Cross-Domain Connections

| Domain | Role of \(\bar{\bar{L}}\) |
|---|---|
| **Dielectric ellipsoid** | Internal field: \(\mathbf{E}_{\text{in}} = \mathbf{E}_0 - \bar{\bar{L}}\cdot\mathbf{P}/\varepsilon_0\) — gives polarizability tensor |
| **Dyadic Green's function \(\bar{\bar{G}}\)** | Singular source-region term: \(\bar{\bar{G}}_{\text{sing}} \propto \bar{\bar{L}}\,\delta(\mathbf{r})\) — the depolarization dyadic governs the principal-volume exclusion shape |
| **Clausius–Mossotti relation** | Generalized for ellipsoids: \(\alpha = V\varepsilon_0(\varepsilon_r - 1)[\bar{\bar{I}} + \bar{\bar{L}}(\varepsilon_r - 1)]^{-1}\) — reduces to sphere \(\bar{\bar{L}} = \bar{\bar{I}}/3\) |
| **Plasma / anisotropic media** | Magnetized plasma permittivity tensor leads to Fresnel surfaces that are ellipsoids — depolarization factors determine resonance cones and wave-normal surfaces |
| **Effective medium theory** | Maxwell Garnett and Bruggeman mixing rules use \(\bar{\bar{L}}\) for ellipsoidal inclusions |
| **Electrostatics** | Polarizability of conducting ellipsoid: \(\alpha_i = 4\pi\varepsilon_0 V / L_i\) |

## Principal-Volume Dependence

The singular term in \(\bar{\bar{G}}\) depends on the shape of the infinitesimal exclusion volume.
Only for ellipsoidal principal volumes (and their degenerate limits: sphere, disk, needle) does
the dyadic take the simple diagonal form \(\bar{\bar{L}}\). Yaghjian (1980) showed that for
arbitrary exclusion shapes, the depolarization dyadic is generally non-diagonal and
shape-dependent.

## Key Takeaways

1. \(\bar{\bar{L}}\) is shape-dependent and diagonal only for ellipsoidal geometries.
2. The three depolarization factors sum to 1 — a consequence of the trace of the singular
   Green's dyadic.
3. \(\bar{\bar{L}}\) connects electrostatics (polarizability), electrodynamics (Green's
   function singularity), and effective medium theory.
4. Sphere/large-disk/long-needle limits are analytically simple and widely used in
   homogenization and scattering problems.
