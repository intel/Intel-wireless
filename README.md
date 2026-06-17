# Intel® Wi-Fi Integration Guide for Non-x86 Platforms

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![GitHub Pages](https://img.shields.io/badge/docs-GitHub%20Pages-blue)](https://intel.github.io/Intel-wireless/)

This repository provides documentation, patches, and integration guidance for enabling Intel® Wi-Fi modules on non-x86 platforms (ARM, RISC-V). It is intended for system architects and software engineers integrating Intel® Wi-Fi into embedded and SoC-based systems.

## 📖 Documentation

Full documentation is available at: **[intel.github.io/Intel-wireless](https://intel.github.io/Intel-wireless/)**

## Topics Covered

- **Hardware Considerations** — PCIe Root Complex requirements (MSI-X, de-emphasis, relaxed ordering, tags, NoSnoop)
- **Driver Build Methods** — Native build from source, cross-compilation, and DKMS for Ubuntu
- **Firmware Installation** — Deploying `*.ucode` and `*.pnvm` files to the target
- **Platform Guides** — Canonical Ubuntu (DKMS), NVIDIA Jetson (Orin, Thor)
- **Configuration** — UEFI variables, ACPI _DSM methods, Device Tree bindings
- **Troubleshooting** — Driver and firmware log collection, FAQ

## Repository Structure

```
Intel-wireless/
├── docs/                          # Documentation source (Markdown)
│   ├── index.md                   # Home page
│   ├── getting-started/           # Hardware requirements & verification
│   ├── build/                     # Native build, cross-compilation
│   ├── firmware/                  # Firmware installation
│   ├── platforms/                 # Per-platform guides
│   │   ├── canonical-ubuntu.md    #   DKMS-based installation
│   │   └── jetson/                #   NVIDIA Jetson specifics
│   ├── configuration/             # UEFI, ACPI, Device Tree settings
│   └── troubleshooting/           # Debugging, log collection, FAQ
├── patches/                       # Platform-specific patches (planned)
├── scripts/                       # Build helpers (planned)
├── mkdocs.yml                     # MkDocs site configuration
└── .github/workflows/             # CI/CD for GitHub Pages (planned)
```

## Building the Documentation Locally

```bash
pip install mkdocs mkdocs-material
mkdocs serve
```

Then open [http://localhost:8000/Intel-wireless/](http://localhost:8000/Intel-wireless/) in your browser.

## Contributing

We welcome contributions! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a pull request.

## Security

To report a security vulnerability, please refer to [SECURITY.md](SECURITY.md).

## License

Documentation in this repository is licensed under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/).
Patches and code are licensed under [GPL-2.0-only](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html) (inheriting from the upstream Linux kernel).
