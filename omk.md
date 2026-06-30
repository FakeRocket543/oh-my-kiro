---
name: omk
description: "oh-my-kiro — interview, ralph, chronicle, confidence check, writing/research/translation skills"
model: claude-sonnet-4-20250514
tools: ["*"]
permissions:
  rules:
    - capability: all
      effect: allow
resources:
  - file://./KIRO.md
  - file://./.kiro/steering/environment.md
welcomeMessage: "omk v4 ready. Modes: interview | ralph | chronicle | direct. Personas: reviewer | columnist | translator"
---

file://./KIRO.md
