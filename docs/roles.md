# Roles Overview

Modular Ansible roles keep configuration clear, testable, and reusable.

---

| Role        | Purpose                                                                                       |
|-------------|-----------------------------------------------------------------------------------------------|
| `vm`        | Base OS agents and essentials for new VMs.                                                    |
| `docker`    | Container runtime install, group membership, container metrics exporter.                      |
| `proxy`     | Reverse proxy, identity/security gateway, DB init for Crowdsec to issue API key to Traefik.   |
| `db`        | Relational DB install/config; DB/user provisioning; metrics exporter.                         |
| `monitor`   | Central metrics/logs stack: configs, storage, and UI.                                         |
| `backup`    | Backup tooling, templated config, `systemd` unit/timer, key distribution.                     |
| `media`     | Content management/automation stack (hardware accel enabled).                                 |
| `nextcloud` | Collaboration/document cloud stack with storage/cache layers.                                 |
| `search`    | Private search/metasearch stack.                                                              |
| `vaultwarden`| Personal secrets vault stack.                                                                |
| `budget`    | Finance management stack.                                           |

Each role typically includes:
- **Meta** — Includes role info and dependency definitions
- **Tasks** — idempotent install/config steps
- **Templates** — Jinja2 configs using host/group vars
