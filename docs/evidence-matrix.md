# Evidence Matrix

| Evidence item | Validation question | Repository location | Status |
|---|---|---|---|
| Topology screenshot | Are the endpoints, switch, bridge, and links visible? | `topology/gns3-topology.png` | Captured |
| VLAN configuration screenshot | Are VLAN 10 and VLAN 20 assigned as designed? | `evidence/screenshots/` | Pending; switch configuration capture required |
| Staff ARP observation | Does the broadcast remain inside VLAN 10? | `evidence/screenshots/wireshark-arp-broadcast.png` | Screenshot captured |
| Guest ARP observation | Does the broadcast remain inside VLAN 20? | `evidence/screenshots/wireshark-arp-broadcast.png` | Screenshot captured |
| Same-VLAN ICMP test | Does local communication succeed? | `evidence/screenshots/staff-vlan10-icmp-success.png` | Admin/Staff path captured as successful |
| Cross-VLAN test | Does communication fail without routing? | `evidence/screenshots/admin-cross-vlan-no-gateway.png` | Screenshot captured |
| VLAN error evidence | Can the misconfiguration be isolated and corrected? | `evidence/screenshots/guest-vlan20-initial-failure.png`, `docs/guest-vlan-root-cause.md`, `docs/runtime-validation.md` | Root cause isolated; correction reproduced in a disposable copy; five-reply Guest validation recorded |
| MAC-learning validation | Did the switch learn the four endpoints in the intended VLANs? | `docs/runtime-validation.md` | Recorded; VLAN 10 and VLAN 20 endpoint MACs observed in the Main-Switch table |
| Trunk packet capture | Are VLAN 10 and VLAN 20 tags present on the bridge trunk during same-VLAN validation? | `pcaps/vlan-trunk-runtime-2026-09-28.pcap`, `docs/runtime-validation.md` | Captured; 24 tagged frames across VLANs 10 and 20, including 20 IPv4/ICMP frames |
| Walkthrough video | Can another analyst reproduce the validation? | `evidence/video/` | Pending |
