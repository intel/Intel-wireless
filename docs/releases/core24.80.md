# core24.80 Release Notes

| | |
|---|---|
| **Release** | core24.80 |
| **Branch** | [`release/core24.80`](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/log/?h=release/core24.80) |
| **Status** | Latest |
| **Latest Commit** | [`f9618cf`](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/commit/?id=f9618cfd3464939e7dee08521cb95867a5d19a15) (2026-10-19) |
| **Last Updated** | 2026-10-20 |

To get this release, refer to [Getting the Latest Release](index.md#getting-the-latest-release).

## New Features and Enhancements

- Device Tree support for Wi-Fi platform configuration on Intel® Wi-Fi 7 BE200, in addition to UEFI variables and ACPI. Device Tree provides SAR limits and 6 GHz AP type settings, and is used only when UEFI variables and ACPI methods do not provide the configuration. Refer to [Wi-Fi Configuration](../configuration/index.md).
- 802.11be (Wi-Fi 7) enabled by default in China and South Korea when the platform BIOS does not provide DSM function 12.
- 6 GHz (Wi-Fi 6E) enabled in Nigeria, Pakistan, and Cape Verde.
- Pakistan 5.8 GHz band returned to the previous power profile, with 30 dBm EIRP up to 5875 MHz.
- Cross-core trigger dump for debug data collection.

## Bug Fixes

### Driver

- Fixed the Wi-Fi Aware (NAN) initiator failing to set a new schedule map when two NAN data paths (NDP) are active alongside an infrastructure (BSS) connection.
- Improved validation of the NetDetect (wake on wireless) match information reported by the firmware.

### Firmware

Firmware fixes are delivered in the Intel® Wi-Fi firmware. Refer to [Firmware Installation](../firmware/installation.md).

- Fixed a firmware assert (0x251A) in the data path.
- Fixed a firmware assert (0x28B2) in the PHY.
- Fixed reduced throughput for video (VI) traffic when best-effort (BE) traffic is present.
- Improved validation of Wi-Fi Aware (NAN) availability updates to prevent replayed updates from changing the schedule.
- Secure ranging key material is now cleared after a measurement completes.

### wpa_supplicant

These fixes are in [hostap](https://w1.fi/cgit/hostap/) (wpa_supplicant), which is not part of the backport-iwlwifi branch.

- Fixed lower-than-expected Wi-Fi Aware (NAN) data throughput in the 5 GHz band.
- Fixed NAN follow-up frames not being received by the publisher.
- Fixed a NAN data path (NDP) being established when the schedule maps use the same channel but their time units are not aligned.

## Revision History

| Date | Latest Commit | Changes |
|------|---------------|---------|
| 2026-10-20 | `f9618cf` | Initial release notes for core24.80. |
