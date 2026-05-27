# oh-my-kiro (omk)

Behavioral tuning layer for [Kiro CLI](https://kiro.dev). Makes the agent more persistent, disciplined, and structured.

Three execution modes that activate automatically based on task complexity:

| Mode | When | What it does |
|------|------|--------------|
| **Direct** | Simple fix / question | Normal Kiro behavior |
| **Interview** | Ambiguous request | One question per turn until spec is clear |
| **Ralph** | Large feature, multi-story | PRD tracking, story gates, deslop pass |

## What actually works

- **Ralph mode** — structured persistence with file-based state, gate-driven story completion
- **Interview mode** — coarse-bin clarity assessment, crystallized spec output
- **Anti-slop rules** — no filler comments, no unnecessary abstractions
- **Execution discipline** — read before write, verify after change
- **Parallel tool calls** — multiple reads/searches in one turn

## What doesn't work (yet)

- Subagent model routing (Kiro doesn't support model selection per spawn)
- Parallel subtask execution (spawn is fire-and-forget, no await)
- Multi-agent consensus planning

See [`docs/aspirational.md`](docs/aspirational.md) for designs waiting on platform support.
Relevant Kiro issues: [#2288](https://github.com/kirodotdev/Kiro/issues/2288), [#1408](https://github.com/kirodotdev/Kiro/issues/1408)

## Install

```bash
git clone https://github.com/FakeRocket543/oh-my-kiro.git
cd oh-my-kiro

cp KIRO.md ~/.kiro/KIRO.md
```

## Usage

### Force a mode
```
just do it          → Direct (skip interview)
interview me        → Force interview
ralph mode          → Force persistence loop
```

## What's Inside

```
oh-my-kiro/
├── KIRO.md              # Behavioral prompt (the brain)
├── omk.json             # Kiro agent config
├── LICENSE              # MIT
└── docs/
    ├── acp-integration.md
    └── aspirational.md  # Features pending platform support
```

## Attribution

Built on ideas from (all MIT licensed):
- [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) — ralph, interview
- [oh-my-claude](https://github.com/TechDufus/oh-my-claude) — context protection, communication rules
- [oh-my-hermes](https://github.com/witt3rd/oh-my-hermes) — coarse scoring, file-based state
- [Andrej Karpathy's CLAUDE.md](https://github.com/mulica-ai/andrej-karpathy-skills) — coding discipline

## License

MIT
