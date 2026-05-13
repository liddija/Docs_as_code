# Concept stubs referenced in this prototype

The Markdown file `install-oneagent-linux.md` references concept, entity, and runbook IDs that follow Dynatrace's naming convention (`dt.concept.*`, `dt.entity.*`, `dt.runbook.*`).

In a production context engineering practice, these IDs would resolve to canonical records in Dynatrace's **Semantic Dictionary** — the single source of truth for product concepts and telemetry entities.

This file is illustrative: it lists the IDs used in this prototype and the shape of record each would carry in the Semantic Dictionary. The actual definitions, ownership, and lifecycle rules would be owned by Information Development and Product, not by this prototype.

---

## Concepts

### dt.concept.oneagent_installation
- **Definition:** The act and lifecycle of deploying Dynatrace OneAgent onto a host.
- **Audience:** admin, sre
- **Related entities:** `dt.entity.oneagent`, `dt.entity.host`

### dt.concept.linux_host
- **Definition:** A host running a supported Linux distribution, monitored by OneAgent.
- **Audience:** admin, sre, platform_engineer
- **Related entities:** `dt.entity.host`

### dt.concept.monitoring_mode
- **Definition:** The operational mode OneAgent runs in — Full-Stack, Infrastructure, or Discovery.
- **Audience:** admin, sre

### dt.concept.activegate
- **Definition:** A Dynatrace component that proxies OneAgent traffic to the cluster.
- **Audience:** admin, sre, platform_engineer

### dt.concept.host_groups
- **Definition:** Logical grouping of hosts for organization and configuration.
- **Audience:** admin

### dt.concept.network_zones
- **Definition:** Logical network segmentation used to route OneAgent traffic.
- **Audience:** admin, platform_engineer

### dt.concept.oneagent_monitoring_modes
- **Definition:** The set of supported monitoring modes for OneAgent.
- **Audience:** admin, sre

### dt.concept.download_install_oneagent_permission
- **Definition:** The Dynatrace role required to download and install OneAgent.
- **Audience:** admin

### dt.concept.elevated_privileges
- **Definition:** Root or root-equivalent privileges on the host required to start the installer.
- **Audience:** admin, sre

### dt.concept.access_token_installer_download
- **Definition:** An access token with the `InstallerDownload` scope, required to download the installer.
- **Audience:** admin

---

## Entities

### dt.entity.host
- **Definition:** A monitored host in the Dynatrace environment.
- **Source:** Dynatrace Semantic Dictionary (canonical).

### dt.entity.oneagent
- **Definition:** A deployed OneAgent instance running on a host.
- **Source:** Dynatrace Semantic Dictionary (canonical).

---

## Runbooks

### dt.runbook.oneagent_install_troubleshooting
- **Definition:** Diagnostic procedures for OneAgent installation failures.
- **Source:** Dynatrace support knowledge base (canonical).
