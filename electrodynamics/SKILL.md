---
name: electrodynamics
description: "Electrodynamics reasoning and knowledge graph — extends landau-graph with boundary-value methods, waveguides, antennas, scattering, crystal optics, coherence theory, and nonlinear/strong-field electrodynamics from 6 standard textbooks. Builds ON landau-graph; landau-graph remains self-contained."
---

# Electrodynamics Skill Graph

Extends `landau-graph` with applied electrodynamics, optics, and strong-field
phenomena. All edges point FROM landau-graph TO this skill; landau-graph is
never modified.

## Source Texts

- Jackson, *Classical Electrodynamics* (3rd ed., 1998)
- Griffiths, *Introduction to Electrodynamics* (5th ed., 2023)
- Lechner, *Classical Electrodynamics: A Modern Perspective* (2018)
- Avetissian, *Relativistic Nonlinear Electrodynamics* (2006)
- Born & Wolf, *Principles of Optics* (7th ed., 1999)

## Graph Structure

- **Reasoning nodes**: Boundary-value methods, waveguide modes, antenna radiation,
  scattering cross sections, optical coherence, nonlinear response
- **Knowledge nodes**: Concrete EM phenomena — method of images, Mie scattering,
  Fabry-Perot, birefringence, SHG, pair production, etc.
- **Edges**: Connects to landau-graph reasoning nodes (prerequisite, reasoning-instance,
  analogy). No reverse edges.

## Distillation Plan

See `/home/zhiping/task/Electrodynamics/distillation-plan.md`
