# Ansible Galaxy

## What is Ansible Galaxy?

**Ansible Galaxy** is a hub for sharing and discovering Ansible roles and collections. It's like a package manager for Ansible content - find, download, and use pre-built roles from the community.

## Why Use Galaxy?

- ✅ **Save Time** - Don't reinvent the wheel
- ✅ **Community Tested** - Use battle-tested roles
- ✅ **Best Practices** - Learn from experienced developers
- ✅ **Quick Setup** - Get complex services running fast

## Key Components

### 1. Roles

Pre-built automation for specific services (nginx, mysql, docker, etc.)

### 2. Collections

Bundled content including roles, modules, and plugins

## Essential Commands

### Search for Roles

```bash
ansible-galaxy search nginx
ansible-galaxy search mysql --author geerlingguy
```

### Install Roles

```bash
# Install latest version
ansible-galaxy install geerlingguy.nginx

# Install specific version
ansible-galaxy install geerlingguy.mysql,3.3.0

# Install from requirements file
ansible-galaxy install -r requirements.yml
```

### List Installed Roles

```bash
ansible-galaxy list
```

### Remove Roles

```bash
ansible-galaxy remove geerlingguy.nginx
```

## Requirements File (requirements.yml)

```yaml
---
# From Galaxy
- name: geerlingguy.nginx
  version: 2.8.0

- name: geerlingguy.mysql

# From Git
- src: https://github.com/username/ansible-role-custom.git
  name: custom-role

# Collections
collections:
  - name: community.general
    version: ">=3.0.0"
```

## Using Galaxy Roles in Playbooks

```yaml
---
- name: Setup web server
  hosts: webservers
  become: yes
  roles:
    - geerlingguy.nginx
    - geerlingguy.mysql
  vars:
    nginx_vhosts:
      - listen: "80"
        server_name: "example.com"
        root: "/var/www/html"
```

## Popular Galaxy Roles

- **geerlingguy.nginx** - Nginx web server
- **geerlingguy.mysql** - MySQL database
- **geerlingguy.docker** - Docker installation
- **geerlingguy.apache** - Apache web server
- **elastic.elasticsearch** - Elasticsearch setup

## Working with Collections

```bash
# Install collection
ansible-galaxy collection install community.general

# List collections
ansible-galaxy collection list

# Install from requirements
ansible-galaxy install -r requirements.yml
```

## Best Practices

- Always specify role versions in production
- Review role documentation before using
- Test roles in staging environment first
- Use requirements.yml for dependency management
- Check role ratings and download counts
- Prefer well-maintained roles with recent updates

## Creating Your Own Role

```bash
# Initialize role structure
ansible-galaxy init my-custom-role

# Publish to Galaxy (requires account)
ansible-galaxy import username my-custom-role
```

## Configuration

```bash
# Default install path: ~/.ansible/roles/
# Custom install path
ansible-galaxy install geerlingguy.nginx -p ./roles/

# Galaxy server configuration in ansible.cfg
[galaxy]
server_list = automation_hub, galaxy

[galaxy_server.automation_hub]
url=https://cloud.redhat.com/api/automation-hub/
```

---

**Galaxy = Community Roles + Collections + Time Savings**
