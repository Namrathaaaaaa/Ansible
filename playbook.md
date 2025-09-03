# Ansible Playbooks - Quick Guide

## What is a Playbook?

A **playbook** is a YAML file that defines a series of tasks to be executed on remote hosts. Think of it as a recipe for automation.

## Basic Structure

```yaml
---
- name: Playbook description
  hosts: target_hosts
  become: yes # Run as sudo
  vars:
    variable_name: value
  tasks:
    - name: Task description
      module_name:
        parameter: value
```

## Key Components

### 1. Play

A mapping between hosts and tasks

```yaml
- name: Configure web servers
  hosts: webservers
  become: yes
```

### 2. Tasks

Individual actions to perform

```yaml
tasks:
  - name: Install Apache
    yum:
      name: httpd
      state: present

  - name: Start Apache service
    service:
      name: httpd
      state: started
```

### 3. Variables

Reusable values throughout the playbook

```yaml
vars:
  package_name: httpd
  service_name: httpd

tasks:
  - name: Install {{ package_name }}
    yum:
      name: "{{ package_name }}"
      state: present
```

### 4. Handlers

Tasks triggered by other tasks (usually for restarts)

```yaml
tasks:
  - name: Update config file
    template:
      src: httpd.conf.j2
      dest: /etc/httpd/conf/httpd.conf
    notify: restart apache

handlers:
  - name: restart apache
    service:
      name: httpd
      state: restarted
```

## Important Directives

| Directive | Purpose               | Example                               |
| --------- | --------------------- | ------------------------------------- |
| `hosts`   | Target machines       | `hosts: webservers`                   |
| `become`  | Run as sudo           | `become: yes`                         |
| `vars`    | Define variables      | `vars: { port: 80 }`                  |
| `when`    | Conditional execution | `when: ansible_os_family == "RedHat"` |
| `loop`    | Repeat task           | `loop: ['httpd', 'php']`              |
| `notify`  | Trigger handler       | `notify: restart service`             |

## Example Playbook

```yaml
---
- name: Setup web server
  hosts: webservers
  become: yes
  vars:
    packages:
      - httpd
      - php
      - mysql

  tasks:
    - name: Install packages
      yum:
        name: "{{ item }}"
        state: present
      loop: "{{ packages }}"

    - name: Start and enable httpd
      service:
        name: httpd
        state: started
        enabled: yes

    - name: Copy index.html
      copy:
        content: "<h1>Hello World</h1>"
        dest: /var/www/html/index.html
      notify: restart httpd

  handlers:
    - name: restart httpd
      service:
        name: httpd
        state: restarted
```

### Visual Example

Here's how the playbook execution looks in practice:

![Ansible Playbook Execution Example](https://github.com/user-attachments/assets/3d6a13ed-4fec-4dca-9b43-9444551cacbb)

## Execution Commands

```bash
# Run playbook
ansible-playbook playbook.yml

# Check syntax
ansible-playbook playbook.yml --syntax-check

# Dry run (see what would change)
ansible-playbook playbook.yml --check

# Run specific tags
ansible-playbook playbook.yml --tags "install"

# Limit to specific hosts
ansible-playbook playbook.yml --limit "web1.example.com"
```

## Best Practices

✅ **Do:**

- Use descriptive task names
- Group related tasks with tags
- Use variables for reusability
- Test with `--check` first
- Keep playbooks idempotent

❌ **Don't:**

- Hardcode values
- Make overly complex playbooks
- Forget to handle errors
- Skip documentation

## Common Patterns

### Conditional Tasks

```yaml
- name: Install package (RedHat)
  yum:
    name: httpd
    state: present
  when: ansible_os_family == "RedHat"

- name: Install package (Debian)
  apt:
    name: apache2
    state: present
  when: ansible_os_family == "Debian"
```

### Error Handling

```yaml
- name: Start service
  service:
    name: httpd
    state: started
  ignore_errors: yes

- name: Fail if service not running
  fail:
    msg: "Service failed to start"
  when: service_result.failed
```

### Tags for Organization

```yaml
- name: Install packages
  yum:
    name: httpd
    state: present
  tags:
    - install
    - packages

- name: Configure service
  template:
    src: httpd.conf.j2
    dest: /etc/httpd/conf/httpd.conf
  tags:
    - configure
```

---

**Remember:** Playbooks describe the desired state, Ansible figures out how to achieve it!
