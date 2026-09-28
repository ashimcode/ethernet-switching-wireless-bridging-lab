# Ethernet Switching and Wireless Bridging Lab

This repository documents my hands-on GNS3 lab on Ethernet switching, VLAN segmentation, ARP, ICMP, and Layer 2 wireless bridging.

## Lab scope

The topology uses GNS3 built-in components:

- Four VPCS endpoints
- One built-in Ethernet switch named `Main-Switch`
- One built-in access point named `Wireless-AP-Bridge`

The access point represents Layer 2 bridging between wireless and Ethernet segments. It does not model radio behavior, wireless channels, interference, authentication, or client association.

## Learning objectives

By completing this lab, I should be able to:

1. Distinguish Ethernet switching from IP routing.
2. Explain how a switch learns and forwards frames using MAC addresses.
3. Test communication within and between VLANs.
4. Observe ARP and ICMP traffic in Wireshark.
5. Explain how an access point bridges wireless traffic into an Ethernet LAN.

## Repository structure

```text
docs/                 Lab plan, concepts, and completion notes
topology/             Topology documentation and permitted project exports
evidence/             Sanitized screenshots, captures, and video evidence
notes/                Learning journal and troubleshooting record
submission/           Final write-up and submission checklist
```

## Evidence standard

Evidence must show the lab working without exposing unrelated personal information, credentials, private network details, or restricted course material. Each screenshot, capture, or video should include a short note describing what it proves and which lab task it supports.

## Academic and source-material boundary

The course-provided GNS3 project, instructions, and answer sheet remain outside this public repository unless redistribution is permitted. This repository is for my own configuration notes, observations, screenshots, analysis, and final write-up.

## Status

Planning and repository setup. Lab execution begins after the GNS3 project and answer requirements are reviewed.
