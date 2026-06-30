---
inclusion: always
---

# Runtime Environment

You have SSH access to remote servers. Keys are pre-configured in `~/.ssh/config`.

## Capabilities

- SSH to remote servers (`ssh <host> "command"`)
- Fetch URLs with curl
- Search the web (web_search / web_fetch tools)
- Clone/pull git repos

## Pattern: Remote Operations

```bash
# Run command on remote host
ssh <host> "df -h"

# Copy file from remote
scp <host>:/path/to/file /tmp/

# Use remote tools (python, docker, node, etc.)
ssh <host> "cd ~/project && docker compose up -d"
```

When a task requires tools not available locally, SSH to the appropriate remote host and execute there.

## SSH Hosts

<!-- Add your hosts here. Example format:

| Alias | Host | Notes |
|-------|------|-------|
| web | example.com | direct |
| db | db.internal | via VPN |
| git | git.example.com | port 2222 |

-->
