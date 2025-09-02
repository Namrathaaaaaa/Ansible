# Ansible Quick Reference Guide

## What is Ansible?

**Ansible** is an agentless automation tool for configuration management, application deployment, and orchestration. Simple, powerful, and human-readable.

## Ansible vs Chef - Key Differences

| Aspect             | Ansible               | Chef                         |
| ------------------ | --------------------- | ---------------------------- |
| **Architecture**   | Push-based, agentless | Pull-based, agent-required   |
| **Language**       | YAML (declarative)    | Ruby DSL (procedural)        |
| **Learning Curve** | Easy to start         | Steeper, requires Ruby       |
| **Installation**   | Control node only     | Server + client on all nodes |
| **Network**        | Outbound SSH (22)     | Inbound HTTPS (443)          |

**Why Ansible?**

- ✓ No agent installation
- ✓ Human-readable YAML
- ✓ Simpler architecture
- ✓ Lower learning curve

---

## Core Components

### 1. Control Node

Machine where Ansible is installed.

- Requirements: Python 2.7+, Linux/Unix, SSH client

### 2. Managed Nodes

Target systems Ansible manages.

- Requirements: SSH server, Python 2.6+

### 3. Inventory

Defines hosts and groups:

```ini
[webservers]
web1.example.com
web2.example.com

[databases]
db1.example.com
```

### 4. Playbooks

YAML files defining tasks:

```yaml
---
- name: Configure web servers
  hosts: webservers
  become: yes
  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: present

    - name: Start Apache
      service:
        name: httpd
        state: started
        enabled: yes
```

### 5. Modules

Built-in task units:

- `yum/apt` - Package management
- `service` - Service management
- `copy` - File operations
- `shell/command` - Command execution

---

## How Ansible Works

```
Control Node → SSH → Managed Node → Execute → Return Results
```

**Process:**

1. Parse playbook
2. Read inventory
3. SSH to hosts
4. Transfer & execute modules
5. Return results

---

## Key Features

### Idempotency

Running the same playbook multiple times = same result

### Declarative

Describe desired state, not steps:

```yaml
- name: Ensure user exists
  user:
    name: john
    state: present
    shell: /bin/bash
```

### Agentless

No agents to install or manage on target systems

---

## Essential Commands

```bash
# Install
pip install ansible

# Check connectivity
ansible all -m ping

# Run ad-hoc command
ansible webservers -m shell -a "uptime"

# Execute playbook
ansible-playbook site.yml

# Dry run (check mode)
ansible-playbook site.yml --check

# Verbose output
ansible-playbook site.yml -vvv
```

---

## Project Structure

```
ansible-project/
├── inventory/
│   ├── production
│   └── staging
├── group_vars/
│   └── all.yml
├── roles/
│   ├── common/
│   └── webserver/
└── site.yml
```

---

## Common Use Cases

1. **Configuration Management** - Standardize server configs
2. **Application Deployment** - Deploy apps across environments
3. **Infrastructure Orchestration** - Coordinate complex setups
4. **Cloud Automation** - Manage AWS/Azure/GCP resources

---

## Quick Tips

- Use `--check` for dry runs
- Group related tasks in roles
- Use variables for reusability
- Test in staging before production
- Keep playbooks in version control

---

## Additional Resources

📄 **Detailed Ansible Guide PDF**: [file.pdf](https://github.com/user-attachments/files/22088485/file.pdf)

---

**Remember:** Ansible is about describing the desired state, not the steps to get there!
