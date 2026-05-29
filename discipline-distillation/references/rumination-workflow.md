# Rumination Workflow — Re-Read, Find Gaps, Fix

## Why Rumination Is Necessary

After initial extraction, the graph LOOKS complete. It is not. The extraction
pass captures what jumps out. The rumination pass captures what was hiding in
plain sight: foundational premises in opening paragraphs, footnotes containing
critical subtleties, assumptions Landau states once and never repeats.

**Empirical fact from Landau 10-volume project**: First-pass rumination that
finds "no issues" is DIAGNOSTICALLY WRONG. 6 out of 10 volumes initially
passed fast with zero findings. Every single one, when properly re-read,
yielded 5-20 substantive issues.

## The Rumination Cycle

### STEP 1 — Load and Re-Read

1. Load ALL graph nodes for the target volume/book.
2. Re-read the ORIGINAL text of key sections PARAGRAPH BY PARAGRAPH.
3. For each paragraph, check: does our node capture everything?
4. **Read every footnote.** Landau's footnotes contain the most important
   subtleties (e.g., E(t) separated to avoid δ-singularity in f(τ) at τ=0,
   Vol.8 §82).

### STEP 2 — Check Against Known Patterns

Use the rumination check patterns (see `rumination-check-patterns.md`).
These 13 patterns were discovered through painful experience across
10 volumes. They are a proven checklist.

### STEP 3 — Apply Immediate Fixes

Issues that only affect metadata or graph topology:
- Fix parent/children references in node frontmatter
- Add newly discovered hidden parent nodes
- Remove or redirect incorrect edges in GRAPH.json

### STEP 4 — Record and Apply Content Fixes

Issues requiring body text changes:
1. Write tracking file: `volN-rewrite-fixes.md`
2. Apply each fix to the corresponding node file
3. Mark the tracking file as "ALL APPLIED" when done

### STEP 5 — Write Summary Report

Report structure:
```
# Volume N Rumination Report
## 1. Reasoning Node Reviews (per-node findings)
## 2. Hidden Parent Nodes Discovered
## 3. Cross-Volume Connections Missed
## 4. Summary of Changes
## 5. Rewrite Fixes Applied
```

## The Zero-Issues Sanity Check

If after STEP 1-2 you are about to write "No issues found":
- **STOP.** You have almost certainly missed something.
- Re-read the check patterns and verify each against every section.
- If you STILL find nothing, document explicitly which sections you read,
  which patterns you checked, and why each was not applicable.
- Genuinely clean volumes are extremely rare.

## Redo Protocol

When told "you went too fast, redo":
1. Don't defend. Don't argue. The user is right.
2. Restart from STEP 1. Load ALL nodes. Re-read paragraph by paragraph.
3. Use the checklist religiously.
4. Expect findings. Every volume has hidden premises.
