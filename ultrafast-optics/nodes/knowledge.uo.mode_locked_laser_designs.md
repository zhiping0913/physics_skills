---
node_type: knowledge
domain: ultrafast-optics
topic: mode_locked_laser_designs
tags: [Ti:sapphire, KLM, SESAM, fiber laser, cavity design, astigmatism compensation, Z-fold, ring cavity, thin-disk, VECSEL, MIXSEL]
citations:
  - "Weiner, §6-7"
  - "Diels-Rudolph, §6"
  - "Siegman, §27"
---

# Mode-Locked Laser Designs — Practical Architectures

## Ti:sapphire KLM Oscillator (canonical femtosecond source)

**Cavity**: Astigmatically compensated Z-fold (or X-fold)
```
OC -- M1 -- Ti:S -- M2 -- prism1 -- prism2 -- HR
         \           /
          \--fold--/
```
- Crystal: Ti:sapphire, 2-3 mm, Brewster-cut, pumped by 532 nm CW (DPSS)
- Curved mirrors: R = 10 cm, separation ≈ crystal length + ~2 mm
- Prism pair: SF10 or fused silica, L_sep ≈ 30-60 cm → net anomalous GDD
- Output coupler: 2-5% transmission

**Performance**: τ_p = 5-100 fs, P_avg = 0.5-3 W, f_rep = 80-100 MHz,
E_p = 5-30 nJ, P_peak = 50-500 kW.

**Self-starting**: Requires perturbation. Common techniques:
- Tap cavity mirror (mechanical)
- Slow SESAM integrated into HR (SESAM-assisted KLM) → reliable self-starting
- Transient electronic perturbation of pump laser

## SESAM Mode-Locked Solid-State Lasers

**Yb:YAG thin-disk oscillator**:
- Gain: Yb:YAG thin disk (100-200 μm), multi-pass pump (940 nm)
- Average power: 10-100 W, τ_p = 200 fs–1 ps, f_rep = 10-100 MHz
- SESAM: ΔR ≈ 1-2%, F_sat ≈ 50 μJ/cm², τ_A ≈ 1-10 ps
- Cavity: long (∼1-10 m), multiple reflections off disk

**Er:Yb:glass (ERGO) miniature laser**:
- Telecom wavelength 1.55 μm, τ_p = 150-500 fs, f_rep = 10-50 GHz
- SESAM directly coated on one cavity mirror
- Very compact (mm-scale), used in telecom test equipment

## Fiber Oscillators

**Er fiber laser (1550 nm), NPE mode-locked**:
```
Pump → WDM → EDF → ISO → PC → Output coupler → SMF → back to WDM
```
- Gain: Er-doped fiber (EDF), pumped 980 nm
- NPE: Quarter-wave + half-wave + polarizing beamsplitter
- Net-anomalous GDD from SMF-28 fiber (D ≈ +17 ps/(nm·km))
- τ_p = 50-200 fs (soliton), E_p = 0.1-1 nJ

**Yb fiber CPA system** (high-energy scaling):
- Oscillator: NPE or SESAM, τ_p = 100 fs–1 ps, E_p = 1-10 nJ
- Stretcher: Chirped fiber Bragg grating (CFBG) or grating pair
- Amplifier: Double-clad Yb fiber, multi-stage (preamp + power amp)
- Compressor: Transmission grating pair (high efficiency)
- Output: 10-100 μJ, 100 kHz–1 MHz, τ_p = 100-300 fs

## High-Repetition-Rate Designs

**Harmonically ML fiber laser**:
- SESAM + intracavity etalon to select harmonic
- f_rep = 10-100 GHz, locking multiple pulses per round-trip
- Supermode suppression: comb filter, long cavity for narrow linewidth

**MIXSEL (Modelocked Integrated eXternal-cavity Surface Emitting Laser, Keller 2010)**:
- Semiconductor gain + SESAM integrated in one epitaxial structure
- f_rep = 1-100 GHz, τ_p = 200 fs–few ps, P_avg = 10-100 mW
- No external cavity alignment needed — fully integrated

## Few-Cycle Pulse Generation

**Sub-2-cycle Ti:sapphire oscillator** (Ell 2001):
- Octave-spanning spectrum (600-1200 nm) via double-chirped mirrors
- Net GDD ∼ 0 (balanced by DCM), broad-band KLM
- CEP stabilized via f-2f interferometer + feedback to pump power
- τ_p < 6 fs (∼2 optical cycles at 800 nm)

**Hollow-core fiber compression** (Nisoli 1996):
- Ti:sapphire CPA output (∼25 fs) → noble-gas-filled hollow fiber
- SPM broadens spectrum → chirped mirror compressor → <5 fs
- Pulse energy: 0.1-5 mJ → GW peak power, few-cycle

## Cavity Stability and KLM Design Rules

**Astigmatism compensation** (Kogelnik 1972):
- Brewster-angle crystal introduces different sagittal and tangential foci
- Fold mirrors at angle θ: sagittal focus f_s = f/cos θ, tangential f_t = f·cos θ
- Compensated when mirrors are separated by ∼R sin θ tan θ from crystal center

**KLM stability zone**:
- Operate near inner edge of stability zone (g₁g₂ ≈ 1, one g close to 1)
- KLM strength δ = (1/w)(dw/dP) is maximum at stability edge
- Trade-off: closer to edge → stronger KLM, but more sensitive to misalignment

**CW breakthrough avoidance**:
- SESAM: ΔR > 1% typically sufficient for clean ML
- KLM: alignment-sensitive; pump beam waist must be slightly smaller than
  cavity mode waist at crystal
