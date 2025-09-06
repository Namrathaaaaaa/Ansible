# Passwordless Authentication for Ansible

## What & Why?
**Passwordless authentication** uses SSH keys instead of passwords for automatic server connections. Essential for Ansible automation.

**Benefits:**
- ✅ No manual password entry
- ✅ More secure than passwords  
- ✅ Required for Ansible automation
- ✅ Scalable for multiple servers

---

## SSH-Copy-ID Command

```bash
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

| Part | Purpose | Example |
|------|---------|---------|
| `ssh-copy-id` | Copy SSH key to server | Base command |
| `-f` | Force overwrite existing keys | `-f` |
| `-o IdentityFile` | Specify private key file | `~/.ssh/aws-key.pem` |
| `ubuntu@IP` | Username and server IP | `ubuntu@54.123.45.67` |

**Real Example:**
```bash
ssh-copy-id -f "-o IdentityFile ~/.ssh/aws-key.pem" ubuntu@54.123.45.67
```

---

## Quick Setup Process

1. **Generate key** (if needed):
   ```bash
   ssh-keygen -t rsa -b 4096
   ```

2. **Copy key to server:**
   ```bash
   ssh-copy-id -f "-o IdentityFile ~/.ssh/key.pem" ubuntu@server-ip
   ```

3. **Test connection:**
   ```bash
   ssh -i ~/.ssh/key.pem ubuntu@server-ip
   ```

4. **Use with Ansible:**
   ```bash
   ansible all -m ping
   ```

---

## Visual Examples

### Command Execution:
![SSH-Copy-ID Example](https://github.com/user-attachments/assets/6a959dda-9da1-42fa-9189-0605ee290dd5)

### Ansible Nginx Deployment Result:
![Nginx Website Deployment](https://github.com/user-attachments/assets/e26d6750-cd5d-4233-af49-a6685f4f7db2)

---

## Ansible Integration

**Inventory:**
```ini
[webservers]
web1 ansible_host=54.123.45.67 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/aws-key.pem
```

**Config (ansible.cfg):**
```ini
[defaults]
private_key_file = ~/.ssh/aws-key.pem
remote_user = ubuntu
host_key_checking = False
```

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Permission denied | `chmod 600 ~/.ssh/key.pem` |
| Connection refused | Check SSH service is running |
| Key not found | Verify key file path |

---

**Result:** Set up once, automate forever with Ansible!