# NETWORKWALKS--UMAR-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP

# Cybersecurity Internship - Lab Environment Setup

This repository documents the setup and configuration of my virtualized cybersecurity testing and ethical hacking lab environment.

---

## 🛠️ Lab Architecture & Specifications

### Host Machine & Hardware Requirements
* **Base Operating System:** Windows 10 / Host PC.
* **Hypervisor:** Oracle VirtualBox (Latest Recommended Version).
* **Recommended Hardware Specs:** 8GB RAM or more, 256GB SSD or greater, Core i3/i5 processor (or equivalent).

### Network Architecture
The virtual lab uses a custom isolated **NAT Network** configuration to enable secure routing and communication between the attacking machine and target virtual machines.
* **Subnet:** `10.0.0.0/24`.
* **DHCP Server:** Enabled (IP Range: `10.0.0.2` – `10.0.0.99`).
* **Default Gateway:** `10.0.0.1`.

---

## 📋 Step-by-Step Implementation Guide

### Phase 1: VirtualBox & Network Configuration
1. **Prerequisites & Tools:** Downloaded and installed **7-Zip** and **Oracle VirtualBox** on the host machine.
2. **NAT Network Setup:** 
   * Navigated to `File` > `Tools` > `Network Manager` in VirtualBox.
   * Created a new **NAT Network** named `NatNetwork` with the IPv4 prefix `10.0.0.0/24` and enabled DHCP.

### Phase 2: Attacking Machine Setup (Kali Linux)
1. **Appliance Import:** Downloaded and imported the official **Kali Linux Virtual Machine** template into VirtualBox.
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
* **IP Address:** `10.0.0.10`.
* **Network Settings:** Attached to **NAT Network** (`NatNetwork`), Adapter Type `Intel PRO/1000 MT Desktop`, with Promiscuous Mode set to **Allow All**.
* **Management:** Maintained baseline snapshots (e.g., Snapshot 1) for lab rollbacks.

#### 2. Android Virtual Machine (Optional Target)
* **IP Address:** `10.0.0.9`.
* **Display Settings:** Configured Graphics Controller to `VBoxVGA` and disabled 3D Acceleration (`Disable 3D Acceleration`).
* **Network Details:** Configured static IP settings with IP address `10.0.0.9`, Gateway `10.0.0.1`, Network prefix length `24`, and DNS servers `8.8.8.8` / `10.0.0.1`.

---
