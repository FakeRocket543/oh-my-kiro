# ACP (Agent Client Protocol) Integration

oh-my-kiro works with OpenAB via Kiro CLI's ACP mode, enabling omk behaviors
through Discord, Telegram, or any OpenAB-supported channel.

## Setup

### 1. Install omk agent globally

```bash
mkdir -p ~/.kiro/agents
cp omk.json ~/.kiro/agents/omk.json
```

Ensure `omk.json` points to your local KIRO.md:
```json
{
  "name": "omk",
  "prompt": "file:///path/to/KIRO.md",
  ...
}
```

### 2. Configure OpenAB to use omk

In your OpenAB `config.toml`:

```toml
[agent]
command = "kiro-cli"
args = ["acp", "--trust-all-tools", "--agent", "omk"]
working_dir = "/path/to/working/dir"
```

### 3. Restart OpenAB

```bash
# Kill existing process
pkill -f openab
# Start fresh
./openab &
```

## How it works

```
User (Discord/Telegram)
  → OpenAB (message routing)
    → kiro-cli acp --agent omk
      → KIRO.md loaded as system prompt
        → Mode auto-detection
          → Ultrawork / Ralph / Interview / Direct
```

## Usage via chat

Once connected, just message naturally. omk modes activate automatically:

- **Ambiguous request** → Interview mode (asks clarifying questions)
- **Multi-step task** → Ultrawork (parallel subagents with tier routing)
- **Large feature** → Ralph (persistence loop with phase gates)
- **Simple fix** → Direct mode

### Manual triggers

- `ulw fix all the CSS issues` → Force ultrawork
- `ralph: build the auth system` → Force ralph with PRD tracking
- `interview me about the new feature` → Force interview

## Model routing in ACP

Subagents spawned via omk use the tier routing table:

| Task | Model | Credits |
|------|-------|---------|
| Code review | glm-5 | 0.50x |
| Architecture | claude-opus-4.6 | 2.20x |
| Implementation | claude-sonnet-4.6 | 1.30x |
| Boilerplate | qwen3-coder-next | 0.05x |

## Limitations in ACP mode

- `/spawn` (background sessions) not available — ACP is single-session
- Keyboard shortcuts (Ctrl+Shift+O) not applicable
- File references in chat use server-side paths, not client paths
- Subagent stages work normally (blocking mode)
