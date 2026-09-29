# Runtime validation record

**Validation date:** 2026-09-28  
**Environment:** disposable GNS3 project copy  
**Scope:** corrected Guest bridge-port membership, same-VLAN reachability, expected unrouted boundary, and switch MAC learning

## Correction under test

`Wireless-AP-Bridge Ethernet1` was changed from access VLAN 10 to access VLAN 20. The Main-Switch Guest access port and both 802.1Q trunk endpoints remained unchanged. The source private/course project and its history were not modified.

## Endpoint results

| Test | Result | Observation |
|---|---|---|
| Guest-PC `192.168.20.10/24` → Guest-Wireless-Laptop `192.168.20.20/24` | **Pass** | Five ICMP replies received |
| Guest-Wireless-Laptop `192.168.20.20/24` → Guest-PC `192.168.20.10/24` | **Pass** | Five ICMP replies received |
| Admin-PC `192.168.10.10/24` → Staff-Wireless-Laptop `192.168.10.20/24` | **Pass** | Five ICMP replies received |
| Staff-Wireless-Laptop `192.168.10.20/24` → Admin-PC `192.168.10.10/24` | **Pass** | Five ICMP replies received |
| Admin-PC VLAN 10 → Guest-PC VLAN 20 | **Expected boundary** | `No gateway found` |
| Guest-PC VLAN 20 → Admin-PC VLAN 10 | **Expected boundary** | `No gateway found` |

The result confirms same-VLAN Layer 2 forwarding after the bridge-port correction. It does not claim inter-VLAN routing, because the base topology intentionally has no Layer 3 gateway.

## MAC-learning evidence

After the tests, the Main-Switch MAC table showed the four endpoint MACs in their intended VLANs:

| VLAN | Learned endpoint MACs |
|---:|---|
| 10 | `00:50:79:66:68:00`, `00:50:79:66:68:02` |
| 20 | `00:50:79:66:68:01`, `00:50:79:66:68:03` |

These are simulated VPCS addresses, not production identifiers. The table is included to show that the switch learned the Staff and Guest endpoints in separate broadcast domains.

## Packet-level evidence

The disposable-copy run also produced [`../pcaps/vlan-trunk-runtime-2026-09-28.pcap`](../pcaps/vlan-trunk-runtime-2026-09-28.pcap), captured on the Main-Switch ↔ Wireless-AP-Bridge trunk during the endpoint tests.

The sanitized capture contains 24 frames: 24 802.1Q-tagged frames with VLAN IDs 10 and 20, including 20 IPv4/ICMP frames. The observed MACs are simulated VPCS addresses. This independently supports the VLAN tagging and same-VLAN forwarding claims; it does not establish inter-VLAN routing.

## Reproduction notes

1. Open the disposable project copy.
2. Confirm the wireless bridge Guest-facing access port is VLAN 20.
3. Start all six nodes.
4. Run the endpoint tests in the table above.
5. Inspect the Main-Switch MAC table and verify the VLAN placement.

The repository still has no walkthrough video or dedicated before/after correction screenshot. The text record and sanitized trunk capture together document the verified runtime result for the current portfolio milestone.
