# 🐧 Create Virtual Machine (Kali Linux) on AWS ☁️

<p align="center">
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" />
  <img src="https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/SSH-000000?style=for-the-badge&logo=openssh&logoColor=white" />
  <img src="https://img.shields.io/badge/VNC-00A1E0?style=for-the-badge&logo=realvnc&logoColor=white" />
</p>

---

## 🧾 Summary

This project demonstrates how to **create and configure a Kali Linux virtual machine on AWS EC2**, install a lightweight GUI (XFCE), and securely access it via **VNC over SSH tunneling**.  
The repository contains complete step-by-step documentation, commands, and screenshots — showcasing cloud administration, Linux configuration, and remote access setup skills.

---

## 🧰 Tools & Technologies

- **Operating System:** Kali Linux  
- **Cloud Platform:** Amazon Web Services (EC2)  
- **Access Method:** SSH / OpenSSH (`.pem` keypair)  
- **GUI & Remote Access:** XFCE4, TightVNC, SSH tunneling  
- **Software:** VNC Viewer (Windows/macOS/Linux)  
- **Command-line Tools:** apt, netstat, systemctl, nano  

---

## ⚙️ Prerequisites

- AWS account with EC2 access  
- SSH client (Linux/macOS Terminal or PuTTY on Windows)  
- Installed VNC viewer (RealVNC, TigerVNC, TightVNC, etc.)  
- Basic Linux terminal knowledge  

---

## 🚀 Step-by-Step Setup Guide

### **Step 1:** Create and log in to AWS account
- Sign up for a personal **AWS account**.
- Log in to the **AWS Management Console**.

<img src="https://raw.githubusercontent.com/nabirudd/aws-kali-vm-setup/refs/heads/main/Images/AWS%20Console.png" alt="Setup" height="500" hspace="70">

### **Step 2:** Launch EC2 instance
- Open **EC2** from the AWS console (select your preferred region, e.g., *Ireland*).
- Click **Launch Instance** → name it: `MyTestServer`.
- Choose **Kali Linux** from the AWS Marketplace.
- Select instance type: `t3.small` (2 vCPU, 2 GB memory) — *note: may not be free tier*.
- Create a **key pair** (e.g., `kali.pem`) for SSH access.
- Enable **HTTP** (80), **HTTPS** (443), and **SSH** (22) in the security group.
- Keep storage default and **Launch Instance**.

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/EC2.png?raw=true" alt="Setup" height="500" hspace="70">
<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/OS%20Setup.png?raw=true" alt="Setup" height="500" hspace="70">
<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Instance.png?raw=true" alt="Setup" height="500" hspace="70">
<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/AWS%20Klai.png?raw=true" alt="Setup" height="500" hspace="70">
<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Network%20Setting.png?raw=true" alt="Setup" height="500" hspace="70">
<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Keypair%20Creation.png?raw=true" alt="Setup" height="500" hspace="70">

### **Step 3:** Connect via SSH
Secure the key and connect:
```bash
chmod 400 kali.pem
ssh -i kali.pem kali@<PUBLIC_IP>

````

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Sucessful%20SSH%20connection.png?raw=true" alt="Setup" height="500" hspace="70">


---

### **Step 4:** Update Kali Linux

```bash
sudo apt update && sudo apt upgrade -y
```
<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Kali%20Update.png?raw=true" alt="Setup" height="500" hspace="70">

---

### **Step 5:** Install XFCE desktop and VNC server

```bash
sudo apt install -y xfce4 xfce4-goodies tightvncserver
```

```bash
sudo apt-get install -y gnome-core kali-defaults kali-root-login desktop-base
```

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/VNC%20server%20downloading.png?raw=true" alt="Setup" height="500" hspace="70">


Choose **lightdm** when prompted as the display manager.

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/lighdm.png?raw=true" alt="Setup" height="500" hspace="70">

---

### **Step 6:** Set up VNC

Run TightVNC for the first time:

```bash
tightvncserver :1 -geometry 1024x768
```

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Geomtry%20command.png?raw=true" alt="Setup" height="500" hspace="70">

It prompts to set a password.

---

### **Step 7:** Verify the VNC server is running

```bash
netstat -tulpn
```

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/netstat%20tolpin.png?raw=true" alt="Setup" height="500" hspace="70">

---

### **Step 8:** Create SSH tunnel for secure GUI access

On your local machine:

```bash
ssh -i kali.pem -L 5901:localhost:5901 -N -f kali@<PUBLIC_IP>
```

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Server%20Running.png?raw=true" alt="Setup" height="500" hspace="70">

---

### **Step 9:** Connect via VNC Viewer

* Open **VNC Viewer** (or any compatible client).
* Connect to `localhost:5901`.
* Enter your VNC password.
  ✅ I now have access to the **Kali Linux GUI** remotely!


<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/VNC%20interface.png?raw=true" alt="Setup" height="500" hspace="70">
<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Linux%20%20GUI.png?raw=true" alt="Setup" height="500" hspace="70">

---

## 🧰 Troubleshooting

### ❌ Permission Denied (public key)

* Check key permissions: `chmod 400 kali.pem`
* Ensure correct username: `kali`
* Security group allows SSH from your IP
* Re-download `.pem` if mismatched with instance
* Removed other users' access

<img src="https://github.com/nabirudd/aws-kali-vm-setup/blob/main/Images/Permision%20Denies%20(Public%20Key).png?raw=true" alt="Setup" height="500" hspace="70">


---

## 🧠 What I Learned

* How to provision and configure EC2 instances on AWS.
* Understanding of SSH key management and file permissions.
* Installing and configuring a desktop environment on a cloud VM.
* Setting up and securing VNC access via SSH tunnels.
* Linux package management and system configuration.
* Best practices for AWS cost control and instance security.

