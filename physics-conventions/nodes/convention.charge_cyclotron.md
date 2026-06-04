---
skill_id: convention.charge_cyclotron
type: convention
summary_50t: >
  e > 0 (fundamental constant). Particle charge q_s = z_s·e with z_e=−1, z_i=+Z.
  Cyclotron ω_c = q_s B / m_s (SIGNED, Stix convention): ω_ce < 0 for electrons.
  Unsigned sources (Chen): substitute ω_c → |q|B/m. Larmor ω_L = |q|B/(2m) (factor
  1/2, atomic physics) — distinct from cyclotron.
---

# Charge and cyclotron frequency convention

## Elementary charge

The fundamental charge `e` is **positive**: e ≈ 1.602×10⁻¹⁹ C. A particle's
charge is q_s = z_s·e where z_s is the signed charge number:

| Species | z_s | q_s |
|---------|-----|-----|
| Electron | z_e = −1 | q_e = −e |
| Proton / ion | z_i = +Z | q_i = +Ze |
| Positron | z = +1 | q = +e |

## Cyclotron frequency (signed, Stix convention)

```
ω_cs = q_s B / m_s        (signed)
```

This is the **project default** and follows Stix §1.2:

- **ω_ce < 0** for electrons (q_e = −e < 0)
- **ω_ci > 0** for ions (q_i > 0)

The signed convention matters in plasma physics because:

1. **Resonance conditions** depend on the relative sign of ω and ω_c.
   e.g., the electron cyclotron resonance for a wave with frequency ω > 0
   occurs when ω ≈ |ω_ce|, but the cold-plasma dielectric tensor ε(ω) is
   written in terms of the signed ω_c directly.
2. **Stix R/L wave naming** uses the signed ω_c to define R and L roots.
   The R-wave is defined as the polarization that rotates in the sense of
   positive charge gyration → E rotates opposite to electron gyration for
   B₀ along +z (see [[convention.polarization_handedness]]).

## Unsigned sources (e.g., Chen)

Many textbooks (Chen, Goldston-Rutherford) define the cyclotron frequency as
an **unsigned magnitude**:

```
ω_c (Chen) = |q| B / m          (unsigned, always positive)
```

When citing an unsigned source:

1. **Substitute** ω_c → |q|B/m for magnitude expressions.
2. **Handle the charge sign separately** in R/L definitions, resonance
   conditions, and the cold-plasma dielectric tensor.
3. Convert: ω_c(signed, Stix) = (q/|q|) × ω_c(unsigned, Chen).

## Larmor frequency (atomic physics)

Do not confuse with cyclotron frequency. The Larmor frequency appears in
atomic/quantum contexts and includes a **factor 1/2**:

```
ω_L = |q| B / (2m)              (Larmor, unsigned, factor 1/2)
```

This is the precession frequency of a magnetic dipole in a B field. Relevant
for Zeeman splitting, spin precession, and future `atom` skill nodes. The
factor-of-two difference between ω_c and 2ω_L is a persistent source of errors
when bridging plasma and atomic-physics formulas.

## Summary

| Quantity | Definition | Sign | Used in |
|----------|-----------|------|---------|
| ω_c (project) | q_s B / m_s | signed | plasma, electrodynamics |
| ω_c (Chen) | \|q\| B / m | unsigned | bridging only |
| ω_L (Larmor) | \|q\| B / (2m) | unsigned | atomic, spin physics |

## References

Stix §1.2 (signed ω_c), Chen §2.2 (unsigned), Jackson §12.3 (Larmor
precession), Goldston-Rutherford §4 (unsigned convention context).
