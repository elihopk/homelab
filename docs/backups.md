# Backups

Backups are fully automated using an Ansible-managed role that installs and configures deduplicating, encrypted backup tooling on the backup server.

---

## Overview
The setup includes:

- **Config templating**: Backup paths, repository location, pruning, and retention are all rendered from Jinja2 templates.
- **Scheduled execution**: A `systemd` timer triggers backups at regular intervals.
- **Secure key distribution**: A public key is pushed to target VMs for passwordless access during backup runs.

---

## How It Works
1. **Install backup tool**: The backup role sets up the runtime environment and installs required binaries in an isolated context.
2. **Configure backup**: Templates render a config file defining:
   - Source directories
   - Destination repository (offsite storage)
   - Retention policy (daily/weekly/monthly pruning)
3. **Enable scheduling**: A `systemd` service and timer are created to run backups automatically.
4. **Distribute public key**: Ansible adds the backup server’s public key to each target VM’s `authorized_keys`.

---

## Repository
- Backups are pushed to an **offsite storage endpoint** (Hetzner Storage Box).
- Access is secured using the backup server’s private key (not stored in the repo).

---

## Restore Procedure (high-level)
1. Stop all Docker containers across all hosts.
2. SSH into the backup server.
3. Run `sudo borgmatic list` to get the list of all possible backups.
4. Run `sudo borgmatic extract --archive <name of chosen backup>`. This will pull the backup from Hetzner and restore files to all servers.
5. Run `sudo borgmatic restore --archive <name of chosen backup>`. This will pull the backup from Hetzner and restore all postgres databases.
6. Start all Docker stacks (including alloy stacks) and verify functionality.

---

## Maintenance
- Monitor backup logs for errors or failed runs.
- Periodically test a full restore.
- Rotate keys and credentials periodically.