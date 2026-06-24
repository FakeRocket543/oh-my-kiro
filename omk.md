---
name: omk
description: "oh-my-kiro — interview, ralph, chronicle, confidence check, writing/research/translation skills"
model: claude-sonnet-4-20250514
tools: ["*"]
permissions:
  - capability: builtin
    effect: allow
  - capability: shell
    effect: allow
  - capability: filesystem
    effect: allow
  - capability: mcp
    effect: allow
  - capability: subagent
    effect: allow
resources:
  - file://./KIRO.md
  - file://./.kiro/steering/inff-style.md
  - file://./.kiro/skills/deep-research/SKILL.md
  - file://./.kiro/skills/fact-check/SKILL.md
  - file://./.kiro/skills/translation/SKILL.md
welcomeMessage: "omk ready. Modes: interview | ralph | chronicle | direct. Personas: architect | tester | reviewer | implementer | columnist | translator | editor | researcher"
---

file://./KIRO.md
