---
skill_id: knowledge.optics.fourier_optics_data
type: knowledge
summary_50t: >
  Coherent CTF H=P(λz f_x,λz f_y), cutoff NA/λ. Incoherent OTF=H★H,
  cutoff 2NA/λ. Fresnel: U∝∫U₀ exp[(ik/2z)(Δ²)]dξ. Fraunhofer: U∝FT{aperture}.
  Holography: |U_o+U_r|²→reconstruct. Apodization: pupil modification→sidelobe control.
trigger: computing imaging resolution, designing spatial filters, holograms
reasoning_role: fourier_data
parent: reasoning.optics.fourier_optics_transfer_function
retrieval_cost: 1
---

# knowledge.optics.fourier_optics_data

**Fresnel diffraction** (N_F=a²/λz): U(x,y)=(e^{ikz}/iλz)∬ U₀ exp[(ik/2z)((x−ξ)²+(y−η)²)]dξdη.
**Fraunhofer** (N_F≪1 or lens focal plane): U(x,y)∝FT{U_aperture} at f_x=x/λz, f_y=y/λz.

**Coherent imaging**: CTF H(f)=P(λz f) (pupil). Cutoff f_c=NA/λ. δx=0.61λ/NA (Rayleigh).
**Incoherent**: OTF(f)=H★H/∫|H|². Cutoff 2NA/λ. δx=0.47λ/NA (Sparrow).
Circular aperture OTF: (2/π)[cos⁻¹(f/f_c)−(f/f_c)√(1−(f/f_c)²)] for f≤2f_c.

**Apodization**: modify P to reshape PSF. Gaussian P→Gaussian PSF (no sidelobes),
wider main lobe. Semicircular: sidelobe suppression with minimal broadening.

**Phase contrast** (Zernike): add π/2 to DC in Fourier plane. I(x)∝1+2Δφ(x).
Visible for Δφ∼0.1 rad. **Schlieren**: knife edge blocks half FT → |∇n| imaging.

**Holography**: record I=|U_o+U_r|². Reconstruct: U_r·I=U_r|U_r|²+U_r|U_o|²+U_r²U_o*+|U_r|²U_o.
Last term = original object wave. Off-axis (angle θ): terms separated if θ>arcsin(3f_cλ).

**Talbot effect**: grating at z=N·2d²/λ self-images (Talbot length z_T=2d²/λ).

- Goodman §4-9
