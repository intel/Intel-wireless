# Hardware Integration Phase

In this phase, the firmware of your platform will do the PCIe bus scan. The PCIe Root Complex (RC) will read both PCIe vendor id and PCIe device id from Configuration Space Header and configuration space body. This will allow PCIe link between host and Intel® Wi-Fi endpoint to be configured properly. This phase does not involve Intel® Wi-Fi firmware or drivers and is entirely managed by the platform PCIe host controller.

## Verify PCIe Detection

Use the following Linux command to verify that the module is detected and enumerated correctly:

```bash
lspci
```

Here is example output:

```
6e:00.0 Network controller: Intel Corporation Device 2725
```

![PCIe detection output](../assets/images/pcie-detection-output.png)

- `6e:00.0` — This is the BDF (Bus, Device, Function) node of your PCIe bus.
- `8086` — This is the Intel Vendor ID.
- `2725` — This is the device ID of Intel® Wi-Fi that you use. The example 0x2725 is the device id of AX210.

### Intel Discrete Wi-Fi Device IDs

| Wi-Fi Device | Device ID |
|-------------|-----------|
| AX210 | 0x2725 |
| BE200 | 0x272b |

!!! todo "Suggested Addition: Troubleshooting Detection Failure"
    Consider adding a short checklist for when lspci does not show the Intel device: check M.2 key type (E or A+E), check PCIe lane is enabled in platform DT/UEFI, check physical seating of module.
