# Full Emulation of Enterprise Network & Security Infrastructure

This repository contains my Bachelor graduation project from **Al-Azhar University – Computer & Systems Engineering**.

The goal of the project is to **design and fully emulate an enterprise-grade network and security infrastructure** for a fictional bank (CIB) with multiple branches and a data center, interconnected through a service provider MPLS backbone.

The whole setup is implemented using **EVE-NG** and **VMware Workstation**, with Cisco routers/switches and a modern data center design (spine–leaf).

---

## 🧩 Project Overview

We emulate a realistic enterprise environment with:

- **CIB Headquarters (Cairo)**
- **CIB Branch (Alexandria)**
- **Data Center**
- **Service Provider Core (MPLS ISP)**

Key design goals:

- High availability (HSRP, redundant links & devices)
- Segmentation & L2 security (VLANs, MST, Rapid-PVST, Port Security)
- Dynamic routing & fast convergence (OSPF)
- WAN virtualization using MPLS VPN (VRFs, VPNv4, MP-BGP)
- Modern data center fabric (spine–leaf)
- Secure access to services (HTTPS)

The main documentation is in:

- `full emulation to network and security.pdf` – written report  
- `Graduation project presentation.pptx` – main presentation  
- `Service provider documentation .docx` & `Service privider presentation.pptx` – SP/MPLS details  

---

## 🏗️ High-Level Architecture

### 🏢 Enterprise Sites

**Headquarters & Branch** are built with a classic hierarchical design:

- **Access Layer**
  - VLANs per department
  - Port Security
  - MST (Multiple Spanning Tree)
  - BPDU Guard
  - VTP for VLAN distribution

- **Distribution/Aggregation Layer**
  - OSPF for intra-site routing
  - HSRP for default-gateway redundancy
  - Extension of MST & VTP where needed

### 🗄️ Data Center

The data center hosts servers and banking services and is built on a **spine–leaf** architecture to:

- Reduce latency and hop count
- Provide predictable east–west traffic paths
- Improve scalability and redundancy

Services include:

- Application servers
- HTTPS-secured access to web services

### 🌐 Service Provider (MPLS Core)

The SP network connects all branches using:

- **MPLS + VRF / VPNv4**
  - Separation of customer routes
  - Route Distinguisher (RD) & Route Target (RT)
- **MP-BGP**
  - Exchange of VPNv4 routes and labels between PE routers
- **OSPF**
  - IGP inside the provider core
- **Route Reflectors**
  - Reduce BGP session count and improve scalability

Example configs for two PE routers:

- `PE1_Ales.txt`
- `PE1_Aswan.txt`

---

## 📂 Repository Structure

```text
Bachelor-Graduation-Project-/
├── CIB Head qurter/              # Topology/configs for HQ (access, aggregation, HSRP, MST, VTP...)
├── CIB branch/                   # Topology/configs for branch site
├── CIB data center/              # Data center devices and connections
├── Data center 1/                # Additional DC topology/configs
├── Topology/                     # Overall network topology diagrams / EVE-NG files
├── PE1_Ales.txt                  # PE router config for Alexandria site
├── PE1_Aswan.txt                 # PE router config for Aswan/remote site
├── Graduation project presentation.pptx
├── Service provider documentation .docx
├── Service privider presentation.pptx
└── full emulation to network and security.pdf
