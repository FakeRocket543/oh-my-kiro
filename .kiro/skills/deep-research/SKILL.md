---
name: deep-research
description: Use when conducting investigative research, writing research notes, building source registries, or verifying institutional/structural claims across multiple jurisdictions. Triggers include "查證", "research this", "幫我查", "深度研究", "調研", cross-country comparison requests.
---

# Deep Research

Structured investigative research with source governance, citation registry, and counter-review.

## Overview

Generate evidence-mapped research notes with full source tracing. Every claim traces to a citable source. Distinguish what is known from what is speculated.

## When to Use

- User requests investigative research on a topic
- Cross-jurisdictional or cross-institutional comparison
- Building background for a feature article (Chronicle mode, Research stage)
- Verifying structural/systemic claims (not individual facts — use `fact-check` for that)
- Literature review or policy analysis

## Architecture

```
Research Task Board (decompose question into 3-6 sub-investigations)
  |
  Parallel research waves (web_search + web_fetch per sub-topic)
  |
  Research Notes (one file per sub-topic, structured format)
  |
  Citation Registry (unified, deduplicated, scored)
  |
  Evidence-Mapped Outline (claims → sources → gaps)
  |
  Counter-Review (mandatory opposing interpretation)
  |
  Final Notes or handoff to Chronicle mode drafting
```

## Source Governance

### Source Type Labels

Every source MUST be tagged:

| Label | Examples |
|-------|----------|
| `official` | Government reports, SEC filings, official press releases, legislation text |
| `academic` | Peer-reviewed journals, conference papers, university research |
| `secondary-industry` | Think tank reports, analyst coverage, trade publications |
| `journalism` | Reputable outlets (named reporters, editorial oversight) |
| `community` | Forums, social media, blogs, anonymous sources |

### Quality Gates

- Key claims require ≥2 independent sources
- ≥30% of approved sources must be `official` or `academic`
- No single domain may exceed 25% of total sources
- Minimum 5 unique domains in final registry

### AS_OF Date Policy

- Set `AS_OF` date at research start (today's date)
- Every source citation includes publication date
- Flag stale sources: studies >3 years, news >6 months for fast-moving topics
- Downgrade confidence if source predates relevant policy changes

## Source Independence Analysis

For each cluster of supporting sources, determine:

1. **Is this PRIMARY reporting** (original investigation/data) or **SECONDARY** (reporting on others' work)?
2. **Who published first?** (temporal analysis)
3. **Do multiple sources trace back to a single origin?**
4. **Are sources quoting the same underlying study/report?**

Build citation chain:
```
Source A (primary) ← Source B (cites A) ← Source C (cites B)
```

Flag circular citations: "Sources appear to derive from a single origin rather than independent verification."

## Citation Registry Format

```markdown
## Citation Registry

AS_OF: 2026-06-22

### Approved
[1] Author/Org — Title | URL | Type: official | Date: YYYY-MM-DD | Authority: 8/10
[2] ...

### Dropped
x Source | URL | Type: community | Authority: 2/10 | Reason: single anonymous blog post

### Stats
Approved: N/M total | Domains: N | Official share: XX%
```

## Counter-Review (Mandatory)

After building the evidence map, ask:

1. Could the main conclusion be wrong? What would that look like?
2. Which high-impact claims depend on a single source?
3. Which claims lack official/academic backing?
4. Are there stale sources used for time-sensitive claims?
5. What is the strongest counter-argument?

Output a `## Counter-Review` section with ≥3 identified issues.

## Research Notes Format

Each sub-topic outputs:

```markdown
# [Sub-topic Title]

## Sources
[1] ... (with type, date, authority)

## Findings
- Finding 1 [1][3]
- Finding 2 [2]

## Gaps
- What was searched but NOT found
- What remains unverified

## Counter-Interpretations
- Alternative explanation for Finding 1
```

## Output

Final output is `.omk/research-notes-[topic].md` containing:
- Citation registry
- Evidence-mapped findings per sub-topic
- Gap analysis
- Counter-review section
- Recommended next steps (more research needed? ready to draft?)

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Treating secondary coverage as independent confirmation | Trace citation chains |
| Using undated sources for time-sensitive claims | Always check publication date |
| Stopping at first confirming source | Search for disconfirming evidence |
| Mixing verified facts with inferences | Label clearly: VERIFIED vs. INFERRED |
| Circular verification (using user's own data to "discover" what they know) | Research from external investigator perspective |
