# Guidance For Debugging

## Request Intel's Support

Intel provides official support to NDA customers. Requests for assistance must be submitted through an Intel Support Forum ticket that includes the following information:

- Issue symptoms
- Issue reproduction steps
- The SoC you are using
- Logs

!!! note "Required Logs"
    Logs include the driver information, driver log, and firmware log. Refer to the sections below for the detailed steps to collect each type.

## Collecting Logs – Driver Information

To identify the driver version on the platform, run the following command and collect the output:

```bash
sudo modinfo iwlwifi
```

## Collecting Logs – Driver Log

The following method collects driver logs by enabling the driver debug mask when the driver is loaded. Modify the `/etc/modprobe.d/iwlwifi.conf` to include the driver debugging mask. Add following content in the file:

```ini
options iwlwifi debug=0xffffffff
```

Reboot system after editing file. Share the full kernel log by following command when issue is reproduced:

```bash
sudo dmesg
```

## Collecting Logs – Firmware Log

To collect the firmware log (e.g., firmware exception), the following method creates a udev rule and script to collect firmware logs.

### Create udev rule

Install udevd on the platform and create the udevd rule to trigger firmware log collection. Add file at `/etc/udev/rules.d/85-iwl-dump.rules` with the following content:

```ini
SUBSYSTEM=="devcoredump", ACTION=="add", RUN+="/usr/sbin/fwdump.sh"
```

### Create firmware dump shell script

Create the shell script `/usr/sbin/fwdump.sh` and add the following content:

```bash
#!/bin/bash

timestamp=$(date +%F_%H-%M-%S)
filename=/var/log/iwl-fw-error_${timestamp}.dump
cat /sys/${DEVPATH}/data > ${filename}
echo 1 > /sys/${DEVPATH}/data
```

### Change permission for shell scripts

To allow udevd to run the shell script collection, change the script permissions:

```bash
sudo chmod a+x /usr/sbin/fwdump.sh
```

### Collect the firmware log

When the firmware crashes, messages will be shown in kernel log like this:

```
iwlwifi 0000:01:00.0: Microcode SW error detected. Restarting 0x82000000.
[...]
iwlwifi 0000:01:00.0: Loaded firmware version: XX.XX.XX.XX
iwlwifi 0000:01:00.0: 0x0000090A | ADVANCED_SYSASSERT
```

A firmware log dump file will be generated at `/var/log/iwl-fw-error_<timestamp>.dump` where `<timestamp>` represents the timestamp string. Share those files with Intel.

!!! todo "Suggested Addition: Quick Diagnostic Commands"
    Consider adding a summary of quick diagnostic commands in one block for easy copy-paste: lspci, lsmod, dmesg | grep iwlwifi, ip link show, iw dev — to help users quickly gather initial system state before diving into detailed log collection.
