---
skill_id: reasoning.optics.dispersion_management_gdd
type: reasoning
summary_50t: >
  GDD = d²φ/dω² (ps²). Gratings: anom. GDD, prism: norm./anom.
  Grating pair GDD = −(λ³L_g)/(2πc²d² cos²θ_d). Prism pair: GDD∝L_prism.
  Chirped mirrors: λ-dependent penetration. TOD from β₃ also managed.
  CPA: GDD_stretcher + GDD_compressor = 0 (up to TOD).
trigger: designing stretcher/compressor, compensating material dispersion
reasoning_role: dispersion_management
parent: reasoning.optics.pulse_propagation_nlse
retrieval_cost: 1
---

# reasoning.optics.dispersion_management_gdd — GVD/TOD → Pulse Control

## Core Picture

To generate and maintain ultrashort pulses, dispersion must be precisely
controlled. Group-delay dispersion (GDD = d²φ/dω²) broadens pulses via
GVD; third-order dispersion (TOD) distorts them asymmetrically. Optical
elements (gratings, prisms, chirped mirrors) provide CONTROLLABLE dispersion
to compensate material paths (Siegman §9, Svelto §8.6).

## Algorithm

```
1. SPECTRAL PHASE EXPANSION (Taylor at ω₀):
   φ(ω) = φ₀ + φ₁(ω−ω₀) + ½φ₂(ω−ω₀)² + ⅙φ₃(ω−ω₀)³ + ...
   φ₁ = GD (group delay, fs). φ₂ = GDD (fs²). φ₃ = TOD (fs³).
   Transform-limited: φ₂=φ₃=0 (all frequencies in phase at t=0).

2. MATERIAL DISPERSION: φ₂_mat = (λ³L/2πc²)(d²n/dλ²).
   Fused silica at 800nm: d²n/dλ² ≈ 0.04 μm⁻² → φ₂≈+360 fs²/cm.
   NORMAL dispersion (φ₂>0): red leads blue (positive chirp).

3. GRATING PAIR (negative GDD):
   φ₂ = −(λ³ L_g) / (2πc² d² cos²θ_d)
   L_g=grating separation, d=groove spacing, θ_d=diffraction angle.
   Typical: 1200 l/mm, L_g=10cm → φ₂≈−10⁵ fs² at 800nm.
   φ₃ also negative (TOD in same direction as GDD).

4. PRISM PAIR:
   φ₂ ∝ L_prism (d²n/dλ²)(dn/dλ)². Can be positive or negative.
   Brewster-angle insertion minimizes loss. φ₃ can be tuned independently
   (material choice, apex separation).

5. CHIRPED MIRROR: λ-dependent penetration depth → negative GDD.
   Multi-layer dielectric stack, no spatial separation needed.
   Used for few-cycle pulses (cannot tolerate grating losses).

6. CPA MATCHING:
   φ₂_stretcher + φ₂_material + φ₂_compressor = 0.
   Treacy compressor (grating pair): φ₂<0, φ₃<0.
   Martinez stretcher (grating+lens): φ₂>0 (sign reversed), φ₃>0.
   Matched pair cancels GDD; residual TOD limits compressibility.
```

## Key Formula (Grating Pair)

GDD = −(λ³ L_g)/(2πc² d² cos²θ_d) × [1 − (λ/d − sin γ)²]^{−1}
γ = incidence angle. Littrow: θ_d ≈ γ, maximum efficiency.

## Cross-References

- Siegman §9, Svelto §8.6; Trebino §3 (dispersion in pulse measurement)
- optics: reasoning.optics.pulse_propagation_nlse (GVD term in NLSE)
