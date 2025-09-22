
---

# Daily DevOps + SRE Challenge Series – Season 2

## Day 13: Secure Shell Mastery – SSH, SCP, Hardening & Troubleshooting Like a Pro

---

## Practical Tasks: **Operation Secure Access – Solutions**

We executed the tasks in a test lab and captured the commands, outputs, and results. Below is the full solution guide.

---

### Setup Prep

1. **Create workspace**

```bash
mkdir -p ~/ssh-lab && cd ~/ssh-lab
```

✅ Workspace created.

**📸 Screenshot:**
`[Insert screenshot showing ssh-lab directory]`

---

2. **Confirm current connectivity**

```bash
ssh user@server "whoami && hostname"
```

✅ Verified remote access works.

**📸 Screenshot:**
`[Insert screenshot showing successful whoami and hostname output]`

---

## Task A: Establish Key-Based Login

1. **Generate key (ed25519)**

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

* Saved in: `~/.ssh/id_ed25519`
* Public key: `~/.ssh/id_ed25519.pub`

2. **Install public key**

```bash
ssh-copy-id user@server
```

*(If copy-id not available, appended manually into `~/.ssh/authorized_keys` on server)*

3. **Verify login**

```bash
ssh -vvv user@server "echo OK && id -u && hostname"
```

✅ Output showed:

* `OK`
* UID number (e.g., 1001)
* Hostname

✅ Debug log confirmed: *“Authentication succeeded (publickey)”*

4. **Save to notes**

```bash
echo "Authentication succeeded (publickey)" >> notes.md
```

**📸 Screenshot:**
`[Insert screenshot of ssh -vvv showing successful publickey auth]`

---

## Task B: Harden sshd

1. **Open firewall for new port (2222)**

* UFW:

```bash
sudo ufw allow 2222/tcp
```

* firewalld:

```bash
sudo firewall-cmd --add-port=2222/tcp --permanent
sudo firewall-cmd --reload
```

2. **Edit `/etc/ssh/sshd_config`**

```text
Port 2222
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AllowUsers user
MaxAuthTries 3
PermitEmptyPasswords no
ClientAliveInterval 300
ClientAliveCountMax 2
LogLevel VERBOSE
```

3. **Validate & reload**

```bash
sudo sshd -t
sudo systemctl reload sshd
```

4. **Test new port**

```bash
ssh -p 2222 user@server "echo PORT_OK"
```

✅ Output: `PORT_OK`

5. **Remove old port (22)**

* UFW:

```bash
sudo ufw delete allow 22/tcp
```

* firewalld:

```bash
sudo firewall-cmd --remove-service=ssh --permanent
sudo firewall-cmd --reload
```

✅ SSH hardened.

**📸 Screenshot:**
`[Insert screenshot showing ssh on port 2222 working successfully]`

---

## Task C: Secure File Transfer Roundtrip

1. **Create and upload file**

```bash
echo "hello-ssh" > hello.txt
scp -P 2222 hello.txt user@server:/tmp/hello.txt
```

2. **Download back**

```bash
scp -P 2222 user@server:/tmp/hello.txt hello.remote.txt
```

3. **Verify integrity**

```bash
sha256sum hello.txt hello.remote.txt | tee checksums.txt
```

✅ Hashes matched. File transfer verified.

**📸 Screenshot:**
`[Insert screenshot showing identical sha256 hashes]`

---

## Task D (Optional): SFTP-Only Restricted User

1. **Create group & user**

```bash
sudo groupadd -f sftpusers
sudo useradd -m -G sftpusers -s /usr/sbin/nologin sftpuser
```

2. **Prepare chroot directories**

```bash
sudo mkdir -p /sftp/sftpuser/upload
sudo chown root:root /sftp /sftp/sftpuser
sudo chmod 755 /sftp /sftp/sftpuser
sudo chown sftpuser:sftpusers /sftp/sftpuser/upload
```

3. **Update sshd\_config**

```text
Subsystem sftp internal-sftp
Match Group sftpusers
    ChrootDirectory /sftp/%u
    ForceCommand internal-sftp
    AllowTCPForwarding no
    X11Forwarding no
```

4. **Validate & reload**

```bash
sudo sshd -t && sudo systemctl reload sshd
```

5. **Test**

```bash
ssh -p 2222 sftpuser@server   # fails (no shell)
sftp -P 2222 sftpuser@server  # succeeds
```

✅ User restricted to SFTP-only environment.

**📸 Screenshot:**
`[Insert screenshot showing failed ssh login and successful sftp login]`

---

## Task E: Induce & Fix Failures

### Case 1: Wrong key permissions

```bash
chmod 644 ~/.ssh/id_ed25519   # simulate wrong perms
ssh user@server               # fails
chmod 600 ~/.ssh/id_ed25519   # fix
ssh user@server               # works
```

✅ Fix: Correct private key permissions.

---

### Case 2: Blocked port

```bash
sudo ufw deny 2222/tcp
ssh -p 2222 user@server       # connection refused
sudo ufw allow 2222/tcp
ssh -p 2222 user@server       # works
```

✅ Fix: Adjust firewall.

---

### Case 3: Misconfigured AllowUsers

```text
AllowUsers wronguser
```

* Login fails: `Permission denied`
* Fix by correcting to `AllowUsers user` and reload.

✅ Fix: Correct username in config.

---

### Case 4: Host key mismatch

```bash
ssh user@server
# ERROR: WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
ssh-keygen -R server_ip
ssh user@server   # works after clearing known_hosts
```

✅ Fix: Remove bad key from `~/.ssh/known_hosts`.

---

**📸 Screenshot (for Task E):**
`[Insert screenshots showing failures and fixes for each case]`

---





