<!--
  CURRENT RECOMMENDED RELEASE - single source of truth.

  The build pages (native build, cross-compilation, NVIDIA Jetson) include
  the named sections below through pymdownx.snippets. Links use docs-root
  absolute paths (/releases/...) so they resolve from any page.

  New Core release (e.g. core24.80 -> core24.90):
    1. Update the release name, branch and release-notes link in this file.
    2. Add docs/releases/core<version>.md, using the previous page as a template.
    3. In docs/releases/index.md, add the new release as Latest and mark the
       previous one as Previous (also update Status on its release notes page).
    4. Add the new page to the Releases section of nav in mkdocs.yml.

  Update to the current release branch:
    1. Add the new items to the release notes page.
    2. Update Latest Commit and Last Updated, and add a Revision History row.

  Run `mkdocs build --strict` to confirm all links and snippets resolve.
-->

<!-- --8<-- [start:note] -->
!!! info "Latest Release: core24.80"
    The latest validated release of the Intel® Wi-Fi backport driver is **core24.80**, available on the [`release/core24.80`](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/log/?h=release/core24.80) branch. See the [core24.80 Release Notes](/releases/core24.80.md) for the changes in this release.

    Cloning without `-b` checks out `master`, the development branch, which is not a validated release. Release branches receive updates over time; to refresh an existing clone, see [Updating an Existing Clone](/releases/index.md#updating-an-existing-clone).
<!-- --8<-- [end:note] -->

<!-- --8<-- [start:clone] -->
git clone -b release/core24.80 https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git
<!-- --8<-- [end:clone] -->

<!-- --8<-- [start:update] -->
git fetch origin
git checkout release/core24.80
git pull
<!-- --8<-- [end:update] -->
