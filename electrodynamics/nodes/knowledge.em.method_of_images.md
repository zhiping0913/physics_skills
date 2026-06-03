---
skill_id: knowledge.em.method_of_images
type: knowledge
summary_50t: >
  For a point charge near a grounded conducting plane: replace plane
  by image charge −q at mirror position. Result satisfies Poisson + BC
  → by uniqueness, it IS the solution. Works for plane, sphere, cylinder.
trigger:
  - point charge near conducting boundary
  - need to compute potential, field, induced charge, force
reasoning_role: boundary_value_method
parent: reasoning.em.uniqueness_theorem_boundary_value
retrieval_cost: 1
---

# knowledge.em.method_of_images

**Principle**: Replace conducting boundaries by equivalent IMAGE CHARGES
outside the region of interest. The image configuration must produce the
same potential on the boundary as the conductor. Uniqueness theorem
guarantees this is THE solution.

## Canonical Cases

**Point charge near grounded infinite conducting plane** (z=0):
Image: −q at (0,0,−d). Potential in z>0: φ(r) = (q/4πε₀)(1/R₁ − 1/R₂)
where R₁ = √[ρ²+(z−d)²], R₂ = √[ρ²+(z+d)²].
Surface charge: σ(ρ) = −qd/[2π(ρ²+d²)^{3/2}].
Force on charge: F = −q²/(16πε₀d²) ẑ (attraction to plane).

**Point charge near grounded conducting sphere** (radius a, center at origin,
charge q at distance y > a on z-axis):
Image: q' = −(a/y)q at z' = a²/y.
Potential: φ(r) = (1/4πε₀)[q/|r−yẑ| + q'/|r−(a²/y)ẑ|].
Force: F = −(1/4πε₀)q²ay/[(y²−a²)²] (attraction).

**Line charge parallel to conducting cylinder**: Image line charge inside cylinder.
**Point charge in corner (two perpendicular planes)**: Three image charges.

## Limitations

- Works ONLY for point/line charges near simple geometries (plane, sphere, cylinder)
- Does not generalize to arbitrary source distributions or geometries
- For dielectrics (not conductors): image method also works but with fractional image charge

- Jackson §2.1-2.4, Griffiths §3.2
