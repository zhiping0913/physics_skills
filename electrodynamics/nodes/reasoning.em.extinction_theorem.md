---
skill_id: reasoning.em.extinction_theorem
type: reasoning
summary_50t: >
  Extinction theorem = Stratton-Chu plus equivalence principle: tangential fields
  on a closed surface can be replaced by equivalent electric/magnetic surface
  currents. With stated normal convention, the currents reproduce the field on
  one side and extinguish it on the other; scalar Kirchhoff, Ewald-Oseen, and
  EFIE/MFIE are limiting formulations.
trigger:
  - applying Huygens/equivalence principle with correct surface-current signs
  - deriving Stratton-Chu, aperture radiation, EFIE/MFIE, or Ewald-Oseen extinction
  - deciding whether fields are reproduced inside or outside a closed surface
reasoning_role: equivalence_extinction_theorem
parent: mathematics.vector_green_identities
retrieval_cost: 1
sign_convention: >
  Time dependence e^{-iωt}. S bounds region V; n points outward from V into V+.
  Boundary jumps use n×(H+−H−)=K and n×(E+−E−)=−K*. Thus currents
  K=−n×H, K*=n×E reproduce the interior field and extinguish the exterior.
  The common Love/exterior convention J_s=n×H, M_s=−n×E uses the same outward
  normal to reproduce exterior fields and extinguish interior fields, or the
  reversed normal for the interior problem.
---

# reasoning.em.extinction_theorem — Huygens currents reproduce one side, cancel the other

## Core Picture

The extinction theorem says that fields on a closed surface S can be replaced by
surface currents that generate the original field on one side of S and exactly
zero field on the other side. It is not an approximation: it is Green's identity
(Stratton-Chu) plus Maxwell boundary jump conditions.

This node fixes the sign convention explicitly because the two common current
notations differ by normal orientation:

- S bounds region V, n points outward from V into the exterior V+.
- Interior fields are E-,H-; exterior fields are E+,H+.
- Surface electric current K and magnetic current K* satisfy
  ```
  n × (H+ - H-) = K,
  n × (E+ - E-) = -K*.
  ```

Therefore, to reproduce the interior field E,H in V and extinguish the exterior:
```
E- = E,   H- = H,      E+ = 0,   H+ = 0
K  = - n × H,
K* =   n × E.
```
The frequently used Love/exterior equivalent currents
```
J_s = n × H,
M_s = - n × E
```
with the same outward normal reproduce the exterior field and extinguish the
interior. They are the same theorem with the kept/zero side interchanged (or with
normal reversed).

Compact sign mnemonic: `J_s=n×H, M_s=-n×E` for exterior reproduction with
outward object normal; `K=-n×H, K*=n×E` for interior reproduction/exterior
extinction with the outward-from-V convention used here.

## Derivation Sketch

### 1. Stratton-Chu from vector Green identities

For source-free fields in V satisfying Maxwell/Helmholtz equations, apply the
vector Green identity from `mathematics-theorems: mathematics.vector_green_identities`
with scalar outgoing Green function G=e^{ikR}/(4πR). For r in V:
```
E(r) = ∮_S [ iωμ (n×H) G
           + (n×E)×∇G
           + (n·E) ∇G ] dS,
```
with an analogous expression for H. For r outside V, the same closed-surface
integral gives zero (up to the usual 1/2 limiting value on a smooth boundary).
This is the vector Huygens principle: tangential E and H on S are enough to
reconstruct the field on the chosen side.

### 2. Equivalent surface currents

Instead of carrying E,H explicitly in Stratton-Chu, define electric and magnetic
surface currents. For the interior-reproducing convention fixed above:
```
K  = - n × H,
K* =   n × E.
```
The radiated field of these currents in the homogeneous medium filling both
sides of S is
```
(E_eq,H_eq) = (E,H)  inside V,
              (0,0) outside V.
```
The proof is the boundary-jump calculation:
```
n×(H+ - H-) = n×(0 - H) = -n×H = K,
n×(E+ - E-) = n×(0 - E) = -n×E = -K*.
```
Thus the currents produce exactly the discontinuity needed to join the original
field to a zero field. Uniqueness then guarantees the piecewise field is the
solution.

For the exterior-reproducing convention, set interior zero and exterior equal to
E,H. The jumps become
```
J_s = n × H,
M_s = -n × E,
```
and the currents reproduce the exterior field while extinguishing the interior.
This is the convention most often used for scattering from a closed object with
n directed outward from the object.

### 3. Extinction theorem wording

"Extinction" means the equivalent currents emit a field on the zero side that is
exactly the negative of the field that would otherwise be present there. In a
material medium, induced dipoles radiate a forward field that cancels the incident
vacuum wave inside the medium and leaves the refracted wave; this is the
Ewald-Oseen extinction theorem.

## Algorithm — Apply Equivalence/Extinction Without Sign Mistakes

```
1. CHOOSE THE KEPT REGION:
   Decide whether you want fields reproduced inside S or outside S.

2. ORIENT THE NORMAL:
   This node uses n outward from the interior V.
   Keep the boundary jumps fixed:
     n×(H+−H−)=K,   n×(E+−E−)=−K*.

3. SET THE ZERO SIDE:
   Interior reproduction / exterior extinction:
     E−=E, H−=H, E+=0, H+=0 → K=−n×H, K*=n×E.
   Exterior reproduction / interior extinction:
     E−=0, H−=0, E+=E, H+=H → J_s=n×H, M_s=−n×E.

4. COMPUTE RADIATED FIELD:
   Use Stratton-Chu or dyadic Green potentials for the chosen currents.
   For an aperture approximation, integrate only over the aperture and set the
   screen contribution by an impedance/PEC approximation.

5. TAKE BOUNDARY LIMITS IF SOLVING SCATTERING:
   Let r approach S from the exterior/interior. The 1/2 jump terms produce EFIE,
   MFIE, CFIE, PMCHWT, or aperture integral equations.

6. VERIFY:
   Check tangential boundary conditions, power conservation, reciprocity, and
   whether the chosen current signs reproduce the intended side.
```

## Formulation Links

| Level | Theorem/formula | Unknown data on S | Extinction statement | Typical use |
|---|---|---|---|---|
| Scalar | Kirchhoff/Helmholtz integral | U and ∂U/∂n | Aperture field reproduces transmitted scalar wave; screen approximation extinguishes geometric-shadow field | Scalar diffraction, Fresnel/Fraunhofer optics |
| Microscopic optics | Ewald-Oseen extinction | Polarization/dipole radiation in matter | Forward radiation from induced dipoles cancels the incident vacuum wave inside the dielectric, leaving the refracted wave | Refractive index, dispersion, crystal optics |
| Vector | Stratton-Chu | n×E, n×H, sometimes n·E terms | Huygens surface currents reproduce one side of a closed surface and cancel the other | Aperture antennas, near-to-far transforms, vector diffraction |
| Dyadic boundary IE | EFIE/MFIE/CFIE | Equivalent J_s and/or M_s | Limiting forms of the same Green representation enforce zero tangential E on PEC or continuity across dielectric interfaces | MoM scattering and radiation |
| Dielectric surface IE | PMCHWT/Müller | Both electric and magnetic equivalent currents on interface | Interior and exterior representations cancel unphysical fields in the wrong region while enforcing field continuity | Penetrable-body scattering |

## Cross-Domain Table

| Domain | Equivalent source | What is extinguished? | What is reproduced? | Notes |
|---|---|---|---|---|
| Antenna/aperture EM | Huygens J_s=n×H, M_s=-n×E on aperture or closed surface | Field on the side not selected by the equivalence construction | Radiated field in the selected half-space/region | Basis of aperture antennas and near-field to far-field transforms |
| PEC scattering | Induced surface electric current J_s | Incident tangential E on the conductor surface | Scattered field outside; total tangential E=0 on PEC | EFIE uses n×(E_inc+E_scat)=0; MFIE uses magnetic-field boundary limit |
| Dielectric scattering | Paired electric/magnetic currents on material interface | Nonphysical continuation of each medium's field into the other medium | Correct interior and exterior fields satisfying tangential continuity | PMCHWT combines two extinction representations |
| Crystal/continuum optics | Bound polarization current -iωP | Incident free-space wave inside matter | Refracted wave with k=nω/c | Ewald-Oseen microscopic explanation of refraction |
| Acoustics | Monopole/dipole layer on boundary | Pressure field on one side of S | Pressure/velocity field on the other side | Scalar analog of single/double-layer potentials |
| Elastic waves | Traction and displacement layer potentials | Elastodynamic field in excluded region | Displacement/stress in retained region | Boundary integral methods mirror EM equivalence |
| **Time-domain reciprocity (antenna)** | **TD Huygens currents J_s(R,t), M_s(R,t) with causal retardation** | **Fields in unselected time-space region** | **Radiated/received pulse at antenna terminals** | **Štumpf 2019 §7: TD reciprocity uses time-convolution form ∫(E_a·J_b − H_a·K_b)dV dt. For a one-port antenna, self-reciprocity relates the transmit effective length to the receive open-circuit voltage: V_oc = h_eff · E_inc (time-domain vector effective height).** |

## Boundary-Integral Consequences

- EFIE: enforce tangential electric field boundary condition using the electric
  field radiated by J_s through the dyadic Green function.
- MFIE: take the magnetic field limit on S; the surface-current operator has a
  ±1/2 identity jump term depending on the side approached.
- CFIE: combine EFIE and MFIE to avoid internal resonance of closed PEC bodies.
- PMCHWT: use both J_s and M_s on dielectric interfaces so exterior and interior
  extinction representations satisfy the same tangential E,H.

## Edge Cases

- Open surfaces/apertures are not exact closed-surface equivalence problems;
  Kirchhoff or physical optics approximations supply the missing screen fields.
- At edges/corners the 1/2 boundary factor is replaced by a solid-angle factor.
- In inhomogeneous backgrounds, the Green function must match the background;
  using free-space G where a layered-medium G is required breaks extinction.
- Sign errors usually show up as fields reproduced on the wrong side. Re-check
  normal direction and whether you are using interior or exterior equivalence.

## Cross-References

- mathematics-theorems: mathematics.vector_green_identities (parent — Stratton-Chu from Green identity)
- electrodynamics: reasoning.em.dyadic_green_function (dyadic potentials for J_s/M_s)
- electrodynamics: reasoning.em.scalar_diffraction_kirchhoff (scalar Kirchhoff limit)
- computational-physics: reasoning.cp.moment_method (EFIE/MFIE discretization by MoM)
