# Rumination Patterns Discovered Across 10 Volumes

These are recurring types of issues found during critical re-reading.
Future rumination sessions can use this as a checklist.

## Pattern 1: Order of Limits
**Example**: Vol.10 §29 — Landau damping requires linearization BEFORE ν→0.
The limits DO NOT COMMUTE.
**Check**: When a derivation involves multiple limits (small parameter, long time,
thermodynamic limit, etc.), does the template specify the correct ORDER?

## Pattern 2: Hidden Cancellation
**Example**: Vol.5 §32 — In thermodynamic perturbation theory, V/T ∝ N is NOT small
for macroscopic bodies. But ln Z causes large extensive terms to cancel, leaving
a series in the genuinely small per-particle parameter.
**Check**: When a template expands in a parameter that appears extensive (∝ N),
is there a hidden cancellation via logarithm/cumulant that makes it valid?

## Pattern 3: Missing Derivation Steps
**Example**: Vol.2 §27 — Landau's construction of the EM field action has 6
explicit reasoning steps (superposition→linear→quadratic; gauge→F_ik; scalar→F²;
sign from min action; pseudoscalar exclusion; S_mf linear in A_i). Our template
initially captured only 4.
**Check**: Re-read the original derivation step by step. Are ALL of Landau's
explicit steps present in the Algorithm? He never skips a logical link.

## Pattern 4: Sign Determination from Minimum Principle
**Example**: Vol.2 §8 — The negative sign in S = −mc∫ds is forced by requiring
S to have a minimum for small worldline segments (same logic as Vol.1 §2).
**Check**: When a constant/sign is determined in the original text, is the
REASON for that specific choice (not just the value) captured in the template?

## Pattern 5: Minimum vs Extremum Distinction
**Example**: Vol.1 §2 footnote, used crucially in Vol.2 §8.
δS = 0 only requires extremum, not minimum. For the FULL trajectory, the
action may be a saddle point. Small segments guarantee minima.
**Check**: Does the template distinguish between "stationary" and "minimum"?
This distinction becomes physically decisive in several places.

## Pattern 6: Integrability Requirements
**Example**: Vol.1 §49 — Adiabatic invariant derivation requires p = p(q;E,λ),
possible only for integrable systems. Template initially missed this constraint.
**Check**: When a template assumes the system can be expressed in a certain
form (p(q), separable coordinates, etc.), is there an explicit integrability/
separability requirement stated?

## Pattern 7: Fictitious vs True Motion in Averaging
**Example**: Vol.1 §49 — The average in adiabatic invariant derivation is over
the FICTITIOUS motion with λ constant, not the true (non-periodic) motion.
**Check**: When a template averages over a period/orbit, does it specify WHICH
orbit (true or fictitious)?

## Pattern 8: Additivity as Defining Criterion
**Example**: Vol.1 §6 — Among 2s−1 integrals, only 7 are additive. Landau
uses additivity (not just conservation) to identify "important" quantities.
**Check**: When a template lists conserved quantities, does it distinguish
between system-specific and universal (additive) integrals?

## Pattern 9: Connection to Charge/Gauge Conservation
**Example**: Vol.2 §18 footnote — Gauge invariance and charge conservation
are two aspects of the same U(1) symmetry. Template initially missed this link.
**Check**: Are symmetry→conservation connections fully traced, including
footnoted ones?

## Pattern 10: Spatial Dispersion as Mechanism
**Example**: Vol.10 §29 — Landau explicitly states: "Механизм затухания
Ландау тесно связан с пространственной дисперсией." Without k-dependence,
Im ε = 0 and there's no Landau damping.
**Check**: When a template describes a phenomenon that relies on nonlocality
or k-dependence, is the connection to the underlying mechanism explicit?
