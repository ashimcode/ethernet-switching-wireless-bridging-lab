# Contribution and Publishing Workflow

This repository is a public network-security lab portfolio. Keep `main` reproducible, evidence-based, and safe to publish.

Use this sequence for every lab change:

```text
Configure → Validate → Capture evidence → Sanitize → Review → Commit → Push → Portfolio update
```

Use focused commit messages such as:

- `docs(topology): define Staff and Guest VLAN boundaries`
- `test(vlan): verify same-segment and cross-segment behavior`
- `docs(wireshark): record ARP and ICMP validation evidence`
- `security(evidence): remove personal addresses from captures`
- `chore(repo): update reproducibility notes`

Before pushing, confirm that the GNS3 topology, endpoint addresses, packet captures, screenshots, and troubleshooting notes are real, sanitized, and clearly labeled as verified or pending. Never commit credentials, private keys, personal data, raw captures, or production network information.
