# Firmware Installation

This section applies to the "Native Build from Source" and "Cross-Compilation from Source" methods. The DKMS method manages firmware automatically via the `linux-firmware` package.

## Deploy Firmware Files

Intel® Wi-Fi firmware files must be placed in `/lib/firmware/` on the target filesystem. To deploy firmware, follow the commands below:

```bash
git clone https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
cd linux-firmware
cp -rf iwlwifi-*.* <target firmware path>
```

Where `<target firmware path>` is the firmware folder in rootfs (typically `/lib/firmware/`).

!!! note "Selecting a Firmware Release"
    By default, this clones the latest firmware. To use a specific release, check out the desired tag after cloning: `git checkout <tag>` (e.g., `git checkout iwlwifi-fw-2026-03-17`).

## Firmware Files

| File Pattern | Purpose |
|-------------|---------|
| `iwlwifi-*.ucode` | Wi-Fi firmware binary |
| `*.pnvm` | Regulatory configuration data |

!!! todo "Suggested Addition: Firmware Version Matrix"
    Consider adding a compatibility matrix showing which firmware versions are validated with which driver releases and Wi-Fi modules (BE200, AX210).
