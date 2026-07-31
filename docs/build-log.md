# Build Log

## 1. Rack assembly
<img src="../images/icons/check.svg" width="17" align="top" alt="Done"> Done — [GeeekPi 8U 10-inch cabinet](https://www.amazon.com/dp/B0FWJXF7FM) (DeskPi RackMate T1 Plus, 260 mm depth) assembled and standing on a bench.

## 2. Node mounting
<img src="../images/icons/check.svg" width="17" align="top" alt="Done"> Done — top to bottom: touchscreen (mounted on top, hinged), PVE1, PVE2, PVE3, TP-Link switch, then 3x OptiPlex 7050 units. PDU mounted in the rear/side section above the OptiPlex bank. Middle OptiPlex was swapped for a replacement after failing — all 3 physically good now.

Each node sits on a [GeeekPi 1U mini-PC shelf](https://www.amazon.com/dp/B0FN44R7F2). These carry an RJ45 CAT6 and an HDMI pass-through on the front face, so each node's rear ports are brought forward and everything patches from the front of the rack rather than reaching around the back.

## 3. Power wiring
<img src="../images/icons/check.svg" width="17" align="top" alt="Done"> Done — all 6 nodes confirmed connected and working, PDU powered on.

Every node runs the same [Anker Nano 65W GaN II PPS](https://www.amazon.com/dp/B08T5QN2TR) charger. Neither machine takes USB-C power natively, so a short adapter cable does the translation:

- **ThinkCentre Tiny** — [USB-C to Lenovo slim tip, 100W PD](https://www.amazon.com/dp/B0947RD4H2)
- **OptiPlex 7050 Micro** — [USB-C to 4.5 x 3.0 mm barrel, 100W PD](https://www.amazon.com/dp/B0975DWM1R)

One charger model across the whole rack: a single spare covers any node, the GaN bricks stack without fighting for outlet space, and a dead PSU is a cheap generic part instead of a discontinued OEM adapter.

Worth noting: 65W matches the OEM rating for both machines rather than exceeding it, so there is no headroom for a higher-draw configuration. Six nodes at full tilt is roughly 390W against the [PDU's](https://www.amazon.com/dp/B0FRMQJGJB) 15A / 1875W, so the rail has plenty of room — the per-node budget is the constraint, not the total.

## 4. Network cabling
<img src="../images/icons/check.svg" width="17" align="top" alt="Done"> Done — all 6 Ethernet runs made and connected:
- 3x cable (green boots) — PVE1/PVE2/PVE3 → switch
- 3x cable (white boots) — switch → each OptiPlex node

All 6 HDMI cables also installed, running to the [HMTECH 10.1" IPS touchscreen](https://www.amazon.com/dp/B0987468N2) (1024 x 600, driver-free over HDMI) hinged on top of the rack. Used for checking each node's boot and video output, not as a permanent console.

## 5. Proxmox install verification
<img src="../images/icons/check.svg" width="17" align="top" alt="Done"> Proxmox installed on all 3 ThinkCentres (PVE1, PVE2, PVE3) — configuration (clustering, storage, networking) still to be done. See [`proxmox-ha.md`](proxmox-ha.md).

## 6. AI cluster node setup
<img src="../images/icons/progress.svg" width="17" align="top" alt="In progress"> In progress — hardware ready (middle node replaced), nodes are un-imaged (no OS installed yet). Next step: image with Ubuntu Server. See [`ai-cluster.md`](ai-cluster.md).

---

## Known issues / resolved

- <img src="../images/icons/check.svg" width="17" align="top" alt="Done"> ~~Middle Dell OptiPlex node died~~ — replaced, all 3 OptiPlex nodes physically good to go.

## Open questions

- VLAN split between Proxmox management traffic and AI cluster traffic, or flat/single subnet?
- IP addressing scheme — static assignments vs DHCP reservations for the 6 nodes.
- Wireless AP hardware/placement — not yet installed.
