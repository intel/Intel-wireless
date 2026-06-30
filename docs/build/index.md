# Guidance for Software Integration

## About Driver and Firmware

Intel® Wi-Fi is natively supported in Linux. Intel upstreams the Wi-Fi driver kernel source tree to kernel.org. Customers can use it to enable Intel® Wi-Fi without any extra effort. Intel also upstreams the driver called backport driver to kernel.org. This approach benefits customers who require support for newer driver features on older kernel versions. This section provides guidance on how to integrate the Intel® Wi-Fi backport driver.

## Software Stack for Backport Driver

The backport driver can be compatible with multiple kernel versions and tested against recent long-term kernel versions.

![Software stack for backport driver](../assets/images/software-stack-diagram.png)

### Tool and Daemon Components

These components include wireless tool (iw tool), client daemon (wpa_supplicant) and AP daemon (hostapd). These components are not maintained by Intel and fully leverage components from the open-source community.

| Name | Purpose | Open-Source Community Website |
|------|---------|-------------------------------|
| wpa_supplicant | Daemon for controlling Wi-Fi in STA mode | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/wpa_supplicant.html) |
| hostapd | Daemon for controlling Wi-Fi in soft access point mode | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/hostapd.html) |
| iw tool | Tool for query and control Wi-Fi settings | [Documentation](https://wireless.docs.kernel.org/en/latest/en/users/documentation/iw.html) |

### Intel Driver Components

These components include Wi-Fi framework — `mac80211.ko` and `cfg80211.ko`, backport driver abstraction layer — `compat.ko`, and Intel driver implementation — `iwlwifi.ko`, `iwlmld.ko` and `iwlmvm.ko`.

### Intel Firmware Components

These components include Wi-Fi firmware — `*.ucode` and regulatory supported file `*.pnvm`.

## Intel® Wi-Fi Integration

This section describes the recommended workflow for enabling and integrating Intel® Wi-Fi on the target platform.

![Integration workflow](../assets/images/integration-workflow.png)

## Build Methods

!!! tip "Building for Canonical Ubuntu or NVIDIA Jetson?"
    If your platform runs Canonical Ubuntu (including NVIDIA Jetson with JetPack), the recommended approach is the DKMS-based installation. See [Platform Guides → Canonical Ubuntu](../platforms/canonical-ubuntu.md) for the simplest path.

Choose the build method that best fits your platform:

| Method | Best For | Details |
|--------|----------|---------|
| [Native Build from Source](native-build.md) | Vendor-customized kernels | Build directly on the target platform |
| [Cross-Compilation from Source](cross-compile.md) | Embedded/resource-limited targets | Build on x86 host, deploy to target |

## Installing Prerequisites

Building the backport driver requires standard Linux kernel build tools: a C compiler, `make`, `flex`, `bison`, `bc`, and kernel header/crypto development libraries. Ensure these tools are installed on the machine performing the build — either the target platform (for native builds) or the x86 host (for cross-compilation).

For cross-compilation, a toolchain for the target architecture is also required.

Here is an example command to install prerequisites in Ubuntu:

```bash
sudo apt update
sudo apt install git build-essential bc flex bison libssl-dev libelf-dev
```

For other distributions or building environments, install the equivalent packages using your platform's package manager.

!!! note "Network Connectivity"
    If apt commands or git clone operations fail with connection errors (e.g., timeouts, "Could not resolve host", or "Failed to connect"), make sure the machine is able to connect to the APT Server. In some network environments the proxy setting may be required. Contact the network administrator regarding proxy setup.
