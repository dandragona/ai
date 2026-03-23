# Research Report Output Template

Use this structure for the final assembled report in Phase 3.

---

## Report Structure

```markdown
# Research Report: {Topic}

**Date**: {current_date}
**Research Method**: Multi-agent expert panel (4 researchers, 3 analysts)

---

## Executive Summary

{3-5 sentences. What did we find? What's the overall confidence level? What's the single most important takeaway? A busy decision-maker should be able to read only this and walk away informed.}

---

## Expert Panel

| Expert | Archetype | Focus Area |
|--------|-----------|------------|
| {Name, Title} | {Archetype} | {1-line description of their angle} |
| {Name, Title} | {Archetype} | {1-line description of their angle} |
| {Name, Title} | {Archetype} | {1-line description of their angle} |
| {Name, Title} | {Archetype} | {1-line description of their angle} |

---

## Key Findings

Ranked by confidence level. Each finding includes its evidence basis.

### High Confidence

{Findings supported by 3-4 experts and/or strong sources}

**1. {Finding title}**
> {Clear statement of the finding}

- **Evidence**: {Supporting details}
- **Sources**: {Citation(s) with URLs}
- **Expert agreement**: {Which experts corroborate}

{Repeat for each high-confidence finding}

### Moderate Confidence

{Findings supported by 2 experts or moderate sources}

**{N}. {Finding title}**
> {Clear statement}

- **Evidence**: {Details}
- **Sources**: {Citations}
- **Expert agreement**: {Which experts}

{Repeat}

### Emerging/Preliminary

{Single-expert findings or those with limited sourcing that are still noteworthy}

**{N}. {Finding title}**
> {Clear statement}

- **Evidence**: {Details}
- **Source**: {Citation}
- **Note**: {Why this is included despite limited evidence}

---

## Contradictions & Debates

Active disagreements or tensions in the evidence.

### {Debate topic 1}

- **Position A**: {Claim} — supported by {expert(s)} citing {source(s)}
- **Position B**: {Counterclaim} — supported by {expert(s)} citing {source(s)}
- **Assessment**: {Which has stronger evidence, or if genuinely unresolved}

{Repeat for each contradiction}

---

## Gaps & Open Questions

### Blind Spots in This Research
- {Important aspect not adequately covered}
- {Missing stakeholder perspective}
- {Geographic or temporal gap}

### Open Questions Requiring Further Research
1. {Question}
2. {Question}
3. {Question}
{etc.}

### Source Quality Concerns
- {Any findings relying on weak sources}
- {Any uncited claims that were flagged}

---

## Recommendations

### Immediate Actions (0–6 months)

**1. {Recommendation}**
- **Based on**: {Finding(s) #{numbers}}
- **Feasibility**: {high | medium | low}
- **Key risk**: {Main obstacle}

{Repeat}

### Medium-Term Strategies (6–24 months)

**{N}. {Recommendation}**
- **Based on**: {Finding(s)}
- **Feasibility**: {Rating}
- **Key risk**: {Obstacle}

{Repeat}

### Long-Term Considerations (2+ years)

**{N}. {Recommendation}**
- **Based on**: {Finding(s)}
- **Feasibility**: {Rating}
- **Key risk**: {Obstacle}

{Repeat}

### What to Avoid
- {Common mistake and why, with supporting evidence}
- {Approach the evidence suggests against}

---

## Source Quality Assessment

**Overall evidence quality**: {strong | moderate | mixed | limited}

{1-2 paragraph honest assessment of the evidence base. How much peer-reviewed research exists? Is the topic well-studied or emerging? Are there notable biases in available sources? How much confidence should the reader place in this report?}

---

## Methodology Note

This report was produced using a multi-agent research methodology:

1. **Scoping**: The topic was analyzed and 4 expert archetypes were selected from 5 available (Domain Specialist, Methodologist, Contrarian, Practitioner, Historian/Contextualist). The dropped archetype was {archetype} because {reason}.
2. **Parallel Research**: 4 AI research agents, each embodying a distinct expert persona, independently searched the web for findings relevant to their expertise.
3. **Parallel Synthesis**: 3 AI analyst agents (Consensus, Gap & Contradiction, Recommendations) independently analyzed the combined research output without additional web access.
4. **Assembly**: Findings were compiled into this structured report.

**Limitations**:
- AI-conducted web research may miss sources behind paywalls or not indexed by search engines
- Expert personas are simulated, not real domain experts
- Web search results are influenced by search engine algorithms and indexing
- This report reflects information available as of {current_date}

---

## All Sources

Deduplicated, numbered list of every source cited in this report.

1. {Author/Org}. "{Title}." {Publication/Site}, {Date if available}. {URL}
2. {etc.}

---

*Research conducted {current_date} using multi-agent expert panel methodology.*
```

---

## Assembly Notes

When filling in this template:

- **Deduplicate sources**: Multiple experts may cite the same source. Assign each unique source one number and use that number consistently throughout.
- **Cross-reference finding numbers**: When recommendations say "Based on Finding #3", make sure #3 in the Key Findings section actually matches.
- **Don't inflate confidence**: If the evidence is genuinely weak, say so. A report that honestly says "we don't know" is more valuable than one that overstates certainty.
- **Keep the Executive Summary updated last**: Write it after everything else so it accurately reflects the full report.
- **Flag fabricated-looking sources**: If any URL looks suspicious or any source can't be verified from the agent output, add a note rather than silently including it.
