---
skill_id: knowledge.optics.nonspherical_scattering
type: knowledge
summary_50t: >
  T-matrix: expand incident+scattered in VSWF→T=transition matrix. Spheroid:
  prol/obl, a/b ratio←scattering. Cylinder: Mie-type with Bessel/Hankel.
  RDG: P(q)=|∫e^{iq·r}dV|². Aggregates: superposition T-matrix. Atmosphere:
  dust, water droplets, ice crystals. vs Mie sphere.
trigger: scattering from non-spherical particles, atmospheric optics
reasoning_role: nonspherical_scattering
parent: knowledge.em.scattering_mie
retrieval_cost: 1
---

# knowledge.optics.nonspherical_scattering

**T-matrix** (extended boundary condition method): incident field expanded in
vector spherical wavefunctions (VSWF): E_inc=Σ a_n RgΨ_n. Scattered: E_sca=Σ f_n Ψ_n.
f_n=Σ T_nm a_m. T-matrix connects incident → scattered coefficients.
Depends ONLY on particle (shape, size, index, orientation), NOT on incident field.
Once T is computed → scattering for any incidence.

**Spheroids**: prolate (a>b=c, cigar) and oblate (a=b>c, disk). T-matrix:
analytical for spheroids (separable in spheroidal coordinates). Scattering
diagram: Q_ext vs a/b shows strong shape dependence. Rayleigh limit:
polarizability tensor α_ij (diagonal in body frame).

**Infinite cylinder**: Mie-type solution with cylindrical Bessel/Hankel.
TE (E∥axis) and TM (H∥axis) modes. Oblique incidence: conical diffraction.
Carbon nanotubes, fibers. Depolarization: s→s and s→p coupling.

**RDG** (Rayleigh-Debye-Gans): same as Born (see knowledge.em.born_approximation).
Form factor P(q)=|(1/V)∫ e^{iq·r} dV|². For spheroid: P(q)=[3j₁(u)/u]² with
u²=(qa)²[cos²β+(a/b)²sin²β cos²φ]. Guinier: I(q)∝exp(−q²R_g²/3), R_g from shape.

**Aggregates**: superposition T-matrix for N particles. Translation addition
theorem for VSWF. Fractal aggregates (DLA): D_f≈1.8, R_g∝N^{1/D_f}.
Soot, biological cells, interstellar dust.

- Bohren & Huffman §5-8
