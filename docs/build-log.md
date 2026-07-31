# Build Log

## 1. Rack assembly
✅ Done — mini rack assembled and standing on a shelf/bench.

## 2. Node mounting
✅ Done — top to bottom: touchscreen (mounted on top, hinged), TC1, TC2, TC3, TP-Link switch, then 3x OptiPlex 7050 units. PDU mounted in the rear/side section above the OptiPlex bank. Middle OptiPlex was swapped for a replacement after failing — all 3 physically good now.

## 3. Power wiring
✅ Done — all 6 nodes on Anker 65W USB-C adapters, confirmed connected and working. PDU powered on.

## 4. Network cabling
✅ Done — all 6 Ethernet runs made and connected:
- 3x cable (green boots) — TC1/TC2/TC3 → switch
- 3x cable (white boots) — switch → each OptiPlex node

All 6 HDMI cables also installed (used for checking each node's boot/video output on the touchscreen, not as a permanent console).

## 5. Proxmox install verification
✅ Proxmox installed on all 3 ThinkCentres (TC1, TC2, TC3) — configuration (clustering, storage, networking) still to be done. See [`proxmox-ha.md`](proxmox-ha.md).

## 6. AI cluster node setup
🟡 In progress — hardware ready (middle node replaced), nodes are un-imaged (no OS installed yet). Next step: image with Ubuntu Server. See [`ai-cluster.md`](ai-cluster.md).

---

## Known issues / resolved

- ✅ ~~Middle Dell OptiPlex node died~~ — replaced, all 3 OptiPlex nodes physically good to go.

## Open questions

- VLAN split between Proxmox management traffic and AI cluster traffic, or flat/single subnet?
- IP addressing scheme — static assignments vs DHCP reservations for the 6 nodes.
- Wireless AP hardware/placement — not yet installed.
