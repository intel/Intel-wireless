# Build Method 1: Native Build from Source

This method involves compiling the backport driver from the source directly onto the target platform. It provides more flexibility and is suitable for platforms running a vendor-customized Linux kernel where the DKMS package may not be available.

## Clone and Build

--8<-- "release.md:note"

To clone and build the driver, run these commands:

```bash
--8<-- "release.md:clone"
cd backport-iwlwifi
make defconfig-iwlwifi-public
make -j$(nproc)
```

## Install

Once the build completes successfully, install the driver modules and update module dependencies by running these commands:

```bash
sudo make install
sudo depmod -a
```

## Firmware

For firmware installation, refer to the [Firmware Installation](../firmware/installation.md) page.
