# Software

Everything running or planned on the rack, by layer. Hardware and purchase links are in [`gear.md`](gear.md) — this tracks what's installed on top of it.

## Proxmox cluster

<img src="../images/proxmox-badge.svg" width="200" alt="Proxmox VE logo">

| Software | Role | Status |
|---|---|---|
| [Proxmox VE](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) | Hypervisor on `TC1`, `TC2`, `TC3` | <img src="../images/icons/check.svg" width="16" align="top" alt="Done"> Installed on all three nodes |
| Proxmox clustering | Joins the three nodes into one cluster, 2-of-3 quorum | <img src="../images/icons/progress.svg" width="16" align="top" alt="Next up"> Not yet formed |
| ZFS | Local storage backend, required for replication | <img src="../images/icons/planned.svg" width="16" align="top" alt="Planned"> Not yet configured |
| Proxmox Storage Replication | Periodic ZFS snapshot sync between nodes — the HA mechanism in place of shared storage | <img src="../images/icons/planned.svg" width="16" align="top" alt="Planned"> Depends on ZFS + clustering |
| [Uptime Kuma](https://github.com/louislam/uptime-kuma) | Self-hosted uptime/status monitoring, as an LXC | <img src="../images/icons/planned.svg" width="16" align="top" alt="Planned"> Not yet deployed |
| [Portainer](https://www.portainer.io/) | Docker/container management UI, as an LXC | <img src="../images/icons/planned.svg" width="16" align="top" alt="Planned"> Not yet deployed |

Full reasoning on the clustering and storage design is in [`proxmox-ha.md`](proxmox-ha.md).

## AI cluster

| Software | Role | Status |
|---|---|---|
| [Ubuntu Server 24.04 LTS](https://ubuntu.com/server) | Bare-metal OS on `AI1`, `AI2`, `AI3` — no hypervisor layer | <img src="../images/icons/planned.svg" width="16" align="top" alt="Planned"> Not yet imaged |
| [k3s](https://k3s.io/) | Lightweight Kubernetes — 1 server node, 2 agents | <img src="../images/icons/planned.svg" width="16" align="top" alt="Planned"> Depends on OS imaging |
| [Ollama](https://ollama.com/) | Model server, run as an independent replica on each node behind a load-balanced Service | <img src="../images/icons/planned.svg" width="16" align="top" alt="Planned"> Depends on k3s |

**Starting models**, once Ollama is deployed:

| Model | Size |
|---|---|
| Llama 3.2 | 3B |
| Phi-3.5-mini | — |
| Qwen2.5 | 7B (Q4) |

Full reasoning on the serving pattern — replicas instead of one model split across nodes — is in [`ai-cluster.md`](ai-cluster.md).

---

Nothing in this doc is aspirational: a row marked planned has no config behind it yet. See the [build progress chart](../README.md#status) on the main README for the current percentage.
