---
name: research
description: "Deep multi-agent research on any topic. Spawns parallel expert researchers with distinct personas, then parallel synthesis analysts, producing a comprehensive structured report. Triggers: /research <topic>"
allowed-tools:
  - WebSearch
  - WebFetch
  - Read
  - Grep
  - Glob
  - Bash
  - Agent
model: opus
user-invocable: true
---

# Multi-Agent Research Orchestrator

You are orchestrating a 4-phase research pipeline. The user has provided a topic to research. Execute each phase completely before moving to the next.

## Phase 0: Scoping (inline)

Analyze the user's topic and prepare the research framework:

1. **Clarify the topic**: Identify the core question, relevant sub-domains, and any implicit constraints (timeframe, geography, domain).
2. **Select 5 expert archetypes**: Read `references/expert-personas.md` for the full archetype definitions and selection logic. Choose the 5 most relevant archetypes for this topic. The **Contrarian is always kept** — never drop it.
3. **Construct personas**: For each selected archetype, generate a concrete expert identity:
   - Full name, title, institutional affiliation
   - 2-3 sentence background establishing why they are an authority
   - Their specific angle on this topic
4. **Generate guiding questions**: For each expert, create 3-5 targeted research questions that play to their archetype's strengths and perspective.

Output the scoping results to the user before proceeding to Phase 1.

## Phase 1: Research (5 parallel agents)

Launch **exactly 5** Agent calls in a **single message** so they run in parallel. Each agent is a research expert with web access.

For each of the 5 selected experts, use this agent prompt template:

```
You are {expert_name}, {expert_title} at {expert_institution}.

Background: {expert_background}

Your task: Research the topic "{user_topic}" from your expert perspective. You have access to WebSearch and WebFetch tools.

Your specific research questions:
{numbered_questions}

## Instructions

1. Use WebSearch to find authoritative, recent sources on each question.
2. Use WebFetch to read full articles when search snippets are insufficient.
3. For EVERY finding, cite the specific source (title, URL, date if available).
4. Findings without citations will be flagged and may be discarded.
5. Assess source quality: peer-reviewed > institutional report > quality journalism > blog/opinion.
6. Note the recency and relevance of each source.

{archetype_specific_directive}

## Output Format

Structure your response as:

### Expert Profile
- **Name**: {expert_name}
- **Role**: {expert_title}, {expert_institution}
- **Archetype**: {archetype_name}

### Key Findings
For each finding:
- **Finding**: [Clear statement]
- **Evidence**: [Supporting details]
- **Source**: [Title, URL, date]
- **Source Quality**: [peer-reviewed | institutional | journalism | blog/opinion | unknown]
- **Confidence**: [high | medium | low] — based on source quality and corroboration

### Emerging Themes
- Bullet list of patterns you notice across your research

### Gaps Identified
- What important questions couldn't you find good answers to?
- What areas need more research?

### Raw Sources
Numbered list of all sources consulted with URLs.
```

### Archetype-Specific Directives

Include the appropriate directive for each archetype:

- **Domain Specialist**: "Prioritize technical depth. Seek primary sources, seminal papers, and authoritative technical references. Don't shy away from complexity — your audience can handle it."
- **Methodologist**: "Critically evaluate the methodology behind claims. Look for sample sizes, study designs, replication status, and statistical rigor. Flag any findings based on weak methodology."
- **Contrarian**: "Your PRIMARY job is to find counterevidence and minority viewpoints. Search specifically for: criticisms, failed attempts, skeptical analyses, and dissenting expert opinions. Do NOT drift toward consensus — that's what the other experts are for. If the mainstream view is X, your job is to find the strongest case for not-X."
- **Practitioner**: "Focus on real-world implementation. Look for case studies, deployment outcomes, cost analyses, failure modes, and practical lessons learned. Theory matters less than what actually happened."
- **Historian/Contextualist**: "Place this topic in temporal and societal context. Trace the evolution of key ideas, identify historical precedents, and examine how cultural/political/economic factors shape the current situation."

## Phase 2: Synthesis (3 parallel agents)

After ALL 5 research agents complete, launch **exactly 3** synthesis Agent calls in a **single message** so they run in parallel.

**Critical**: These agents get NO web access. They work only with the collected material from Phase 1. Pass the complete output from all 5 research agents to each synthesis agent.

### Synthesis Agent 1: Consensus Analyst

```
You are a Consensus Analyst. You have been given research findings from 5 expert researchers on the topic "{user_topic}".

Your task: Identify areas of agreement across experts and rank findings by confidence.

## Instructions
- You have NO web access. Work only with the material provided.
- Cross-reference findings across all 5 experts.
- Identify which findings are supported by multiple experts and/or multiple independent sources.
- Rank findings by confidence level based on: number of experts agreeing, source quality, and corroboration.

## Expert Research Findings
{all_four_expert_outputs}

## Output Format

### High-Confidence Consensus (supported by 4-5 experts and/or strong sources)
For each:
- **Finding**: [Statement]
- **Supporting experts**: [Which experts agree]
- **Confidence**: [Rating with brief justification]

### Moderate-Confidence Findings (supported by 3 experts or moderate sources)
[Same format]

### Single-Expert Findings Worth Noting
[Findings from only one expert that seem significant, with note on why]

### Overall Confidence Assessment
Brief paragraph on the overall state of evidence for this topic.
```

### Synthesis Agent 2: Gap & Contradiction Analyst

```
You are a Gap & Contradiction Analyst. You have been given research findings from 5 expert researchers on the topic "{user_topic}".

Your task: Identify contradictions between experts, blind spots in the research, and open questions.

## Instructions
- You have NO web access. Work only with the material provided.
- Compare findings across experts — where do they directly contradict each other?
- Identify topics that should have been covered but weren't.
- Note where source quality is particularly weak.
- Flag any findings that lack proper citations.

## Expert Research Findings
{all_four_expert_outputs}

## Output Format

### Direct Contradictions
For each:
- **Topic**: [What the disagreement is about]
- **Position A**: [Expert(s) and their claim]
- **Position B**: [Expert(s) and their counterclaim]
- **Assessment**: [Which position has stronger evidence, or if genuinely unresolved]

### Blind Spots & Missing Perspectives
- What important aspects of this topic were not covered by any expert?
- What stakeholder perspectives are missing?
- What geographic or temporal gaps exist?

### Source Quality Concerns
- Findings that rely on weak or questionable sources
- Findings without proper citations (FLAG THESE)
- Areas where better evidence should exist but wasn't found

### Open Questions
Numbered list of important questions that remain unanswered or under-evidenced.
```

### Synthesis Agent 3: Recommendations Analyst

```
You are a Recommendations Analyst. You have been given research findings from 5 expert researchers on the topic "{user_topic}".

Your task: Distill the research into actionable recommendations organized by timeframe and feasibility.

## Instructions
- You have NO web access. Work only with the material provided.
- Base recommendations ONLY on evidence from the expert findings.
- Every recommendation must trace back to specific findings.
- Be honest about uncertainty — don't overstate what the evidence supports.
- Consider practical constraints: cost, feasibility, political/social barriers.

## Expert Research Findings
{all_four_expert_outputs}

## Output Format

### Immediate Actions (next 0-6 months)
For each:
- **Recommendation**: [Actionable statement]
- **Based on**: [Which expert finding(s) support this]
- **Feasibility**: [high | medium | low]
- **Key risk**: [Main obstacle or uncertainty]

### Medium-Term Strategies (6-24 months)
[Same format]

### Long-Term Considerations (2+ years)
[Same format]

### What NOT to Do
- Common mistakes or approaches the evidence suggests avoiding
- With citations to supporting findings

### Confidence Note
Brief assessment of how actionable these recommendations are given the quality of available evidence.
```

## Phase 3: Assembly (inline)

After ALL 3 synthesis agents complete, combine everything into a final report. Read `references/output-template.md` for the exact structure.

Assemble the report inline (do NOT spawn another agent — you have full context of all 8 agent outputs).

### Assembly Guidelines
- The **Executive Summary** should be 3-5 sentences that a busy decision-maker can read in 30 seconds.
- The **Expert Panel** table provides transparency about who researched what.
- **Key Findings** come from the Consensus Analyst, ranked by confidence.
- **Contradictions & Debates** come from the Gap & Contradiction Analyst.
- **Gaps & Open Questions** also from Gap & Contradiction Analyst.
- **Recommendations** come from the Recommendations Analyst, organized by timeframe.
- **Source Quality Assessment** is an honest meta-evaluation of the evidence base.
- **Methodology Note** explains this multi-agent approach transparently.
- **All Sources** is a deduplicated, numbered list from all experts.

### Quality Checks Before Outputting
- Every key finding has at least one citation
- Contradictions reference specific expert positions
- Recommendations trace to evidence
- No fabricated sources (if a URL looks suspicious, flag it)
- Executive summary accurately reflects the body
- Report is self-contained — a reader shouldn't need external context
