# LinkedIn project brief — draft only

This is a working draft. Publish only after the repository link and final visual evidence have been reviewed.

## Flagship launch draft

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
