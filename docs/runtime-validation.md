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

## Reproduction notes

1. Open the disposable project copy.
2. Confirm the wireless bridge Guest-facing access port is VLAN 20.
3. Start all six nodes.
4. Run the endpoint tests in the table above.
5. Inspect the Main-Switch MAC table and verify the VLAN placement.

The repository still needs a sanitized before/after screenshot or packet capture if visual packet-level evidence is required for a future release. This text record is the verified runtime result for the current portfolio milestone.
