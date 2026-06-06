---
skill_id: mathematics.sommerfeld_integral
type: reasoning
summary_50t: >
  Sommerfeld identity: e^{ikR}/R = (i/2)∫₀^∞ H₀^(1)(k_ρ ρ) e^{ik_z|z|} (k_ρ/k_z) dk_ρ.
  Cylindrical wave → plane waves. Used for layered media dyadic Green's
  functions, branch cuts from k_z = √(k²−k_ρ²), surface wave poles,
  leaky wave poles. Riemann sheet selection per radiation condition.
trigger:
  - computing fields from sources in planar stratified media
  - constructing Green's functions for layered geometries
  - evaluating radiation from sources on or near interfaces
reasoning_role: sommerfeld_integral
parent: mathematics.plane_wave_spectrum
retrieval_cost: 1
---

# mathematics.sommerfeld_integral — 3D Wave → 1D k_ρ Integral

## Core Picture

A spherical wave e^{ikR}/R can be decomposed into cylindrical waves via the
Sommerfeld identity, reducing a 3D problem to a 1D integral over radial
wavenumber k_ρ (Sommerfeld 1909). This is the MATHEMATICAL ENGINE of layered
media Green's functions — each cylindrical wave component independently
interacts with planar interfaces.

## Derivation Sketch

Starting from `mathematics-theorems: mathematics.plane_wave_spectrum` (the
Weyl identity representing e^{ikR}/R as a 2D plane wave integral):

### 1. Sommerfeld Identity

Convert the Cartesian (k_x, k_y) integral to polar (k_ρ, α):
```
k_ρ² = k_x² + k_y²
∬ [...] dk_x dk_y = ∫₀^{2π} dα ∫₀^∞ dk_ρ k_ρ [...]
```
The angular integral yields the Bessel function J₀(k_ρ ρ). With the outgoing
Hankel function H₀^(1) = J₀ + iY₀ (proper for the radiation condition):
```
e^{ikR}/R = (i/2) ∫₀^∞ H₀^(1)(k_ρ ρ) e^{i k_z |z|} (k_ρ/k_z) dk_ρ
```
where k_z = √(k² − k_ρ²), ρ = √(x²+y²), R = √(ρ²+z²).

### 2. Branch Cuts and Riemann Sheets

k_z = √(k²−k_ρ²) is DOUBLE-VALUED in the complex k_ρ plane:
- **Top sheet** (physical): Im(k_z) ≥ 0 → waves decay or propagate outward.
- **Bottom sheet** (unphysical): Im(k_z) < 0 → waves grow at infinity.
Branch points at k_ρ = ±k. Branch cut connects them; standard choice is
the hyperbolic cut Im(k²−k_ρ²) = 0.

### 3. Singularities in the k_ρ Plane

```
Surface wave poles: k_z₁/k_z₂ = −ε₁/ε₂ (TM) or −μ₁/μ₂ (TE).
  → Real k_ρ > max(k₁,k₂) → Im(k_z₁,₂) > 0 → wave bound to interface.
  These are the discrete spectrum (guided modes).

Leaky wave poles: Complex k_ρ with Im(k_ρ) < 0, Im(k_z) < 0.
  → Initially on the bottom sheet; when the integration contour is
  deformed, these poles may be captured, contributing radiation at angles
  θ = sin⁻¹(Re(k_ρ)/k).

Branch cut integral: Continuous spectrum (radiation modes). Important
  for near-field and intermediate-zone calculations.
```

### 4. Application to Layered Media

In a planar stratified medium (e.g., substrate with ground plane), the
dyadic Green's function is expressed as a Sommerfeld integral:
```
G̿_e(r,r') = (i/8π²) ∬ A̿(k_ρ) e^{i k_ρ·(ρ−ρ')} e^{i k_z z} dk_x dk_y
```
For each k_ρ, the transmission-line analogy gives the reflection/transmission
coefficients → A̿(k_ρ). This is computationally the Method of Moments for
planar antennas and circuits (Okhmatovski & Zheng 2024).

## Algorithm — Concrete Decision Tree

```
STEP 1 — SETUP
├── Source: J(r') in/above layered medium (ε_i, μ_i per layer)
├── Goal: field E, H at observation point r
└── Output quantity: dyadic Green's function G̿_e(r,r')

STEP 2 — SOMMERFELD REPRESENTATION
├── Express G̿_e as Sommerfeld integral:
│   G̿_e = ∫₀^∞ F(k_ρ) J_n(k_ρ ρ) dk_ρ   via Sommerfeld identity
├── Each k_ρ = transverse wavenumber: cylindrical wave → plane-wave spectrum
└── k_zi = √(k_i² − k_ρ²)  for each layer i

STEP 3 — TRANSMISSION-LINE ANALOGY
├── For each k_ρ, compute layer impedances:
│   Z_TE(i) = ωμ_i / k_zi
│   Z_TM(i) = k_zi / (ωε_i)
├── Build TL cascade: impedance transformers at each interface
├── Compute total reflection coeff Γ̃(k_ρ) via standard TL formulas
│   (recursive: load → interface → ... → source layer)
└── Result: spectral-domain kernel F(k_ρ) fully determined

STEP 4 — INTEGRAND ANALYSIS (complex k_ρ plane)
├── 4a. Locate branch points:
│   k_ρ = ±k_i  for each layer i  (k_i = ω√(μ_iε_i))
├── 4b. Locate poles of F(k_ρ):
│   ├── Surface wave poles: Real k_ρ > max(k_i), Im(k_zi) > 0 ∀i
│   │   → discrete spectrum, bound to interface
│   └── Leaky wave poles: complex k_ρ, Im(k_zi) < 0 in outermost layer
│       → initially on bottom sheet, may be captured on contour deformation
└── 4c. Determine Riemann sheet:
    Physical sheet: Im(k_zi) ≥ 0 for outermost (radiation) layer
    Branch cuts: standard hyperbolic Im(k_i²−k_ρ²) = 0

STEP 5 — CONTOUR CHOICE (decision branch)
│
├── [FAR-FIELD] kρ ≫ 1 ?
│   ├── YES → Steepest-descent path (SDP)
│   │   ├── Saddle point: k_ρ ≈ k sin θ  (θ = observation angle)
│   │   ├── Deform original real-axis contour → SDP through saddle
│   │   ├── Capture any poles crossed during deformation → residue sum
│   │   └── Asymptotic evaluation: saddle-point + residues → space wave
│   │       + surface/leaky wave contributions
│   │
│   └── NO ↓
│
├── [NEAR-FIELD / INTERMEDIATE] ?
│   ├── Direct real-axis integration 0 → ∞
│   ├── Singularity extraction:
│   │   ├── Subtract quasistatic / free-space term analytically
│   │   ├── Integrate remainder numerically (smooth, no singularities)
│   │   └── Add back extracted term
│   └── Mitigate oscillation when k_ρ ρ is moderate:
│       Weighted-average (WA) method or Filon quadrature
│
└── [ANY POLES CROSSED] ?
    └── YES → Add residue contributions:
        Residue = 2πi × lim_{k_ρ→k_pole} (k_ρ−k_pole) F(k_ρ) J_n(k_ρ ρ)
        Each pole → one guided/leaky mode contribution

STEP 6 — EVALUATE
├── Numerical quadrature along chosen contour
├── Post-process kernel to spatial domain:
│   G̿_e(ρ,z; ρ',z') = (i/8π²) ∫₀^∞ A̿(k_ρ) H_n^(1)(k_ρ|ρ−ρ'|) k_ρ dk_ρ
└── Compute fields: E(r) = iωμ₀ ∫_V' G̿_e(r,r') · J(r') dV'
```

## Key Features

- **Transmission-line analogy**: In planar stratified media, the problem
  for each k_ρ reduces to a 1D transmission line with characteristic
  impedances Z_TE = ωμ/k_z, Z_TM = k_z/(ωε). Reflection/transmission
  coefficients follow the same formulas as voltage waves on lines.
- **Fresnel reflection coefficients naturally emerge** from matching
  the transmission-line impedances at each interface.

## Edge Cases

- **k_ρ ρ ≫ 1**: Integrand oscillates rapidly. Use asymptotic methods
  (steepest descent) or Filon integration. The saddle point k_ρ ≈ k sin θ
  gives the geometric-optics ray direction.
- **Source and observation on same interface (z=z'=0)**: The integral
  converges slowly. Extract the direct term (free-space G₀) analytically
  and integrate the reflected part numerically.
- **Lossy media (complex k)**: Branch points move off the real axis;
  contour deformation must track them.

## Cross-Domain Bridges

The Sommerfeld integral framework is not confined to classical
electromagnetics — the same complex k_ρ-plane analysis transfers
directly across domains via the shared structure of planar stratified
Green's functions:

### Planar Antenna / Microwave Circuit MoM
*Okhmatovski & Zheng (2024)*

```
Source → Method of Moments (MoM) for planar conductors
  ├── Sommerfeld integral kernel: A̿(k_ρ) computed via TL analogy
  ├── MoM matrix fill: double Sommerfeld integral per basis-test pair
  │   Z_mn = ∫_S_m ∫_S_n f_m(r) · G̿_e(r,r') · f_n(r') dS' dS
  ├── Discrete complex image method (DCIM): approximate F(k_ρ) as
  │   sum of complex exponentials → closed-form spatial Green's function
  └── Enables full-wave EM simulation of patch antennas, filters, interconnects
```

The Sommerfeld integral is the computational engine behind all planar
MoM codes (ADS Momentum, Sonnet, IE3D). The TL analogy (Step 3 of the
decision tree) provides the spectral kernel; DCIM or direct numerical
Sommerfeld integration provides the spatial MoM matrix entries.

### Plasma: Magnetized Surface Waves
*Dispersion from k_ρ poles*

```
Magnetized plasma half-space (B₀ ∥ interface, ⊥ k_ρ)
  ├── Permittivity tensor ε̿(ω) with off-diagonal gyrotropic terms
  ├── Surface wave poles: solutions of det[boundary-condition matrix] = 0
  │   in complex k_ρ plane
  ├── k_ρ(ω) dispersion branches:
  │   ├── Forward surface wave: v_ph > 0
  │   └── Backward surface wave: v_ph < 0 (unique to magnetized plasma)
  └── Application: plasma diagnostics, fusion edge physics,
      space-plasma wave coupling
```

The same pole-locating machinery from Step 4b applies: the magnetized
plasma modifies the transmission-line impedances (anisotropic Z_TE, Z_TM
with cross-coupling), but the fundamental Sommerfeld decomposition and
contour deformation logic are unchanged.

### Optics: Surface Plasmon Polariton (SPP) Dispersion
*Pole location gives SPP dispersion*

```
Metal-dielectric interface (ε_m(ω) < 0, ε_d > 0)
  ├── TM surface wave pole condition (Step 4b):
  │   k_z(d)/ε_d + k_z(m)/ε_m = 0
  │   where k_z(i) = √(k_i² − k_ρ²),  k_i = k₀√ε_i
  ├── Solve for k_ρ (pole location):
  │   k_SPP = k₀ √(ε_m ε_d / (ε_m + ε_d))
  │   Requires Re(ε_m) < −ε_d for bound SPP (Real k_ρ > k₀√ε_d)
  ├── SPP propagation length: L_SPP = 1/(2 Im(k_SPP))
  └── Cross-over to electrostatics: as k_SPP → ∞,
      ε_m(ω) → −ε_d → surface plasmon resonance frequency ω_SP
```

This is Step 4b applied to the simplest layered medium: one interface.
The SPP is precisely a TM surface wave pole of the Sommerfeld integrand.
The residue contribution from this pole gives the SPP field profile:
exponentially decaying into both media, with maximum intensity at the
interface — the defining characteristic of surface plasmon polaritons.

## Cross-References

- Chew, *Waves and Fields in Inhomogeneous Media* (1999) Ch.2
- Okhmatovski & Zheng, *Theory and Computation of EM Fields in Layered Media* (2024)
- Felsen & Marcuvitz, *Radiation and Scattering of Waves* (1994) Ch.5
- mathematics-theorems: mathematics.plane_wave_spectrum (parent — Weyl identity)
- mathematics-theorems: mathematics.steepest_descent (asymptotic evaluation)
- electrodynamics: reasoning.em.dyadic_green_function (layered media G̿ via Sommerfeld)
