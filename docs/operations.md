# Operations — Day to Day Management

Common commands and routines for running the homelab.

---

## Playbooks

### Reconfigure Services (no OS updates)
```bash
ansible-playbook homelab-services.yml
```

### Update OS Packages + Services
```bash
ansible-playbook update-services.yml
```

---

## Targeting Hosts/Groups
```bash
ansible-playbook homelab-services.yml --limit monitor
ansible-playbook homelab-services.yml --tags proxy
```

---

## Service Restarts
Service roles handle stop/start for containerized stacks. Re‑apply the role/play after config changes.

---

## Backups
- Check schedule: `systemctl status backup.timer`
- Review recent logs on the backup host
- Perform periodic restore tests

---

## Adding a New Service Role
1. Setup VM on desired Proxmox server. Be sure to **enable start on boot and qemu guest agent**.
2. Create `roles/<service>` (tasks/templates/handlers). Be sure to assign necessary dependencies (usually vm and docker).
3. Add/assign a host group in `hosts`.
4. Include the role in all playbooks.
5. Test with `--limit <host>` and iterate.

---

## Secrets Rotation
Edit vaulted secrets safely:
```bash
ansible-vault edit vars/secrets.yml
```
Re‑run the affected plays.
