# ansible role for a ripe atlas software probe

Installs RIPE Atlas Software Probe using official packages from ftp.ripe.net

## Variables

### `atlas_probe_version`
Version to install. Default: `""` (auto-detect latest)

- Set to a specific version (e.g., `"5120"`, `"5110"`)
- Empty string `""` = auto-detect the latest available version from RIPE repository

### `atlas_probe_key` (optional)
Private SSH key for the RIPE Atlas probe. If defined, the key will be deployed to:
- `/etc/ripe-atlas/probe_key` (mode 0600, owner root:root)
- `/etc/ripe-atlas/probe_key.pub` (mode 0644, owner root:root) - auto-generated from private key

## Changes from v5080 (atlasswprobe)

Starting with v5090, the package naming and structure changed:
- Package name: `ripe-atlas-probe` (was `atlasswprobe`)
- Service name: `ripe-atlas` (was `atlas`)
- Key location: `/etc/ripe-atlas/` (was `/var/atlas-probe/etc/`)

## Example Playbook

```yaml
- hosts: probes
  roles:
    - role: atlas-install
```

With probe key:

```yaml
- hosts: probes
  roles:
    - role: atlas-install
      atlas_probe_key: "{{ vault_atlas_probe_key }}"
```

With specific version:

```yaml
- hosts: probes
  roles:
    - role: atlas-install
      atlas_probe_version: "5110"
      atlas_probe_key: "{{ vault_atlas_probe_key }}"
```
