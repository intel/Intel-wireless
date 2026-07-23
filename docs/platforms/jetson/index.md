# Guidance for NVIDIA Jetson Platforms

This guide covers Intel® Wi-Fi integration on NVIDIA Jetson platforms (AGX Orin, Orin Nano, Thor) running JetPack.

## Recommended: DKMS Installation

For Jetson platforms running Canonical Ubuntu (JetPack 5.x or 6.x), the DKMS-based installation is the recommended approach. Follow the instructions in [Canonical Ubuntu](../canonical-ubuntu.md).

## Cross-Compilation for Jetson

If building from source on an x86 host for Jetson, refer to the [Cross-Compilation](../../build/cross-compile.md) guide. The following Jetson‑specific details apply.

### Kernel Preparation

```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- tegra_defconfig
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

!!! warning "Full Kernel Build Required"
    NVIDIA Jetson platforms require a **full kernel build** (`make` instead of `modules_prepare`) to generate `Module.symvers`, which is needed for proper module symbol resolution. If "no symbol version" warnings or unresolved symbols occur, a full kernel build is required before proceeding.

### Building the Backport Driver

```bash
git clone https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git
cd backport-iwlwifi
make ARCH=arm64 KLIB_BUILD=<path to jetson kernel source> defconfig-iwlwifi-public
make ARCH=arm64 KLIB_BUILD=<path to jetson kernel source> CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
```

### Deploying Modules to the Target

```bash
find . -name "*.ko" | xargs cp -t <jetson rootfs>/lib/modules/<kernel version>/extra/
depmod -a -b <jetson rootfs> <kernel version>
```

For firmware installation, refer to the [Firmware Installation](../../firmware/installation.md) page.
