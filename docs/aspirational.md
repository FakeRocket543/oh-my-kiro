# Aspirational — Features pending Kiro platform support

> These patterns are valid designs but **cannot execute in Kiro CLI today**.
> They require platform-level features (subagent model routing, task graphs, spawn callbacks).
> Kept here for reference; re-integrate when Kiro supports them.

---

## Ultrawork: Multi-model subagent routing

**Requires:** Subagent model selection, spawn await/callback

**Subagent routing heuristic:**
- Simple search/read tasks → `model: "claude-haiku-4.5"` (0.40x)
- Code generation, standard implementation → `model: "claude-sonnet-4.6"` (1.30x)
- Chinese text quality review, zh-TW naming → `model: "glm-5"` (0.50x)
- Code review, bug finding → `model: "deepseek-3.2"` (0.25x)
- Complex architecture, judgment calls → keep in main thread (opus 2.20x)
- Throwaway scaffolding, boilerplate → `model: "qwen3-coder-next"` (0.05x)

**Multi-LLM review pattern (fire all in parallel):**
```
Stage A (opus):    correctness + logic review
Stage B (glm-5):  zh-TW quality + naming + cultural fit
Stage C (deepseek): code bugs + edge cases
→ Main agent: synthesize consensus + flag disagreements
```

**Cost-aware execution:**
| Task Type | Model | Credits | Rationale |
|-----------|-------|---------|-----------|
| File read + summarize | haiku-4.5 | 0.40x | Comprehension only |
| Boilerplate generation | qwen3-coder-next | 0.05x | Template work |
| Standard implementation | sonnet-4.6 | 1.30x | Balance quality/cost |
| Chinese proofreading | glm-5 | 0.50x | Native zh + frontier reasoning |
| Code review + bug finding | glm-5 | 0.50x | SWE-bench #1 tier at 1/4 Opus cost |
| Agentic multi-step tasks | glm-5 | 0.50x | Specifically tuned for tool-calling workflows |
| Long-context analysis | glm-5 | 0.50x | 200K context, can ingest full codebases |
| Architecture decision | opus-4.6 | 2.20x | Complex judgment calls |
| Multi-file refactor | sonnet-4.6 | 1.30x | One subagent per file |
| Cheap code generation | deepseek-3.2 | 0.25x | Good enough for scaffolding |

---

## Ultrawork: Parallel subagent task graph

**Requires:** Spawn with await, subagent dependency coordination

**Execution pattern:**
```
1. Decompose task into subtasks
2. Identify dependencies (A→B means B needs A's output)
3. Group into levels:
   Level 0: [independent tasks] → fire in parallel
   Level 1: [tasks depending on level 0] → fire after level 0 completes
   Level N: ...
4. Execute each level, verify after each
5. Final verification: build + test + lint
```

---

## Consensus Planning via parallel subagents

**Requires:** Multiple subagents with different roles running simultaneously, results synthesis

1. **Planner perspective** (via subagent): Propose implementation plan
2. **Architect perspective** (via subagent): Review for technical soundness
3. **Critic perspective** (via subagent): Challenge assumptions, find gaps

---

## Agent Roles (subagent delegation)

**Requires:** Subagent spawn with await, role-specific prompts

| Role | Job |
|------|-----|
| **Advisor** | Gap analysis, scope risks |
| **Critic** | Review plans BEFORE execution |
| **Validator** | Tests, linters, verification |
| **Librarian** | Read large files, summarize |
| **Security** | OWASP, secrets, injection audit |

---

## Orchestrator Protocol

**Requires:** Subagent coordination, spawn await

- **Find** → subagent search → **Understand** → subagent read/summarize → **Plan** → consensus → **Execute** → parallel subagents → **Verify** → shell commands

---

## Feature Requests for Kiro

1. `spawn --model <model>` — specify model for spawned agent
2. `spawn --await` — block until spawned agent completes, return result
3. Task graph primitive — define dependencies between spawned tasks
4. Subagent result forwarding — spawned agent output enters parent context
