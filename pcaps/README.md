# Packet Captures

Store sanitized Wireshark captures here after reviewing them for unnecessary addresses, usernames, host identifiers, and other sensitive data.

Recommended filenames:

- `staff-vlan10-arp-baseline.pcapng`
- `guest-vlan20-arp-baseline.pcapng`
- `same-vlan-icmp-validation.pcapng`
- `cross-vlan-icmp-routing-boundary.pcapng`

For each capture, add a companion note describing the test, expected result, observed result, display filter, and what the capture proves.

## Captured runtime artifact

`vlan-trunk-runtime-2026-09-28.pcap` is a sanitized capture from the disposable GNS3 validation copy. It was collected on the Main-Switch ↔ Wireless-AP-Bridge 802.1Q trunk while the corrected same-VLAN tests ran.

- **Expected result:** VLAN 10 and VLAN 20 traffic remains tagged and separate; same-VLAN ICMP succeeds.
- **Observed result:** 24 frames total; all 24 were 802.1Q-tagged, with VLAN IDs 10 and 20 present. The capture contained 20 IPv4 frames, all ICMP, across the simulated VPCS endpoints.
- **Cross-VLAN boundary:** cross-VLAN tests returned `No gateway found`; no routing claim is made.
- **Sanitization:** the capture contains only simulated VPCS addresses and MACs from the lab. No usernames, host paths, credentials, or production identifiers were included.
- **Related record:** [`../docs/runtime-validation.md`](../docs/runtime-validation.md)
