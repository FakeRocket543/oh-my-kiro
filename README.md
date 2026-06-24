# oh-my-kiro (omk)

Behavioral tuning layer for [Kiro CLI v3](https://kiro.dev/docs/cli/v3/). Makes the agent more persistent, disciplined, and structured — for both code and prose.

Requires **kiro-cli ≥ 2.9.0** (v3 engine via `--v3` flag or native v3 mode).

## Modes

| Mode | When | What it does |
|------|------|--------------|
| **Direct** | Simple fix / question | Normal Kiro behavior with omk discipline |
| **Interview** | Ambiguous request | One question per turn until spec is clear |
| **Ralph** | Large feature, multi-story | PRD tracking, story gates, deslop pass |
| **Chronicle** | Multi-stage writing project | Research → outline → draft → review → publish |
| **Spec** | Structured feature dev | Native Kiro `/spec` with omk gates applied |

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

## Hooks (.kiro/hooks/)

v3 hooks that enforce omk discipline automatically:

| Hook | Trigger | What it does |
|------|---------|--------------|
| Confidence gate | PreToolUse (writes) | Blocks writes if confidence <70% or file not read |
| Verify reminder | PostTaskExec | Reminds stop conditions after each task |
| Ralph state loader | SessionStart | Loads active PRD if one exists |

## Key Features

- **Confidence check** — assess before acting, stop if <70% confident
- **Spec integration** — native Kiro v3 `/spec` with omk behavioral gates
- **Chronicle mode** — structured writing pipeline with editorial gates
- **Source governance** — citation registry, independence analysis, counter-review
- **Three-pass translation** — translate / proofread / polish with glossary
- **Anti-slop rules** — no filler, no unnecessary abstractions
- **Wave execution** — parallel tool calls in structured batches
- **Subagent delegation** — task DAGs, review loops (native v3)

## Install

### As a global agent (recommended)

```bash
git clone ssh://git@git.lcn.tw:2222/felix/oh-my-kiro.git ~/.kiro/oh-my-kiro
ln -sf ~/.kiro/oh-my-kiro/omk.md ~/.kiro/agents/omk.md
ln -sf ~/.kiro/oh-my-kiro/KIRO.md ~/.kiro/KIRO.md
```

Skills and steering (optional — for writing/research workflows):
```bash
ln -sf ~/.kiro/oh-my-kiro/.kiro/skills/* ~/.kiro/skills/
ln -sf ~/.kiro/oh-my-kiro/.kiro/steering/* ~/.kiro/steering/
ln -sf ~/.kiro/oh-my-kiro/.kiro/hooks/* ~/.kiro/hooks/
```

### Per-project

Copy the `.kiro/` directory into your project:
```bash
cp -r ~/.kiro/oh-my-kiro/.kiro/ /path/to/project/.kiro/
cp ~/.kiro/oh-my-kiro/KIRO.md /path/to/project/.kiro/steering/omk.md
```

### Verify

```bash
kiro-cli agent list
# Should show: omk  Global  oh-my-kiro — interview, ralph, chronicle...
```

Launch:
```bash
kiro-cli --agent omk
# or with v3 engine:
kiro-cli --v3 --agent omk
```

## Usage

```
just do it          → Direct (skip interview)
interview me        → Force interview
ralph mode          → Force persistence loop
chronicle mode      → Force writing pipeline
/spec new <name>    → Native Kiro spec (omk discipline applied)
be columnist        → Feature writing persona
be translator       → Translation persona
be editor           → Proofreading persona
be researcher       → Fact-finding persona
```

## Structure

```
oh-my-kiro/
├── KIRO.md                              # Behavioral prompt (the brain)
├── omk.md                               # v3 agent config (markdown format)
├── omk.json                             # Legacy v2 agent config (kept for compat)
├── .kiro/
│   ├── hooks/
│   │   └── omk.json                    # v3 hooks (confidence gate, verify, state)
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

## Migration from v2

If you were using `omk.json` (v2 format):

1. The new `omk.md` replaces it as the primary agent config
2. `omk.json` is kept for backwards compatibility with kiro-cli <2.9
3. Update your symlink: `ln -sf ~/.kiro/oh-my-kiro/omk.md ~/.kiro/agents/omk.md`
4. Copy hooks: `ln -sf ~/.kiro/oh-my-kiro/.kiro/hooks/* ~/.kiro/hooks/`

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
