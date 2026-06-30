# Chronicle Mode — Writing Persistence Loop

**Trigger:** `chronicle mode` or multi-stage writing project — feature articles, series, investigative pieces.

**Core philosophy: Research precedes opinion. Cold prose, hot facts.**

## Protocol

1. **Create an editorial brief** at `.omk/editorial-brief.md`:
   ```markdown
   # Brief: [title]
   ## Angle: [one sentence thesis]
   ## Structure: [numbered sections]
   ## Style: [constraints — load project style from .kiro/steering/]
   ## Word target: [range]
   ## Status: research | drafting | review | published
   ## Current: [stage]
   ```

2. **Execute stage-by-stage:**
   - **Research** → use `deep-research` skill. Output: `research-notes.md` with citation registry.
   - **Outline** → mega-outline with source mapping per section. User approves before drafting.
   - **Draft** → write by section. Every factual claim needs a citation. No filler.
   - **Review iterations** → user gives line-level feedback → patch in place.
   - **Final pass** → kill filler, kill adverbs, confirm no markdown residue for target platform.
   - **Deploy** → platform-specific (CMS publish, DB insert, etc.)

3. **GATE per stage** (all must pass before advancing):
   - Research: ≥2 sources per key claim, gaps documented
   - Outline: user-approved
   - Draft: style rules pass, no [unverified] tags remaining
   - Final: platform render check (no broken formatting)

4. **Never stop until:**
   - All stages complete, OR
   - Hard blocker requiring user input (missing source, angle pivot)

5. **Completion report:**
   ```markdown
   ## Published: [title]
   - Sources cited: N
   - Word count: N
   - Platform: [target]
   - Style violations: 0
   ```
