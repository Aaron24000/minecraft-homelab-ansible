
# Minecraft Homelab — Ansible

Ansible automation for managing my Ubuntu-based Minecraft homelab.

## Infrastructure

| Host | Role |
|---|---|
| minecraft01 | Modded Minecraft server running Docker |
| monitor01 | Ansible control node, Prometheus, and Grafana |

Both servers run Ubuntu Server 26.04.

## Playbooks

| Playbook | Purpose |
|---|---|
| system_info.yml | Gather system information |
| maintenance_check.yml | Check for available Ubuntu package updates |
| update_packages.yml | Refresh APT package lists |

## Setup

1. Install Ansible on the control node.
2. Configure SSH key authentication.
3. Copy `inventory.example.ini` to `inventory.ini`.
4. Update the inventory with the correct IP addresses, username, and SSH key path.
5. Verify connectivity.

```bash
ansible all -i inventory.ini -m ansible.builtin.ping
```

## Usage

Gather system information:

```bash
ansible-playbook -i inventory.ini system_info.yml
```

Check for package updates:

```bash
ansible-playbook -i inventory.ini maintenance_check.yml
```

Refresh APT package lists:

```bash
ansible-playbook -i inventory.ini update_packages.yml --ask-become-pass
```

## Security

- SSH key authentication is used for remote management.
- The private inventory is excluded from Git.
- Private SSH keys and credentials are never committed.
- Ansible uses `/usr/bin/sudo.ws` for compatibility with Ubuntu 26.04.
- Maintenance automation does not automatically upgrade packages or reboot servers.
