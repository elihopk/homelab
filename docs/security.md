# Security

Secure defaults across SSH, services, and secret handling.

---

## SSH Hardening
- Disable password authentication.
- Restrict root login to key‑based (`PermitRootLogin prohibit-password`).
- Restart `sshd` after applying changes.

---

## Access Control
- Roles applied per group — only services confirmed to be necessary and secure are bypassed.
- Identity/MFA is enforced via authelia traefik middleware.
- Suspicious activity is detected by crowdsec and banned using a traefik plugin

---

## Secrets
- `vars/secrets.yml` is **not** committed.
- Store with **Ansible Vault** or an external secret manager.
  ```bash
  ansible-vault edit vars/secrets.yml
  ```

---

## Keys
- Public keys distributed to VMs for backup operations.
- Rotate keys periodically; remove stale entries from `authorized_keys`.

---

## Network & Services
- Explicit allowlists for sensitive services.
- Least‑privilege service users and systemd unit overrides/capabilities where required.
