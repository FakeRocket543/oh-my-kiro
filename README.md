# oh-my-kiro (omk)

Multi-agent orchestration behavioral layer for [Kiro CLI](https://kiro.dev).

Four execution modes that activate automatically based on task complexity:

| Mode | When | What it does |
|------|------|--------------|
| **Direct** | Simple fix / question | Normal Kiro behavior |
| **Interview** | Ambiguous request | One question per turn until spec is clear |
| **Ultrawork** | Multi-step, parallelizable | DAG pipeline with model-tier routing |
| **Ralph** | Large feature, multi-story | PRD tracking, story gates, deslop pass |

## Install

```bash
# Clone
git clone https://github.com/anthropic-felix/oh-my-kiro.git
cd oh-my-kiro

# Install agent config + behavioral prompt
cp KIRO.md ~/.kiro/KIRO.md
cp omk.json ~/.kiro/agents/omk.json

# Fix path in omk.json to point to your KIRO.md location
# (edit the "prompt" and "resources" fields)
```

Then edit `~/.kiro/agents/omk.json`:
```json
{
  "prompt": "file:///Users/YOUR_USER/.kiro/KIRO.md",
  "resources": ["file:///Users/YOUR_USER/.kiro/KIRO.md"]
}
```

## Usage

### As default agent
```bash
kiro-cli settings chat.defaultAgent omk
kiro-cli chat
```

### Per-session
```bash
kiro-cli chat --agent omk
```

### With OpenAB (ACP mode)
```toml
# config.toml
[agent]
command = "kiro-cli"
args = ["acp", "--trust-all-tools", "--agent", "omk"]
working_dir = "/path/to/your/project"
```

### Force a mode
```
just do it          → Direct (skip interview)
let's plan this     → Consensus planning
interview me        → Force interview
ralph mode          → Force persistence loop
```

## Model Routing (Ultrawork)

Subagents are dispatched by cost tier:

| Task | Model | Rationale |
|------|-------|-----------|
| File read / summarize | haiku-4.5 | Comprehension only |
| Boilerplate | qwen3-coder-next | Cheap template work |
| Standard implementation | sonnet-4.6 | Quality/cost balance |
| Code review / bugs | deepseek-3.2 | Good at 1/4 cost |
| Chinese proofreading | glm-5 | Native zh quality |
| Architecture decisions | opus-4.6 | Complex judgment |

> If a model isn't available in your setup, stages fall back to the default model. Adjust the tier table in `KIRO.md` to match your available models.

## What's Inside

```
oh-my-kiro/
├── KIRO.md          # Behavioral prompt (the brain)
├── omk.json         # Kiro agent config
├── LICENSE          # MIT
└── docs/
    └── acp-integration.md
```

## Requirements

- [Kiro CLI](https://kiro.dev) installed
- For Ultrawork parallel execution: models accessible via your subscription or API keys

## Attribution

Built on ideas from (all MIT licensed):
- [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) — ultrawork, ralph
- [oh-my-claude](https://github.com/TechDufus/oh-my-claude) — context protection, orchestrator protocol
- [SuperClaude Framework](https://github.com/SuperClaude-Org/SuperClaude_Framework) — behavioral modes
- [oh-my-hermes](https://github.com/witt3rd/oh-my-hermes) — one-task-per-invocation, subagent isolation
- [Andrej Karpathy's CLAUDE.md](https://github.com/multica-ai/andrej-karpathy-skills) — coding discipline

## License

MIT
