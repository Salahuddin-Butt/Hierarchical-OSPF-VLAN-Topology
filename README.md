# Enterprise Network Topology Design

## 📌 Project Overview
This project simulates a medium-to-large scale enterprise network using the **Cisco Hierarchical Network Model** (Core, Distribution, and Access layers).

The design connects multiple branch offices and user groups using **OSPF** for dynamic routing and **Inter-VLAN routing** on Multilayer Switches. It includes robust security measures like **Port Security**, **BPDU Guard**, and **Extended ACLs** to segment traffic between departments.

## 🏗️ Topology Architecture
* **Core Layer:** 3x Cisco 2811 Routers interconnecting via Serial WAN links (/30 subnets).
* **Distribution Layer:** 2x Cisco 3560 Multilayer Switches acting as gateways for VLANs.
* **Access Layer:** 9x Cisco 2960 Switches providing connectivity to end devices.
* **End Devices:** Dedicated Servers, PCs, and Printers assigned to specific subnets.

## ⚙️ Key Features & Configurations
### 1. VLAN & Subnetting
* Implemented **9 distinct VLANs** (IDs 10–90) using **CIDR /22** subnetting for scalability (1022 hosts per VLAN).
* **VLAN 90** acts as a remote branch, separated by the Core WAN.

### 2. Routing Protocols
* **OSPF (Open Shortest Path First):** Configured in **Area 0** on all Routers and Multilayer Switches for full connectivity.
* **Inter-VLAN Routing:** Enabled on Multilayer Switches using SVIs (Switch Virtual Interfaces).

### 3. Network Services
* **DHCP:** Multilayer Switches configured as DHCP servers to automatically assign IPs to all user VLANs.
* **Static Addressing:** Servers and WAN links use static IP assignment for stability.

### 4. Security & Hardening
* **Extended ACLs:** Applied to enforce strict traffic rules:
    * *Group A (VLAN 10-40)*: Can only communicate within their group and to servers.
    * *Group B (VLAN 50-60)*: Isolated from other groups.
    * *Group C (VLAN 70-80)*: Isolated from other groups.
    * *VLAN 90*: Restricted from initiating connections to other VLANs.
* **Port Security:** Enabled on access ports (Max 1 MAC, Sticky learning, Violation Shutdown).
* **BPDU Guard & PortFast:** Enabled to prevent loops and rogue switch attacks.
* **Device Hardening:** `enable secret`, encrypted passwords, and secured VTY/Console lines.

## 🔧 Technologies Used
* Cisco Packet Tracer
* OSPFv2
* VLANs (802.1Q)
* Access Control Lists (ACLs)
* DHCP / DNS
* Switching Security (PortSec, BPDU Guard)

## 🚀 How to Run
1.  Download the `.pkt` file from this repository.
2.  Open it with **Cisco Packet Tracer** (Version 8.0 or newer recommended).
3.  Let the network converge (wait for OSPF neighbors to form).
4.  Test connectivity by pinging from **PC0 (VLAN 10)** to **Server 0**.
