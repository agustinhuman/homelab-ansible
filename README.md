# Playbooks

## Bootstrapping

This is a bootstrapping utility meant to be run manually to configure a new host.

It sets up the bare minimum configuration so the rest of playbooks can be run.

That is, configuring networking and admin user.

Sample execution:
```shell
# Debian
ansible-playbook -i 192.168.1.10, -u alejandro -bkK --ask-vault-password bootstrapping.yml -e "interface=eno1 ip=192.168.1.10 gateway=192.168.1.1"

# Pi
ansible-playbook -i 192.168.1.16, -bkK --ask-vault-password bootstrapping.yml -e "interface=eno1 ip=192.168.1.16 gateway=192.168.1.1"
```


