---
layout: post
title: "High-Availability OLVM 4.5 Deployment for Victoria Commercial Bank's Core Database"
subtitle: "Architecting a Hybrid Cloud-Ready Infrastructure Solution for Financial Workloads"
author: Bradley Otieno
categories: [Infrastructure, Virtualization, HA/DR, Storage]
tags: [OLVM, KVM, Oracle Database, Huawei Dorado, Fibre Channel, High Availability, RHEL]
---
## 1. Project Overview & Business Mandate

This project involved designing and implementing a **High-Availability (HA)** and **Disaster Recovery (DR)** enterprise virtualization platform using **Oracle Linux Virtualization Manager (OLVM) 4.5** to host the mission-critical **Oracle Database 19c** environment. The primary goal was to achieve **99.99%+ uptime** and guarantee near-zero data loss (low RPO) for core banking operations.

**Role:** Infrastructure Engineer / Virtualization Specialist

---

## 2. Solved: The Invisible Problems (Value Proposition)

This architecture was engineered to address common challenges in enterprise database hosting:

### Problem A: Ensuring Uninterrupted Management (High Availability)
* **Challenge:** The management component (**OLVM Engine**) is a single point of failure (SPOF).
* **Solution:** Deployment of a **Self-Hosted Engine (SHE)** configuration across two physical hosts. This ensures the engine VM automatically fails over if a host fails, guaranteeing **continuous orchestration and management** capabilities.

### Problem B: Achieving Database Performance and Low Latency
* **Challenge:** Financial database I/O demands require high throughput and extremely low latency.
* **Solution:** We bypassed standard hypervisor file storage and implemented dedicated **Direct LUNs** mapped via **32Gb Fibre Channel (FC)** to the KVM guests. This was backed by **Huawei Dorado 5000 V6 All-Flash NVMe SAN** storage.
    * *Result:* Guaranteed sub-millisecond I/O response times for Oracle Automatic Storage Management (ASM).

### Problem C: Operational Resilience and Backup
* **Challenge:** How to guarantee the quick recovery of the entire virtualization management plane.
* **Solution:** Implementation of an **automated `ovirt-engine-backup.sh`** procedure scheduled via **Crontab**. This ensures daily, consistent backups of the OLVM metadata and configuration database, simplifying future maintenance and recovery.

---

## 3. Engineered Context: The Technical Architecture

This section uses market keywords to showcase compliance and systems thinking.

### Technology Stack
* **Virtualization Platform:** Oracle Linux Virtualization Manager (OLVM) 4.5
* **Hypervisor:** Oracle Linux 8.x with KVM
* **Compute:** Huawei FusionServer RH2288 V3 / Lenovo ThinkSystem SR650
* **Storage:** Huawei Dorado 5000 V6 All-Flash NVMe SAN via Brocade G610S FC Switches
* **Workload:** Oracle Database 19c (RAC or Single Instance) running on RHEL/Oracle Linux VMs

### Key Architectural Decisions

1.  **Storage Access:** Used **Direct LUNs** for the Oracle VMs instead of VDSM storage domains to maximize I/O performance and stability for ASM.
2.  **Host Zoning:** The **Brocade G610S FC Switches** were zoned to ensure hosts had **redundant paths** to both Production and DR storage arrays, eliminating a fabric-level SPOF.
3.  **Tuning:** Configured **HugePages** and specific **kernel parameters** on the Oracle VMs to optimize the performance of the System Global Area (SGA).

---

## 4. Visualizing the Solution (GitHub + Diagram)

This project focused heavily on redundancy and performance. The primary site architecture illustrates the **Self-Hosted Engine (SHE)** configuration across dual KVM hosts and the redundant 32Gb Fibre Channel (FC) connectivity to the All-Flash SAN.

!
/assets/img/VCB_Primary_Site.png

---
### Key Virtualization Components

The **OLVM Engine** (running the **ovirt-engine** service) acts as the central control plane, managing the life cycle and high availability of the KVM Hosts via the **VDSM** service.

!
/assets/img/Virtualization_Components.png

---

## 5. Operational Proof (The 2-min Walkthrough)

**(Note: This is where you will add your Loom video link.)**

A quick video demonstration of key operational commands and the proof of High Availability:

[Link to your Loom video] - *Example demo: Verifying the SHE status and host roles.*
