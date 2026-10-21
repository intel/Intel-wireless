# Releases

Intel publishes validated releases of the Intel® Wi-Fi backport driver as **Core releases**. Each Core release is a snapshot of the Intel® Wi-Fi driver (`iwlwifi`), the wireless stack (`mac80211`, `cfg80211`), and the backport layer, tested together with the matching firmware. Core releases are published as `release/core<version>` branches in the [backport-iwlwifi](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git) repository on kernel.org.

As a rule, use the latest Core release for new integrations.

## Release Overview

| Release | Branch | Status | Release Notes |
|---------|--------|--------|---------------|
| core24.80 | [`release/core24.80`](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/log/?h=release/core24.80) | **Latest** | [core24.80 Release Notes](core24.80.md) |

- **Latest** — the recommended release for new and existing integrations.
- **Previous** — superseded by a newer release. Move to the latest release to receive new features and fixes.

All release branches, including earlier releases, are listed in the [backport-iwlwifi branch list](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/refs/heads).

## Getting the Latest Release

Clone the latest release branch with this command:

```bash
--8<-- "release.md:clone"
```

Then build and install the driver as described in [Native Build from Source](../build/native-build.md) or [Cross-Compilation](../build/cross-compile.md).

!!! note "Development Branch"
    Cloning without `-b` checks out `master`, the development branch, which is not a validated release.

## Updating an Existing Clone

Release branches receive updates over time. Each update is listed in the **Revision History** section of the release notes, together with the latest commit on the branch. To bring an existing clone up to date, or to move it to a newer release, run these commands from the `backport-iwlwifi` directory:

```bash
--8<-- "release.md:update"
```

To confirm the clone includes the latest update, run `git log -1 --oneline` and compare the commit with the **Latest Commit** shown in the release notes.

After updating, rebuild and reinstall the driver.
