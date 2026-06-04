---
skill_id: convention.pulse_phase_chirp
type: convention
summary_50t: >
  Sign conventions for chirp, group delay dispersion (GDD), and ABCD matrix
  ordering in ultrafast optics. C > 0 = up-chirp, β₂ > 0 = normal dispersion,
  grating pair gives anomalous (negative) GDD.
---

# Pulse phase and chirp conventions

Ultrafast optics uses several sign conventions that must be kept consistent
across calculations.

## Chirp sign

**C > 0 → UP-CHIRP**: instantaneous angular frequency ω_inst(t) increases with
time t. The phase is φ(t) = φ₀ + ω₀ t + (C/2)(t − t₀)².

This convention is paired with the NLSE retarded time frame:

```
T = t − z / v_g
```

where v_g is the group velocity. The retarded time T is zero at the pulse peak
for a pulse traveling in the +z direction.

## Dispersion sign

```
β₂ > 0  → NORMAL dispersion   (red leads blue in time)
φ₂ = GDD > 0  → NORMAL dispersion
```

A **grating pair** produces **NEGATIVE** GDD (anomalous dispersion), which is
used to compensate positive dispersion from optical elements.

## ABCD matrix conventions

**Multiplication order** (Siegman):

```
M_total = M_last · M_{...} · M_first
```

This is **right-to-left** — the sequence of optical elements is multiplied
in reverse propagation order. Each element's individual ABCD matrix is defined
for light traveling left to right.

## q-parameter sign

The complex beam parameter is:

```
1/q = 1/R − iλ/(π w²)
```

This assumes the time dependence e^{−iωt}. Under the engineering sign convention
e^{+iωt}, the imaginary part of 1/q flips sign.

**References**: Siegman (1986) Lasers, Trebino (2000) FROG, Diels and Rudolph
(2006) Ultrashort Laser Pulse Phenomena.
