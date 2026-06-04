---
skill_id: convention.polarization_handedness
type: convention
summary_50t: >
  Right circular: E rotates CCW in xy plane as viewed from +z looking back along
  −k toward source. = CW from source's view. = helicity +1. = (x̂+iŷ)/√2 with
  e^{i(kz−ωt)}. Stokes s_3 > 0. Stix plasma R-wave naming is a SEPARATE
  convention — bridge required between optical and plasma handedness.
---

# Polarization handedness convention

## Definition (project standard, IEEE / physics)

With k along +ẑ and the plane wave E = Re[ε̂ E₀ e^{i(kz−ωt)}], **right
circular polarization** is:

```
ε̂_RHC = (x̂ + i ŷ) / √2
```

At z = 0, the real electric field traces:

```
E(t) = (cos ωt, sin ωt, 0)
```

which rotates **counterclockwise** in the xy plane as viewed from +z (observer
looking back along −k toward the source). Equivalently: **clockwise** as viewed
from the source looking along +k toward the observer.

**Helicity**: this is helicity +1 (photon spin along +k).

**Left circular** is ε̂_LHC = (x̂ − i ŷ) / √2, helicity −1.

## Stokes parameters

With this convention (Born & Wolf §1.4):

```
s₀ = |E_x|² + |E_y|²              (intensity)
s₁ = |E_x|² − |E_y|²              (horizontal vs vertical linear)
s₂ = 2 Re[E_x E_y*]               (±45° linear)
s₃ = 2 Im[E_x E_y*]               (s₃ > 0 = right circular)
```

The sign of s₃ is **the** handedness check: s₃ > 0 ⇔ helicity +1 ⇔ right
circular in the project convention. For purely RHC: s₃ = +s₀.

## Handedness and propagation direction

Polarization handedness is defined relative to the observer's view port. For
a wave propagating along −ẑ (k = −k ẑ), the handedness relative to a lab-fixed
observer at +z looking into the beam is **reversed** compared to the k-aligned
definition above. Always specify the viewing direction or use the helicity
(spin angular momentum along k) to disambiguate.

## Bridge to plasma R / L naming (Stix convention)

The plasma **R-wave** (e.g., whistler / electron-cyclotron branch) is named for
the direction in which E rotates in the same sense as the **positive-charge**
gyration around B₀. For electrons (q < 0), the gyration is counterclockwise
viewed along −B₀; so the R-wave drives electrons resonantly.

**Therefore**: a Stix R-wave propagating along +B₀ has E rotating in the sense
opposite to electron gyration — but Stix calls this R because it is named after
the POSITIVE charge. With B₀ along +z and the standard right circular defined
above:

- **Stix R-wave = optical LEFT-circular** (helicity −1)
- **Stix L-wave = optical RIGHT-circular** (helicity +1)

This is genuinely confusing; the recommended writing pattern in any node
that uses both:

> "Stix's R-wave is right-circular in the plasma-physics sense (E rotates
> in the sense of positive-ion gyration); in optical handedness this is the
> opposite of what we call right-circular. Both conventions are internally
> consistent; the names differ."

## Quick-reference table

| Term | ε̂ (k along +z) | Helicity | s₃ sign | Stix name (B₀ along +z) |
|------|-----------------|----------|---------|--------------------------|
| Right circular (optics) | (x̂ + iŷ)/√2 | +1 | > 0 | L-wave |
| Left circular (optics) | (x̂ − iŷ)/√2 | −1 | < 0 | R-wave |

## References

Born & Wolf §1.4 (optical RHC = ours), Jackson §7.2 (helicity), Stix §1.5
(plasma R/L naming), IEEE Std 149-1979 (IEEE polarization definition).
