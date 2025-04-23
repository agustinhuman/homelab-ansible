# Playbooks

## Bootstrapping

A bootstrapping utility meant to be run manually to configure a new host.

It sets up the bare minimum configuration so the rest of playbooks can be run (networking and admin user).

Sample execution:
```shell
ansible-playbook -i 192.168.1.193, -bkK --vault-password-file=~/.ssh/vault bootstrap.yml -e "ansible_ssh_user=alejandro ip=192.168.5.44 gateway=192.168.5.1"
```

## NFS Mounts

The playbook supports two types of NFS mounts:

1. **Permanent NFS Mount**: This mount is established during system startup and remains mounted throughout the node's lifetime. Configure it in `group_vars/all/vars.yml` under `nas.permanent`.

2. **Backup NFS Mount**: This mount is temporarily established when backup operations are performed and then unmounted. Configure it in `group_vars/all/vars.yml` under `nas.backup`.

### Configuration

Example configuration in `group_vars/all/vars.yml`:

```yaml
nas:
  host: "192.168.5.15"
  # Permanent NFS mount that will be present during the lifetime of a node
  permanent:
    mount_point: "/mnt/nas_permanent"
    share: "/shared"
    options: "rw,sync,hard,intr"
  # Temporary NFS mount for backups (mounted and unmounted as needed)
  backup:
    user: backup
    password: "{{ vault_nas_backup_password }}"
    mount_point: "/mnt/nas_backups"
    share: "/backups"
    options: "rw,sync,hard,intr"
```
