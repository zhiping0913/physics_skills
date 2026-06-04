---
skill_id: convention.fresnel_rp
type: convention
summary_50t: >
  Fresnel r_p: Verdet (H-tangential) convention. r_p = (n₂cosθ_i−n₁cosθ_t) /
  (n₂cosθ_i+n₁cosθ_t). At normal incidence r_p = −r_s. Born & Wolf uses opposite
  E-tangential convention: r_p(B&W) = −r_p(Verdet). Both equivalent; convert by
  flipping sign. Power R = |r|² is unambiguous.
---

# Fresnel r_p sign convention

## Two conventions exist

Both conventions trace to the definition of the **positive direction** of the
p-polarized electric field upon reflection. They differ by a sign, but
reflectance R = |r|² is **identical** in both.

### Verdet convention (project default)

Based on the tangential **H** field (Verdet, 1869). The positive direction
for the p-polarized E-field is chosen so that the tangential H-field of the
incident and reflected waves have the **same** sign convention. Result:

```
r_p (Verdet) = (n₂ cos θ_i − n₁ cos θ_t) / (n₂ cos θ_i + n₁ cos θ_t)
```

At normal incidence (θ_i = θ_t = 0):

```
r_p(Verdet) = (n₂ − n₁) / (n₂ + n₁) = −r_s
```

### Born & Wolf convention (E-tangential)

Born & Wolf (§1.5) defines the positive p-direction so that the tangential
**E** field of incident and reflected waves align. This gives:

```
r_p (B&W) = (n₁ cos θ_t − n₂ cos θ_i) / (n₁ cos θ_t + n₂ cos θ_i) = −r_p(Verdet)
```

At normal incidence:

```
r_p(B&W) = (n₁ − n₂) / (n₁ + n₂) = +r_s
```

## Which convention do project skills use?

- **`optics`, `electrodynamics`**: Verdet (H-tangential). This is the default
  in Jackson §7.3, Hecht §4.6, and most electrodynamics textbooks.
- **Born & Wolf citations in nodes**: must be flagged with a sign conversion.

## Conversion between conventions

To convert a Born & Wolf r_p into the project (Verdet) convention:

```
r_p(Verdet) = −r_p(B&W)
```

This sign flip propagates to any **field** expression, but **power** and
**reflectance** are invariant: R = |r_p|² = |r_s|² is the same in both.

## Phase shift on reflection

The physical phase shift on reflection depends on the convention:
- In Verdet: for n₂ > n₁ at normal incidence, r_s = (n₁−n₂)/(n₁+n₂) < 0 →
  180° phase shift. r_p = −r_s > 0 → 0° phase shift.
- In B&W: both r_s and r_p are negative for n₂ > n₁ → both have 180° shift.

The **observable** is the relative phase between s and p upon reflection
(ellipsometric angle Δ), which is convention-dependent. When citing
ellipsometry results, always specify the convention used.

## References

Jackson §7.3 (Verdet, H-tangential), Born & Wolf §1.5 (E-tangential, the
"other" convention), Hecht §4.6 (uses Verdet), Azzam & Bashara §1.6
(ellipsometric conventions).
