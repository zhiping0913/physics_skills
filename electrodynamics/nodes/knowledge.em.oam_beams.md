---
node_type: knowledge
domain: electrodynamics
topic: oam_beams
tags: [orbital angular momentum, OAM, Laguerre-Gauss, Bessel beam, twisted wavefront, vortex beam, Hansen vector, SAM-OAM, metasurface, multiplexing]
citations:
  - "Papathanasopoulos, Tang, Yu & Yin (eds), *Electromagnetic Vortices*, IEEE Press, 2021"
  - "Allen, L., et al., 'Orbital angular momentum of light and the transformation of Laguerre-Gaussian laser modes,' Phys. Rev. A 45:8185, 1992"
  - "Yan, Y., et al., 'High-capacity millimetre-wave communications with orbital angular momentum multiplexing,' Nature Commun. 5:4876, 2014"
---

# Orbital Angular Momentum (OAM) Beams

## The Defining Feature — Helical Phase

An OAM beam is characterized by an azimuthal phase factor exp(ilφ) on its
wavefront, where the integer l is the **topological charge** (azimuthal
quantum number). Each photon carries **OAM = lℏ**, independent of the spin
angular momentum (SAM = ±ℏ from polarization).

**Helical phase ansatz**:
```
E(r, φ, z, t) = u(r, z) exp(ilφ) exp(i(kz − ωt))
```

The exp(ilφ) factor creates a **phase singularity** at r = 0 (undefined φ)
and a **helical wavefront**: the phase gradient ∇S has an azimuthal component
∇S_φ = l/(r sin θ). For l = 1, one complete screw turn per wavelength; for
l = 2, a double helix; etc.

## Laguerre-Gauss Modes (Paraxial)

The paraxial scalar amplitude for an OAM-carrying Laguerre-Gauss mode LG_{p,l}:

```
u_{p,l}(r, z) = (C/w(z)) (r√2/w(z))^|l| L_p^|l|(2r²/w²(z))
              × exp(−r²/w²(z)) exp(ikr²/(2R(z))) exp(iψ_G(z))
```

where:
- L_p^|l| = generalized Laguerre polynomial
- w(z) = beam radius, R(z) = wavefront curvature
- ψ_G(z) = Gouy phase = (2p + |l| + 1) arctan(z/z_R)
- z_R = π w₀²/λ = Rayleigh range

**Mode orthogonality**:
```
∫₀^∞ ∫₀^{2π} u*_{p,l} u_{p',l'} r dr dφ = 0 unless p = p', l = l'
```

## Bessel Beams (Non-Paraxial)

```
E(r, φ, z) = J_l(k_r r) exp(ilφ) exp(ik_z z)
```
with k_r² + k_z² = k₀². Bessel beams are **diffraction-free** over a finite
range (limited by the physical aperture). They carry OAM = lℏ per photon
and are the non-paraxial generalization of LG beams.

## Twisted Wavefront Geometry

The phase of an OAM beam generalizes standard wavefronts:
```
S_plane    = k · r          (constant gradient, no OAM)
S_sphere   = k₀ r           (radial gradient, no OAM)  
S_twisted  = k₀ r + lφ      (radial + azimuthal gradient, OAM = lℏ)
```

**Far-field cone angle**: the angular spread of an OAM beam scales as
```
θ_c = sin^{−1}(√(2|l|) / (k₀ w_g))
```
where w_g is the Gaussian waist of the generating beam. Larger |l| →
larger cone angle. The √l scaling is a consequence of the azimuthal momentum
contribution to the total transverse momentum.

**Aperture efficiency**: OAM beams suffer from reduced aperture efficiency
compared to a standard Airy disk. For l = 1, the efficiency is ~50% of the
Airy disk power within the main lobe. The efficiency decreases with
increasing |l|.

## Hansen Vector Wave Function Unification

The azimuthal index m in Hansen M_nm, N_nm (see `knowledge.em.vector_wave_functions`)
**is** the OAM quantum number l. Three formulations share the same exp(ilφ)
structure:

| Formulation | Azimuthal dependence | OAM per photon | Domain |
|------------|---------------------|----------------|--------|
| Hansen M_nm, N_nm | exp(imφ) | mℏ | Spherical / cylindrical (exact Maxwell) |
| Laguerre-Gauss LG_{p,l} | exp(ilφ) | lℏ | Cylindrical (paraxial) |
| Bessel beam J_l | exp(ilφ) | lℏ | Cylindrical (non-paraxial) |

This unification is fundamental: the OAM beam concept is not a separate
phenomenon but the recognition that the azimuthal index in any cylindrical
or spherical wave expansion carries quantized orbital angular momentum.

## OAM Generation Methods

1. **Spiral Phase Plate (SPP)**: Transparent plate with thickness ∝ lφ/(n−1).
   Transmits a plane wave with an l-dependent helical phase delay.

2. **Holographic grating**: Fork grating — a diffraction grating with an
   l-fold dislocation at center. First-order diffraction carries OAM = lℏ.

3. **Helical reflector**: Spiral-cut mirror — the reflection phase is
   azimuthally dependent.

4. **Metasurface**: 2D array of subwavelength elements with engineered phase.
   Two strategies:
   - **Pancharatnam-Berry (geometric) phase**: CP input → element orientation
     α(r,φ) = lφ/2 → output gains PB phase = ±2α = ±lφ. Spin-orbit conversion:
     SAM (handedness flip) ↔ OAM gain.
   - **Resonance-tuning phase**: Vary resonator dimensions → local phase
     shift from Lorentzian response → φ(r,φ) = lφ profile.

5. **Computer-generated hologram (CGH)**: Digital hologram displayed on SLM.

6. **q-plate**: Liquid-crystal device — topological charge q converts
   SAM to OAM: Δl = ±2q.

## OAM Conservation in Nonlinear Optics

In χ⁽ⁿ⁾ nonlinear processes with OAM input, total OAM is conserved:
```
l_out = Σ l_in          (total OAM conservation)
```
For SHG: l_SH = 2 l_fund. For nth-harmonic: l_n = n × l_1.
Discrete crystal symmetry relaxes conservation: l_out = Σ l_in ± n_crystal × m.
See `reasoning.em.nonlinear_optical_response` §Angular Momentum Conservation.

## Applications

- **Mode-division multiplexing**: Independent data channels on separate l
  values (l = 1, 2, 3, ...). Orthogonality guarantees zero crosstalk in free
  space. Yan-Wang 2014 demonstrated 32 Gbit/s mm-wave OAM multiplexing.

- **Optical tweezers / manipulation**: OAM transfers torque to trapped
  particles → optical spanner. The lℏ angular momentum transfer rotates
  microscopic objects.

- **Twisted radar / imaging**: OAM radar beams encode azimuthal information
  in the l spectrum → single-pulse angular resolution beyond the Rayleigh
  diffraction limit.

- **Quantum information**: OAM states form an infinite-dimensional Hilbert
  space (l = −∞ ... +∞) → high-dimensional quantum key distribution (QKD).

## Key Takeaways

1. OAM beam = exp(ilφ) helical phase → lℏ per photon, independent of SAM.
2. Three equivalent formulations: Hansen M,N (exact Maxwell), Laguerre-Gauss
   (paraxial), Bessel (non-paraxial) — all share azimuthal index = OAM number.
3. Twisted wavefront S = k₀ r + lφ introduces phase singularity at r = 0.
4. OAM is conserved in χ⁽ⁿ⁾ nonlinear processes: l_n = n × l_1.
5. Generation methods span from SPP to metasurface (PB phase) to q-plate.
6. Applications: multiplexing, tweezers, twisted radar, quantum information.
