# Aspirational — Features pending Kiro platform support

> Only features that **cannot execute today**. Everything else has moved to KIRO.md.

---

## Multi-model subagent routing

**Requires:** Model selection per subagent (not just agent config)

**Current state:** Kiro subagents use the agent config's model. You cannot specify a different model per spawn.

**Desired:**
- Route comprehension tasks → small/cheap model
- Route standard implementation → mid-tier model
- Route architecture decisions → strongest model
- Route domain-specific review (e.g., zh-TW quality) → specialized model

**Multi-LLM review pattern (desired, not yet possible):**
```
Subagent A (strong model): correctness + logic review
Subagent B (specialized): domain-specific quality check
Subagent C (cheap model): mechanical bug finding
→ Main agent: synthesize consensus + flag disagreements
```

---

## Feature Request for Kiro

- `spawn --model <name>` or model field in agent config that overrides the session model

Relevant issue: [#2288](https://github.com/kirodotdev/Kiro/issues/2288)

---

## Already implemented (moved to KIRO.md)

These were previously aspirational but now work:
- ~~Parallel subagent execution~~ → up to 4 concurrent
- ~~Task dependency graphs~~ → DAG support built-in
- ~~Spawn with await~~ → results auto-return via summary tool
- ~~Review loops~~ → trigger-based retry with max iterations
