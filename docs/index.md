# Guidance for Integrating Intel® Wi‑Fi into Non‑x86 Platforms

## Introduction

### Scope of The Document

This document provides guidance for integrating Intel® Wi-Fi solutions on non-x86 platforms. It covers hardware considerations, software integration, platform configuration, and certification requirements. This document is intended to help customers integrate Intel® Wi-Fi modules into non-x86 SoC platforms.

### Hardware Support Scope

The scope includes Intel® Wi-Fi discrete solutions based on standard PCIe.

- Intel® Wi-Fi 7 BE200
- Intel® Wi-Fi 6E AX210

### Software Support Scope

The scope includes Linux-based operating systems. Intel provides the Wi-Fi driver and firmware for customers to integrate. However, Intel is not responsible for maintaining the Linux kernel or making changes for specific platforms.

## Quick Links

- [Hardware Requirements](getting-started/hardware-requirements.md) — PCIe Root Complex considerations
- [Build the Driver](build/index.md) — Native build or cross-compilation from source
- [Firmware Installation](firmware/installation.md) — Deploy firmware to target
- [Platform Guides](platforms/jetson/index.md) — NVIDIA Jetson, Canonical Ubuntu (DKMS)
- [Wi-Fi Configuration](configuration/index.md) — UEFI, ACPI, and Device Tree settings
- [Debugging](troubleshooting/index.md) — Log collection and support
