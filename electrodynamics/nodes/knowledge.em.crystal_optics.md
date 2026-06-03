---
skill_id: knowledge.em.crystal_optics
type: knowledge
summary_50t: >
  Uniaxial: n_o (ordinary), n_e(θ) (extraordinary). Birefringence Δn=n_e−n_o.
  Index ellipsoid (1/n²)_ij x_i x_j=1. Optical activity: circular birefringence,
  rotatory power ρ=πΔn/λ. Pockels (linear EO): Δ(1/n²)=r_ijk E_k.
trigger:
  - light propagation in anisotropic/crystalline media
  - polarization optics, electro-optic modulators
reasoning_role: crystal_optics_knowledge
parent: reasoning.constitutive_relation_from_symmetry
retrieval_cost: 1
references:
  - landau-graph: reasoning.constitutive_relation_from_symmetry
---

# knowledge.em.crystal_optics

**Dielectric tensor**: D_i = ε_ij E_j. In principal axes: ε_ij = diag(ε_x,ε_y,ε_z).
n_i = √(ε_i/ε₀). Isotropy → ε_ij=εδ_ij. Uniaxial → ε_x=ε_y≠ε_z. Biaxial → all three ≠.

**Uniaxial crystals**: n_o=√(ε_x/ε₀), n_e=√(ε_z/ε₀). Ordinary ray obeys Snell.
Extraordinary: 1/n_e²(θ) = cos²θ/n_o² + sin²θ/n_e². Walk-off angle α between
k and S: tan α = ½Δn sin 2θ / (n_o² sin²θ + n_e² cos²θ).

**Index ellipsoid**: (x²/n_x² + y²/n_y² + z²/n_z²) = 1. The intersection of the
ellipsoid with the plane ⊥ k gives the two refractive indices for that direction.

**Optical activity** (quartz, sugar solution): ε_ij(ω,k) = ε(ω)δ_ij + iγ e_ijl k_l.
Circular birefringence: n_R ≠ n_L → rotation of linear polarization.
Rotatory power: φ = π(n_L−n_R)/λ (rad/m). Quartz: φ≈21.7°/mm at 589nm.

**Electro-optic effects**:
Pockels (linear): Δ(1/n²)_ij = r_ijk E_k. Changes index ellipsoid.
Kerr (quadratic): Δ(1/n²)_ij = s_ijkl E_k E_l. In liquids/gases, induced
birefringence: Δn = λK E² (Kerr constant). CS₂: K≈3×10⁻¹⁴ m/V².

**Jones calculus**: 2×2 matrix for polarization state [E_x;E_y].
Wave plate: J = diag(1, e^{iφ}). Quarter-wave: φ=π/2. Half-wave: φ=π.
**Stokes parameters**: S₀=I, S₁=I_x−I_y, S₂=I_45−I_−45, S₃=I_R−I_L.
Poincaré sphere: all polarization states on sphere of radius S₀.

- Born & Wolf §14, Jackson §7.3-7.4
