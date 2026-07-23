# Guidance for Debugging

## Requesting Intel Support

Intel provides official support when using an Intel® wireless module in both x86 and non-x86. Requests for assistance must be submitted through the [Intel Wireless Support Forum](https://community.intel.com/t5/Wireless/bd-p/wireless) that includes the following information:

- Issue symptoms
- Steps to reproduce the issue
- SoC/platform information
- Logs

!!! note "Required Logs"
    Logs include the driver information, driver log, and firmware log. Refer to the sections below for the detailed steps to collect each type.

## Collecting Logs – Driver Information

To identify the driver version on the platform, run this command and collect the output:

```bash
sudo modinfo iwlwifi
```

## Collecting Logs – Driver Log

The following method collects driver logs by enabling the driver to debug mask when the driver is loaded. Modify the `/etc/modprobe.d/iwlwifi.conf` to include the driver debugging mask. Add the following content to the file:

```ini
options iwlwifi debug=0xffffffff
```

Reboot the system after editing the file. Share the full kernel log using this command when issue is reproduced and share the output with Intel:

```bash
sudo dmesg
```

## Collecting Logs – Firmware Log

To collect the firmware log (e.g., firmware exception), the following method creates a udev rule and script to collect firmware logs.

### Create a udev Rule

Install udev and create the following rule to trigger firmware log collection. Create the file `/etc/udev/rules.d/85-iwl-dump.rules` with this command:

```ini
SUBSYSTEM=="devcoredump", ACTION=="add", RUN+="/usr/sbin/fwdump.sh"
```

### Create a Firmware Dump Shell Script

Create the shell script `/usr/sbin/fwdump.sh` and add this script:

```bash
#!/bin/bash

timestamp=$(date +%F_%H-%M-%S)
filename=/var/log/iwl-fw-error_${timestamp}.dump
cat /sys/${DEVPATH}/data > ${filename}
echo 1 > /sys/${DEVPATH}/data
```

### Change the Shell Script Permission

To allow udevd to run the shell script collection, change the script permission:

```bash
sudo chmod a+x /usr/sbin/fwdump.sh
```

### Collect the Firmware Log

If the firmware crashes, messages will be shown in the kernel log, such as:

```
iwlwifi 0000:01:00.0: Microcode SW error detected. Restarting 0x82000000.
[...]
iwlwifi 0000:01:00.0: Loaded firmware version: XX.XX.XX.XX
iwlwifi 0000:01:00.0: 0x0000090A | ADVANCED_SYSASSERT
```

A firmware log dump file will be generated at `/var/log/iwl-fw-error_<timestamp>.dump` where `<timestamp>` represents the timestamp string. Provide these files when submitting a support request.
