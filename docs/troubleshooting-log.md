# Troubleshooting Log

| Time | Symptom | Evidence | Hypothesis | Change | Result | Lesson |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |
| 2026-09-28 | Guest-PC could not reach `192.168.20.20` on the expected same-VLAN path | `evidence/screenshots/guest-vlan20-initial-failure.png` | Guest endpoint addressing, VLAN assignment, or bridge forwarding may be incomplete | No corrective change recorded yet | Historical baseline preserved; later inspection isolated the cause | Preserve the original failure before changing the topology |
| 2026-09-28 | Configuration inspection found `Guest-Wireless-Laptop` on `Wireless-AP-Bridge Ethernet1`, which was configured as access VLAN 10 while the endpoint uses `192.168.20.20/24` | `docs/guest-vlan-root-cause.md` and the supplied local GNS3 project | The wireless Guest access port is misclassified; it should be in VLAN 20 | Correction target identified: change only `Wireless-AP-Bridge Ethernet1` to access VLAN 20 in a disposable project copy | Static root cause confirmed; runtime test performed next | Check endpoint addressing and Layer 2 membership before changing routing or gateways |
| 2026-09-28 | Corrected Guest endpoints needed a live same-VLAN retest | `docs/runtime-validation.md` | The bridge correction should restore local Layer 2 reachability without adding a gateway | Applied only in the disposable copy; reloaded the project and started all six nodes | Both Guest directions returned five ICMP replies; Staff/Admin also returned five; cross-VLAN tests remained `No gateway found` | Minimal, isolated correction restored the intended VLAN 20 path without weakening segmentation |

Record one row for each issue. Do not overwrite the original observation after a fix; document the before and after states.
