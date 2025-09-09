# Ansible Inventory

## What is Inventory?

Inventory defines which hosts Ansible manages. Files can be `.ini` or `.yaml` format.

## INI Format Example:

```ini
[webservers]
web1.example.com
web2.example.com ansible_host=192.168.1.10

[databases]
db1.example.com ansible_user=admin
```

## YAML Format Example:

```yaml
webservers:
  hosts:
    web1.example.com:
    web2.example.com:
      ansible_host: 192.168.1.10
```

## Usage Commands:

```bash
ansible all -i inventory.ini -m ping
ansible webservers -i hosts.yaml -m shell -a "uptime"
```

## Ad-hoc Commands:

Quick one-time tasks without playbooks. Format: `ansible [hosts] -m [module] -a [arguments]`

```bash
ansible all -m shell -a "df -h"
ansible webservers -m yum -a "name=httpd state=present" --become
```
