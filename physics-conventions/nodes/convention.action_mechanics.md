---
skill_id: convention.action_mechanics
type: convention
summary_50t: >
  Adiabatic invariant J = ∮p dq (full action, Landau Vol 1), NOT the reduced
  action J = (1/2π)∮p dq (Bohr-Sommerfeld). The factor 2π affects all
  quantization rules.
---

# Action and adiabatic invariant conventions

The adiabatic invariant (action variable) is defined with two competing
conventions across physics literature. This node states the project standard and
the conversion rule.

## Project standard: full action (Landau)

```
J = ∮ p dq
```

This is the **full action**, used throughout Landau and Lifshitz Vol 1
(Mechanics) and consistent with the landau-graph reasoning system.

## Alternative: reduced action (Bohr-Sommerfeld)

```
J_reduced = (1/2π) ∮ p dq
```

Used in older atomic-physics texts and some quantum mechanics books that adopt
the Bohr-Sommerfeld quantization rule in the form ∮ p dq = (n + γ)h (not ℏ).

## Impact on quantization rules

The factor 2π propagates into the quantization condition:

| Convention | Quantization |
|------------|--------------|
| Full action | J = (n + γ) h |
| Reduced action | J_reduced = (n + γ) ℏ |

When citing atomic-physics texts that use the reduced action:

```
J_full = 2π · J_reduced
```

## landau-graph consistency

The landau-graph system uses the full-action convention throughout, so no
conversion is needed when bridging results from landau-graph to downstream
skills that also adopt this standard.

**References**: Landau & Lifshitz Vol 1 §49, Goldstein (2002) Classical
Mechanics §10.7.
