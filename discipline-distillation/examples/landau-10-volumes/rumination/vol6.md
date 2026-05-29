# Volume 6 Rumination Report — REDO

Date: 2026-05-26. Re-read §1-2, §3, §7, §15, §19 of original text with graph nodes loaded.

---

## 1. continuum_limit_to_field_equations — Major Gaps

### Missing: The "physically infinitesimal volume" premise
Landau §1 opens by DEFINING the continuum approximation:
"всякий малый элемент объема жидкости считается все-таки настолько
большим, что содержит еще очень большое число молекул... 'физически'
бесконечно малый объем."

This is THE foundational scale-separation argument of all continuum
mechanics: dV ≪ L_body but dV ≫ a_molecular. Without this premise, the
entire field description (ρ(x), v(x), p(x) as continuous functions) is
unjustified. Our template starts with ∂ρ/∂t+div(ρv)=0 without establishing
WHY we can talk about ρ(x) as a continuous field in the first place.

### Missing: Eulerian description framing
Landau §1: "v(x,y,z,t) есть скорость жидкости в каждой данной точке
x,y,z пространства в момент времени t, т.е. относится к определенным
точкам пространства, а не к определенным частицам жидкости."

Our template jumps to the substantial derivative without first
establishing that the basic description is EULERIAN (fields at fixed
spatial points). This is crucial because the substantial derivative
d/dt = ∂/∂t + v·∇ is precisely the translation from Eulerian to
Lagrangian description. Without this framing, the substantial derivative
appears as a mysterious non-linear term rather than a logical consequence
of the Eulerian description choice.

### Missing: §7 momentum flux tensor — foundation of Navier-Stokes
Landau derives Π_ik = pδ_ik + ρ v_i v_k as the momentum flux tensor
for ideal fluid. This is not a side note — it is THE form in which the
Euler equation is written: ∂(ρv_i)/∂t = −∂Π_ik/∂x_k. In §15, Navier-Stokes
is obtained by ADDING the viscous stress σ'_ik to Π_ik: Π_ik → pδ_ik +
ρ v_i v_k − σ'_ik. This structural connection is completely absent from
our template. An agent reading the Navier-Stokes node would not understand
WHERE in the Euler equation the viscous term is inserted.

### Oversimplified: The adiabatic condition
Our template: "Energy: ρT(∂s/∂t + v·∇s) = 0 (ideal, adiabatic)."
Landau's actual treatment (§2) goes through FOUR forms:
1. ds/dt = 0 (following a particle)
2. ∂s/∂t + v·grad s = 0
3. ∂(ρs)/∂t + div(ρsv) = 0 ("continuity equation for entropy")
4. s = const (isentropic — special case when s uniform initially)
The fourth form (isentropic) is what allows writing ∇p/ρ = ∇w where
w = enthalpy. Our template collapses all this into one line, missing
the key distinction between adiabatic (ds/dt=0 per particle) and
isentropic (s=const everywhere).

### Missing: Enthalpy form of Euler equation
Landau §2 derives ∇p/ρ = ∇w (for isentropic flow), giving the alternative
form ∂v/∂t + (v·∇)v = −∇w. This is used extensively in Bernoulli's
theorem and compressible flow. Our template never mentions enthalpy.

### Priority: high
### Fixes needed:
1. Add "physically infinitesimal volume" to Core Picture
2. Add Eulerian description framing
3. Add §7 momentum flux tensor and connection to §15
4. Expand adiabatic condition into distinct forms
5. Add enthalpy form

---

## 2. constitutive_relation_from_symmetry — One Gap

### Missing: Connection to ideal momentum flux tensor
The derivation in §15 starts from the ideal momentum flux Π_ik = pδ_ik +
ρv_i v_k and adds σ'_ik. Our template presents the viscous stress
derivation in isolation without showing WHERE it fits into the existing
Euler equation structure. The line:
"уравнение движения вязкой жидкости можно получить, прибавив к
'идеальному' потоку импульса (7.2) дополнительный член σ'_ik"

This direct structural connection between §7 and §15 is not in our
template. Fix: add to Algorithm step 1: "Start from ideal momentum flux
Π_ik = pδ_ik + ρv_i v_k. Viscous fluid: Π_ik → Π_ik − σ'_ik."

### Priority: med

---

## 3. dimensional_analysis_to_similarity — No Issues
Reynolds number derivation is clear and correctly captured. Connection
to Π-theorem already added via Vol.1 rumination fix.

---

## 4. Hidden Parent Nodes — One Candidate

### timescale_separation (already added in Vol.1 rumination)
The "physically infinitesimal volume" concept is itself a scale-separation
argument. Could connect continuum_limit to timescale_hierarchy, but
that parent was designed for timescales, not length scales.

### Candidate: reasoning.scale_separation_spatial
Separate from timescale_hierarchy — this is about LENGTH scale separation.
Children would include: continuum_limit (Vol.6), multipole_expansion (Vol.2),
spatial_dispersion (Vol.8). All involve: macro-scale ≫ micro-scale →
effective description.
Priority: low. Worth noting but maybe not worth a separate node yet.

---

## 5. Summary

### Rewrite fixes: 6

| # | Node | Issue | Priority |
|---|------|-------|---------|
| 1 | continuum_limit | Add physically infinitesimal volume premise | high |
| 2 | continuum_limit | Add Eulerian description framing | high |
| 3 | continuum_limit | Add §7 momentum flux tensor + connection to §15 | high |
| 4 | continuum_limit | Expand adiabatic condition into distinct forms | high |
| 5 | continuum_limit | Add enthalpy form of Euler equation | med |
| 6 | constitutive_relation | Add connection to ideal momentum flux Π_ik | med |

### Rewrite fixes count: 6 (4 high, 2 med).
### Hidden parent candidate: reasoning.scale_separation_spatial (low priority).
