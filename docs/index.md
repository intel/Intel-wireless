# Guidance for Integrating Intel® Wi-Fi into Non-x86 Platforms

!!! todo "Review: Legal Boilerplate"
    The legal notices below are kept from the original document. These need to be reviewed before public release — determine what to keep, modify, or remove for the open-source GitHub Pages site.

## Legal Notices

You may not use or facilitate the use of this document in connection with any infringement or other legal analysis concerning Intel products described herein. You agree to grant Intel a non-exclusive, royalty-free license to any patent claim thereafter drafted which includes subject matter disclosed herein.

No license (express or implied, by estoppel or otherwise) to any intellectual property rights is granted by this document.

All information provided here is subject to change without notice. Contact your Intel representative to obtain the latest Intel product specifications and roadmaps.

The products described may contain design defects or errors known as errata which may cause the product to deviate from published specifications. Current characterized errata are available on request.

Intel technologies' features and benefits depend on system configuration and may require enabled hardware, software or service activation. Learn more at [intel.com](http://www.intel.com/) or from the OEM or retailer.

No product or component can be absolutely secure.

Intel and the Intel logo are trademarks of Intel Corporation in the U.S. and/or other countries. *Other names and brands may be claimed as the property of others.

© Intel Corporation. Intel, the Intel logo, and other Intel marks are trademarks of Intel Corporation or its subsidiaries. Other names and brands may be claimed as the property of others.

---

## Introduction

### Scope of The Document

This document provides guidance for integrating Intel® Wi-Fi solutions on non-x86 platforms. It covers hardware considerations, software integration, platform configuration, and certification requirements. This document is intended  integrating Intel® Wi-Fi modules into non-x86 SoC platforms.

### Hardware Support Scope

The scope includes Intel® Wi-Fi discrete solution based on standard PCIe.

- Intel® Wi-Fi 7 BE200
- Intel® Wi-Fi 6E AX210

### Software Support Scope

The scope includes Linux-based operating systems. Intel provided the Wi-Fi driver and firmware for customers to integrate. But Intel is not responsible for maintaining the Linux kernel and changes for specific platforms.

## Quick Links

- [Hardware Considerations](getting-started/hardware-requirements.md) — PCIe Root Complex requirements
- [Build the Driver](build/index.md) — Native build or cross-compilation from source
- [Firmware Installation](firmware/installation.md) — Deploy firmware to target
- [Platform Guides](platforms/canonical-ubuntu.md) — DKMS for Canonical Ubuntu, NVIDIA Jetson
- [Wi-Fi Configuration](configuration/index.md) — UEFI, ACPI, and Device Tree settings
- [Debugging](troubleshooting/index.md) — Log collection and support

!!! todo "Suggested Addition: Getting Started Quickstart"
    Consider adding a quickstart flowchart page that walks through the recommended workflow: hardware verification → choose build method → firmware → configuration → test connectivity. The docx has a "high-level flow diagram" reference but no actual diagram content was embedded.
