# Troubleshooting Log

| Time | Symptom | Evidence | Hypothesis | Change | Result | Lesson |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |
| 2026-09-28 | Guest-PC could not reach `192.168.20.20` on the expected same-VLAN path | `evidence/screenshots/guest-vlan20-initial-failure.png` | Guest endpoint addressing, VLAN assignment, or bridge forwarding may be incomplete | No corrective change recorded yet | Initial failure captured; root cause remains open | Do not label the guest VLAN path complete until addressing, port membership, and bridge behavior are checked |
| 2026-09-28 | Configuration inspection found `Guest-Wireless-Laptop` on `Wireless-AP-Bridge Ethernet1`, which was configured as access VLAN 10 while the endpoint uses `192.168.20.20/24` | `docs/guest-vlan-root-cause.md` and the supplied local GNS3 project | The wireless Guest access port is misclassified; it should be in VLAN 20 | Correction target identified: change only `Wireless-AP-Bridge Ethernet1` to access VLAN 20 in a disposable project copy | Static root cause identified; runtime correction and before/after capture still pending | Same-subnet failures must be checked against both endpoint addressing and Layer 2 membership before changing routing or gateways |

Record one row for each issue. Do not overwrite the original observation after a fix; document the before and after states.
