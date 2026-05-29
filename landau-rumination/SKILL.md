---
name: landau-rumination
description: "Systematic rumination workflow for LandauGraph — re-read original Landau text with graph nodes loaded, discover hidden assumptions, merge duplicates, extract hidden parent patterns. Produces per-volume reports and rewrite fix lists."
---

# LandauGraph Rumination Workflow

After a volume's reasoning and knowledge nodes are written, run this
workflow to critically review and improve the graph.

## Prerequisites

- Completed graph nodes for the target volume
- Access to original Landau text via `knowledge-base` skill
- Existing GRAPH.json at `/home/zhiping/.hermes/skills/landau-graph/GRAPH.json`
- **Before starting**: read `references/rumination-check-patterns.md` for
  recurring issues found in previous volumes. Use it as a checklist.

## Workflow

### STEP 1 — Load and re-read

```
1. Load landau-course skill for the volume's chapter map and KB path
2. Load the graph nodes for the volume (read nodes/ from landau-graph/)
3. Re-read the ORIGINAL text of key sections with these loaded
```

For each reasoning node in the volume, re-read the corresponding
original Landau section and ask:

- **Edge Cases**: Does the original text mention failure conditions
  that our template missed?
- **Algorithm**: Are there hidden steps in the original derivation
  that our template glosses over?
- **Assumptions**: Does Landau state assumptions explicitly that we
  omitted? Are they discussed in the text?
- **Connections**: Does Landau cross-reference other volumes or
  sections that we should link to?
- **[CRITICAL] Check against `references/rumination-check-patterns.md`**:
  The recurring pattern types (currently 15) are a proven checklist. A fast pass
  without this check misses 85% of real issues (see Vol.6 fast pass:
  0 found → redone properly: 6 found).
- **Rumination patterns**: Cross-check against `references/rumination-patterns.md`
  for recurring issue types (order of limits, hidden cancellation,
  sign determination, integrability requirements, etc.)

### STEP 2 — Apply immediate fixes (reference-level)

Issues that only affect metadata (frontmatter) or graph topology
can be fixed immediately:

```
- Fix parent/children references in node .md files
- Add newly discovered hidden parent nodes (write .md + add to GRAPH.json)
- Remove or redirect incorrect edges in GRAPH.json
```

Use `patch` tool for parent reference changes.
Use `write_file` for new hidden parent nodes.
Use `execute_code` for GRAPH.json updates.

### STEP 3 — Record AND apply content-level fixes

Issues that require changing the body text of nodes (Core Picture,
Algorithm, Edge Cases, Key Insights, etc.) should be recorded in a
tracking file AND APPLIED IMMEDIATELY once the volume's rumination
is complete. The user expects fixes to be in the graph before the
next volume's rumination begins.

1. Write tracking file: `/home/zhiping/.hermes/skills/landau-graph/rumination/volN-rewrite-fixes.md`
2. Apply each fix to the corresponding node file using `patch`
3. Mark the tracking file header as "ALL APPLIED" when done

Format per fix:
```markdown
## Fix N: node_id — Short description
...
```
Use `patch` tool for each fix. If a fix requires adding a new section
to a node, read the node first with `read_file` to find the exact
insertion point.

### STEP 4 — Write summary report

Write to: `/home/zhiping/.hermes/skills/landau-graph/rumination/volN.md`

Report structure:
```
# Volume N Rumination Report

Date. Methodology summary.

## 1. Reasoning Node Reviews
Per-node findings: what was checked, what was found.

## 2. Hidden Parent Nodes Discovered
Candidate nodes with rationale and proposed children.

## 3. Cross-Volume Connections Missed
Links to other volumes that should be added to GRAPH.json.

## 4. Summary of Changes Made
Nodes added, edges changed, references fixed.

## 5. Rewrite Fixes Pending
Link to volN-rewrite-fixes.md, count by priority.
```

## Output Files

| File | Content |
|------|---------|
| `rumination/volN.md` | Full rumination report |
| `rumination/volN-rewrite-fixes.md` | Content-level fixes pending |
| Updated `GRAPH.json` | New nodes + corrected edges |
| Updated `nodes/*.md` | Fixed parent/children references |

## Redo Protocol — When told "you went too fast, redo"

When the user says a volume's rumination was too fast (e.g., "Vol.6 was done
in one pass with no issues found — redo it"), the ONLY correct response is:

1. **Don't defend. Don't argue.** The user is right. A fast pass that finds
   nothing is the strongest signal that it was done wrong.
2. **Restart from STEP 1.** Load ALL nodes for the volume. Re-read the
   original text paragraph by paragraph, with the nodes side by side.
3. **Use the checklist.** Read `references/rumination-check-patterns.md`
   before starting and check each pattern against every section.
4. **Expect findings.** Every volume has hidden premises. If the original
   rumination was fast, the redo WILL find 5–10 substantive issues.

Historical data: Vol.6 fast pass → 0 issues → redo → 6 major gaps found.
Vol.3 fast pass → 0 issues → redo → 7 gaps found. Vol.4 fast pass → 0 issues
→ redo → 5 gaps found. Vol.7 fast pass → 0 issues → redo → 6 gaps found.
Vol.8 fast pass → 0 issues → redo → 20 gaps found. Vol.9 fast pass → 0 issues
→ redo → 17 gaps found. The pattern is consistent: zero-issue passes are
diagnostically wrong. Average yield from redo: ~10 issues/volume.
6 of 10 volumes required redoes.

## Zero-Issues Sanity Check

After STEP 1 re-reading, if you are about to write "No issues found":

- **STOP.** You have almost certainly missed something.
- Re-read `references/rumination-check-patterns.md` and check every pattern
  against every section you covered.
- If you STILL find nothing after a second pass with the checklist, document
  explicitly which sections you read, which patterns you checked, and why
  each one was not applicable. This documentation goes in the rumination
  report.
- Genuinely clean volumes are extremely rare. Across 8 volumes ruminated,
  zero produced zero findings.

## Common Pitfalls

- **THE BIGGEST PITFALL — Skipping the re-read**: Never rely on memory
  from the extraction pass. You MUST re-read the original text for every
  volume, section by section. When you skip this, you miss foundational
  premises that Landau states in opening paragraphs — e.g., the "physically
  infinitesimal volume" concept (Vol.6 §1), the Eulerian description
  framing (Vol.6 §1), the momentum flux tensor connection (Vol.6 §7→§15).
  If you find yourself writing "No issues found" after minimal re-reading,
  you are doing it wrong. See **Redo Protocol** above — this pitfall has
  been triggered on 4 of 7 volumes so far (Vol.3, 4, 6, 7).
- **Deferring content fixes across sessions**: Apply both reference-level
  and content-level fixes in the same session as the rumination. The user
  expects fixes to be in the graph before moving to the next volume.
- **Missing cross-volume parents**: When you notice the same reasoning
  pattern in 2+ volumes, create the parent node immediately (Step 2),
  don't just note it.
- **Forgetting to update GRAPH.json**: After adding hidden parent nodes,
  always run the edge update code. Stale edges cause retrieval failures.
- **Skipping volumes because they seem "done"**: Every volume benefits
  from rumination. Even Vol.7 (Elasticity) revealed the deep constitutive
  symmetry pattern shared with Vol.6.
- **Missing the footnotes**: Landau's footnotes often contain the most
  important subtleties (min-vs-extremum, ln Z cancellation, gauge↔charge
  conservation). Always read footnotes during STEP 1 re-reading.
