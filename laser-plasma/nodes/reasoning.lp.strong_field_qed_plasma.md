---
skill_id: reasoning.lp.strong_field_qed_plasma
type: reasoning
summary_50t: >
  Strong-field QED in laser-plasma: quantum parameter χ = eℏ|F·p|/(m³c⁴)
  controls photon emission (nonlinear Compton) and pair production (Breit-
  Wheeler). χ ~ 1 → QED effects dominate. Schwinger field E_cr = m²c³/eℏ
  ≈ 1.3×10¹⁶ V/cm. QED cascades: γ → e⁺e⁻ → γ′ → e⁺e⁻ → ... (avalanche).
  Reachable at I > 10²² W/cm² (ELI-NP, multi-PW). Modifies laser-plasma
  dynamics: radiation reaction, pair plasma generation, opacity.
trigger:
  - computing χ parameter for given laser/plasma conditions
  - determining when QED effects become important
  - analyzing pair production in laser-solid interactions
reasoning_role: strong_field_qed
parent: reasoning.lp.relativistic_transparency
retrieval_cost: 1
sign_convention: >
  χ_e = (eℏ/m³c⁴) √(F_{μν} p^ν)² — Lorentz invariant quantum parameter.
  E_cr = m²c³/eℏ = 1.32×10¹⁶ V/cm. I_cr ≈ 4.6×10²⁹ W/cm² (Schwinger).
  a₀_S = mc²/ℏω ≈ 4×10⁵ at 1 eV (pair production threshold in field).
---

# reasoning.lp.strong_field_qed_plasma — χ Parameter → QED Cascade

## Core Picture

At laser intensities approaching I > 10²² W/cm², the electric field in the
electron rest frame approaches the Schwinger critical field E_cr. In this
regime, quantum electrodynamics (QED) processes — nonlinear Compton
scattering (photon emission by accelerated electrons) and Breit-Wheeler
pair production (γ → e⁺e⁻ in strong field) — become dominant. The
quantum parameter χ governs the rate of these processes. For χ ≳ 1,
QED effects fundamentally alter laser-plasma dynamics: radiation reaction
damps electron motion, pair plasma modifies the dielectric response, and
QED cascades can convert a significant fraction of laser energy into
electron-positron pairs (Di Piazza et al. 2012, Ridgers et al. 2014,
SF-2025).

## Derivation Sketch

### 1. Quantum parameter χ

For an electron with 4-momentum p^μ in an EM field F^{μν}:
```
χ_e = (eℏ/m³c⁴) √(F_{μν} p^ν)²
```

For an electron counter-propagating with a plane wave (a₀):
```
χ_e ≈ 2 γ_e (E_lab/E_cr) ≈ 2 γ_e a₀ (ℏω/mc²)          [lab frame]
```

More conveniently:
```
χ_e ≈ (γ_e a₀) × (ℏω₀/mc²) ≈ 3.8×10⁻⁶ γ_e a₀        [for λ₀=0.8μm]
```

For an electron in LWFA (γ_e ~ 1000) with a₀ = 100: χ_e ≈ 0.38 — entering QED regime.

For an electron with maximum Lorentz factor in a laser field (γ_e ~ a₀):
```
χ_e ≈ a₀² (ℏω₀/mc²)                                     [co-propagating]
χ_e ≈ 2 γ_e a₀ (ℏω₀/mc²) ≈ 2 a₀² (ℏω₀/mc²)              [counter-propagating]
```

### 2. Key QED processes and thresholds

**Nonlinear Compton scattering** (e⁻ → e⁻ + γ):
Electron emits a high-energy photon in the laser field. Rate becomes
significant at χ_e ≳ 0.1.
```
ℏω_γ ≈ 0.44 χ_e γ_e m c² / (1+χ_e^{2/3})               [typical photon energy]
```
For χ_e = 1, γ_e = 1000: ℏω_γ ≈ 220 MeV.

**Breit-Wheeler pair production** (γ → e⁺e⁻):
The emitted photon interacts with the laser field to produce an e⁺e⁻ pair.
Threshold: χ_γ ≳ 0.1 for the photon:
```
χ_γ = (eℏ/m³c⁴) √(F_{μν} k^ν)² ≈ (ℏω_γ/mc²)(E_lab/E_cr)
```
For χ_γ = 1 at λ₀=0.8μm: photon energy threshold ℏω_γ ≈ 2mc²/a₀,
or equivalently a₀ ≳ 100 for multi-MeV photons.

### 3. QED cascades

When χ_e ≳ 1, a self-sustaining avalanche occurs:
```
Laser → e⁻ acceleration → γ emission (Compton) → e⁺e⁻ pair (BW) →
e⁺e⁻ acceleration → more γ → more pairs → ...
```

**Cascade growth rate**:
```
Γ_cascade ≈ α m c² / (ℏ χ_e^{1/3})    [for χ_e ≳ 1]
```

The cascade converts laser energy into a dense e⁺e⁻ plasma. At extreme
intensities (I > 10²⁴ W/cm²), the pair plasma density can exceed the
initial target density → QED plasma regime.

### 4. Conditions for QED-dominated regime

| Parameter | Threshold | Meaning |
|-----------|----------|---------|
| χ_e | > 0.1 | Significant photon emission |
| χ_e | > 1 | Pair production, cascades |
| a₀ | > 10² (with γ~a₀) | χ_e ~ 0.1 at optical |
| a₀ | > 4×10⁵ | Schwinger pair production (vacuum) |
| I (at 0.8μm) | > 10²² W/cm² | χ_e ~ 0.1 for LWFA electrons |
| I (at 0.8μm) | > 10²³ W/cm² | χ_e ~ 1 for reflected electrons |

### 5. Observable signatures

- **Gamma-ray flash**: collimated MeV–GeV photons, fs duration.
- **Pair plasma density**: n_e⁺e⁻ ≫ n_c → new opacity source.
- **Radiation reaction**: electron energy loss limits maximum γ (see R12).
- **Modified reflectivity**: pair plasma changes the dielectric response
  at the critical surface.
- **Positron jets**: angularly separated e⁺ beams from asymmetric cascades.

## Algorithm — Given (a₀, γ_e, λ₀) → QED Regime

```
1. COMPUTE χ_e ≈ 2 γ_e a₀ (ℏω₀/mc²).

2. IF χ_e < 0.01: QED negligible. Classical plasma physics suffices.
   IF 0.01 < χ_e < 0.1: weak QED — photon emission begins, radiation
   reaction becomes noticeable in electron dynamics.
   IF χ_e > 0.1: strong QED — frequent photon emission, pair production
   possible, radiation reaction significant.
   IF χ_e > 1: QED-dominated — cascades, pair plasma.

3. ENERGY LOSS per laser period: δγ/γ ≈ α χ_e a₀ / 3.
   For χ_e=1, a₀=100: δγ/γ ~ 0.24 → 24% energy loss per cycle.

4. PAIR YIELD per laser period: N_pairs ≈ N_γ × P_BW(χ_γ).
   P_BW ≈ 0.23 α χ_γ exp(−8/3χ_γ) for χ_γ ≪ 1.
```

## Edge Cases

- **Spin and polarization effects**: at χ_e ≳ 1, electron spin dynamics
  become important (Sokolov-Ternov effect). The photon emission spectrum
  depends on initial electron spin → spin-polarized pair plasmas possible.
- **Finite laser pulse duration**: cascades require sufficient time to
  develop. τ_cascade ≈ 1/Γ_cascade ≈ few fs at χ_e = 1.
- **Collective plasma effects**: the self-generated pair plasma modifies
  the laser propagation → coupled QED-PIC (PIC with Monte Carlo QED
  modules) needed for self-consistent modeling.

## Cross-References

- Di Piazza et al., RMP 84, 1177 (2012) — comprehensive strong-field QED review
- Ridgers et al., PRL 2014 — QED-PIC simulations
- Avetissian §7-8, SF-2025, Brabec §9
- laser-plasma: reasoning.lp.relativistic_transparency (parent — χ threshold connected to transparency)
- laser-plasma: reasoning.lp.radiation_reaction (radiation losses)
- laser-plasma: reasoning.lp.laser_wakefield_acceleration (LWFA electrons experience χ)
