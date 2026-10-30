# 🖥️ Cybersecurity & Pentesting Lab Setup

**Project 1 | Tools: VirtualBox + Kali Linux + Vulnerable Target VMs**

---

## 📌 Project Overview

This project sets up a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux.

The lab is a controlled, isolated environment where security tools, network scanning, reconnaissance, vulnerability assessment and monitoring can be practiced safely and repeatedly, without putting the host computer or the home network at risk.

The lab runs on a private virtual **NAT Network**, so attacker, target and monitoring machines can talk to each other while staying separated from the real network.

---

## 🎯 Objectives

- Install and configure VirtualBox.
- Import Kali Linux as the attacker machine.
- Create a private **NAT Network** for the lab.
- Give the Kali VM a consistent IP address.
- Add target VMs (Metasploitable 2, Kioptrix 1, devguru, Windows 10) and a monitoring VM (Wazuh).
- Verify connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the whole process for future projects.

---

## 🛡️ Purpose of the Lab

The lab can be used for:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice on intentionally vulnerable machines
- Security monitoring and log analysis with Wazuh

⚠️ **Important:** Use this lab only on systems you own or have explicit permission to test. Never use these tools against unauthorized systems.

---

## 🏗️ Lab Architecture

![VirtualBox Manager showing the lab virtual machines](1-screenshot-title-image.png)

| 🖥️ Virtual Machine | 🎭 Role | 📍 Status when documented |
| --- | --- | --- |
| kali-linux-2025.4-virtualbox-amd64 | Attacker machine | Powered Off (snapshot taken) |
| csec 1 | Practice VM | Powered Off |
| Wazuh v4.14.4 OVA | Security monitoring (SIEM/XDR) | Powered Off |
| devguru | Vulnerable target | Powered Off |
| Metasploitable 2 | Vulnerable target | Powered Off |
| Kioptrix 1 | Vulnerable target | Powered Off |
| windows (Windows 10) | Windows target / test machine | Saved |

All machines are intended to attach to the same NAT Network so they can reach each other.

---

## ⚙️ Lab Configuration

| 🧩 Component | ⚙️ Configuration |
| --- | --- |
| 🖥️ Host OS | Windows 10 _(update if different)_ |
| 🧠 Host RAM | _(fill in)_ |
| ⚡ Processor | _(fill in)_ |
| 🧰 Hypervisor | Oracle VirtualBox _(add version)_ |
| 🐉 Security OS | Kali Linux 2025.4 (VirtualBox amd64 image) |
| 🌐 Virtual Network | NAT Network (`NatNetwork`) |
| 📡 Network Address | 10.0.0.0/24 |
| 🔧 DHCP Server | Enabled |
| 🌐 IPv6 | Disabled |
| 🐧 Kali IP Address | 10.0.0.2/24 (static, added alongside DHCP) |
| 🚪 Default Gateway | 10.0.0.1 |
| 🌍 DNS Servers | 8.8.8.8, 10.0.0.1 |

---

# 🪜 Lab Setup Procedure

## Step 1. Install VirtualBox

VirtualBox was installed on the Windows host as the hypervisor.

---

## Step 2. Create the NAT Network

A dedicated NAT Network was created in **File → Tools → Network Manager → NAT Networks**.

```
Name:        NatNetwork
IPv4 Prefix: 10.0.0.0/24
DHCP:        Enabled
IPv6:        Disabled
```

![VirtualBox NAT Network settings](2-screenshot-network-settings-1.png)

A **NAT Network** was chosen because VMs on the same NAT Network can communicate with each other and still have outbound Internet access.

---

## Step 3. Import Kali Linux

The Kali Linux 2025.4 VirtualBox image was downloaded from the official Kali website and imported into VirtualBox. Its network adapter was attached to the NAT Network:

```
Adapter 1
Attached to: NAT Network
Name:        NatNetwork
```

![Kali Linux desktop running in VirtualBox](3-screenshot-kali-linux.png)

---

## Step 4. Configure the Kali Linux Network

In Kali, the **Wired connection 1** profile was edited (IPv4 Settings tab). The method stayed on **Automatic (DHCP)** and an additional static address was added:

```
Address:  10.0.0.2
Netmask:  24
Gateway:  10.0.0.1
DNS:      8.8.8.8, 10.0.0.1
```

![Kali Linux IPv4 settings](4-screenshot-kali-network-settings.png)

A consistent address makes the Kali machine easy to reference in later exercises.

---

## Step 5. Create a Clean VM Snapshot

After the initial setup, a snapshot named **my fresh kali linux** was taken on the Kali VM (10/25/2026, 11:12 PM).

If a later exercise breaks the VM, it can be restored to this clean baseline.

---

# 🔎 Lab Verification

| ✅ Test | 🧾 Command | 🎯 Expected Result |
| --- | --- | --- |
| Check IP address | `ip a` | 10.0.0.2/24 displayed |
| Test gateway | `ping -c 4 10.0.0.1` | Successful replies |
| Test Internet | `ping -c 4 8.8.8.8` | Successful replies |
| Test DNS | `nslookup example.com` | Domain resolves |
| Verify Nmap | `nmap --version` | Version displayed |
| Test target reachability | `nmap -sn 10.0.0.0/24` | Running lab VMs listed |
| Verify snapshot | Restore snapshot, run `ip a` | Baseline restored |

---

# 🐞 Problems Encountered & Solutions

_Add the real problems you hit here. Two common ones for this setup:_

## Problem 1. No Internet after setting a static IP

Connection names differ between systems, so first find yours:

```
nmcli connection show
```

Then re-check the address, gateway and DNS in the connection profile, restart the connection, and test with `ping 8.8.8.8` and `nslookup example.com`.

## Problem 2. VirtualBox virtualization (VT-x / AMD-V) error

If a VM refuses to start, hardware virtualization may be disabled in BIOS/UEFI. Enable Intel VT-x or AMD-V, save, restart, and start the VM again.

---

# 💡 What I Learned

1. **NAT vs NAT Network.** A NAT Network lets many VMs share one private network and still reach the Internet.
2. **VM networking.** How VirtualBox adapters connect machines and how that affects communication.
3. **Static addressing.** Setting and verifying IPv4 address, netmask, gateway and DNS in Kali.
4. **Snapshots.** Take a clean snapshot before risky experiments.
5. **Documentation.** Recording configuration, screenshots, problems and fixes is part of professional security work.

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for education and authorized testing. Vulnerable VMs such as Metasploitable 2 and Kioptrix 1 must never be exposed to a real network.

---

# 🔗 Tools & Resources

- **VirtualBox:** <https://www.virtualbox.org/wiki/Downloads>
- **Kali Linux:** <https://www.kali.org/get-kali/>
- **Wazuh:** <https://wazuh.com/>
- **Metasploitable 2:** <https://docs.rapid7.com/metasploit/metasploitable-2/>
- **VulnHub (Kioptrix, devguru):** <https://www.vulnhub.com/>

---

# 👤 Author

**Rachael Chukwueke**
Cybersecurity learner, Lagos, Nigeria

LinkedIn: _(add your link)_

---

## 📌 Project Information

**Project:** Cybersecurity & Pentesting Lab Setup
**Repository:** GitHub
