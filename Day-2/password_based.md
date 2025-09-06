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
sudo systemctl restart ssh


```
## Setup Commands

**Set password for ubuntu user:**

```bash
sudo passwd ubuntu
```

**Copy SSH key:**

```bash
ssh-copy-id ubuntu@13.233.196.218

**SSH connect:**

```bash
ssh ubuntu@13.233.196.218
```

---

**Note:** Use only for initial setup, then switch to SSH keys.
