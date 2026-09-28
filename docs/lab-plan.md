# Lab Plan

## Purpose

This lab uses GNS3 to observe how Ethernet switches forward frames, how VLANs separate broadcast domains, how ARP resolves local IP-to-MAC mappings, and how a wireless access point can bridge traffic into an Ethernet LAN.

## Execution sequence

1. Review the supplied topology and answer requirements.
2. Confirm the GNS3 project opens without changing the original file.
3. Identify each VPCS endpoint, switch port, VLAN, and IP address.
4. Start the topology and verify link status.
5. Establish a normal communication baseline.
6. Test communication within the same VLAN.
7. Test communication across VLAN boundaries and explain the result.
8. Capture ARP and ICMP traffic in Wireshark.
9. Diagnose the intentional VLAN configuration error.
10. Document the wireless bridge behavior.
11. Capture sanitized evidence and complete the write-up.

## OSI model mapping

| Layer | Lab focus |
|---|---|
| 1 Physical | Virtual links and GNS3 device connectivity |
| 2 Data Link | Ethernet frames, MAC addresses, switching, VLANs, ARP, and wireless bridging |
| 3 Network | IPv4 addressing and subnet behavior |
| 4 Transport | Not the primary focus; document only if observed during testing |
| 7 Application | VPCS command output and Wireshark display filters |

## Key distinction

The built-in switch and access point operate at Layer 2 for this lab. They forward frames based on MAC addresses and VLAN membership. They do not route traffic between IP networks. Communication between different VLANs requires a Layer 3 routing function, which is intentionally absent from this topology unless the supplied project specifies otherwise.

## Completion gate

The lab is complete when the topology behavior is verified, the intentional error is diagnosed, required evidence is captured, the questions are answered in my own words, and the final write-up is reviewed for accuracy and clarity.
