# Evidence Security Review

## Review scope

The supplied screenshots were reviewed before public release. Only screenshots that directly support the topology, addressing, reachability, or packet-analysis narrative were included.

## Sanitization actions

- Re-encoded selected images as new PNG files.
- Cropped Wireshark images to the application window, removing the surrounding desktop and unrelated open-application context.
- Cropped VPCS images to the relevant addressing output, removing the startup banner and unrelated vendor contact information.
- Excluded screenshots containing local installation paths, project filesystem paths, installer errors, or source-document content.
- Used descriptive repository filenames instead of the original desktop screenshot names.

## Exposure assessment

- The included addresses are private RFC 1918 lab addresses.
- The MAC addresses are synthetic VPCS lab values and are not tied to a physical network location.
- No GPS or location metadata was identified in the selected image files.
- The selected images do not display a street address, geographic coordinates, public IP address, Wi-Fi name, or personal contact information.
- The screenshots show lab labels such as `Admin-PC`, `Guest-PC`, and `Wireless-AP-Bridge`; these are simulated device names.

## Excluded material

The following material remains outside the public repository:

- GNS3 installer and repair screenshots containing local Windows paths;
- GNS3 error screenshots containing local project paths or process details;
- screenshots of course instructions and answer-sheet pages;
- raw packet captures until each file is reviewed and intentionally approved for publication.

## Remaining review items

- Capture and inspect the actual `.pcap` or `.pcapng` files before committing them.
- Capture a clean VLAN configuration view if it is required for the final report.
- Record the root cause and correction for the Guest VLAN initial failure.
- Review the final video frame by frame for desktop notifications, paths, usernames, and unrelated applications.
