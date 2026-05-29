# Volume 8 Rewrite Fixes

Status: ALL APPLIED (2026-05-27)

---

## Fix 1: reasoning.causality_to_analyticity — E(t) separation footnote

Node misses the physical rationale for separating the E(t) term in (77.3):
Landau §82 line 11341 footnote: the E(t) term is explicitly extracted to avoid
a δ-function singularity in f(τ) at τ=0. Without this separation, f(τ) would
have a δ-like singularity, making the integral ill-defined.

## Fix 2: reasoning.causality_to_analyticity — UHP no-zeros theorem and monotonicity

§82 proves a theorem the template omits: ε(ω) takes NO real values in any finite
point of the upper half-plane except on the imaginary axis. On the imaginary axis,
ε(ω) monotonically decreases from ε₀>1 (or +∞ for metals) at ω=i0 to 1 at ω=i∞.
Consequence: ε(ω) has NO zeros in the UHP.

## Fix 3: reasoning.causality_to_analyticity — Asymmetry of KK formulas

§82 explicitly notes the practical asymmetry: (82.8), giving ε' from ε'', is
"safe" (any ε''>0 produces a physically possible ε'). (82.7), giving ε'' from ε',
does NOT guarantee ε''>0 — it is not "safe." The algorithm should flag this.

## Fix 4: reasoning.causality_to_analyticity — ε(−ω*) = ε*(ω) for complex ω

The symmetry ε(−ω)=ε*(ω) generalizes to complex ω: ε(−ω*) = ε*(ω) (82.2).
This implies ε(iω'') is real on the imaginary axis. The node only covers real ω.

## Fix 5: reasoning.spatial_dispersion — ε_l(k≠0) does NOT diverge at ω→0

§103 line 14604: The ω=0 pole in ε(ω) for conductors is an artifact of k=0.
For k≠0, ε_l(k,ω) remains finite as ω→0 — no subtraction needed in KK.
This is a qualitatively new effect of spatial dispersion that should be a
Key Insight.

## Fix 6: reasoning.spatial_dispersion — No B-term needed because E↔B linked

§103 lines 14528-14530: One might think the nonlocal response should include
a B term in (103.1). Not needed because E and B are linked by Maxwell:
B-dependence = dependence on spatial derivatives of E = nonlocality already
captured by ε_ik(k).

## Fix 7: reasoning.spatial_dispersion — M=0 convention

§103 lines 14542-14546: With spatial dispersion, the (P,M) split is not unique.
Convenient convention: set M=0, B=H, absorb all averaged microscopic currents
into D. The connection between (ε_l,ε_t) and (ε,μ) at k→0 is given in
Problem 1 (equation in node already, but context missing).

## Fix 8: reasoning.spatial_dispersion — Poynting vector modification

§103 lines 14613-14617: Spatial dispersion adds an extra term to the Poynting vector:
S̄ = (c/8π)Re[E*×B] − (ω/16π)(∂ε_ik/∂k)E_i*E_k.
This is qualitatively new — the energy flux direction is modified by ∂ε/∂k.

## Fix 9: knowledge.continuous.kramers_kronig — Conductor form with 4πσ/ω term

The KK formula for ε'' in conductors has an extra 4πσ/ω term (82.9):
ε''(ω) = −(1/π)P∫ε'(x)/(x−ω)dx + 4πσ/ω.
The node's "one subtraction" form only partially captures this.

## Fix 10: knowledge.continuous.kramers_kronig — Oscillator strength formulation

§82 (82.10-82.11): The standard dispersion theory formulation:
ε'(ω)−1 = −(4πe²/m)∫₀^∞ f(x)/(ω²−x²)dx
where f(ω) = (m/2π²e²)ωε''(ω) is the oscillator strength.
f-sum rule: ∫₀^∞ f(ω)dω = N (total electron density).

## Fix 11: knowledge.continuous.kramers_kronig — Safe vs unsafe KK direction

(82.8)→ε' is safe (any ε''>0 works). (82.7)→ε'' is unsafe (no ε''>0 guarantee).
Important practical guidance for using KK in data analysis.

## Fix 12: knowledge.continuous.dielectric_dispersion — No thermodynamic energy in absorbing media

§80 explicitly states: in general dispersive (absorbing) media, NO reasonable
definition of EM energy as a thermodynamic quantity is possible. The energy
formula ∂(ωε')/∂ω only applies in transparency regions where ε''≈0.

## Fix 13: knowledge.continuous.dielectric_dispersion — ε'' never truly zero

§80 insists: ε''(ω) never strictly vanishes at any ω≠0 — this has principle
significance. "Transparency" means ε''≪ε', not ε''=0.

## Fix 14: knowledge.continuous.dielectric_dispersion — ε' can be negative

§80: ε''>0 is required by second law (for bodies in thermodynamic equilibrium),
but ε' has NO sign constraint — can be positive or negative.

## Fix 15: knowledge.continuous.moving_media_electrodynamics — Exact Minkowski forms

The node only shows the linear-in-v/c approximations (76.10-76.11). §76 derives
the EXACT forms first (76.9):
D + [v×H]/c = ε(E + [v×B]/c)
B + [E×v]/c = μ(H + [D×v]/c)

## Fix 16: knowledge.continuous.moving_media_electrodynamics — 4-tensor foundation

§76 uses F_μν and H_μν 4-tensors. D and H form H_μν — they transform as a
4-tensor, not as vectors. This is the relativistic foundation of the Minkowski
equations. The node skips this entirely.

## Fix 17: knowledge.continuous.moving_media_electrodynamics — Boundary conditions

§76 (76.13-76.14): boundary conditions for moving interface:
[n,E₂−E₁] = (v_n/c)(B₂−B₁), [n,H₂−H₁] = −(v_n/c)(D₂−D₁).
Linearized: [n,E₂−E₁] = (v_n/c)(μ₂−μ₁)H_t, etc.

## Fix 18: Remove unsourced Minkowski vs Abraham controversy

The node mentions "Minkowski tensor vs Abraham tensor controversy." §76 does not
discuss this — it's from later literature. Either remove or mark as not from Landau.

## Fix 19: knowledge.continuous.spatial_dispersion — Poynting vector modification

Same as Fix 8 — the ∂ε_ik/∂k term in the Poynting vector (103.15) is a
qualitatively new effect of spatial dispersion not mentioned in the node.

## Fix 20: knowledge.continuous.moving_media_electrodynamics — Velocity gradient caveat

§76 footnote (line 10643): The Minkowski formulation neglects weak effects from
velocity gradients (gyromagnetic effects, §36). The node should note this limitation.
