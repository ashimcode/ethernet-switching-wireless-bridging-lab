# Evidence Index

Store only sanitized evidence in this repository.

## Evidence categories

- `screenshots/` — GNS3 topology, VPCS commands, switch settings, and Wireshark results
- `packet-captures/` — sanitized or summarized captures permitted for publication
- `video/` — short demonstrations of the topology and test results

## Evidence record format

For every item, record:

- filename;
- lab task or question supported;
- date captured;
- what the evidence proves;
- sanitization performed;
- related section of the final write-up.

Do not publish credentials, personal information, unrelated host details, restricted course material, or raw captures that contain unnecessary data.

## Included screenshot evidence

- `../topology/gns3-topology.png` — clean GNS3 topology view
- `screenshots/wireshark-arp-broadcast.png` — ARP broadcast observation
- `screenshots/wireshark-arp-and-icmpv6.png` — supplemental ARP and ICMPv6 observation
- `screenshots/staff-vlan10-icmp-success.png` — successful Staff VLAN reachability test
- `screenshots/admin-cross-vlan-no-gateway.png` — cross-VLAN reachability failure with no gateway configured
- `screenshots/guest-vlan20-initial-failure.png` — initial Guest VLAN test failure before troubleshooting
- the three `*-addressing.png` files — VPCS addressing and gateway state

The screenshots are sanitized copies. Installer-error views, local filesystem paths, source-document pages, and unrelated desktop content were excluded.
