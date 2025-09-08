# Ansible Roles

## What are Ansible Roles?
**Roles** are reusable collections of tasks, variables, files, and templates organized in a standardized directory structure. They promote code reusability and organization.

## Why Use Roles?
- ✅ **Reusable** - Use across multiple playbooks
- ✅ **Organized** - Clean directory structure
- ✅ **Modular** - Break complex playbooks into components
- ✅ **Shareable** - Share via Ansible Galaxy
- ✅ **Maintainable** - Easier to update and debug

## Role Directory Structure
```
roles/
└── webserver/
    ├── tasks/
    │   └── main.yml          # Main tasks file
    ├── handlers/
    │   └── main.yml          # Handlers (service restarts, etc.)
    ├── templates/
    │   └── httpd.conf.j2     # Jinja2 templates
    ├── files/
    │   └── index.html        # Static files
    ├── vars/
    │   └── main.yml          # Role variables
    ├── defaults/
    │   └── main.yml          # Default variables
    ├── meta/
    │   └── main.yml          # Role metadata
    └── README.md             # Role documentation
```

## Creating a Role
```bash
# Create role structure
ansible-galaxy init webserver

# Create role in specific directory
ansible-galaxy init roles/database
```

## Example Role Structure

### tasks/main.yml
```yaml
---
- name: Install Apache
  yum:
    name: httpd
    state: present

- name: Start Apache service
  service:
    name: httpd
    state: started
    enabled: yes
  notify: restart apache
```

### handlers/main.yml
```yaml
---
- name: restart apache
  service:
    name: httpd
    state: restarted
```

### defaults/main.yml
```yaml
---
apache_port: 80
document_root: /var/www/html
```

## Using Roles in Playbooks
```yaml
---
- name: Configure web servers
  hosts: webservers
  become: yes
  roles:
    - webserver
    - common

# With variables
- name: Configure with custom vars
  hosts: webservers
  become: yes
  roles:
    - role: webserver
      apache_port: 8080
      document_root: /var/www/myapp
```

## Best Practices
- Keep roles focused on single functionality
- Use meaningful role names
- Document variables in README.md
- Use defaults for commonly changed values
- Test roles independently
- Version control your roles

---
**Remember:** Roles make your Ansible code modular, reusable, and maintainable!
