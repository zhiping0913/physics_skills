---
skill_id: knowledge.em.separation_of_variables
type: knowledge
summary_50t: >
  ∇²φ=0 in Cartesian→sin/cos/sinh, cylindrical→Bessel J_m,Y_m+I_m,K_m,
  spherical→Legendre P_l^m+spherical Bessel. Eigenfunction expansion from
  Sturm-Liouville. BCs fix eigenvalues. Completeness: Σ over discrete + ∫ over continuous spectrum.
trigger: solving Laplace/Poisson/Helmholtz in separable coordinate systems
reasoning_role: separation_of_variables
parent: reasoning.em.uniqueness_theorem_boundary_value
retrieval_cost: 1
---

# knowledge.em.separation_of_variables

**Cartesian**: φ=X(x)Y(y)Z(z). X''/X+Y''/Y+Z''/Z=0 → −k_x²−k_y²−k_z²=0.
Solutions: sin/cos (oscillatory), sinh/cosh (exponential). Rectangular waveguide,
capacitor fringe fields.

**Cylindrical** (ρ,φ,z): Φ=R(ρ)Q(φ)Z(z). Q(φ)=e^{imφ}. R(ρ): Bessel J_m, Y_m
(oscillatory inside), I_m, K_m (exponential outside). Coaxial cable, optical fiber.

**Spherical** (r,θ,φ): Φ=R(r)Θ(θ)Q(φ). Θ(θ)=P_l^m(cos θ) (associated Legendre).
R(r)=A r^l + B r^{−l−1} (Laplace). For Helmholtz: j_l(kr), y_l(kr) (spherical Bessel).
Conducting/dielectric sphere, Mie scattering.

**Sturm-Liouville theory**: each separated ODE is self-adjoint → orthogonal
eigenfunctions → expand arbitrary function: f(x)=Σ c_n φ_n(x). Completeness:
Σₙ φ_n(x)φ_n*(x')=δ(x−x') (discrete) + integral over continuous branch cuts.

**BCs**: Dirichlet (φ=0), Neumann (∂φ/∂n=0), or impedance. BCs discretize
eigenvalues. The expansion coefficients are found by projecting BCs onto
the eigenfunction basis.

- Jackson §2.5-2.11, §3
