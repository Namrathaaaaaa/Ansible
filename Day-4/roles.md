# Ansible Roles

## What are Roles?
**Roles** are reusable collections of tasks, variables, and files organized in a standard structure. They make playbooks modular and reusable.

## Why Use Roles?
- ✅ **Reusable** across multiple playbooks
- ✅ **Organized** with standard structure
- ✅ **Modular** - break complex tasks into components

## Role Structure
```
roles/webserver/
├── tasks/main.yml      # Main tasks
├── handlers/main.yml   # Service restarts
├── templates/          # Jinja2 templates
├── files/              # Static files
├── vars/main.yml       # Variables
└── defaults/main.yml   # Default values
```

## Create Role
```bash
ansible-galaxy init webserver
```

## Example tasks/main.yml
```yaml
---
- name: Install Apache
  yum:
    name: httpd
    state: present

- name: Start Apache
  service:
    name: httpd
    state: started
```

## Using Roles in Playbooks
```yaml
---
- name: Configure servers
  hosts: webservers
  become: yes
  roles:
    - webserver
    - database
```

---
**Roles = Reusable + Organized + Modular**
