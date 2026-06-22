# oh-my-kiro (omk)

Behavioral tuning layer for [Kiro](https://kiro.dev). Makes the agent more persistent, disciplined, and structured — for both code and prose.

## Modes

| Mode | When | What it does |
|------|------|--------------|
| **Direct** | Simple fix / question | Normal Kiro behavior |
| **Interview** | Ambiguous request | One question per turn until spec is clear |
| **Ralph** | Large feature, multi-story | PRD tracking, story gates, deslop pass |
| **Chronicle** | Multi-stage writing project | Research → outline → draft → review → publish |

## Personas

| Keyword | Focus |
|---------|-------|
| `be architect` | Design only. Diagrams, tradeoffs, decisions. |
| `be tester` | Write tests. Find edge cases. |
| `be reviewer` | Code review. Bugs, style, missing tests. |
| `be implementer` | Default. Write code, fix bugs, ship. |
| `be columnist` | Feature writing. inff.cc style. Cold prose, no filler. |
| `be translator` | Translation. Faithful, glossary-managed, flagged uncertainties. |
| `be editor` | Proofreading. Line-by-line comparison, three-pass protocol. |
| `be researcher` | Fact-finding. Source governance, citation registry, counter-review. |

## Skills (.kiro/skills/)

On-demand loaded skills for specific workflows:

| Skill | Triggers |
|-------|----------|
| [deep-research](.kiro/skills/deep-research/SKILL.md) | 查證, research, 調研, cross-country comparisons |
| [fact-check](.kiro/skills/fact-check/SKILL.md) | verify, 數字對嗎, validate claims, pre-publish review |
| [translation](.kiro/skills/translation/SKILL.md) | 翻譯, 校譯, 精修, proofread translation |

## Steering (.kiro/steering/)

Persistent context loaded into sessions:

| File | Inclusion | Purpose |
|------|-----------|---------|
| [inff-style.md](.kiro/steering/inff-style.md) | manual | Editorial style rules for inff.cc feature writing |

## Key Features

- **Confidence check** — assess before acting, stop if <70% confident
- **Chronicle mode** — structured writing pipeline with editorial gates
- **Source governance** — citation registry, independence analysis, counter-review
- **Three-pass translation** — translate / proofread / polish with glossary
- **Anti-slop rules** — no filler, no unnecessary abstractions, no prohibited words
- **Wave execution** — parallel tool calls in structured batches

## Install

```bash
git clone ssh://git@git.lcn.tw:2222/felix/oh-my-kiro.git
cd oh-my-kiro
cp KIRO.md ~/.kiro/KIRO.md
cp -r .kiro/skills/* ~/.kiro/skills/
cp -r .kiro/steering/* ~/.kiro/steering/
```

Or symlink:
```bash
ln -sf $(pwd)/KIRO.md ~/.kiro/KIRO.md
ln -sf $(pwd)/.kiro/skills/* ~/.kiro/skills/
ln -sf $(pwd)/.kiro/steering/* ~/.kiro/steering/
```

## Usage

```
just do it          → Direct (skip interview)
interview me        → Force interview
ralph mode          → Force persistence loop
chronicle mode      → Force writing pipeline
be columnist        → Feature writing persona
be translator       → Translation persona
be editor           → Proofreading persona
be researcher       → Fact-finding persona
```

## Structure

```
oh-my-kiro/
├── KIRO.md                              # Behavioral prompt (the brain)
├── omk.json                             # Kiro agent config
├── .kiro/
│   ├── steering/
│   │   └── inff-style.md               # Editorial style rules
│   └── skills/
│       ├── deep-research/
│       │   └── SKILL.md                # Investigative research protocol
│       ├── fact-check/
│       │   └── SKILL.md                # Claim verification workflow
│       └── translation/
│           └── SKILL.md                # Translation/proofread/polish
└── LICENSE                              # MIT
```

## Attribution

Built on ideas from (all MIT licensed):
- [SuperClaude Framework](https://github.com/SuperClaude-Org/SuperClaude_Framework) — confidence check, personas, wave execution
- [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) — ralph, interview
- [oh-my-claude](https://github.com/TechDufus/oh-my-claude) — context protection, communication rules
- [oh-my-hermes](https://github.com/witt3rd/oh-my-hermes) — coarse scoring, file-based state
- [Andrej Karpathy's CLAUDE.md](https://github.com/mulica-ai/andrej-karpathy-skills) — coding discipline
- [daymade/claude-code-skills](https://github.com/daymade/claude-code-skills) — deep-research, fact-checker, source governance
- [cellear/claude-fact-check-skill](https://github.com/cellear/claude-fact-check-skill) — source independence analysis
- [obra/superpowers](https://github.com/obra/superpowers) — skill writing methodology

## License

MIT
