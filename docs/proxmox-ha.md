# Proxmox Cluster + HA Plan

<img src="../images/proxmox-badge.svg" width="200" alt="Proxmox VE logo">

Nodes: `TC1`, `TC2`, `TC3` — Lenovo ThinkCentre Tiny, Proxmox VE installed on all three.

Software versions and every other piece running on the rack are tracked in [`software.md`](software.md).

## Cluster formation

Join all 3 nodes into a single Proxmox cluster. Quorum with 3 nodes is a majority of 2 — no external QDevice/tie-breaker needed (that's only required for 2-node clusters).

## HA strategy

Rather than dedicating one full node as a pure backup, all 3 stay live cluster members with different roles:

- **TC1 + TC2** — primary compute pair, higher-priority HA group, run the workloads that should auto-failover
- **TC3** — lower HA priority, hosts backup/monitoring services day-to-day, but remains a full cluster member and automatically picks up VMs if TC1 or TC2 goes down

This gets real automatic failover on the two primary nodes plus a dedicated backup/monitoring role on the third, without sacrificing quorum or a third of total compute capacity.

## Storage for HA

ThinkCentre Tiny nodes have no shared storage (no SAN/NAS). Plan: **ZFS + Proxmox Storage Replication** — periodic (e.g. every few minutes) disk sync between nodes, the standard approach for small clusters without shared storage. Requires ZFS as the local storage backend on each node.

A shared NFS/iSCSI target via a NAS would be a cleaner alternative if one gets added later.

## Planned services (as VMs/LXCs on the cluster)

- **Uptime Kuma** — self-hosted uptime/status monitoring
- **Portainer** — Docker/container management UI
- *(add more here as decided)*

Given the ThinkCentre Tiny's limited RAM, lean toward LXC containers over full VMs for these — much lower overhead per service.

## Next steps

1. Form the cluster (Datacenter → Cluster → Join)
2. Set up ZFS + storage replication
3. Configure HA groups/priorities per the split above
4. Spin up LXCs for Uptime Kuma / Portainer
