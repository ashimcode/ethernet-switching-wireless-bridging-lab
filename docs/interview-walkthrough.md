# Ethernet lab interview walkthrough

## 60-second explanation

I built a GNS3 access-layer lab that separates Staff and Guest endpoints with VLAN 10 and VLAN 20, carries both VLANs over an 802.1Q trunk, and models a wireless access point as a Layer 2 bridge. I validated Staff same-VLAN communication, the expected no-routing boundary between VLANs, and ARP behavior with packet evidence. During troubleshooting, I found that the simulated wireless Guest port was assigned to VLAN 10 even though the Guest wireless endpoint used the VLAN 20 subnet. I documented the correction target and kept the project status bounded until a live before/after retest is captured.

## Three-minute technical walkthrough

1. **Objective:** demonstrate that segmentation is a control boundary, not just a diagram. Staff and Guest are separate broadcast domains.
2. **Data flow:** endpoints connect to access ports; the main switch carries both VLANs across an 802.1Q trunk; the simulated wireless bridge maps endpoint ports back to the wired VLANs.
3. **Baseline:** Staff same-VLAN communication succeeds. Staff-to-Guest communication is not routed because the base topology intentionally has no Layer 3 gateway.
4. **Evidence:** topology, VPCS addressing, ICMP output, ARP observations, and sanitized Wireshark screenshots are stored in the repository evidence index.
5. **Failure analysis:** the original project assigned `Wireless-AP-Bridge Ethernet1` to access VLAN 10 while `Guest-Wireless-Laptop` used `192.168.20.20/24`. The Guest wireless endpoint therefore was not in the wired Guest broadcast domain.
6. **Next validation:** change only that bridge access port to VLAN 20 in a disposable copy, rerun both Guest directions, confirm Staff remains stable, and preserve before/after evidence.

## What broke?

The Guest wireless path was misclassified at Layer 2. The addressing looked consistent with VLAN 20, but the bridge port membership contradicted it. That is why checking IP settings alone was insufficient.

## How was it verified?

The source project configuration was inspected directly, and the finding is recorded in [`guest-vlan-root-cause.md`](guest-vlan-root-cause.md). Runtime correction evidence is intentionally still marked pending.

## Production improvement

In production, I would pair VLAN segmentation with explicit trunk allow-lists, DHCP snooping, Dynamic ARP Inspection, BPDU Guard, port security, storm control, firewall policy at the routing boundary, centralized logging, and a change-controlled validation checklist.
