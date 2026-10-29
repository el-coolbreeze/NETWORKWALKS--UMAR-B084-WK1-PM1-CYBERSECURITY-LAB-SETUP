# NETWORKWALKS--UMAR-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP

# Cybersecurity Internship - Lab Environment Setup

## 📌 Project Overview
This repository documents the setup and configuration of a virtualized cybersecurity testing and ethical hacking lab environment. It establishes an isolated, controlled network infrastructure designed to host both attacking and target virtual machines safely for practical security assessments and coursework.

## 🎯 Objectives
* Configure a secure, isolated local hypervisor network environment for penetration testing practice.
* Deploy and configure a Kali Linux virtual machine to serve as the primary attacking/evaluation platform.
* Setup target virtual machines (such as Windows 10 and Android) to simulate real-world network nodes.
* Establish reliable internal routing, shared folders, and host-to-guest integration tools.

## 💡 Purpose of the Lab
The primary purpose of this lab is to provide a dedicated, isolated sandboxed environment to practice ethical hacking, vulnerability assessment, and network security concepts safely without impacting production systems or external networks.

---

## 🛠️ Lab Architecture & Specifications

### Host Machine & Hardware Requirements
* **Base Operating System:** Windows 10 / Host PC
* **Hypervisor:** Oracle VirtualBox (Latest Recommended Version)
* **Recommended Hardware Specs:** 8GB RAM or more, 256GB SSD or greater, Core i3/i5 processor (or equivalent)

### Network Architecture
The virtual lab uses a custom isolated **NAT Network** configuration to enable secure routing and communication between the attacking machine and target virtual machines.
* **Subnet:** `10.0.0.0/24`
* **DHCP Server:** Enabled (IP Range: `10.0.0.2` – `10.0.0.99`)
* **Default Gateway:** `10.0.0.1`

---

## 📋 Lab Setup Procedure

### Phase 1: VirtualBox & Network Configuration
1. Downloaded and installed **7-Zip** and **Oracle VirtualBox** on the host machine.
2. Navigated to `File` > `Tools` > `Network Manager` in VirtualBox.
3. Created a new **NAT Network** named `NatNetwork` with the IPv4 prefix `10.0.0.0/24` and enabled DHCP.

### Phase 2: Attacking Machine Setup (Kali Linux)
1. Downloaded and imported the official **Kali Linux Virtual Machine** template into VirtualBox.
2. **VM Settings & Integration:**
   * **System:** Assigned base memory and verified processor acceleration settings.
   * **Network Adapter 1:** Attached to **NAT Network** (`NatNetwork`), Adapter Type `Intel PRO/1000 MT Desktop`, with Promiscuous Mode set to **Allow All**.
   * **Integration Features:** Enabled bi-directional **Clipboard** and **Drag and Drop** sharing.
   * **Shared Folders:** Configured a machine folder mapping pointing to the host machine's `/downloads` folder with **Full Access** and **Auto-mount** enabled.
3. **Static IP Configuration:**
   * Configured the network interface (`Wired connection 1`) with manual IPv4 settings:
     * **IP Address:** `10.0.0.2`
     * **Netmask:** `24` (`255.255.255.0`)
     * **Gateway:** `10.0.0.1`
     * **DNS Server:** `8.8.8.8`

### Phase 3: Target Virtual Machines Setup

#### 1. Windows 10 Virtual Machine
* **IP Address:** `10.0.0.10`
* **Network Settings:** Attached to **NAT Network** (`NatNetwork`), Adapter Type `Intel PRO/1000 MT Desktop`, with Promiscuous Mode set to **Allow All**.
* **Management:** Maintained baseline snapshots (e.g., Snapshot 1) for lab rollbacks.

#### 2. Android Virtual Machine (Optional Target)
* **IP Address:** `10.0.0.9`
* **Display Settings:** Configured Graphics Controller to `VBoxVGA` and disabled 3D Acceleration (`Disable 3D Acceleration`).
* **Network Details:** Configured static IP settings with IP address `10.0.0.9`, Gateway `10.0.0.1`, Network prefix length `24`, and DNS servers `8.8.8.8` / `10.0.0.1`.

---

## ⚠️ Problems Encountered & Solutions

### Issue: Post-Configuration Internet Inaccessibility
* **Problem Description:** After assigning the static IP address to the Kali Linux virtual machine, internet access was initially unreachable due to a known DAD (Duplicate Address Detection) timeout issue common in VirtualBox v7 and newer Kali Linux builds.
* **Solution Implemented:** 
  1. Executed the network manager terminal commands to disable DAD timeout and restart the connection interface:
     ```bash
     sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
     sudo nmcli connection down "Wired connection 1"
     sudo nmcli connection up "Wired connection 1"
     ```
  2. Additionally, as required, I performed a full restart of both the virtual machine and the host machine to clear adapter states, successfully restoring stable internet connectivity.

---

## 📚 What I Learned
* How to design and configure a custom isolated NAT network topology using Oracle VirtualBox.
* Procedures for managing static IP assignments and gateway routing across mixed operating systems (Linux, Windows, Android).
* Troubleshooting network interface bugs and DAD timeout behaviors in modern Linux network stacks.
* The importance of baseline snapshots for maintaining clean disaster-recovery states in security labs.

---

## 🛡️ Security and Ethical Use Disclaimer
This lab environment is built strictly for educational purposes, authorized security testing, and professional skills development within a controlled sandbox. Unauthorized scanning, testing, or attacking of networks or systems outside of this isolated environment is strictly prohibited and illegal.

---

## 🧰 Tools Used
* **Oracle VirtualBox:** Type-2 Hypervisor used for running virtual machines.
* **Kali Linux:** Linux distribution packed with security and penetration testing tools.
* **Windows 10:** Host operating system and secondary target environment.
* **Android OS:** Mobile virtualization target for testing.
* **7-Zip:** Archive utility used for extracting appliance files.

---

## ✍️ Author
* **Umar Abubakar**
