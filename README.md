# Multi-Node Proxmox Security & Infrastructure Lab (Nov 2025)

This repository documents my comprehensive homelab, built on a 2-node Proxmox VE cluster. This project serves as a practical sandbox for learning and implementing enterprise-grade virtualization, advanced network security, and modern infrastructure management.

It features a complete "defense-in-depth" security posture, integrating a SIEM (Wazuh) with an IDS (Suricata) and an NGFW (OPNSense/Zenarmor). The environment also virtualizes core services like Active Directory, network-attached storage, and secure remote access.

## Proxmox Dashboard
<img width="1440" height="813" alt="image" src="https://github.com/user-attachments/assets/4fec4684-35c9-4378-a58e-4b3e84701aa9" />

## 🚀 Project Objectives

* **Architect** a redundant and scalable virtualization platform using Proxmox VE.
* **Implement** a multi-layered security model (Zero Trust, IDS/IPS, NGFW).
* **Deploy & Manage** a complete SIEM solution (Wazuh) for centralized logging, threat detection, and response.
* **Virtualize** core network services including Active Directory, DNS filtering, and file storage.
* **Test** high-performance Virtual Desktop Infrastructure (VDI) capabilities with GPU passthrough.

---

## 🏛️ Core Infrastructure & Architecture

The foundation of the lab is a 2-node Proxmox cluster, which hosts all critical services and test environments.

* **Virtualization Platform:** 2-Node Proxmox VE Cluster ("pve" & "pve2") providing high availability and resource balancing.
* **Storage:** **TrueNAS Core** virtualized and deployed to provide centralized, redundant SMB/NFS storage for the cluster, VMs, and user data.
* **Directory Services:** **Windows Server (WIN-AD)** running Active Directory Domain Services for centralized user authentication and policy management across the lab.
* **Network-Wide DNS:** **AdGuard Home** serving as the primary DNS resolver for all networks, providing blocking of ads, trackers, and malicious domains.
* **Testing & Analysis VMs:** Various instances of **Kali Linux** and **Ubuntu** for security testing, network analysis, and general utility.

---

## 🛡️ Security & Network Stack

The security of this lab is built on an integrated, "defense-in-depth" model that provides comprehensive visibility and control, mimicking a professional Security Operations Center (SOC) setup.

### 1. Perimeter & Network Security (NGFW/IDS)
* **Firewall / Router:** **OPNSense** serves as the primary gateway, managing all routing, VLANs, and firewall rules for the network.
* **Next-Gen Firewall (NGFW):** **Zenarmor** (run as a plugin on OPNSense) provides Layer 7 application control, web filtering, and advanced threat intelligence.
* **Intrusion Detection (IDS):** **Suricata** is integrated directly with OPNSense, actively monitoring all network traffic for malicious signatures, anomalies, and potential intrusion attempts.

### 2. SIEM & Endpoint Security (Wazuh)
* **SIEM/XDR:** A dedicated **Wazuh** server is deployed to aggregate, correlate, and analyze logs from all components in the lab.
* **Log Ingestion:** Wazuh is configured to ingest logs directly from OPNSense and Suricata, providing a single pane of glass for network-level threats.
* **Endpoint Protection (HIDS):** Wazuh agents are deployed on all critical VMs and endpoints, including:
    * Windows AD Server
    * Windows 11 VDI
    * TrueNAS Core
    * Ubuntu/Kali VMs
* This provides host-based intrusion detection, file integrity monitoring, vulnerability detection, and automated incident response.

### 3. Secure Remote Access
* **Zero-Trust Network:** A **Tailscale** mesh network is established for secure, point-to-point remote access. This provides encrypted connectivity to the entire lab infrastructure (including Proxmox nodes, OPNSense, and internal VMs) without exposing any ports to the public internet.

---

## ✨ Key Feature: High-Performance VDI with GPU Passthrough

A key highlight of this project is the successful implementation of PCI-Passthrough for a high-performance VDI (Virtual Desktop Infrastructure) instance.

* **Hardware:** An **NVIDIA GeForce RTX 3050** is passed directly from the Proxmox host to a guest VM.
* **Guest VM:** A **Windows 11 Pro** virtual machine, fully domain-joined to the AD environment.
* **Outcome:** This setup enables a true high-performance virtual desktop experience, capable of running graphics-intensive applications, video processing, and modern gaming, all while being centrally managed and secured within the lab.

---

## 📸 Dashboard Showcase

The composite screenshot below provides a "day-in-the-life" overview of the entire stack in operation.

*(**Note:** You've got a great composite image. I'd also recommend uploading each of these screenshots separately and embedding them here under relevant sub-headings for a clearer, more detailed view.)*

* **Proxmox:** Cluster-wide management.
* **OPNSense:** Core network routing and firewalling.
* **Zenarmor:** NGFW blocking threats.
* **TrueNAS:** Storage pool management.
* **AdGuard:** DNS query filtering.
* **Wazuh:** Security event correlation and agent status.
* **Tailscale:** Zero-trust device connectivity.
* **Windows 11 VDI:** Task Manager confirming the successful passthrough of the RTX 3050.

![Composite screenshot of the Proxmox Lab dashboards](image_46e41c.jpg)

---

## 💻 Technologies Used

* **Hypervisor:** Proxmox VE
* **Firewall/Router:** OPNSense
* **NGFW:** Zenarmor
* **IDS/IPS:** Suricata
* **SIEM/XDR:** Wazuh
* **Storage:** TrueNAS Core
* **DNS Filtering:** AdGuard Home
* **Directory:** Windows Active Directory
* **Zero-Trust Access:** Tailscale
* **Operating Systems:** Windows 11, Windows Server, Ubuntu, Kali Linux
* **Hardware:** NVIDIA RTX 3050 (for Passthrough)
