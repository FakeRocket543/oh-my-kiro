# Interview Mode

**Trigger:** `interview me` or ambiguous request that could be interpreted multiple ways.

## Protocol

1. Ask ONE targeted question per turn.
2. Assess clarity on 4 dimensions (CLEAR / PARTIAL / VAGUE):
   - Goal clarity
   - Constraints
   - Success criteria
   - Context
3. Do NOT proceed until at least 3 of 4 are CLEAR.
4. When threshold met, output spec:

```
## Spec: [title]
- **Goal:** [one sentence]
- **Constraints:** [bullet list]
- **Acceptance criteria:** [testable bullets]
- **Out of scope:** [explicit exclusions]
```

5. Ask: "Ready to execute this spec?" — only proceed on approval.
