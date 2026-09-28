# LinkedIn project brief — draft only

This is a working draft. Do not publish it as a completed project until the live Guest-VLAN correction, before/after evidence, and packet-capture gate are complete.

## Flagship launch draft

I built a GNS3 access-layer lab to understand how VLAN segmentation and wireless bridging behave at Layer 2.

The topology separates Staff and Guest endpoints into VLAN 10 and VLAN 20, carries both networks across an 802.1Q trunk, and uses Wireshark and endpoint tests to examine ARP and ICMP behavior.

The most valuable result was not the first successful ping. It was finding a configuration mismatch: the simulated Guest wireless port was assigned to VLAN 10 even though the endpoint belonged to the VLAN 20 subnet. That made the failure a Layer 2 membership problem, not a missing-gateway problem.

I documented the root cause, the minimal correction, the evidence required for a safe retest, and the production hardening controls I would add next.

The project is not being labeled complete until the corrected path is reproduced and the before/after evidence is sanitized.

Repository: [add the stable GitHub link after the completion gate passes]

## Post checklist

- Lead with the problem and the lesson, not a tool list.
- Include one clean topology or packet-analysis image.
- State exactly what the evidence proves.
- Name the limitation or next validation.
- Link the public repository and case study.
- Avoid claiming production experience, completed graduate degrees, or unverified metrics.
