# Secure your Linux Servers

> [!TIP]
>Are your Linux servers safe from hackers? Can they be hacked?  
I shows you how to secure and HARDEN your Linux server.  
While nothing is full-proof, taking these steps to harden your Linux server is VITAL and will help protect you from attacks.


## STEP 1 - Enable Automatic Updates
**Manual Updates:**

```bash
apt update
apt dist-upgrade
```

**Automatic Updates:**

```bash
apt install unattended-upgrades
dpkg-reconfigure --priority=low unattended-upgrades
```


## STEP 2 - Create a Limited User Account

**Create a User:**

```bash
adduser {username}
```

**Add user to the sudo group:**

```bash
usermod -aG sudo {username}
```


## STEP 3 - Passwords are for SUCKERS!

**Create the Public Key Directory on your Linux Server**

```bash
mkdir ~/.ssh && chmod 700 ~/.ssh
```

**Create Public/Private keys on your computer**

```bash
ssh-keygen -t ed25519 -C "add_name_to_identify_key"
```

>[!NOTE]
>If you are using a legacy system that doesn't support the Ed25519 algorithm, use:
>```bash
>ssh-keygen -t rsa -b 4096 -C "add_name_to_identify_key"
>```

**Upload your Public key to the your Linux Server (Windows)**

```bash
scp $env:USERPROFILE/.ssh/id_rsa.pub {username}@{server ip}:~/.ssh/authorized_keys
```

**Upload your Public key to the your Linux Server (MAC)**

```bash
scp ~/.ssh/id_rsa.pub {username}@{server ip}:~/.ssh/authorized_keys
```

**Upload your Public key to the your Linux Server (LINUX)**

```bash
ssh-copy-id {username}@{server ip}
```


## STEP 4 - Lockdown Logins

**Edit the SSH config file**

```bash
sudo nano /etc/ssh/sshd_config
```

## STEP 5 - FIREWALL IT UP

**See open ports**

```bash
sudo ss -tupln
```

**Install UFW**

```bash
apt install ufw
```

**See UFW status**

```bash
sudo ufw status
```

**Allow port through firewall**

```bash
sudo ufw allow {port number}
```

**Enable Firewall**

```bash
sudo ufw enable
```

**Reload Firewall**

```bash
sudo ufw reload
```


**Drop pings**

Edit the UFW config file

```bash
sudo nano /etc/ufw/before.rules
```

**Add this line of config:**

```bash
-A ufw-before-input -p icmp --icmp-type echo-request -j DROP
```
