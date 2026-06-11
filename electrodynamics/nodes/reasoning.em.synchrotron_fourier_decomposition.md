---
skill_id: reasoning.em.synchrotron_fourier_decomposition
type: reasoning
summary_50t: >
  LW acceleration field for circular motion → E(t) periodic with ω₀.
  Fourier: E(t)=Σ[A_n cos(nω₀t)+B_n sin(nω₀t)]. π-component (in-plane):
  E_π(−t)=E_π(t) → B_n=0 → pure cosine → all harmonics in phase at t=0.
  σ-component (⊥-plane): E_σ(−t)=−E_σ(t) → A_n=0 → pure sine → zero at t=0.
  CEP=0 for π, CEP=π/2 for σ. Bessel: A_n∝n K_{2/3}'(nω₀/ω_c).
trigger:
  - computing harmonic phases of synchrotron radiation
  - understanding CEP of relativistic circular-motion radiation
  - time-domain → frequency-domain bridge for periodic radiation
reasoning_role: synchrotron_fourier
parent: reasoning.em.lienard_wiechert_radiation
retrieval_cost: 1
---

# reasoning.em.synchrotron_fourier_decomposition — LW → Harmonics → CEP

## Core Picture

For a charge in uniform circular motion, the far-field radiation is PERIODIC
with the gyration period T = 2π/ω₀. The acceleration field from the
Liénard-Wiechert formula (`reasoning.em.lienard_wiechert_radiation`) gives
E(t) at the observer. Because E(t + T) = E(t), it can be expanded in a
Fourier series. The SYMMETRY of the orbit determines whether each harmonic
n enters as cos(n ω₀ t) or sin(n ω₀ t) — and this determines the CEP.

## Derivation Sketch

### 1. Geometry and the acceleration field

Electron in circular orbit in the x-y plane, radius R, speed v = βc:
```
r₀(t') = R(cos ω₀ t', sin ω₀ t', 0)
β(t')  = β(−sin ω₀ t', cos ω₀ t', 0)         [v = βc = R ω₀]
β̇(t') = −β ω₀ (cos ω₀ t', sin ω₀ t', 0)    [centripetal, toward origin]
```

Observer at large distance in the x-z plane, direction n̂ = (sin θ, 0, cos θ)
where θ = 0 corresponds to the orbital axis (z) and θ = π/2 to the orbital
plane. The LIÉNARD-WIECHERT ACCELERATION FIELD is:

```
E_rad(t) = (e/4π ε₀ c) [n̂ × ((n̂ − β) × β̇) / (κ³ R)]_ret
```

where κ = 1 − n̂·β and [·]_ret means evaluate at retarded time t' satisfying
t' = t − R(t')/c (observer time t, emission time t').

### 2. Time-domain periodicity

The motion is T-periodic: β(t' + T) = β(t'), β̇(t' + T) = β̇(t'). The retarded
time mapping t(t') = t' + R(t')/c preserves periodicity (R(t'+T) = R(t') for
distant observer). Therefore the observed field is also T-periodic:
```
E(t + T) = E(t)    →    E(t) = Σ_{n=1}^∞ [A_n cos(n ω₀ t) + B_n sin(n ω₀ t)]
```

The n=0 (DC) term is zero: no net static field from a charge in closed orbit.

### 3. Parity analysis — the key to the CEP

Choose the time origin t = 0 as the instant when the electron velocity points
directly AT the observer (pulse peak, see below). Consider the time-reversal
transformation: t → −t.

Under t → −t:
- Electron position: r₀ → r₀ (x unchanged, y → −y)
- Velocity: β → (−β_x, β_y) — x-component REVERSES
- Acceleration: β̇ → (−β̇_x, −β̇_y) — both components reverse

For an observer in the orbital plane along +x (n̂ = (1, 0, 0)):
- At t = 0: β = (β, 0, 0), β̇ = (0, −β ω₀, 0)
- The LW numerator n̂ × ((n̂ − β) × β̇) = (0, −(1−β) β ω₀, 0)
- This is purely along −y: the π-component (in-plane polarization)

Under t → −t, the electron approaching from y < 0 at t < 0 is mirrored to
the electron receding toward y > 0 at t > 0. The RADIATION PATTERN is
symmetric about the closest-approach point because:
- The denominator κ = 1 − n̂·β = 1 − β_x is even in t (β_x reverses sign
  under t → −t, but so does the sign of t in the retarded mapping)
- The numerator transforms as: n̂ × ((n̂ − β(−t)) × β̇(−t)) has the same
  y-component (both β and β̇ acquire compensating sign changes)

**Result for π-component** (in orbital plane): E_π(−t) = E_π(t) → EVEN.
Even functions have pure cosine Fourier series: B_n = 0 for all n.
```
E_π(t) ∝ Σ_{n=1}^∞ A_n cos(n ω₀ t),   A_n ≠ 0
```

**Result for σ-component** (⊥ to orbital plane): E_σ(−t) = −E_σ(t) → ODD.
Odd functions have pure sine Fourier series: A_n = 0 for all n.
```
E_σ(t) ∝ Σ_{n=1}^∞ B_n sin(n ω₀ t),   B_n ≠ 0
```

### 4. CEP — what it means for synchrotron radiation

The carrier-envelope phase (CEP) for a harmonic train is the phase φ_n of
each harmonic n at the pulse envelope peak. From the above:

- **π-polarization** (dominant in orbital plane): φ_n = 0 for ALL n.
  At the pulse peak (t = 0 mod T), cos(0) = 1: all harmonics add CONSTRUCTIVELY.
  The CEP is identically ZERO, locked by the geometric symmetry of the circular
  orbit — no external phase stabilisation needed.

- **σ-polarization**: φ_n = π/2 for all n. At t = 0, sin(0) = 0: the σ-component
  contributes NOTHING at the pulse peak. All σ radiation is in the wings.

This is fundamentally different from HHG (`reasoning.uo.attosecond_pulse_generation`),
where each harmonic's CEP depends on the driver laser CEP via φ_n = n φ_CEP + const,
requiring active CEP stabilisation to produce isolated attosecond pulses.

### 5. Connection to the spectral formula

The Fourier coefficients for the π-component are given by the standard
synchrotron radiation integrals (Jackson §14.5):

```
A_n(ω) ∝ n ∫_{ω/ω_c}^∞ K_{5/3}(x) dx    [π-component]
A_n ∝ (√3 e² γ / 4π ε₀ c) n K_{2/3}'(n ω₀/ω_c)    [asymptotic, ω_c = (3/2)γ³ ω₀]
```

The FACT that these are all positive at t=0 (all cos(0)=1) guarantees that
the inverse Fourier sum produces a sharp pulse at t=0 — the synchrotron pulse.

### 6. The pulse peak — why it's at t = 0

The pulse peak occurs when the electron velocity points toward the observer.
At this instant:
- κ = 1 − n̂·β is MINIMAL (= 1 − β for head-on) → the κ³ denominator is
  SMALLEST → field is LARGEST (relativistic beaming factor 1/κ³).
- For γ ≫ 1, the pulse width is Δt ∼ 1/(γ³ ω₀) (from the κ³ beaming).

This explains the "carrier" interpretation: the pulse envelope (width ∼ 1/γ³ ω₀)
is modulated by the harmonic carrier at ω ∼ γ³ ω₀, and because all harmonics are
in cosine phase, the carrier peak coincides exactly with the envelope peak.

## Algorithm — Given (γ, B, observer angle θ) → harmonic phases

```
1. Compute ω₀ = eB/γm, critical ω_c = (3/2)γ³ ω₀.
2. Determine observer polarisation: in orbital plane → π dominant.
3. Symmetry: E_π even → cos(n ω₀ t), φ_n = 0.
4. Fourier amplitude from Bessel: A_n ∝ K_{2/3}(n ω₀/ω_c).
5. Pulse peak at t = 0 (mod T): all cos(n·0) = 1 → coherent sum.
6. CEP: φ_n = 0 for π-component (dominant), φ_n = π/2 for σ-component.
```

## Edge Cases

- **Observer at finite θ ≠ π/2 (out of orbital plane)**: both π and σ
  components contribute. The π-component is still cos-like, σ still sin-like,
  but the relative amplitude A_n/B_n changes with θ → the total polarisation
  becomes elliptical and the effective CEP deviates from 0 (partial cancellation).
- **Non-circular motion**: for elliptical or non-uniform motion, the periodicity
  is preserved but the simple even/odd parity breaks. The Fourier phases φ_n
  become n-dependent (non-zero, non-π/2) and must be computed from the full
  LW integral.
- **Curvature radiation vs synchrotron**: in astrophysical contexts, curvature
  radiation (electron following a curved B-field line) gives the same cos-phase
  result because the local geometry is identical — the radiation depends only
  on the instantaneous curvature radius, not on whether the motion is globally
  circular.

## Cross-References

- Jackson §14.5, Landau Vol.2 §74
- electrodynamics: reasoning.em.lienard_wiechert_radiation (parent — LW field)
- landau-graph: knowledge.em.synchrotron_radiation (spectral envelope)
- landau-graph: reasoning.symmetry_drives_physics (parity → Fourier phase)
- ultrafast-optics: reasoning.uo.attosecond_pulse_generation (CEP concept, HHG comparison)
- mathematics-theorems: mathematics.plane_wave_spectrum (spatial Fourier decomposition)
