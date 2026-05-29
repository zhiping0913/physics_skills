# Worked Example: Landau-Lifshitz 10-Volume Distillation

This is the complete record of distilling the Landau-Lifshitz Course of
Theoretical Physics (10 volumes, ~7000 pages, Russian original) into a
96-node, 188-edge reasoning graph validated by blind-derivation experiments.

## Source

All 10 volumes in Russian (2001-2005 ФИЗМАТЛИТ editions), stored as
markdown in `/home/zhiping/knowledge_base/book/`. Original `book.md`
files with LaTeX equations and section structure preserved.

## Output

The production graph lives in the `landau-graph` skill:
- 96 nodes (37 reasoning templates + 59 knowledge nodes)
- 188 typed edges (prerequisite, reasoning-instance, abstraction, analogy)
- 3 hidden parent nodes discovered during rumination

## Extraction Process

Three-track extraction per volume (see `references/extraction-workflow.md`):
- **Track A**: Mined reusable physical thinking patterns (not chapter summaries)
- **Track B**: Grounded each pattern in concrete physics with equations and validity conditions
- **Track C**: Built a DAG of conceptual dependencies, ignoring textbook exposition order

Volume order: 1→2→5→10→8→6→3→9→4→7 (by conceptual dependency, not numerical).

## Rumination

All 10 volumes were systematically re-read with graph nodes loaded.
Key findings:
- 80+ issues discovered and fixed across 10 volumes
- 3 hidden parent nodes extracted (symmetry_drives_physics, timescale_hierarchy, causality_as_constraint)
- 6 of 10 volumes required complete redo after initial fast passes found "no issues"
- Most common missed patterns: hidden premises in opening paragraphs, footnote subtleties, unstated assumptions

Full reports: `rumination/vol{N}.md` + `vol{N}-rewrite-fixes.md`

## Validation: Blind-Derivation Experiment

Two independent AI agents (DeepSeek V4 Flash + Claude Opus 4.7) were given
ONLY the reasoning graph nodes, WITHOUT the original Landau text. They
attempted to derive all core results and reported every point where they
got stuck.

**Results**:
- Round 1 (original 37 nodes): 60+ confusions, ~0% resolved
- Round 2 (improved nodes): ~40% resolved
- Round 3 (new nodes + expansions): ~95% resolved

**Top agent complaints**:
1. "Templates give conclusions but no constructive algorithm" (most common)
2. "I know X connects to Y but don't know HOW"
3. "This pattern appears in Vol.A and Vol.B but isn't flagged as the same thing"

Full reports: `validation/` (gap analysis, verification reports, changelog)

## Timeline

| Phase | Duration | Output |
|-------|----------|--------|
| Initial extraction | ~2 weeks | 89 nodes, 152 edges across 10 volumes |
| Rumination pass 1 | ~1 week | Fast passes (redone for 6 volumes) |
| Rumination pass 2 (redo) | ~1 week | 80+ fixes, 3 hidden parents |
| Blind-derivation experiment | 1 day | 60+ confusions from 2 agents |
| Improvement round 1 | 1 day | 10 node fixes, 3 new nodes |
| Improvement round 2 | 1 day | 7 new nodes, 4 expansions |
| Improvement round 3 | 1 day | 2 supplements, math skill, cleanup |
| **Total** | **~4 weeks** | **96 nodes, 188 edges, validated** |

## Key Lessons

1. **Fast passes are dangerous.** "No issues found" after a quick re-read
   is the strongest signal that you missed something. Every volume had issues.
2. **Constructive algorithms are essential.** Agents need the "HOW", not just
   the "WHAT". State conclusions, then show the step-by-step derivation.
3. **Cross-volume bridges unlock transfer.** The biggest wins came from
   flagging that Legendre transforms, perturbation theory, and constitutive
   relations are the SAME pattern across volumes.
4. **Validation is mandatory.** Your own agent (with access to the original)
   cannot judge whether the templates work. Only blind agents can.
5. **Mathematics needs a home.** Pure mathematical theorems (Bertrand,
   Liouville-Arnold) don't fit in reasoning templates but agents need them.
   A separate mathematics reference skill solves this cleanly.
