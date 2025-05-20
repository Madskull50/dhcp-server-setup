# dhcp-server-setup
dhcp-server-setup/
│
├── README.md
├── docs/
│   └── dhcp-setup-guide.md
├── screenshots/
│   └── [optional: UI step images here]

# 🖥️ DHCP Server Setup on Windows Server

This project documents the step-by-step process for setting up a DHCP (Dynamic Host Configuration Protocol) Server using **Windows Server**. It includes complete instructions, configuration screenshots (optional), and troubleshooting tips. Ideal for labs, homelabs, or learning IT infrastructure basics.

---

## ✅ Features

- Install the DHCP role on Windows Server
- Configure DHCP scope (IP range, lease time, etc.)
- Set default gateway and DNS via DHCP options
- Authorize DHCP server in Active Directory
- Test client IP lease from DHCP
- Troubleshooting and DHCP reservation setup

---

## 📋 Prerequisites

- A Windows Server VM or physical machine (2016 or later)
- Static IP address configured
- Administrative privileges
- (Optional) Joined to a domain (for DHCP authorization)

---

## 🔧 Basic Setup Steps

1. Install the DHCP Server Role
2. Authorize the DHCP server (if on a domain)
3. Create and configure a DHCP scope
4. Set gateway and DNS options
5. Activate the scope
6. Test client IP address assignment

---

## 🧪 Testing the DHCP Server

On a client machine:
```cmd
ipconfig /release
ipconfig /renew
ipconfig


---

## 📄 `docs/dhcp-setup-guide.md`

```markdown
# 🖧 Step-by-Step DHCP Server Setup (Windows Server)

This guide explains how to install and configure a DHCP server on a Windows Server system.

---

## 🧰 Prerequisites

- Windows Server installed (2016/2019/2022)
- Static IP assigned (e.g., 192.168.1.10)
- Server Manager access
- Local admin rights
- (Recommended) Domain-joined for DHCP authorization

---

## 🔧 Step 1: Install DHCP Server Role

1. Open **Server Manager**
2. Click **Manage > Add Roles and Features**
3. Choose **Role-based or feature-based installation**
4. Select your server
5. In **Server Roles**, check: ✅ **DHCP Server**
6. Click **Next** through all prompts, then click **Install**
7. Click **Complete DHCP configuration** after install
8. Use domain admin credentials to **authorize the DHCP server**

---

## 🔐 Step 2: Authorize DHCP Server

- If joined to a domain:
  - Go to **DHCP console > Right-click server name > Authorize**

Authorization prevents unauthorized DHCP servers from handing out IPs on the network.

---

## 🌐 Step 3: Create and Configure Scope

1. In the DHCP console:
   - Right-click **IPv4 > New Scope**
2. Name: `Office LAN`
3. Define IP Range:
   - Start: `192.168.1.100`
   - End: `192.168.1.200`
4. Subnet Mask: `255.255.255.0`
5. Add Exclusions (optional): e.g., `192.168.1.150`
6. Lease Duration: default 8 days
7. Configure Scope Options:
   - Router: `192.168.1.1`
   - DNS Server: `192.168.1.10` or `8.8.8.8`
8. Finish and **Activate** the scope

---

## 🔄 Step 4: Restart DHCP Service

```powershell
Restart-Service dhcpserver
