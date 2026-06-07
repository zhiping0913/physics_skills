---
node_type: knowledge
domain: ultrafast-optics
topic: dispersion_data
tags: [GDD, TOD, Sellmeier, fused silica, Ti:sapphire, SF10, prism pair, grating pair, chirped mirror, zero-dispersion, material dispersion]
citations:
  - "Weiner, A.M., Ultrafast Optics, §4.1-4.3"
  - "Diels, J.-C., Rudolph, W., Ultrashort Laser Pulse Phenomena, §1-2"
---

# Dispersion Data for Ultrafast Optics

## Common Material GDD at 800 nm

| Material | GDD (fs²/mm) | TOD (fs³/mm) | Zero-λ (μm) |
|----------|-------------|-------------|-------------|
| Fused silica (SiO₂) | +36.2 | +2.7 | 1.27 |
| BK7 glass | +44 | +3.5 | 1.31 |
| SF10 glass | +159 | +8.9 | 1.62 |
| Sapphire (Al₂O₃) | +34 | +2.5 | 1.35 |
| Ti:sapphire crystal | +58 | +4.1 | 1.52 |
| CaF₂ | +21 | +1.8 | 1.55 |
| Water | +25 | ~+2 | 1.00 |
| Air (STP, 1 m) | +0.02 | — | — |
| YAG | +65 | +4.8 | 1.58 |

**Rule of thumb**: Most optical glasses have GDD ≈ +30-60 fs²/mm at 800 nm.
Dense flint glasses (SF series) have 3-5× stronger GDD.

## Ti:sapphire Gain Crystal (typical 2-3 mm path)

Per pass through 3 mm Ti:sapphire at Brewster angle:
- GDD ≈ +170 fs² (single pass)
- TOD ≈ +12 fs³

Oscillator round-trip (two passes through crystal, two passes through SF10 prism pair):
- Net material GDD ≈ +340 fs²
- Compensated by prism pair with L_sep ≈ 30-60 cm → net small anomalous GDD.

## Fiber Dispersion (standard single-mode fiber SMF-28)

| Parameter | Value |
|-----------|-------|
| D at 1550 nm | +17 ps/(nm·km) (anomalous) |
| D at 800 nm | −100 ps/(nm·km) (normal) |
| β₂ at 1550 nm | −22 fs²/mm |
| β₂ at 800 nm | +110 fs²/mm |
| Zero-dispersion λ | ~1310 nm |
| Dispersion slope S₀ | 0.086 ps/(nm²·km) |

## Prism Pair GDD Formula

For SF10 prism pair at Brewster angle (θ_B ≈ 58.6° at 800 nm):

```
GDD ≈ −(2λ³/πc²) (dn/dλ)² L_sep  [single pass]

GDD ≈ −3400 fs²  for L_sep = 30 cm, SF10 at 800 nm
GDD ≈ −700 fs²   for L_sep = 30 cm, fused silica at 800 nm
```

Tunable by translating one prism along the beam path. Double-pass doubles GDD.

## Grating Pair GDD Formula

For parallel grating pair, Littrow angle, double-pass:

```
GDD = −(λ₀³ L_g) / (2π c² d² cos² θ_d)   [double pass]
```

| Grating (l/mm) | d (μm) | GDD at 800 nm (fs² per cm L_g) |
|---------------|--------|-------------------------------|
| 600 | 1.67 | −3,300 |
| 1200 | 0.833 | −13,200 |
| 1800 | 0.556 | −30,000 |

Larger groove density → stronger negative GDD. Typical CPA compressor:
1200 l/mm, L_g ≈ 50 cm → GDD ≈ −6.6 × 10⁵ fs².

## Chirped Mirror Typical Parameters

| Parameter | Typical Value |
|-----------|---------------|
| GDD per bounce | −40 to −60 fs² |
| Bandwidth | 600-1200 nm (octave) |
| GDD ripple | < ±20 fs² (standard), < ±5 fs² (advanced DCM) |
| Reflectivity | > 99.9% |
| Number of bounces for oscillator | 4-6 per round-trip |
| Group delay range | 10-30 fs delay across bandwidth |

For a 6-bounce oscillator design: net GDD_CM ≈ −300 fs² per round-trip.

## Typical CPA System Dispersion Budget

| Element | GDD contribution |
|---------|-----------------|
| Material in stretcher (fiber or bulk glass) | +10⁵ to +10⁶ fs² |
| Amplifier gain medium | +10³ to +10⁴ fs² |
| Material in compressor path | +10³ fs² |
| Grating compressor (matched) | −(10⁵ to 10⁶) fs² |
| **Residual GDD** | ~0 fs² (matched) |
| **Residual TOD** | ~−10⁴ to −10⁵ fs³ (grating dominated) |
| TOD-limited pulse duration | ~25-30 fs for Ti:sapphire CPA |

## Wavelength Scaling of GDD

All GDD values scale with wavelength. For bulk material:
```
GDD(λ) ≈ GDD(λ₀) · (λ/λ₀)³
```
For grating pairs:
```
GDD(λ) ∝ λ³ (exact from formula)
```
