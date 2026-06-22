---
name: translation
description: Use when translating, proofreading translations, revising translated text, or polishing multilingual content. Triggers include "翻譯", "校譯", "精修", "translate", "proofread translation", "review this translation", comparing source and target text, glossary management.
---

# Translation / Proofreading / Polishing

Three-pass protocol for translation, revision, and refinement of multilingual text.

## Overview

Structured approach to translation and post-editing. Distinguishes between three distinct activities with different goals and constraints.

## Modes

| Activation | Mode | Goal |
|-----------|------|------|
| `translate [lang]` | Translation | Produce faithful target text from source |
| `校譯` / `proofread` | Proofreading | Compare source↔target, flag errors |
| `精修` / `polish` | Polishing | Improve target text fluency without changing meaning |

## Mode 1: Translation

### Principles

1. **Fidelity first.** Meaning > style > brevity.
2. **Transparency.** Flag difficult passages with `[T: note]` inline comments.
3. **Register match.** Academic → academic. Colloquial → colloquial. Don't elevate or flatten.
4. **Cultural adaptation.** Localize references only when meaning would be lost. Otherwise preserve with explanation.

### Protocol

1. Read entire source before starting.
2. Translate paragraph by paragraph (not sentence by sentence — preserve flow).
3. For terms with no clean equivalent: provide transliteration + explanation on first occurrence, then use chosen term consistently.
4. Maintain glossary in `.omk/glossary.md`:
   ```markdown
   | Source term | Target term | Context/Notes |
   |-------------|-------------|---------------|
   | Gemeinschaft | 禮俗社會 | 費孝通譯法，用於鄉土中國語境 |
   ```
5. Output: clean target text + separate `[T: ...]` notes file if needed.

### What NOT to Do

- Don't add explanations not in the source
- Don't merge or split paragraphs
- Don't "improve" the original's logic
- Don't translate proper nouns without checking standard translations

## Mode 2: Proofreading (校譯)

### Three-Pass Protocol

**Pass 1 — Accuracy (硬傷)**
- Mistranslations (wrong meaning)
- Omissions (content skipped)
- Additions (content not in source)
- Number/date errors
- Name/term inconsistencies

**Pass 2 — Fluency (語感)**
- Unnatural phrasing in target language
- Calques (source-language syntax leaking through)
- Register mismatch
- Ambiguity introduced by translation

**Pass 3 — Consistency (統一)**
- Term consistency throughout document
- Style consistency (formal/informal mixing)
- Formatting preservation (headers, lists, emphasis)

### Output Format

```markdown
## Proofread Report

### Pass 1: Accuracy
| Location | Source | Current target | Issue | Suggested fix |
|----------|--------|----------------|-------|---------------|
| §2 ¶3 | "différend" | 「不同」 | Mistranslation: différend = 爭端, not 不同 | 「爭端」 |

### Pass 2: Fluency
| Location | Current | Issue | Suggestion |
|----------|---------|-------|------------|
| §1 ¶1 | 「這是因為...的原因」 | Redundant causation | 「這是因為...」 |

### Pass 3: Consistency
| Term | Occurrences | Issue | Resolution |
|------|-------------|-------|------------|
| parquet | §2: 檢察署 / §5: 地檢署 | Inconsistent | Use 檢察署 throughout |

### Summary
- Accuracy issues: N (critical: N, minor: N)
- Fluency issues: N
- Consistency issues: N
```

## Mode 3: Polishing (精修)

### Principles

1. **Don't change meaning.** Polish ≠ rewrite.
2. **Target-language native fluency.** Read as if originally written in target language.
3. **Kill translationese.** Remove patterns that only exist because of source-language interference.
4. **Preserve voice.** If the source is dry, target should be dry. Don't add personality.

### Common Translationese Patterns (zh-TW)

| Pattern | Example | Fix |
|---------|---------|-----|
| Passive overuse | 「被認為是」 | 「人們認為」or restructure |
| Nominal style | 「進行了一個調查」 | 「調查了」 |
| Redundant pronouns | 「他們的國家，他們的人民」 | 「該國人民」 |
| Calque connectors | 「在另一方面」 | 「另一面」or delete |
| Over-specification | 「在2026年6月的時候」 | 「2026年6月」 |

### Protocol

1. Read target text once without source (感受是否通順).
2. Mark passages that feel "translated" (不自然).
3. Revise those passages. Minimal changes.
4. Re-read revised version for flow.
5. Compare with source only at the end to confirm no meaning drift.

### Output

Two options (ask user which):
- **Inline markup**: `~~deleted~~` + **added** in same document
- **Clean version**: final polished text only, with change summary at end

## Glossary Management

Maintain `.omk/glossary.md` across sessions:

```markdown
# Translation Glossary

## [Project/Domain]

| Source | Target | Notes | First used |
|--------|--------|-------|------------|
| opportunité des poursuites | 起訴便宜主義 | FR legal term | lyhanna-notes |
| classement sans suite | 結案不起訴 | FR legal term | lyhanna-notes |
| Barnahus | 兒童之家（一站式中心） | Nordic model | lyhanna-notes |
```

Rules:
- New terms get added automatically during translation
- Conflicts flagged for user resolution
- Glossary is authoritative once entries are confirmed

## Language-Pair Specific Notes

### FR → zh-TW
- French nominal style → convert to verbal where possible
- Relative clauses (qui/que/dont) → restructure, don't nest
- Subjunctive mood → find Chinese equivalent emphasis or delete

### EN → zh-TW
- Sentence-initial "However" → don't translate as 「然而」(see inff-style prohibitions)
- Passive voice → active voice preferred
- Long attributive chains → break into separate sentences

### zh-CN → zh-TW
- Script conversion is trivial; **register** is the real work
- 「的得地」usage differs
- Political/cultural terms may need annotation

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Translating without reading full source first | Always read complete text before starting |
| Inconsistent terminology | Maintain and check glossary |
| Polishing beyond recognition | Compare with source after polishing |
| Ignoring register (formalizing informal text) | Match source register explicitly |
| Not flagging uncertain translations | Use `[T: ...]` markers liberally |
