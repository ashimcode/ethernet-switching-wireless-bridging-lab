# LinkedIn project brief — draft only

This is a working draft. Publish only after the repository link and final visual evidence have been reviewed.

## Flagship launch draft

### Post-ready copy

I found a VLAN bug by testing the path—not by trusting the diagram.

I built a GNS3 access-layer lab with Staff and Guest endpoints separated into VLAN 10 and VLAN 20, carried across an 802.1Q trunk and a simulated wireless Layer 2 bridge.

The first Guest test failed even though both endpoints used the `192.168.20.0/24` subnet.

The root cause was a Layer 2 membership mismatch:

- the Guest wireless endpoint belonged to VLAN 20;
- its bridge access port was still assigned to VLAN 10.

I changed only that bridge access port in a disposable project copy and retested:

- Guest → Guest: five ICMP replies in both directions;
- Staff → Staff: five ICMP replies in both directions;
- Staff ↔ Guest: still blocked with `No gateway found`, as expected because the base topology has no Layer 3 gateway;
- switch MAC learning: all four endpoints appeared in their intended VLANs.

The lesson: an IP address can look correct while the switch-port membership quietly contradicts it. I documented the original failure, root cause, correction, runtime evidence, and production hardening considerations in the repository.

Repository: https://github.com/ashimcode/ethernet-switching-wireless-bridging-lab

Next step: add packet-level evidence and a controlled firewall boundary so the segmentation policy can be tested beyond the Layer 2 baseline.

Suggested tags: `#Cybersecurity` `#Networking` `#IncidentResponse` `#GNS3` `#BlueTeam`

I built a GNS3 access-layer lab to understand how VLAN segmentation and wireless bridging behave at Layer 2.

The topology separates Staff and Guest endpoints into VLAN 10 and VLAN 20, carries both networks across an 802.1Q trunk, and uses Wireshark and endpoint tests to examine ARP and ICMP behavior.

The most valuable result was not the first successful ping. It was finding a configuration mismatch: the simulated Guest wireless port was assigned to VLAN 10 even though the endpoint belonged to the VLAN 20 subnet. That made the failure a Layer 2 membership problem, not a missing-gateway problem. After correcting the bridge port in a disposable copy, both Guest directions returned five ICMP replies and the switch learned the endpoints in VLAN 20. Staff VLAN 10 communication remained healthy, while cross-VLAN traffic stayed blocked because no Layer 3 gateway is present.

I documented the root cause, the minimal correction, the runtime validation, and the production hardening controls I would add next.

The repository records the runtime result in a sanitized validation note; a packet capture or before/after configuration image can be added as a follow-up evidence layer.

Repository: https://github.com/ashimcode/ethernet-switching-wireless-bridging-lab

## Post checklist

- Lead with the problem and the lesson, not a tool list.
- Include one clean topology or packet-analysis image.
- State exactly what the evidence proves.
- Name the limitation or next validation.
- Link the public repository and case study.
- Avoid claiming production experience, completed graduate degrees, or unverified metrics.
