---
skill_id: reasoning.uo.attosecond_pulse_generation
type: reasoning
summary_50t: >
  HHG three-step model: tunnel ionization → acceleration → recombination →
  XUV burst. Attosecond pulse train (APT) from multi-cycle driver: comb of
  odd harmonics → τ ∼ 100 as bursts each half-cycle. Isolated attosecond
  pulse (IAP): amplitude gating (few-cycle driver), polarization gating
  (time-dependent ellipticity), double optical gating (DOG), attosecond
  lighthouse. Attosecond streaking: IR dressing field → photoelectron
  spectrogram → FROG-CRAB retrieval. CEP control essential.
trigger:
  - designing attosecond beamlines for HHG-based XUV sources
  - choosing IAP gating technique for a given driver laser
  - interpreting attosecond streaking measurements
reasoning_role: attosecond_pulse_generation
parent: reasoning.uo.mode_locking_passive
retrieval_cost: 1
sign_convention: >
  HHG cutoff: E_cutoff = I_p + 3.17 U_p where U_p = e²E₀²/(4mω²) ∝ I λ².
  APT: train of pulses separated by T/2 (half laser period). IAP: single
  pulse within one or few laser cycles. Streaking: vector potential A_L(t)
  of IR field maps electron momentum to time.
references:
  - ultrafast-optics: reasoning.uo.carrier_envelope_phase (CEP for IAP)
  - electrodynamics: reasoning.em.nonlinear_optical_response (HHG nonlinearity)
  - plasma: reasoning.plasma.laser_plasma_interaction (HHG in plasma context)
---

# reasoning.uo.attosecond_pulse_generation — HHG → XUV Burst → IAP

## Core Picture

When an intense femtosecond laser pulse (I ∼ 10¹⁴ W/cm²) is focused into a
gas target, the electric field can tunnel-ionize an atom. The freed electron
is accelerated by the laser field, and when the field reverses direction,
the electron can recollide with the parent ion, releasing its kinetic energy
as an extreme ultraviolet (XUV) photon burst lasting ∼100 attoseconds. This
is the three-step model of High-Harmonic Generation (HHG). By controlling
the driving laser's carrier-envelope phase (CEP) and using temporal gating
techniques, a single isolated attosecond pulse (IAP) can be generated —
the shortest controlled events ever created (Corkum 1993, Krausz 2001,
PUILS-XIII).

## Derivation Sketch

### 1. Three-step model (Corkum 1993)

**Step 1 — Tunnel ionization**: The strong laser field (E ∼ 10¹⁰ V/m)
suppresses the Coulomb barrier → electron tunnels out near the field maximum.
Ionization rate: ADK (Ammosov-Delone-Krainov) formula:
```
w(t) ∝ exp(−2(2I_p)^{3/2}/(3|E(t)|))
```
Occurs within ∼0.5 fs around each field crest.

**Step 2 — Acceleration**: The free electron is driven by the laser field.
In the strong-field approximation (neglecting the Coulomb potential after
ionization):
```
m dv/dt = −e E_L(t)
v(t) = −(e/m) ∫_{t_i}^t E_L(t') dt' = −(e/m)[A_L(t) − A_L(t_i)]
```
The electron acquires kinetic energy E_kin(t). For the optimal ionization
phase (∼17° after the field maximum for a cosine pulse), the electron
returns with maximum energy.

**Step 3 — Recombination**: At t_r when x(t_r) = 0, the electron recollides
with the parent ion. The kinetic energy plus the ionization potential is
released as an XUV photon:
```
ℏω_XUV = I_p + E_kin(t_r)
```

### 2. HHG spectrum and cutoff

The harmonic spectrum consists of odd harmonics of the driving frequency
(for a centrosymmetric target gas). The spectrum has three regions:
- **Perturbative** (low orders, n < ∼10): rapid drop-off, ∝ I^n
- **Plateau** (n ∼ 10 to cutoff): nearly constant yield over many harmonics
- **Cutoff**: E_cutoff = I_p + 3.17 U_p where U_p ∝ I λ² (ponderomotive energy)

**Cutoff scaling** (Corkum 1993):
```
U_p[eV] = 9.33 × 10⁻¹⁴ I[W/cm²] × (λ[μm])²
E_cutoff = I_p + 3.17 U_p
```
For Ar (I_p = 15.8 eV) with 800 nm, 10¹⁴ W/cm²: U_p ≈ 6 eV, E_cutoff ≈ 35 eV.
For Ne (I_p = 21.6 eV) with 800 nm, 5×10¹⁴ W/cm²: U_p ≈ 30 eV, E_cutoff ≈ 117 eV.

### 3. Attosecond pulse train (APT) from multi-cycle drivers

Each half-cycle of the driving laser produces one XUV burst at the field
maximum → a train of attosecond pulses separated by T₀/2 (∼1.3 fs at 800 nm).
In the frequency domain: comb of odd harmonics (2k+1)ω₀.

For a multi-cycle (∼30 fs) driver: train of ∼15-20 attosecond pulses.
Not isolated, but useful for:
- RABBITT (Reconstruction of Attosecond Beating By Interference of
  Two-photon Transitions)
- Attosecond transient absorption spectroscopy (ATAS)

### 4. Isolated attosecond pulse (IAP) — gating techniques

**Amplitude gating** (few-cycle driver, τ_p < 5 fs):
- With a CEP-stabilized few-cycle pulse, only the CENTRAL half-cycle is
  intense enough to generate HHG cutoff harmonics.
- Filter the cutoff region (highest harmonics) → single IAP.
- Simplest method, but requires sub-5-fs driver.

**Polarization gating** (Corkum 1994):
- Use two counter-rotating circularly polarized pulses with a small delay.
- The polarization is linear only during a brief temporal window (<1 fs)
  → HHG gated to a single half-cycle.
- Produces IAP with >5 fs drivers. Depends critically on delay precision.

**Double optical gating (DOG)** (Mashiko 2008):
- Polarization gating + second-harmonic field → extends the ellipticity
  window → cleaner gate.

**Attosecond lighthouse** (Vincenti 2012):
- Wavefront rotation (spatial chirp) + angular filtering → spatial gating.
- Each attosecond pulse is emitted in a different direction → single pulse
  selected by aperture.

### 5. Attosecond streaking characterization

An IAP is too short for FROG/SPIDER. Instead, attosecond streaking is used:

**Streaking principle** (Itatani 2002):
```
XUV IAP → gas target → photoelectrons
           ↑ IR dressing field (few-cycle, CEP-controlled)
```
The IR field's vector potential A_L(t) imparts a momentum shift to
photoelectrons. By scanning the XUV-IR delay τ, a streaking spectrogram
is recorded: P(E_kin, τ).

**FROG-CRAB retrieval** (Frequency-Resolved Optical Gating for Complete
Reconstruction of Attosecond Bursts): The streaking spectrogram is a FROG
trace. The GP algorithm (same as standard FROG) retrieves the attosecond
pulse amplitude and phase.

**Attosecond pulse duration record**: 43 as (Gaumnitz 2017, using HHG in
Ne gas with sub-2-cycle 1.8 μm driver).

## Algorithm — Given Driver Laser → IAP Design

```
1. SELECT target gas: Ne (high I_p → high cutoff), Ar (lower cutoff,
   higher flux), He (highest cutoff). Gas cell or gas jet.

2. COMPUTE cutoff: E_cutoff = I_p + 3.17 U_p. Ensure filter can select
   cutoff region. XUV filters: metal foils (Al for 17-72 eV, Zr for
   60-120 eV).

3. CHOOSE gating:
   - τ_driver < 5 fs + CEP-stabilized → amplitude gating (simplest).
   - τ_driver > 5 fs → polarization gating or DOG.
   - For the ultimate shortest IAP: few-cycle + amplitude gating.

4. PHASE MATCHING: HHG is a coherent buildup process. Requires:
   - Neutral gas dispersion + plasma dispersion + geometric (Gouy) phase
     to be balanced.
   - Phase matching pressure: P_opt ∼ few-100 mbar.
   - Absorption limit: L_abs ∼ 1/(n σ_abs).

5. XUV OPTICS: Multilayer mirrors (Mo/Si for ∼90 eV, bandwidth ∼5 eV).
   Filter for fundamental. XUV spectrometer (grating + CCD/MCP).

6. CHARACTERIZE: Attosecond streaking → FROG-CRAB → τ_IAP, φ(ω).
```

## Cross-References

- PUILS-XIII §1-4; Corkum 1993; Krausz 2001; Gaumnitz 2017
- ultrafast-optics: reasoning.uo.carrier_envelope_phase (CEP for gating)
- ultrafast-optics: reasoning.uo.mode_locking_passive (few-cycle driver)
- electrodynamics: reasoning.em.nonlinear_optical_response (χ⁽ⁿ⁾ in HHG)
- plasma: reasoning.plasma.laser_plasma_interaction (HHG in plasma, relativistic regime)
- ultrafast-optics: knowledge.uo.attosecond_physics_data (HHG data, IAP records)
