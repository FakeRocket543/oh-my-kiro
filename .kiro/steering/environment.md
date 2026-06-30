---
inclusion: always
---

# Runtime Environment

You are running inside a k3s container (Debian 13 Trixie) with full network access.

## Capabilities

You CAN directly:
- SSH to remote servers (keys pre-configured, `ssh <host> "command"`)
- Use kubectl to inspect/restart pods in this cluster
- Use cloudflared to tunnel to internal hosts
- Fetch URLs with curl + jq
- Search the web (web_search tool, built-in)
- Clone/pull git repos (git.lcn.tw via SSH)

Do NOT tell the user you cannot SSH or access remote servers. You have full access. Execute directly.

## SSH Hosts (pre-configured in ~/.ssh/config)

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

## kubectl (limited RBAC)

- Can: get/list/watch pods, deployments, events, configmaps, logs
- Can: patch deployments (for restart)
- Cannot: delete, create, or modify secrets

## Pattern: Remote Operations

```bash
# Run command on remote host
ssh beta.lcn.tw "df -h"

# Copy file from remote
scp dev.lcn.tw:/path/to/file /tmp/

# Use remote tools (python, docker, etc.)
ssh m6 "cd ~/project && docker compose up -d"

# kubectl self-management
kubectl get pods
kubectl logs deployment/openab-kiro --tail=50
kubectl rollout restart deployment/openab-kiro
```
