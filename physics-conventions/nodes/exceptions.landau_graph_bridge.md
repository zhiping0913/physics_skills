---
skill_id: exceptions.landau_graph_bridge
type: convention
summary_50t: >
  landau-graph uses Gaussian units, metric (+−−−), Landau's circular-pol
  naming. When citing landau-graph from downstream: convert ε₀↔1/4π (via
  convention.units_systems in this skill), flip metric signs in 4-vector
  contractions, and check pol-handedness if relevant.
---

# Landau-graph → downstream bridge

`landau-graph` is the production reasoning graph for the Landau-Lifshitz
10-volume Course. It uses Landau's conventions, which differ from project
standards. This node catalogs the differences and the conversion rules to
apply when a downstream skill cites a landau-graph node.

## Differences

| Topic | Landau | Project (downstream) | Conversion |
|-------|--------|----------------------|------------|
| Units | Gaussian | SI | [[convention.units_systems]] (this skill) |
| Metric | (+−−−) | (−+++) | Flip sign of every g_μν / g^μν contraction |
| Plane wave | e^{i(k·r − ωt)} | same | — |
| FT convention | same | same | — |
| ω_c (plasma) | signed (Stix-equiv) | signed (Stix) | — |
| Right circular | Landau Vol 8 §81 (Born & Wolf-equiv) | IEEE / project | check page-by-page; usually equivalent for k along +z |
| J action | ∮p dq | ∮p dq | — |
| Helmholtz G | (∇² + k²)G = −4πδ (Gaussian) | (∇² + k²)G = −δ (SI) | factor 1/(4π) where G is substituted |
| χ⁽ⁿ⁾ | Gaussian P = χ E (with 4π) | SI P = ε₀ χ E | use SI form in downstream; χ_G = 4π χ_SI / (factor depends on units) |
| 4-velocity | u^μ u_μ = c² (Landau Vol 2) | u^μ u_μ = −c² (with −+++) | flip sign |
| Action S = ∫L dt | sign conventions vary by chapter | adopt project (−+++) downstream | check L sign |

## When to bridge

A downstream node that cites a landau-graph node typically needs:

1. **Restate the result in SI** (use [[convention.units_systems]] within this skill).
2. **Flip metric signs**: If the result is a 4-vector contraction (radiation
   4-momentum, action), flip the relevant sign.
3. **Helmholtz Green's function**: If the result involves a Helmholtz Green's
   function, absorb the factor of 4π appropriately.
4. **Polarization handedness**: If the result names a polarization, check
   whether Landau and project handedness disagree (usually they don't for
   3-vector E-field, but they do for some matrix elements in QED).

## When NOT to bridge

Most landau-graph results are conventionally dimensional / qualitative (scaling
laws, conservation arguments). These transport across unit and metric
conventions with no rewriting needed.

## Worked example

`landau-graph: knowledge.em.lienard_wiechert` gives:

```
φ = e / [R − v·R/c]_ret    (Gaussian, no ε₀)
```

In project SI:

```
φ = (e / 4πε₀) / [R(1 − n·v/c)]_ret
```

Both reduce to the formula in `electrodynamics: reasoning.em.lienard_wiechert_radiation`
step 1.

**References**: Landau-Lifshitz prefaces of each volume (unit choices);
[[convention.units_systems]] (SI↔Gaussian conversion tables); this skill's
other convention nodes (signs and normalizations).
