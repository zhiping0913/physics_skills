---
skill_id: reasoning.lp.plasma_diagnostics_lpi
type: reasoning
summary_50t: >
  Laser-plasma diagnostics: proton radiography (E/B field imaging,
  resolution ~μm, temporal ~ps), optical probing (interferometry,
  shadowgraphy, schlieren — electron density maps), X-ray spectroscopy
  (K_α, bremsstrahlung, betatron — T_e, n_e and energetic electron
  info), neutron time-of-flight (ion temperature, ρR in ICF). Multi-
  diagnostic integrated approach for LPI experiments.
trigger:
  - choosing diagnostic method for specific plasma parameter measurement
  - interpreting proton radiography images (field reconstruction)
  - understanding what each diagnostic measures (and doesn't measure)
reasoning_role: plasma_diagnostics
parent: reasoning.lp.laser_absorption_mechanisms
retrieval_cost: 1
sign_convention: >
  Proton deflection angle ∝ ∫∇(n_e B) dz. Optical phase shift
  Δφ = (2π/λ) ∫(N−1)dz ∝ ∫n_e dz (interferometry). K_α at 8.05 keV (Cu),
  2.01 keV (Si), 3.69 keV (Ca). Neutron time-of-flight Δt → energy spread.
---

# reasoning.lp.plasma_diagnostics_lpi — Multi-Method Plasma Characterization

## Core Picture

Laser-plasma interactions create extreme conditions (TV/m fields, 100 Mbar
pressure, keV–MeV particles) over ps-mm scales. No single diagnostic can
fully characterize this. The standard approach combines: (1) proton
radiography for E/B field imaging, (2) optical probing for electron density,
(3) X-ray spectroscopy for temperature and energetic electrons, and (4)
neutron diagnostics for ICF. The key principle: each diagnostic has blind
spots — integrated measurements are essential (Hutchinson, HPP-3).

## Derivation Sketch

### 1. Proton radiography — E/B field imaging

Laser-accelerated protons (TNSA, typically 1–50 MeV) traverse the plasma.
Deflection by E and B fields:
```
Δθ = (e/m_p v_p²) ∫ (E_⟂ + v_p × B) dz
```
where E_⟂ is transverse to the proton trajectory.

**Resolution**: δx ≈ L Δθ, with magnification M = (L_det+L_obj)/L_obj.
Spatial resolution: ~few μm (limited by proton source size). Temporal:
~ps (proton bunch duration from TNSA).

**Field reconstruction**: measure proton deflection pattern → invert
Poisson-type equation for field distribution. Requires multiple proton
energies for tomographic reconstruction (discriminate E vs B).

**Typical sensitivity**: E > 10⁷ V/m, B > 10 T at 10 MeV proton energy,
50 μm spatial resolution.

**Worked example**: For 10 MeV protons (v≈0.14c), L=1 mm, 1 mrad deflection:
  Δθ_min = e B_min L / (m_p v) → B_min = m_p v Δθ_min/(e L) ≈ 10 T.
  At 50 MeV (v≈0.3c): sensitivity improves to B_min ≈ 2 T.

### 2. Optical probing — density measurement

Laser probe beam (typically frequency-doubled, synchronized) intersects
plasma. Three configurations:

| Method | Measures | Spatial res. | Temporal res. |
|--------|----------|-------------|---------------|
| **Interferometry** (Nomarski/shearing) | n_e (from phase shift) | ~μm | ~ps |
| **Shadowgraphy** | ∇²n_e (refraction) | ~μm | ~ps |
| **Schlieren** | ∇n_e | ~10 μm | ~ps |

**Phase shift in interferometry**:
```
Δφ = (2π/λ_probe) ∫ (N−1) dz = −(e²λ_probe/4π²ε₀m_ec²) ∫ n_e dz
```
where N = √(1−n_e/n_c_probe) is the refractive index.

For λ_probe = 400 nm (2ω): fringe shift of 1 = n_e L ≈ 1.7×10¹⁷ cm⁻².
For mm-scale plasma with n_e ~ 10¹⁹ cm⁻³: ~60 fringe shifts — resolvable.

### 3. X-ray spectroscopy

**K_α emission**: cold K-shell lines identify target material and provide
spatial fiducial. Cu K_α at 8.05 keV — standard for electron transport
imaging.

**Bremsstrahlung continuum**: slope gives hot electron temperature.
```
dN_γ/dE ∝ exp(−E/k_B T_hot)    [thermal bremsstrahlung]
```

**Betatron X-rays**: from LWFA/DLA electrons. Synchrotron-like spectrum
with critical energy ℏω_c ∝ γ². Spectral analysis → γ and a₀.

**X-ray spectrometers**: HOPG (Highly Oriented Pyrolytic Graphite) crystal
for keV range, transmission grating for sub-keV. Resolving power E/ΔE ~ 100–1000.

### 4. Impurity radiation diagnostics (VTP Vol.12, 1984)

In magnetically confined fusion plasmas, impurity ions — sputtered from
walls or intentionally seeded — dominate the radiative power balance.
Key diagnostics (VTP Vol.12, Vainshtein & Shevelko review):

**Coronal equilibrium model**: at low density (n_e < 10¹³ cm⁻³ for visible,
< 10¹⁶ cm⁻³ for XUV), collisional excitation is balanced by radiative decay
(no collisional de-excitation). The line intensity:
```
I_λ = n_e n_Z ⟨σv⟩_exc B_λ    [photons/cm³/s]
```
where ⟨σv⟩_exc is the excitation rate coefficient (van Regemorter formula)
and B_λ is the branching ratio. This provides local n_Z from measured I_λ.

**Z_eff diagnostic**: the effective charge
```
Z_eff = Σ_Z n_Z Z² / n_e    [≥ 1, = 1 for pure hydrogen]
```
is measured from bremsstrahlung continuum slope (dN_γ/dE ∝ Z_eff exp(−E/T_e))
or from visible bremsstrahlung (VB) at λ ∼ 523 nm. Z_eff > 2 indicates
significant impurity contamination → enhanced radiation losses.

**Radiation power loss**: P_rad = n_e Σ_Z n_Z L_Z(T_e) where L_Z(T_e) is
the cooling rate (coronal equilibrium). For carbon at 100 eV: L_C ∼ 10⁻³¹
W·m³; for tungsten at 1 keV: L_W ∼ 10⁻³² W·m³. P_rad can exceed P_α
(fusion alpha heating) if Z_eff is too high → radiative collapse.

### 4. Neutron diagnostics (ICF)

In DT ICF implosions:
- **Neutron yield**: total fusion yield via activation (Cu, In) or
  scintillator detectors.
- **Neutron time-of-flight (nTOF)**: neutron energy spread → ion
  temperature (Gaussian broadening at high T_i).
- **Neutron imaging**: penumbral or pinhole imaging → burn region size.
- **Areal density (ρR)**: from neutron down-scattering fraction
  (DT neutrons at 14.1 MeV lose energy when scattering in dense fuel).

### 5. Integrated diagnostic strategy

For a typical laser-plasma experiment:
```
Phase 1: optical probing → n_e profile, shock position.
Phase 2: X-ray spectroscopy → T_e, T_hot from bremsstrahlung.
Phase 3: proton radiography → E/B field structure.
Phase 4: (IF ICF) neutron diagnostics → T_i, ρR, burn symmetry.
```

## Algorithm — Choosing Diagnostics for LPI Experiment

```
1. ELECTRON DENSITY: interferometry/shadowgraphy (n_e up to n_c_probe).
   For n_e > n_c: X-ray radiography (higher energy probe).

2. ELECTRON TEMPERATURE: Thomson scattering (local T_e, n_e),
   bremsstrahlung slope (hot electron T_hot, line-integrated).

3. MAGNETIC FIELDS: proton radiography (>MG), Faraday rotation
   (polarization rotation of optical probe, < MG).

4. ELECTRIC FIELDS: proton radiography, Stark broadening of spectral lines.

5. ION TEMPERATURE: neutron TOF (>1 keV), Doppler broadening of
   impurity lines (<1 keV), collective Thomson scattering.

6. ρR (ICF): neutron down-scatter, proton slowing (knock-on deuterons).
```

## Edge Cases

- **Refraction limitations**: for large density gradients (∇n_e > 10²⁰ cm⁻⁴),
  optical probes are refracted out of collection optics → no signal.
  Use shorter λ_probe or X-ray probing.
- **Proton source brightness**: TNSA produces ~10¹² protons/shot, but only
  ~10⁸ at >10 MeV → low statistics at high energy.
- **Non-Maxwellian electrons**: bremsstrahlung slope fitting assumes Maxwellian
  T_hot. If the spectrum is non-Maxwellian (DLA, direct injection), the slope
  is NOT a temperature → need full spectral modeling.

## Cross-References

- Hutchinson, *Principles of Plasma Diagnostics* (2002)
- HPP-3, McKenna §7
- laser-plasma: reasoning.lp.laser_absorption_mechanisms (parent — absorption determines T_e, n_e)
- laser-plasma: reasoning.lp.tnsa_ion_acceleration (TNSA proton source for radiography)
- laser-plasma: knowledge.lp.electron_acceleration_scaling (betatron X-ray diagnostics)
