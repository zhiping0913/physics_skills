---
skill_id: knowledge.optics.computational_methods
type: knowledge
summary_50t: >
  RCWA: periodic ε→Fourier+Floquet→eigenvalue/layer. BPM: paraxial FFT
  (split-step) or FD. FDTD: Yee, Δt<Δx/c√3, PML. FEM: variational+meshing.
  Ray tracing: Snell+Fresnel. Optimization: merit function→damped LS→design.
trigger: selecting computational method for EM/optical simulation
reasoning_role: comp_optics
parent: reasoning.optics.fourier_optics_transfer_function
retrieval_cost: 1
---

# knowledge.optics.computational_methods

**RCWA** (rigorous coupled-wave analysis): Periodic structures (gratings, metasurfaces).
Expand ε(r) in Fourier series, apply Floquet theorem → eigenvalue problem per layer.
S-matrix algorithm cascades layers. Excellent for 1D/2D periodic; memory ∝ N² (N harmonics).

**BPM** (beam propagation method): Paraxial (slowly-varying envelope).
FFT-BPM (split-step): propagate in Fourier domain (diffraction) + real domain (refraction).
FD-BPM: Crank-Nicholson, handles wide-angle via Padé approximants. Best for waveguides, fibers.

**FDTD** (Yee algorithm): Full Maxwell, time domain. Δx<λ_min/10. Δt<Δx/(c√3) (3D).
PML (Berenger): absorbs outgoing waves, <−60dB reflection. Total-field/scattered-field
formulation for scattering. Broadband: single run→FFT→full spectrum.

**FEM**: Weak formulation, adaptive meshing. Best for complex geometries, resonances.
COMSOL, Ansys HFSS. Eigenmode solvers for cavity/waveguide problems.

**Ray tracing**: Snell's law + Fresnel coefficients. For lenses, mirrors, prisms.
Sequential (imaging) vs non-sequential (illumination, stray light).
Merit function optimization: damped least-squares. Global: simulated annealing, genetic.

- Jarem & Banerjee §1-8
