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
