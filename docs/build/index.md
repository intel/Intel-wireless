# Guidance for Software Integration

## Driver and Firmware Overview

Intel® Wi-Fi is natively supported in Linux. Intel upstreams the Wi-Fi driver kernel source tree to kernel.org., making it easy for customers to enable Intel® Wi-Fi. Intel also maintains an upstream backport driver to kernel.org. This approach benefits customers who require support for newer driver features on older kernel versions. This section provides guidance on how to integrate the Intel® Wi-Fi backport driver.

## Software Stack for the Backport Driver

The backport driver can be compatible with multiple kernel versions and tested against recent long-term kernel versions.

![Software stack for backport driver](../assets/images/software-stack-diagram.png)

### User-Space Tool and Daemon Components

These components include the wireless tool (iw tool), client daemon (wpa_supplicant) and AP daemon (hostapd). These components are not maintained by Intel and fully leverage components from the open-source community.

| Name | Purpose | Open-Source Community Website |
|------|---------|-------------------------------|
| wpa_supplicant | Daemon for controlling Wi-Fi in STA mode | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/wpa_supplicant.html) |
| hostapd | Daemon for controlling Wi-Fi in soft access point mode | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/hostapd.html) |
| iw tool | Tool for query and control Wi-Fi settings | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/iw.html) |

### Intel Driver Components

These components include the Wi-Fi frameworks — `mac80211.ko` and `cfg80211.ko`, backport driver abstraction layer — `compat.ko`, and Intel driver implementation — `iwlwifi.ko`, `iwlmld.ko` and `iwlmvm.ko`.

### Intel® Firmware Components

These components include the Wi-Fi firmware — `*.ucode` and regulatory support file `*.pnvm`.

## Intel® Wi-Fi Integration

This section describes the recommended workflow for enabling and integrating Intel® Wi-Fi on the target platform.

![Integration workflow](../assets/images/integration-workflow.png)

## Build Methods

Choose the build method that best fits your platform:

| Method | Best For | Details |
|--------|----------|---------|
| [Native Build from Source](native-build.md) | Vendor-customized kernels | Build directly on the target platform |
| [Cross-Compilation from Source](cross-compile.md) | Embedded/resource-limited targets | Build on x86 host, deploy to target |

## Installing Prerequisites

Building the backport driver requires standard Linux kernel build tools: a C compiler, `make`, `flex`, `bison`, `bc`, and kernel header/crypto development libraries. Ensure these tools are installed on the build system — either the target platform (for native builds) or the x86 host (for cross-compilation).

For cross-compilation, a toolchain for the target architecture is also required.

Here is an example command to install prerequisites in Ubuntu:

```bash
sudo apt update
sudo apt install git build-essential bc flex bison libssl-dev libelf-dev
```

For other distributions or building environments, install the equivalent packages using your platform's package manager.

!!! note "Network Connectivity"
    If apt commands or git clone operations fail with connection errors (e.g., timeouts, "Could not resolve host", or "Failed to connect"), make sure the machine is able to connect to the APT Server. In some network environments the proxy setting may be required. Contact the network administrator regarding proxy setup.
