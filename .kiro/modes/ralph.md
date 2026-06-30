# Ralph Mode — Persistence Loop

**Trigger:** `ralph mode` or task has multiple stories, sustained effort, acceptance criteria.

**Core philosophy: The boulder never stops rolling.**

## Protocol

1. **Create a PRD file** at `.omk/prd.md`:
   ```markdown
   # PRD: [feature name]
   ## Stories
   - [ ] Story 1: [title] — [acceptance criteria]
   - [ ] Story 2: [title] — [acceptance criteria]
   ## Status: in-progress | blocked | complete
   ## Current: Story N
   ```

2. **Execute story-by-story.** For each story:
   - **GATE before marking complete** (all must pass):
     - [ ] Acceptance criteria met
     - [ ] Build passes
     - [ ] Relevant tests pass
     - [ ] No regressions
   - Gate failure → fix and re-verify (do NOT move on)
   - Gate pass → mark complete, proceed to next

3. **Never stop until:**
   - All stories complete, OR
   - Hard blocker requiring user input

4. **After all stories — deslop pass:**
   - Remove commented-out code
   - Remove dead imports
   - Remove overly defensive error handling
   - Consolidate duplicate logic
   - Consistent naming

5. **Final regression check** after deslop.

6. **Completion report:**
   ```markdown
   ## Done: [feature name]
   - Stories completed: N/N
   - Tests: passing
   - Deslop: applied
   - Regressions: none
   ```
