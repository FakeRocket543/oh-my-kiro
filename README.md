# oh-my-kiro (omk)

Behavioral tuning layer for [Kiro CLI v3](https://kiro.dev/docs/cli/v3/). Makes the agent more persistent, disciplined, and structured — for both code and prose.

Requires **kiro-cli ≥ 2.9.0** (v3 engine via `--v3` flag or native v3 mode).

## Design Philosophy (v4)

**Slim core, on-demand everything else.** Only always-active rules live in `KIRO.md` (~100 lines). Modes, skills, and project-specific steering load only when triggered. This keeps token overhead minimal for simple tasks while retaining full power for complex workflows.

## Modes

| Mode | Trigger | File | When |
|------|---------|------|------|
| **Direct** | default | — | Simple fix, question, focused change |
| **Interview** | `interview me` | `.kiro/modes/interview.md` | Ambiguous request, missing constraints |
| **Ralph** | `ralph mode` | `.kiro/modes/ralph.md` | Large feature, multi-story scope |
| **Chronicle** | `chronicle mode` | `.kiro/modes/chronicle.md` | Multi-stage writing project |
| **Spec** | `/spec new <name>` | native Kiro v3 | Structured feature dev with requirements |

Default is Direct. Auto-fallback: confidence <70% → ask one clarifying question.

## Personas

| Keyword | Focus |
|---------|-------|
| `be reviewer` | Code review: bugs, style, missing tests, security |
| `be columnist` | Feature writing: cold prose, no filler (load project style) |
| `be translator` | Translation: faithful, glossary-managed, flag uncertainties |

## Skills (.kiro/skills/)

On-demand loaded skills for specific workflows:

| Skill | Triggers |
|-------|----------|
| [deep-research](.kiro/skills/deep-research/SKILL.md) | 查證, research, 調研, cross-country comparisons |
| [fact-check](.kiro/skills/fact-check/SKILL.md) | verify, 數字對嗎, validate claims, pre-publish review |
| [translation](.kiro/skills/translation/SKILL.md) | 翻譯, 校譯, 精修, proofread translation |

## Steering (.kiro/steering/)

Persistent context loaded into every session:

| File | Inclusion | Purpose |
|------|-----------|---------|
| [environment.md](.kiro/steering/environment.md) | always | SSH capabilities + host template |

**Project-specific steering** (editorial style, domain rules) belongs in the project's own `.kiro/steering/`, not in omk. See `examples/` for reference.

## Hooks (.kiro/hooks/)

v3 hooks that enforce omk discipline automatically:

| Hook | Trigger | What it does |
|------|---------|--------------|
| Confidence gate | PreToolUse (writes) | Blocks writes if confidence <70% or file not read |
| Verify reminder | PostTaskExec | Reminds stop conditions after each task |
| Ralph state loader | SessionStart | Loads active PRD if one exists |

## Key Features

- **Confidence check** — assess before acting, stop if <70% confident
- **Ralph persistence** — PRD tracking, story gates, deslop pass, regression check
- **Chronicle pipeline** — research → outline → draft → review → publish
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
ln -sf ~/.kiro/oh-my-kiro/KIRO.md ~/.kiro/agents/KIRO.md
```

Skills, steering, and hooks:
```bash
ln -sf ~/.kiro/oh-my-kiro/.kiro/skills/* ~/.kiro/skills/
ln -sf ~/.kiro/oh-my-kiro/.kiro/steering/* ~/.kiro/steering/
ln -sf ~/.kiro/oh-my-kiro/.kiro/hooks/* ~/.kiro/hooks/
ln -sf ~/.kiro/oh-my-kiro/.kiro/modes/* ~/.kiro/modes/
```

### Per-project

Copy the `.kiro/` directory into your project:
```bash
cp -r ~/.kiro/oh-my-kiro/.kiro/ /path/to/project/.kiro/
cp ~/.kiro/oh-my-kiro/KIRO.md /path/to/project/.kiro/steering/omk.md
```

Add project-specific editorial style or domain rules to the project's own `.kiro/steering/`. See `examples/inff-style.md` for a reference implementation.

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
be reviewer         → Code review persona
be columnist        → Feature writing persona
be translator       → Translation persona
```

## Structure

```
oh-my-kiro/
├── KIRO.md                              # Core behavioral prompt (~100 lines, always loaded)
├── omk.md                               # v3 agent config (markdown format)
├── omk.json                             # Legacy v2 agent config (backwards compat)
├── .kiro/
│   ├── hooks/
│   │   └── omk.json                    # v3 hooks (confidence gate, verify, state)
│   ├── modes/                           # On-demand mode definitions
│   │   ├── ralph.md                    # Persistence loop protocol
│   │   ├── interview.md                # Clarification protocol
│   │   └── chronicle.md                # Writing pipeline protocol
│   ├── steering/
│   │   └── environment.md              # Runtime environment (template, always loaded)
│   └── skills/
│       ├── deep-research/
│       │   └── SKILL.md                # Investigative research protocol
│       ├── fact-check/
│       │   └── SKILL.md                # Claim verification workflow
│       └── translation/
│           └── SKILL.md                # Translation/proofread/polish
├── examples/                            # Project-specific reference implementations
│   └── inff-style.md                   # Editorial style example (inff.cc)
├── LICENSE                              # MIT
└── README.md
```

## What Changed in v4

| Change | Why |
|--------|-----|
| KIRO.md slimmed 350→~100 lines | Reduce token overhead for simple tasks |
| Modes extracted to `.kiro/modes/` | On-demand loading instead of always-on |
| Personas reduced 8→3 | Removed overlap with modes/skills; kept only distinct lenses |
| inff-style.md → `examples/` | Project-specific content doesn't belong in framework |
| environment.md → template | No infrastructure data in public repo |
| Skills removed from resources | Already on-demand via `.kiro/skills/` trigger system |

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
