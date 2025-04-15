# 🛡️ System Security Hardening

## ✅ Task 1: Secure a Linux System

### 1️⃣ Disable Root Login via SSH
**Steps:**
1. Open the SSH configuration file:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
2. Find and modify the following line:
   ```bash
   PermitRootLogin no
   ```
3. Save the file and restart SSH:
   ```bash
   sudo systemctl restart ssh
   ```

### 2️⃣ Set Up SSH Key Authentication
**Steps:**
1. Generate an SSH key (on your local machine):
   ```bash
   ssh-keygen -t rsa -b 4096
   ```
2. Copy the public key to the server:
   ```bash
   ssh-copy-id user@server-ip
   ```
3. Disable password authentication:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
   Set:
   ```bash
   PasswordAuthentication no
   ```
4. Restart SSH:
   ```bash
   sudo systemctl restart ssh
   ```

### 3️⃣ Configure Firewall (UFW - Uncomplicated Firewall)
**Steps:**
1. Enable UFW:
   ```bash
   sudo ufw enable
   ```
2. Allow SSH and essential services:
   ```bash
   sudo ufw allow ssh
   sudo ufw allow 80/tcp
   sudo ufw allow 443/tcp
   ```
3. Check firewall status:
   ```bash
   sudo ufw status
   ```

### 4️⃣ Install Fail2Ban (Prevents Brute Force Attacks)
**Steps:**
1. Install Fail2Ban:
   ```bash
   sudo apt install fail2ban -y
   ```
2. Copy the default config file:
   ```bash
   sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
   ```
3. Enable SSH protection:
   ```bash
   sudo nano /etc/fail2ban/jail.local
   ```
   Find `[sshd]` and set:
   ```bash
   enabled = true
   maxretry = 5
   ```
4. Restart Fail2Ban:
   ```bash
   sudo systemctl restart fail2ban
   ```

## ✅ Task 2: Secure a Windows Machine

### 1️⃣ Enable and Configure Windows Firewall
**Steps:**
1. Open **Windows Defender Firewall**
2. Click **Advanced Settings**
3. Create inbound/outbound rules:
   - Block unused ports
   - Allow only necessary services
4. Save changes

### 2️⃣ Set Audit Policies (Track Security Events)
**Steps:**
1. Open **Local Security Policy** (`secpol.msc`)
2. Navigate to **Local Policies > Audit Policy**
3. Enable:
   - Logon Events
   - Account Logon Events
   - System Events
   - Object Access

### 3️⃣ Configure Event Viewer (Track Logs)
**Steps:**
1. Open **Event Viewer** (`eventvwr.msc`)
2. Navigate to:
   - **Windows Logs > Security** (Tracks login attempts)
   - **Windows Logs > System** (System warnings)
3. Set up custom filters to monitor security incidents

### 4️⃣ Enable Windows Defender and Ransomware Protection
**Steps:**
1. Open **Windows Security**
2. Go to **Virus & Threat Protection**
3. Enable:
   - Tamper Protection
   - Ransomware Protection
