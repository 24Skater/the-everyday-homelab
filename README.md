# The Everyday Homelab

A mini rack build documenting two clusters, start to finish: a 3-node Proxmox HA cluster and a 3-node bare-metal cluster for local AI/LLM testing. Written up as I go, for anyone else building something similar on modest mini-PC hardware.

## What's in the rack

- **Proxmox cluster** — 3x Lenovo ThinkCentre Tiny nodes (`TC1`, `TC2`, `TC3`) running Proxmox VE, being configured for HA
- **AI testing cluster** — 3x Dell OptiPlex 7050 Micro nodes, bare-metal Ubuntu Server + k3s, serving small quantized LLMs via Ollama
- **Networking** — TP-Link 8-port switch (3 uplinks, 1 fiber), all 6 nodes wired
- **Power** — Anker 65W USB-C adapters per node, ElecVoztile rack PDU
- **Console** — 10" touchscreen used as a diagnostic monitor (not a permanent console)

## Hardware inventory

| Component | Qty | Model | Role |
|---|---|---|---|
| Compute nodes | 3 | Lenovo ThinkCentre Tiny — `TC1`, `TC2`, `TC3` | Proxmox VE hypervisor nodes |
| AI cluster nodes | 3 | Dell OptiPlex 7050 Micro | Local AI/LLM testing |
| Switch | 1 | TP-Link 8-port (3 uplinks, 1x fiber) | Core network switch |
| Power supplies | 6 | Anker 65W USB-C PD adapter | One per node |
| Power distribution | 1 | ElecVoztile PDU, 125V 15A 1875W | Rack-mounted power strip |
| Display | 1 | 10" touchscreen (Dell mini PC, Windows) | Diagnostic monitor |
| Enclosure | 1 | Mini rack | Houses all nodes + switch |
| Wireless | 1 | Wireless router (planned) | AP mode, not yet installed |

## Status

- [x] Rack assembled, all nodes mounted
- [x] All 6 Ethernet cables made and connected
- [x] All 6 HDMI cables installed
- [x] All power wiring connected and confirmed working
- [x] Proxmox installed on TC1/TC2/TC3 (config pending)
- [ ] Proxmox HA / cluster config
- [ ] Wireless AP setup
- [x] AI cluster hardware ready (failed middle node replaced)
- [ ] AI cluster OS imaging (Ubuntu Server)
- [ ] k3s + Ollama deployment

## Docs

- [`docs/build-log.md`](docs/build-log.md) — step-by-step build log
- [`docs/proxmox-ha.md`](docs/proxmox-ha.md) — Proxmox cluster + HA plan
- [`docs/ai-cluster.md`](docs/ai-cluster.md) — AI cluster architecture + setup plan

## Images

Build photos go in [`images/`](images/) — referenced from the docs as they're added.
