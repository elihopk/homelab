# Bootstrap — Bringing a New Deployment Online

End‑to‑end provisioning from hypervisors → VMs → base OS → services → hardening.

---

## Prerequisites
- SSH connectivity to specified Proxmox servers from the control node.
- Host declared in `hosts` under the appropriate group(s).
- Functional network. If installing a router on a Proxmox server make sure this is done first. It is important to keep backups of router settings.

---

## Steps

### 1) Install Proxmox
- Install Proxmox on all necessary hypervisors
- Be sure to choose btrfs as the filesystem type with zstd compression during installation.

### 2) Setup Hosts File
- Make any adjustments needed to the hosts file including but not limited to updating VMIDs, IP addresses, Proxmox hosts, and required resources.

### 3) Deploy Homelab
- The whole homelab can be deployed with one simple command. Just run this and wait for it to finish: `ansible-playbook deploy-homelab.yml`
