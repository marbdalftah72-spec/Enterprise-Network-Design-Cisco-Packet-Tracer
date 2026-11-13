# 🌐 Enterprise Campus Network Architecture & Cisco Packet Tracer Simulation

[![Simulator](https://img.shields.io/badge/Simulator-Cisco%20Packet%20Tracer%208.x-005073.svg?logo=cisco&logoColor=white)](https://www.netacad.com/)
[![Cert-Aligned](https://img.shields.io/badge/Curriculum-CCNA%20Enterprise-blue.svg)](#)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A complete enterprise-grade multi-tier campus network infrastructure designed and simulated using **Cisco Packet Tracer**. Authored by **Ammar Abdelfattah** for the **Computer Networks & Data Communications** course at **Faculty of Engineering – New Ismailia National University (NINU)**.

---

## 📌 Network Topology & Hierarchical Design

The architecture strictly follows the **Cisco Three-Tier Hierarchical Model** (Core, Distribution, Access) ensuring high availability, fault tolerance, scalability, and deterministic routing:

```mermaid
flowchart TD
    subgraph CoreLayer["Core Layer (High-Speed Backbone)"]
        Core1["Core Router 1 (Cisco 2911)"] <-->|GigabitEthernet / OSPF Backbone| Core2["Core Router 2 (Cisco 2911)"]
    end

    subgraph DistLayer["Distribution Layer (Policy & Inter-VLAN Routing)"]
        DSwitch1["Distribution Multilayer Switch 1 (3560)"]
        DSwitch2["Distribution Multilayer Switch 2 (3560)"]
    end

    subgraph AccessLayer["Access Layer (Port Security & Endpoint Connectivity)"]
        ASwitch1["Access Switch 1 (2960) - Admin"]
        ASwitch2["Access Switch 2 (2960) - Engineering"]
        ASwitch3["Access Switch 3 (2960) - Labs"]
    end

    Core1 --- DSwitch1
    Core1 --- DSwitch2
    Core2 --- DSwitch1
    Core2 --- DSwitch2

    DSwitch1 --- ASwitch1
    DSwitch1 --- ASwitch2
    DSwitch1 --- ASwitch3
    DSwitch2 --- ASwitch1
    DSwitch2 --- ASwitch2
    DSwitch2 --- ASwitch3
```

---

## ⚙️ Implemented Protocols & Network Services

1. **VLAN Segmentation & 802.1Q Trunking**:
   - **VLAN 10**: Management & Administration (`192.168.10.0/24`).
   - **VLAN 20**: Faculty & Staff (`192.168.20.0/24`).
   - **VLAN 30**: Student & Research Labs (`192.168.30.0/24`).
   - **VLAN 99**: Native & Management Untagged VLAN (`192.168.99.0/24`).
2. **Switching & Redundancy**:
   - Spanning Tree Protocol (**Rapid-PVST+**) preventing broadcast storms and loops while ensuring sub-second failover.
   - Cisco EtherChannel (**LACP - 802.3ad**) link aggregation combining physical links into high-bandwidth logical trunks.
3. **Dynamic Routing**:
   - **OSPFv2 (Open Shortest Path First)** configured across Area 0 (Backbone) with link cost metrics optimized for Gigabit interfaces.
4. **Network Services & Security**:
   - **DHCP Pools**: Centralized IP reservation and default-gateway distribution with DHCP Snooping to block rogue servers.
   - **NAT / PAT**: Network Address Translation / Port Address Translation allowing internal RFC-1918 private subnets to communicate across the ISP link.
   - **Access Control Lists (ACLs)**: Extended IP ACLs isolating student lab traffic from financial and administrative management subnets.
   - **Switch Port Security**: Dynamic MAC address learning with violation modes configured to `restrict` / `shutdown`.

---

## 📁 Repository Structure

```text
├── topology/
│   └── enterprise_campus_network.pkt    # Master Cisco Packet Tracer topology file
├── configs/
│   ├── core_routers.ios                 # Cisco IOS startup-configs for Core layer
│   ├── distribution_switches.ios        # Multilayer routing and SVI configs
│   └── access_switches.ios              # Port security, VLAN, and trunking scripts
├── documentation/
│   └── ip_addressing_scheme.pdf         # VLSM sub-netting allocation matrix
└── README.md
```

---

## 👨‍💻 Author

- **Ammar Abdelfattah**
- Faculty of Engineering, **New Ismailia National University (NINU)**
