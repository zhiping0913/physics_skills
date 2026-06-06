---
skill_id: reasoning.cp.modal_expansion_numerical
type: reasoning
summary_50t: >
  Field in waveguide/cavity = Σ a_n E_n(r) e^{±iβ_n z}. Modes from
  2D eigenvalue problem on cross-section. Mode matching: match tangential
  E,H at junction → generalized scattering matrix. FEM eigenanalysis for
  arbitrary cross-sections. Cutoff frequencies, propagation constants.
trigger:
  - waveguide discontinuity, filter, horn, cavity analysis
  - mode matching at junctions, S-parameter extraction
reasoning_role: mode_matching
parent: reasoning.em.waveguide_mode_decomposition
retrieval_cost: 1
sign_convention: "Propagation: e^{i(βz−ωt)} (matches parent waveguide_mode_decomposition)"
---

# reasoning.cp.modal_expansion_numerical — Cross-Section → Eigenmodes → S-Matrix

## Core Picture

The field in a uniform waveguide can be expanded in transverse eigenmodes
E(x,y) e^{±iβ z}. For simple shapes (rectangular, circular) the modes are
analytic (TE_mn, TM_mn). For arbitrary cross-sections, the 2D eigenvalue
problem is solved numerically (FEM). At junctions between waveguides, mode
matching enforces tangential field continuity → scattering matrix.

## Derivation Sketch

From `electrodynamics: reasoning.em.waveguide_mode_decomposition` (analytic
TE/TM modes in separable geometries):

1. **2D Eigenvalue Problem**: For a uniform waveguide along z:
   (∇_⊥² + k_c²) φ = 0 with BC: φ=0 on PEC (TM) or ∂φ/∂n=0 (TE).
   k_c is the cutoff wavenumber; β = √(k² − k_c²).

2. **Numerical solution** (FEM): Discretize cross-section with triangular
   mesh. Generalized eigenvalue problem: [S]{φ} = k_c² [T]{φ} where S_ij
   and T_ij are FEM stiffness/mass matrices. For PEC: remove boundary DoFs.

3. **Mode matching at junction** (z=0 between guide A and guide B):
   Tangential E,H continuous → Σ a_n^A E_n^A = Σ a_n^B E_n^B  (and same for H).
   Test with mode m of guide A: integrate over cross-section → GSM formulation.

## Algorithm — Given Cross-Section → Modes → S-Matrix

```
1. MESH CROSS-SECTION: 2D triangular mesh. Refine near corners.

2. FEM EIGENVALUE SOLVE:
   - TM modes: [S]{φ} = k_c² [T]{φ}, φ=0 on PEC.
   - TE modes: [S]{ψ} = k_c² [T]{ψ}, ∂ψ/∂n=0 on PEC.
   Use sparse eigenvalue solver (ARPACK, shift-invert for interior eigenvalues).

3. SORT MODES: Order by increasing k_c (or |β| for propagating modes at
   given frequency). Keep modes with |β| > β_cutoff (typically k_c < 2k₀).

   DEGENERATE MODES: If multiple modes share the same k_c (e.g., circular
   waveguide TE₀n/TM₁n, square guide TE_mn/TE_nm), the eigenvalue solver
   returns arbitrary linear combinations. Group by |k_c,i−k_c,j| < 10⁻⁶·k_c,avg.
   Within each degenerate group, apply symmetric Löwdin orthogonalization to
   E_t, H_t vectors. The resulting modes are orthonormal and suitable for
   mode matching.

4. COMPUTE MODAL FIELDS:
   TM: E_z = φ,  E_t = +(iβ/k_c²)∇_t φ,  H_t = (iωε/k_c²) ẑ×∇_t φ
   TE: H_z = ψ,  H_t = +(iβ/k_c²)∇_t ψ,  E_t = −(iωμ/k_c²) ẑ×∇_t ψ

5. NORMALIZE: ∫ E_m × H_n* · ẑ dS = δ_{mn} (orthonormal power basis).

6. MODE MATCHING AT JUNCTION (guide A → B):
   For each mode m in A, project onto modes n in B:
   M_{mn} = ∫_S (E_m^A × H_n^{B*}) · ẑ dS   (coupling matrix)
   GSM: S_{11} = (I + M^H M)⁻¹ (I − M^H M) × ...
   (See formulations in Collin, *Field Theory of Guided Waves* Ch.5.)

7. CASCADE: For multiple junctions, multiply GSMs using standard network
   algebra (connection of 2-ports).
```

## Lossy Waveguides

For lossy walls (finite conductivity): use impedance BC n̂×E = Z_s n̂×(n̂×H) with Z_s = (1+i)R_s. The eigenvalue problem becomes complex non-Hermitian. Conductor attenuation (perturbative, low-loss): α_c = (R_s/2Z₀) · ∮|H_tan|² dl / ∫|H_t|² dS. Dielectric attenuation: α_d = k₀ n tanδ / 2. Propagation: γ = α + iβ, fields ∝ e^{−γz}.

## Edge Cases

- **Evanescent mode access**: Include enough evanescent modes (|β| imaginary,
  decaying) to capture reactive near-field at junctions. Rule: |β| Δz ≤ 3
  for modes within one decay length of discontinuity.
- **Dielectric-loaded waveguide**: ε_r varies over cross-section → generalized
  eigenvalue problem already handles it.
- **Open structures** (dielectric waveguide, fiber): Use PML truncation at
  cross-section boundary to absorb radiation modes.

## Cross-References

- Collin, *Field Theory of Guided Waves* (1990) Ch.5
- electrodynamics: reasoning.em.waveguide_mode_decomposition (parent)
- computational-physics: reasoning.cp.finite_element_method (FEM eigenanalysis)
