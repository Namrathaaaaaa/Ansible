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

| Part              | Purpose                       | Example               |
| ----------------- | ----------------------------- | --------------------- |
| `ssh-copy-id`     | Copy SSH key to server        | Base command          |
| `-f`              | Force overwrite existing keys | `-f`                  |
| `-o IdentityFile` | Specify private key file      | `~/.ssh/aws-key.pem`  |
| `ubuntu@IP`       | Username and server IP        | `ubuntu@54.123.45.67` |

**Real Example:**

```bash
ssh-copy-id -f "-o IdentityFile ~/.ssh/aws-key.pem" ubuntu@54.123.45.67
```

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

| Problem            | Solution                     |
| ------------------ | ---------------------------- |
| Permission denied  | `chmod 600 ~/.ssh/key.pem`   |
| Connection refused | Check SSH service is running |
| Key not found      | Verify key file path         |

---

**Result:** Set up once, automate forever with Ansible!
