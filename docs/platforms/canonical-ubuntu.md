# Guidance for Canonical Ubuntu

This method installs the backport driver and firmware using standard Ubuntu package management. It is the simplest approach for platforms running Ubuntu Linux natively (e.g., Ubuntu for ARM64).

For NVIDIA Jetson platforms (Orin, Thor) or any other platform running Canonical Ubuntu, this method is strongly recommended as it is using the DKMS-based approach. It provides automatic driver rebuilds on kernel updates and is the most maintainable path for production deployments.

## Installation

Run these commands on the target platform:

```bash
sudo apt update
sudo apt install dkms linux-headers-generic git build-essential
sudo apt install linux-firmware
sudo apt install backport-iwlwifi-dkms
```

After installation, reboot the platform. DKMS will automatically build the driver against the running kernel. The driver will be rebuilt whenever the kernel is updated.

!!! note
    This method also installs the required firmware via the `linux-firmware` package. No additional firmware installation steps are needed.

## Wi-Fi Daemon and Tool Integration

The components used in this phase are not provided or maintained by Intel. Refer to the following open-source community websites for details:

| Name | Purpose | Open-Source Community Website |
|------|---------|-------------------------------|
| wpa_supplicant | Daemon for controlling Wi-Fi in STA mode | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/wpa_supplicant.html) |
| hostapd | Daemon for controlling Wi-Fi in soft access point mode | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/hostapd.html) |
| iw tool | Tool for query and control Wi-Fi settings | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/iw.html) |
