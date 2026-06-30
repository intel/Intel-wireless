# Hardware Considerations

## Considerations for PCIe Root Complex

Intel® Wi-Fi acts as a PCIe endpoint that is compliant with the PCIe standard. From the hardware logical design perspective, once you follow the PCIe specification to design the interface connected to Intel® Wi-Fi, the platforms function correctly when PCIe specifications are fully met. However, the PCIe Root Complex (RC) of the target platform may have capability differences and constraints. The key information that is highlighted that need for PCIe Root Complex (RC) is summarized below.

### PCIe Root Complex Capabilities Summary

| Capability | AX210 | BE200 |
|-----------|-------|-------|
| MSI-X Interrupt | Required | Required |
| PCIe de-emphasis | Required | Required |
| PCIe relaxed ordering control | Required | Required |
| 5-Bit tags | Required | Required |
| Disable NoSnoop | — | Required |

### Supported MSI-X Interrupt

Intel® Wi-Fi uses PCIe MSI-X (Message Signaled Interrupts Extended) for IRQ handling. The driver implementation does not support legacy interrupt (line based). In PCIe Gen2, the MSI-X is optional in standard.

To verify this PCIe capability, check the platform using the following command:

```bash
sudo lspci -vvv
```

The output indicates MSI-X capability as `Enable+`.

![MSI-X lspci output](../assets/images/msix-lspci-output.png)

### Supported Control of PCIe De-emphasis

In PCIe Gen2, it is recommended to disable PCIe de-emphasis implemented in the Intel® Wi-Fi module. This configuration helps prevent PCIe device enumeration issues.

### Support PCIe Relaxed Ordering Control

Intel® Wi-Fi does not support PCIe relaxed ordering. Relaxed ordering must be disabled for PCIe Gen2 configurations.

### Support the Use of PCIe 5-Bit Tags

Intel® Wi-Fi supports only the 5-bit extended tag capability. Some PCIe Root Complexes (RCs) enable 8-bit or 10-bit tags by default. If this is the case, disable 8-bit and 10-bit tag support.

### Do Not Support NoSnoop

Intel® BE200 Wi-Fi does not support the NoSnoop capability. Please make sure that NoSnoop is disabled in PCIe Root Complexes (RCs).

!!! todo "Suggested Addition: PCIe Verification Commands"
    Consider adding platform-specific commands to verify each PCIe capability (de-emphasis, relaxed ordering, tags, NoSnoop) — similar to the MSI-X lspci check above. The docx only provides the MSI-X verification command.
