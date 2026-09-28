# Guest VLAN bridge-port root-cause analysis

## Scope

This analysis uses the supplied local GNS3 project as an inspection source. The course project archive is not redistributed in this public repository. The values below are limited to the topology and endpoint settings required to explain the observed Guest-VLAN failure.

## Finding

The original topology assigns the Guest wireless endpoint to the wrong access VLAN on the simulated wireless bridge:

| Path element | Original setting | Expected setting |
|---|---|---|
| Guest-PC address | `192.168.20.10/24` | `192.168.20.10/24` |
| Main-Switch Ethernet1 | access VLAN 20 | access VLAN 20 |
| Main-Switch Ethernet7 | 802.1Q trunk | 802.1Q trunk |
| Wireless-AP-Bridge Ethernet7 | 802.1Q trunk | 802.1Q trunk |
| Guest-Wireless-Laptop address | `192.168.20.20/24` | `192.168.20.20/24` |
| Wireless-AP-Bridge Ethernet1 | access VLAN 10 | **access VLAN 20** |

The Guest-PC and Guest-Wireless-Laptop are addressed in the same IPv4 subnet, so they should resolve each other directly through ARP without a default gateway. Because the wireless bridge's Guest-facing port is in VLAN 10 in the original project, the Guest wireless endpoint is not placed in the same Layer 2 broadcast domain as the wired Guest endpoint. That explains the observed same-subnet failure more directly than a missing router or a VPCS addressing problem.

## Safe correction

Change only `Wireless-AP-Bridge` `Ethernet1` from access VLAN 10 to access VLAN 20. Keep the Main-Switch Guest access port and the Ethernet7 trunk unchanged. This preserves the intended Staff/Guest separation while placing both Guest endpoints in VLAN 20.

## Retest plan

After applying the correction in a disposable copy of the course project:

1. From `Guest-PC`, run `ping 192.168.20.20` and record a successful same-VLAN result.
2. From `Guest-Wireless-Laptop`, run `ping 192.168.20.10` and record the reverse path.
3. Re-run the Staff same-VLAN test to confirm VLAN 10 was not changed.
4. Re-run the Staff-to-Guest test. It should remain blocked in the unrouted baseline because no Layer 3 gateway is present.
5. Capture the before/after switch-port configuration and endpoint output, then sanitize screenshots before publication.

## Evidence status

- **Confirmed:** the original project configuration contains the VLAN mismatch described above.
- **Captured:** the original Guest same-VLAN failure is preserved in `../evidence/screenshots/guest-vlan20-initial-failure.png`.
- **Verified:** the correction was applied in a disposable copy and both Guest directions returned five ICMP replies. Staff/Admin same-VLAN communication also returned five replies, while cross-VLAN tests remained blocked with `No gateway found` as expected without a Layer 3 gateway.
- **Recorded:** the sanitized runtime results and MAC-learning evidence are in [`runtime-validation.md`](runtime-validation.md).
- **Still open:** a sanitized before/after switch-configuration screenshot or packet capture would strengthen the visual evidence package, but it is not required to claim the corrected same-VLAN path is working.
