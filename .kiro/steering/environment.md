---
inclusion: always
---

# Runtime Environment

You have full SSH access to remote servers. Keys are pre-configured in ~/.ssh/config.

## Capabilities

- SSH to remote servers (`ssh <host> "command"`)
- Fetch URLs with curl
- Search the web (web_search / web_fetch tools)
- Clone/pull git repos (git.lcn.tw via SSH)

## SSH Hosts (pre-configured)

| Alias | Host | Notes |
|-------|------|-------|
| beta.lcn.tw | Oracle Tokyo | direct |
| dev.lcn.tw | OVH Singapore | port 22222 |
| hk.lcn.tw / hk | Hong Kong | direct |
| m6 | rk3588 32GB | port 22222 |
| oci | Oracle Cloud | via cloudflared |
| ovh | OVH | via cloudflared |
| shuj | — | via cloudflared |
| p1.lcn.tw | — | via cloudflared |
| git.lcn.tw | Forgejo | port 2222 |

## Pattern: Remote Operations

```bash
# Run command on remote host
ssh beta.lcn.tw "df -h"

# Copy file from remote
scp dev.lcn.tw:/path/to/file /tmp/

# Use remote tools (python, docker, node, etc.)
ssh m6 "cd ~/project && docker compose up -d"
ssh dev.lcn.tw "python3 script.py"
```

When a task requires tools not available locally (python, node, docker, ffmpeg, etc.),
SSH to the appropriate remote host and execute there.
