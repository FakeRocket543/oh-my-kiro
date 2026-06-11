# oh-my-kiro (omk)

Behavioral tuning layer for [Kiro CLI](https://kiro.dev). Makes the agent more persistent, disciplined, and structured.

## Modes

| Mode | When | What it does |
|------|------|--------------|
| **Direct** | Simple fix / question | Normal Kiro behavior |
| **Interview** | Ambiguous request | One question per turn until spec is clear |
| **Ralph** | Large feature, multi-story | PRD tracking, story gates, deslop pass |

## Key Features

- **Confidence check** — assess before implementing, stop if <70% confident
- **Personas** — architect / tester / reviewer / implementer focus switching
- **Ralph mode** — structured persistence with file-based state, gate-driven story completion
- **Interview mode** — coarse-bin clarity assessment, crystallized spec output
- **Wave execution** — parallel tool calls in structured batches
- **Anti-slop rules** — no filler comments, no unnecessary abstractions
- **Execution discipline** — read before write, verify after change

## Install

```bash
git clone https://github.com/FakeRocket543/oh-my-kiro.git
cd oh-my-kiro
cp KIRO.md ~/.kiro/KIRO.md
```

## Usage

```
just do it          → Direct (skip interview)
interview me        → Force interview
ralph mode          → Force persistence loop
be architect        → Design-only persona
be tester           → Test-writing persona
be reviewer         → Code review persona
```

## Structure

```
oh-my-kiro/
├── KIRO.md          # Behavioral prompt (the brain)
├── omk.json         # Kiro agent config
├── LICENSE          # MIT
└── docs/
    └── aspirational.md  # Features pending platform support
```

## Attribution

Built on ideas from (all MIT licensed):
- [SuperClaude Framework](https://github.com/SuperClaude-Org/SuperClaude_Framework) — confidence check, personas, wave execution
- [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) — ralph, interview
- [oh-my-claude](https://github.com/TechDufus/oh-my-claude) — context protection, communication rules
- [oh-my-hermes](https://github.com/witt3rd/oh-my-hermes) — coarse scoring, file-based state
- [Andrej Karpathy's CLAUDE.md](https://github.com/mulica-ai/andrej-karpathy-skills) — coding discipline

## License

MIT
