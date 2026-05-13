---
doc_id: dt.doc.install_oneagent_linux
title: Install OneAgent on Linux
content_type: how-to
intent: how-to
audience: [admin, sre, platform_engineer]
authority_tier: canonical
owner: information_development
last_validated: 2026-04-08
oneagent_version_range: "latest"
supported_os: [linux]
supported_architectures: [x86_64, s390x, arm64, ppc64le]

concept_refs:
  - dt.concept.oneagent_installation
  - dt.concept.linux_host
  - dt.concept.monitoring_mode

entity_refs:
  - dt.entity.host
  - dt.entity.oneagent

permissions:
  - dt.concept.download_install_oneagent_permission
  - dt.concept.elevated_privileges
  - dt.concept.access_token_installer_download

related_concepts:
  - dt.concept.activegate
  - dt.concept.host_groups
  - dt.concept.network_zones
  - dt.concept.oneagent_monitoring_modes

known_limitations:
  - oracle_database_19c
  - nfs_mounted_drives

runbook_uri: dt.runbook.oneagent_install_troubleshooting
---

## Chunk 1 — Permissions for installing OneAgent on Linux

`chunk_id: dt.chunk.oneagent_linux_install_permissions`
`chunk_type: permissions`

This applies to Dynatrace OneAgent installation on a Linux host. The operator needs:

- **Dynatrace role:** `Download/install OneAgent` permission to download and install OneAgent.
- **Host privileges:** Elevated privileges on the target host to start the installer. To run in non-privileged mode, the host must meet specific system requirements; otherwise add `NON_ROOT_MODE=0` to the install command.
- **Service control:** Permissions and credentials to restart all application services on the host (required post-install).

If permissions are not met, installation fails before download. See `runbook_uri` for remediation.

---

## Chunk 2 — Resources required on the host

`chunk_id: dt.chunk.oneagent_linux_install_resources`
`chunk_type: resources`

This applies to OneAgent installation on a Linux host. The host must have:

- **Memory:** 200 MB free memory to run installation and updates.
- **Disk space:** Sufficient free disk space — see disk space requirements.
- **Network connectivity:** Outbound connectivity to the Dynatrace cluster, either directly or via an ActiveGate. Firewall must allow the outbound endpoints listed on the in-product installer page.

---

## Chunk 3 — Known limitations and incompatibilities

`chunk_id: dt.chunk.oneagent_linux_install_limitations`
`chunk_type: limitations`

OneAgent installation on Linux has known limitations in two environments:

1. **Oracle Database Server 19c** — Specific configuration required; see troubleshooting runbook.
2. **NFS-mounted drives** — Installation target should not be on an NFS mount.

These are not blockers but require pre-installation configuration. AI agents answering install questions for these environments should surface this chunk explicitly.

---

## Chunk 4 — Installer parameters and architecture support

`chunk_id: dt.chunk.oneagent_linux_install_parameters`
`chunk_type: configuration`

When installing OneAgent on Linux via the Dynatrace UI (Discovery & Coverage → Install → Install OneAgent), the operator selects:

- **OS type:** Linux
- **Architecture** (one of):
  - `x86` — 64-bit Intel/AMD
  - `s390` — 64-bit IBM Z mainframe
  - `ARM` — ARM64 / AARch64, including AWS Graviton
  - `PowerPC (LE)` — 64-bit PowerPC (ppc64le)
- **Monitoring mode:** Full-Stack, Infrastructure, or Discovery. Full-Stack is recommended for trials. Mode is reversible post-install.
- **Optional:** custom host name, network zone, host groups, tags, host properties. These bind the installed OneAgent to a `dt.entity.host` with the chosen organizational metadata.

The CLI installer supports additional parameters beyond the UI form.

---

## Chunk 5 — Token, download, and signature verification

`chunk_id: dt.chunk.oneagent_linux_install_token_download`
`chunk_type: procedure`

Installation requires an access token with the `InstallerDownload` scope (`Download OneAgent and ActiveGate installers`). The token is generated in-product or pasted from an existing one; it is appended automatically to the download and install commands.

Sequence:

1. **Download:** Run the provided `wget` command in the terminal. Requires up-to-date OpenSSL and CA certificate libraries on the host — outdated libraries cause the download to fail.
2. **Verify signature:** Run the provided verification command from the **Verify signature** box.
3. **Result:** A signed installer script, ready to execute.

If `wget` fails, the installer can be downloaded manually from the in-product page footer.

---

## Chunk 6 — Running the installer

`chunk_id: dt.chunk.oneagent_linux_install_execute`
`chunk_type: procedure`

Run the installer with root access. Elevated privileges are released as soon as OneAgent is deployed. The command varies by environment:

- **Ubuntu Server:** `sudo /bin/sh Dynatrace-OneAgent-Linux-<version>.sh`
- **Red Hat Enterprise Linux:** `su -c '/bin/sh Dynatrace-OneAgent-Linux-<version>.sh'`
- **Existing root session:** `/bin/sh Dynatrace-OneAgent-Linux-<version>.sh`

The installer optionally runs OneAgent under a non-privileged user (default). Post-install, the operator must restart all application processes to enable OneAgent monitoring of them — running processes are not injected retroactively.

---

## Chunk 7 — Verifying the installation

`chunk_id: dt.chunk.oneagent_linux_install_verify`
`chunk_type: verification`

After installation completes, OneAgent registers the host with the Dynatrace environment as a `dt.entity.host`. To confirm:

1. Open Dynatrace → **Infrastructure & Operations** → **Hosts**.
2. The host appears in the Hosts table with its hostname (or custom host name, if set).
3. Once registered, the host is available across Dynatrace's monitoring views.

If the host does not appear within 5 minutes, see `runbook_uri` for diagnostic steps (typically a network or token scope issue).
