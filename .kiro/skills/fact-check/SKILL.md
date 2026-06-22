---
name: fact-check
description: Use when verifying specific factual claims in documents, checking statistics, validating dates/numbers, or confirming quotes and attributions. Triggers include "fact-check", "這個數字對嗎", "verify this", "check accuracy", "validate claims", reviewing drafts for factual errors before publication.
---

# Fact Check

Verify specific factual claims against authoritative sources. Extract, check, report, correct.

## Overview

Systematic claim extraction and verification. Not for broad research (use `deep-research`). This is surgical: identify verifiable assertions, check each against primary sources, produce a structured report.

## When to Use

- Reviewing a draft before publication
- User questions a specific statistic, date, or attribution
- Validating technical specifications or version numbers
- Checking if quoted statements are accurately attributed
- Verifying geographic, demographic, or financial data

## When NOT to Use

- Broad investigative research → use `deep-research`
- Subjective opinions or editorial judgments
- Predictions or forecasts (unfalsifiable)

## Workflow

```
1. Extract Claims → identify all verifiable assertions
2. Triage → uncontroversial / disputed / misdirected
3. Search → authoritative sources per claim
4. Compare → claim vs. source
5. Report → structured findings
6. Correct → with user approval only
```

## Step 1: Claim Extraction

Scan for verifiable statements:

- Numbers (statistics, percentages, counts, dates)
- Attributions ("X said Y", "according to Z")
- Technical specs (context windows, API limits, versions)
- Geographic/demographic facts
- Legal/policy claims (law names, article numbers, effective dates)
- Historical events (dates, participants, outcomes)

Skip: opinions, recommendations, explanatory prose, predictions.

## Step 2: Triage

| Category | Action |
|----------|--------|
| **Uncontroversial** | Widely accepted, skip unless user insists |
| **Disputed** | Conflicting evidence exists — full check |
| **Misdirected** | Main point sound but sub-claims contentious — check sub-claims |

## Step 3: Source Search

Priority order:
1. Primary sources (official documents, original publications)
2. Government/institutional databases
3. Peer-reviewed research
4. Reputable journalism (named reporters)
5. Technical documentation (official docs, GitHub releases)

Search strategy:
- Use specific terms + year for recency
- Check multiple sources when possible
- Prefer sources with named authors and editorial oversight

## Step 4: Compare & Assess

| Status | Meaning |
|--------|---------|
| ✅ Accurate | Claim matches sources |
| ❌ Incorrect | Claim contradicts sources |
| ⚠️ Outdated | Was true, now superseded |
| 🔄 Imprecise | Directionally correct but details wrong |
| ❓ Unverifiable | No authoritative source found |

## Step 5: Report Format

```markdown
## Fact-Check Report

### Summary
- Claims checked: N
- Accurate: N | Incorrect: N | Outdated: N | Unverifiable: N

### Issues

#### 1. [Claim summary]
- **Location:** [file:line or section reference]
- **Current claim:** "[exact text]"
- **Source says:** "[what source actually states]"
- **Status:** ❌ Incorrect
- **Source:** [URL] (published YYYY-MM-DD)
- **Suggested fix:** "[corrected text]"

#### 2. ...
```

## Step 6: Corrections

**Never auto-correct.** Present report → wait for user approval → apply changes.

Include temporal context in corrections:
- Good: 「截至 2026 年 6 月」
- Bad: 「目前」「最新」(becomes stale)

## Rhetorical Fallacy Detection

When checking argumentative text, also flag:

- **Headline-text mismatch**: headline claims X but body only supports weaker Y
- **Appeal to unnamed authority**: "experts say" without naming them
- **Cherry-picking**: selective data ignoring contrary evidence
- **Correlation-as-causation**: implies causation from correlation
- **False precision**: "exactly 47.3%" from a rough estimate

## Ideological Clustering Check

Note if supporting sources cluster on one political/ideological spectrum:
- "Supporting sources are primarily [progressive/conservative/institutional] outlets"
- Flag when evidence comes from one perspective only

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Checking opinions as if they were facts | Only check verifiable assertions |
| Using aggregator sites as primary source | Trace to original publication |
| Accepting first search result as definitive | Cross-reference with official docs |
| Marking "unverifiable" without searching thoroughly | Try 3+ different query phrasings |
| Correcting without temporal context | Always add "as of [date]" |
