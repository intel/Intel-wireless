# Hardware Integration Phase

In this phase, the firmware of your platform will do the PCIe bus scan. The PCIe root complex (RC) will read both PCIe Vendor ID and PCIe Device ID from the Configuration Space Header and configuration space body. This will allow the PCIe link between the host and the Intel® Wi-Fi endpoint to be configured properly. This phase does not involve the Intel® Wi-Fi firmware or drivers, and is entirely managed by the platform PCIe host controller.

## Verify PCIe Detection

Use the following Linux command to verify that the module is detected and enumerated correctly:

```bash
lspci
```

The following is an example output:

```
6e:00.0 Network controller: Intel Corporation Device 2725
```

![PCIe detection output](../assets/images/pcie-detection-output.png)

- `6e:00.0` — This is the BDF (Bus, Device, Function) node of your PCIe bus.
- `8086` — This is Intel's PCI Vendor ID.
- `2725` — This is the Device ID of Intel® Wi-Fi that you use. The example 0x2725 is the Device ID of AX210.

### Intel Discrete Wi-Fi Device IDs

Refer to this table for the Intel discrete Wi-Fi Device ID:

| Wi-Fi Device | Device ID |
|-------------|-----------|
| AX210 | 0x2725 |
| BE200 | 0x272b |
