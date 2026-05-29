# Blind-Derivation Validation

## What It Is

The ultimate test of a reasoning graph: give it to independent AI agents
WITHOUT the original textbook. Ask them to derive the discipline's core
results. Every point where they get stuck is a gap in the graph.

## Why It's Necessary

Extraction and rumination are done by agents WITH access to the original
text. These agents are biased — they "know" the answers and may write
templates that make sense to them but are incomprehensible to an agent
without that background.

Blind-derivation exposes:
- Templates that state conclusions without providing the constructive algorithm
- Hidden dependencies on knowledge the template assumes but doesn't state
- Missing cross-volume connections that a fresh agent won't discover
- Concepts the template author considered "obvious" (but aren't)

## Protocol

### Setup

1. Select 2+ independent AI agents with different architectures/models.
2. Give them ONLY the reasoning graph nodes. NO knowledge nodes. NO original text.
3. If the agents get stuck, allow them to request specific knowledge nodes.
4. For each volume/chapter, have agents attempt derivation and report:
   - What they COULD derive from the templates alone
   - Where they got STUCK and WHY
   - What additional information would have unblocked them

### Collection

For each confusion/gap, record:
- Which node was being used
- What step the agent couldn't complete
- Whether the gap is in the reasoning template itself or in missing cross-volume knowledge

### Fix Cycle

1. Collect all confusions from all agents (aggregate, deduplicate).
2. For each confusion: cross-check against the ORIGINAL TEXT.
3. Categorize:
   - **Template gap**: Fix the existing node (add the missing step/algorithm)
   - **Cross-volume gap**: Add an edge or bridge section to connect patterns
   - **New node needed**: The pattern exists in the original but has no template
   - **Math gap**: Pure mathematical derivation → add to mathematics reference
   - **Out of scope**: Requires mathematical facility beyond reasoning templates
4. Apply fixes, re-validate.

### Iteration

After fixing, run another blind-derivation round. Track the closure rate:
- Round 1: ~40% of confusions resolved (typical for first pass)
- Round 2: ~75% resolved
- Round 3: ~95% resolved (remaining are math details)

## Landau Example Results

Two agents (DeepSeek V4 Flash + Claude Opus 4.7) attempted blind derivation
across all 10 volumes.

| Round | Confusions | Resolved | Methodology |
|-------|-----------|----------|-------------|
| Before improvement | 60+ | 0% | Original 37 nodes |
| Round 1 fixes | ~25 resolved | ~40% | Fixed 10 existing nodes + added 3 new |
| Round 2-3 fixes | ~35 resolved | ~95% | Added 7 more nodes + 4 expansions + math skill |
| Remaining | ~5 | — | Math details (Airy, Bessel, distribution limits) |

**Key lesson**: The most common complaint was "templates give conclusions
but not the constructive algorithm." Agents could follow "L = T − U is a
consequence of Galilean invariance" but couldn't execute the 7-step
derivation from Galilean invariance to L = ½mv². Adding the algorithm
was the single highest-impact fix.

Complete reports: `examples/landau-10-volumes/validation/`
