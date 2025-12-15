
## Server Hardening

---

## 1. SSH Configuration Using Key‑Based Authentication

This section outlines the configuration of Secure Shell (SSH) key‑based authentication as a server hardening measure. Key‑based authentication enhances security by eliminating password‑based logins, thereby reducing exposure to brute‑force and credential‑based attacks.

### Step 1: SSH Key Pair Generation

The initial step involves generating an SSH key pair on the client workstation using the following command:

```bash
ssh-keygen -t ed25519 -C "comments"
```

This command generates a cryptographically secure private key, which remains on the workstation, and a corresponding public key that will be deployed to the remote server.

![ssh key generation image ](assets/images-4/ssh-key.png)

---

### Step 2: Deployment of the Public Key to the Server

After generating the key pair, the public key is securely transferred to the server using the command below:

```bash
ssh-copy-id username@server_ip_address
```

This process appends the public key to the `~/.ssh/authorized_keys` file on the server, enabling authentication via SSH keys.

![Key installation ](assets/images-4/sshpublic.png)

---

### Step 3: SSH Daemon Configuration

To enforce exclusive use of key‑based authentication, the SSH daemon configuration file is modified as follows:

```bash
sudo nano /etc/ssh/sshd_config
```

The following configuration parameters are applied:

```text
PubkeyAuthentication yes
PasswordAuthentication no
```

These settings ensure that public key authentication is enabled while password‑based authentication is disabled, significantly improving access control.

![](assets/images-4/pubkey.png)

![](assets/images-4/passwordauth.png)

Following these changes, the SSH service is restarted to apply the new configuration.

---

### Step 4: Verification of SSH Access

Once configuration is complete, secure access to the server can be established using the following command:

```bash
ssh username@ip_address
```

Successful login without a password confirms correct implementation of key‑based authentication.


---

## 2. Firewall Configuration to Restrict SSH Access

To further strengthen server security, the Uncomplicated Firewall (UFW) is configured to restrict SSH access to a single trusted workstation IP address.

### Firewall Status Prior to Configuration

![](assets/images-4/configurefirewall.png)

### Applied Firewall Rules

```bash
ufw allow from workstation_ip_address to any port 22 proto tcp
ufw deny 22/tcp
```

These rules explicitly permit SSH connections only from the specified IP address while denying all other inbound SSH traffic.

### Firewall Status After Configuration

![](assets/images-4/statusverbose.png)

---




