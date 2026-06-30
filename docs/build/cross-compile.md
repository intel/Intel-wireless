# Build Method: Cross-Compilation from Source

On non-x86 platforms, building the driver natively may not be practical due to limited resources, missing development tools, or the use of a vendor-customized kernel that requires cross-compilation. In these cases, cross-compiling from an x86 host is the recommended approach.

## Step 1: Kernel Preparation - ok - this is my change

Before building out-of-tree modules, the target platform's kernel source must be configured and minimally prepared on the host. This generates the headers, build scripts, and `Module.symvers` required for external module compilation. Contact the SoC vendor to understand steps for kernel preparation.

Following is an example using NVIDIA Jetson — Orin/Thor platform:

```bash
make ARCH=<arch> CROSS_COMPILE=<path to toolchain prefix> tegra_defconfig
make ARCH=<arch> CROSS_COMPILE=<path to toolchain prefix> modules_prepare
```

!!! warning "Full Kernel Build May Be Required"
    Platforms (such as NVIDIA Jetson) require a **full kernel build** (`make` instead of `modules_prepare`) to generate `Module.symvers`, which is needed for proper module symbol resolution. If "no symbol version" warnings or unresolved symbols occur, a full kernel build is required before proceeding.

## Step 2: Building the Backport Driver

```bash
git clone https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git
cd backport-iwlwifi
make ARCH=<arch> KLIB_BUILD=<path to the kernel source> defconfig-iwlwifi-public
make ARCH=<arch> KLIB_BUILD=<path to the kernel source> CROSS_COMPILE=<path to toolchain> -docs/firmwarej<number of threads>
```

Where:

- `<arch>` — the symbol for the target processor. For example: `arm64`.
- `<path to the kernel source>` — path for Linux kernel source.
- `<path to toolchain>` — path and cross compile prefix in toolchain.

!!! note "Selecting a Release"
    By default, the git command clones the latest development branch. To use a specific release, check out the desired branch or tag after cloning: `git checkout <branch or tag>` (e.g., `git checkout release/core103`).

## Step 3: Deploying Modules to the Target

Locate and copy all Intel® Wi-Fi kernel modules to the target root file system. Use the following commands:

```bash
find . -name "*.ko" | xargs cp -t <target kernel module path>
depmod -a -b <target rootfs path> <version>
```

Where:

- `<target kernel module path>` — kernel module folder for generated rootfs.
- `<version>` — kernel version string for target platform.
- `<target rootfs path>` — path for target root file system.

## Firmware

For firmware installation, refer to the [Firmware Installation](../firmware/installation.md) page.
