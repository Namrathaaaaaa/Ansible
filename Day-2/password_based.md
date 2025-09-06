# Password-Based Authentication

## SSH Configuration

```bash
sudo vim /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
```

```bash
sudo vim /etc/ssh/sshd_config
```

**Enable password authentication:**

```bash
PasswordAuthentication yes
```

**Restart SSH:**

```bash
sudo systemctl restart sshd
```

---

**Note:** Use only for initial setup, then switch to SSH keys.
