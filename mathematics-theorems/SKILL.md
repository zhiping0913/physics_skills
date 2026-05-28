---
name: mathematics-theorems
description: "Repository of mathematical theorems referenced by LandauGraph reasoning nodes. Stores complete proofs for results that are asserted but not derived in templates: Bertrand's theorem, Liouville-Arnold theorem, distribution identities, Airy asymptotics, and other mathematical infrastructure required for full derivations."
---

# Mathematics Theorems Repository

Complete proofs for mathematical theorems that LandauGraph reasoning nodes
assert but do not derive. Agents load these when encountering "this is a theorem"
statements in reasoning templates.

## How to Use

When a reasoning node says "this is a theorem — the proof requires...",
load the corresponding reference file. Proofs are mathematical, not physical.

## Index

| Theorem | Used in | File |
|---------|---------|------|
| Bertrand's theorem | `conservation_to_effective_reduction` (V1) | `bertrand-theorem.md` |
| Liouville-Arnold theorem | `separation_of_variables` (V1) | `liouville-arnold.md` |
| Distribution limit sin²(αt)/α²→δ(α) | `quantum_perturbation_theory` (V3) | `distribution-limits.md` |
| Airy function asymptotics | `wkb_quasiclassical` (V3) | `airy-asymptotics.md` |
| 4D δ-function with Jacobian | `retarded_green_function` (V2) | `delta-function-4d.md` |

## Maintenance

Add new entries when a reasoning node asserts a non-trivial mathematical result
or when agents consistently get stuck on a mathematical step.
