Here is the complete `README.md` for your GitHub repository, based *only* on your Excel file and without any team or instructor details. I have matched the structure, tables, and data exactly as they appear in your network documentation.

```markdown
# 🌐 SZABIST Multi-Campus Enterprise Network

<div align="center">

**Complete Enterprise Network Simulation | Computer Networks & Data Communications**

[![Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?logo=cisco)](https://www.netacad.com/)
[![OSPF](https://img.shields.io/badge/Routing-OSPF-green)](#)
[![VLAN](https://img.shields.io/badge/Segmentation-VLAN-blue)](#)

A full-scale, multi-campus enterprise network simulation featuring inter-VLAN routing, dynamic OSPF routing, DHCP services, NAT/PAT for internet access, and comprehensive ACL-based security.

</div>

---

## 📌 Project Overview

This project simulates the complete network infrastructure for a multi-campus university environment. The design connects **6 distinct campuses** through a centralized hub-and-spoke topology using a core `EDGE-99` router. The network is built with:
- **VLAN Segmentation** with 802.1Q Trunking
- **Router-on-a-Stick** for Inter-VLAN routing
- **OSPF (Area 0)** for dynamic routing between campuses
- **DHCP** for dynamic IP allocation per VLAN
- **NAT/PAT** for internet access via a single public IP
- **ACLs** for strict access control to printers and servers
- **Port Security** on lab switches

---

## 🗺️ Network Topology

The `EDGE-99` router at the main campus acts as the hub, connecting to all other campus routers via Ethernet and Serial WAN links. The ISP provides internet connectivity through a dedicated serial link.

```text
                            🌐 ISP  (11.11.11.2)
                              |
                        ┌──[EDGE-99]──┐   (11.11.11.1)
                        │  Main Hub   │
          ┌─────────────┼─────┬───────┼──────────┐
          │             │     │       │           │
       [R-100]       [R-154] [R-153] [R-79]   [R-MEDIA]
      Campus 100    Campus 154  Campus 153  Campus 79  Media Villa
      (13 VLANs)   (5 VLANs)  (3 VLANs)  (6 VLANs)  (3 VLANs)
       Ethernet      Ethernet    Serial     Serial      Serial
```

- **Topology:** Hub-and-Spoke
- **Routing Protocol:** OSPF (Single Area 0)
- **Internet Access:** PAT via EDGE-99

---

## 🏫 Campus Breakdown

| Campus | Router | VLANs | Key Departments | Link Type |
| :--- | :--- | :---: | :--- | :--- |
| **Campus 99 (Main)** | EDGE-99 | 7 | Classrooms, Faculty, IT, Exam, Admin, Data Center | Hub |
| **Campus 100 (Labs)** | R-100 | 13 | CS, AI, Lab3-6, Smart, Gaming, Faculty, Admin, IT | Gigabit Ethernet |
| **Campus 154** | R-154 | 5 | Classrooms, Faculty, Academic, Admin, Mechatronics | Gigabit Ethernet |
| **Campus 153** | R-153 | 3 | Classrooms, Admissions, Academic | Serial |
| **Campus 79 (Admin)** | R-79 | 6 | HR, Finance, Procurement, Admin, Library, EDC | Serial |
| **Media Villa** | R-MEDIA | 3 | Classrooms, Faculty, Academic | Serial |

---

## 🔗 WAN Links (Router Interconnects)

All inter-router connections use `/30` subnets for efficient point-to-point links.

| Connection | Subnet | EDGE-99 IP | Remote Router IP | Medium |
| :--- | :--- | :--- | :--- | :--- |
| EDGE-99 ↔ ISP | `11.11.11.0/30` | `11.11.11.1` (Se0/1/0) | `11.11.11.2` | Serial DCE |
| EDGE-99 ↔ R-100 | `23.12.145.108/30` | `23.12.145.109` (Gi0/1) | `23.12.145.110` (Gi0/0) | Ethernet |
| EDGE-99 ↔ R-154 | `23.12.145.112/30` | `23.12.145.113` (Gi0/2) | `23.12.145.114` (Gi0/0) | Ethernet |
| EDGE-99 ↔ R-153 | `23.12.145.116/30` | `23.12.145.117` (Se0/0/0) | `23.12.145.118` (Se0/0/0) | Serial DCE |
| EDGE-99 ↔ R-79 | `23.12.145.120/30` | `23.12.145.121` (Se0/0/1) | `23.12.145.122` (Se0/0/0) | Serial DCE |
| EDGE-99 ↔ R-MEDIA | `23.12.145.124/30` | `23.12.145.125` (Se0/1/1) | `23.12.145.126` (Se0/1/0) | Serial DCE |

---

## 🗄️ IP Address Plan

| IP Block | Assignment | Available IPs |
| :--- | :--- | :---: |
| `23.12.145.0/24` | Campus 99 VLANs + All WAN Links | 254 |
| `23.12.151.0/24` | Campus 100 (CS, AI, Lab3, Lab4) | 254 |
| `192.168.1.0/24` | Campus 100 (Lab5, Lab6, Smart Labs) | 254 |
| `192.168.2.0/24` | Campus 100 (Departments) | 254 |
| `192.168.3.0/24` | Campus 153 | 254 |
| `192.168.4.0/24` | Campus 79 | 254 |
| `192.168.5.0/24` | Media Villa | 254 |
| `11.11.11.0/30` | ISP WAN Link (Public) | 2 |

---

## 📋 VLAN & DHCP Configuration

<details>
<summary><b>Campus 99 (EDGE-99) — 7 VLANs</b></summary>

| VLAN | Name | Network | Gateway | DHCP Range |
| :--- | :--- | :--- | :--- | :--- |
| 140 | CLASSROOMS-99 | `23.12.145.0/29` | `23.12.145.1` | `.2 - .6` |
| 150 | FACULTY-99 | `23.12.145.48/28` | `23.12.145.49` | `.50 - .62` |
| 160 | ACADEMIC-99 | `23.12.145.16/30` | `23.12.145.17` | `.18` |
| 170 | IT-99 | `23.12.145.20/30` | `23.12.145.21` | `.22` |
| 180 | EXAMINATION | `23.12.145.24/29` | `23.12.145.25` | `.26 - .30` |
| 190 | ADMIN-99 | `23.12.145.32/29` | `23.12.145.33` | `.34 - .38` |
| 200 | DATACENTER | `23.12.145.40/29` | `23.12.145.41` | Static Only |

**Static Devices (Servers & Printers):**
- Web-Server: `23.12.145.42`
- ZABDESK-Server: `23.12.145.43`
- Email-Server: `23.12.145.44`
- CMS-Server: `23.12.145.45`
- Printer-Faculty: `23.12.145.50`
</details>

<details>
<summary><b>Campus 100 (R-100) — 13 VLANs</b></summary>

| VLAN | Name | Network | Gateway |
| :--- | :--- | :--- | :--- |
| 10 | CS-LAB | `23.12.151.0/26` | `23.12.151.1` |
| 20 | AI-LAB | `23.12.151.64/26` | `23.12.151.65` |
| 30 | LAB3 | `23.12.151.128/26` | `23.12.151.129` |
| 40 | LAB4 | `23.12.151.192/26` | `23.12.151.193` |
| 50 | LAB5 | `192.168.1.0/26` | `192.168.1.1` |
| 60 | LAB6 | `192.168.1.64/26` | `192.168.1.65` |
| 70 | SMART-LAB 1+2+3 | `192.168.1.192/26` | `192.168.1.193` |
| 80 | GAMING-LAB | `192.168.2.64/28` | `192.168.2.65` |
| 90 | CLASSROOMS-100 | `192.168.2.128/28` | `192.168.2.129` |
| 100 | FACULTY-100 | `192.168.2.96/27` | `192.168.2.97` |
| 110 | ACADEMIC-100 | `192.168.2.144/28` | `192.168.2.145` |
| 120 | ADMIN-100 | `192.168.2.160/29` | `192.168.2.161` |
| 130 | IT-DEPT | `192.168.2.184/29` | `192.168.2.185` |
</details>

<details>
<summary><b>Campus 154 (R-154) — 5 VLANs</b></summary>

| VLAN | Name | Network | Gateway |
| :--- | :--- | :--- | :--- |
| 210 | CLASSROOMS-154 | `23.12.145.128/28` | `23.12.145.129` |
| 220 | FACULTY-154 | `23.12.145.64/27` | `23.12.145.65` |
| 230 | ACADEMIC-154 | `23.12.145.144/29` | `23.12.145.145` |
| 240 | ADMIN-154 | `23.12.145.152/29` | `23.12.145.153` |
| 250 | MECHATRONICS | `23.12.145.160/27` | `23.12.145.161` |
</details>

<details>
<summary><b>Campus 153 (R-153) — 3 VLANs</b></summary>

| VLAN | Name | Network | Gateway |
| :--- | :--- | :--- | :--- |
| 260 | CLASSROOMS-153 | `192.168.3.16/28` | `192.168.3.17` |
| 270 | ADMISSIONS | `192.168.3.0/28` | `192.168.3.1` |
| 280 | ACADEMIC-153 | `192.168.3.32/29` | `192.168.3.33` |
</details>

<details>
<summary><b>Campus 79 (R-79) — 6 VLANs</b></summary>

| VLAN | Name | Network | Gateway |
| :--- | :--- | :--- | :--- |
| 310 | LIBRARY-79 | `192.168.4.0/28` | `192.168.4.1` |
| 320 | HR-79 | `192.168.4.16/28` | `192.168.4.17` |
| 330 | PROCUREMENT-79 | `192.168.4.32/28` | `192.168.4.33` |
| 340 | ADMIN-79 | `192.168.4.48/28` | `192.168.4.49` |
| 350 | FINANCE-79 | `192.168.4.64/28` | `192.168.4.65` |
| 360 | EDC-79 | `192.168.4.80/28` | `192.168.4.81` |
</details>

<details>
<summary><b>Media Villa (R-MEDIA) — 3 VLANs</b></summary>

| VLAN | Name | Network | Gateway |
| :--- | :--- | :--- | :--- |
| 380 | CLASSROOMS-MEDIA | `192.168.5.0/29` | `192.168.5.1` |
| 390 | FACULTY-MEDIA | `192.168.5.16/28` | `192.168.5.17` |
| 400 | ACADEMIC-MEDIA | `192.168.5.32/29` | `192.168.5.33` |
</details>

---

## 🔒 Security Configuration

### ACL Rules (Applied on EDGE-99 G0/0.200 Outbound)

The Access Control List (ACL) strictly controls access to critical resources:

- **Faculty Printers:** Only traffic from **Faculty VLANs** across all campuses is permitted. All other sources are denied.
- **ZABDESK Server:** Only traffic from **Student Labs** (CS, AI, Lab3-6, Smart, Gaming) and **Faculty-99** is permitted. All others are blocked.

| Rule | Action | Source | Destination | Purpose |
| :---: | :---: | :--- | :--- | :--- |
| 1-4 | PERMIT | Faculty VLANs (all campuses) | `Printer-FAC-99` | Faculty printing |
| 5 | **DENY** | ANY | `Printer-FAC-99` | Block non-faculty |
| 13-21 | PERMIT | Lab VLANs + Faculty-99 | `ZABDESK-Server` | Lab access to server |
| 22 | **DENY** | ANY | `ZABDESK-Server` | Block others |
| 23 | PERMIT | ANY | ANY | Allow all other traffic |

### Port Security

Port security is enabled on all lab and server switches to prevent MAC flooding and unauthorized device connections.

| Switch | Port Range | Max MAC | Violation | Campus |
| :--- | :--- | :---: | :--- | :--- |
| SW-CS, SW-AI, SW-LAB3-6 | `Fa0/2-10` | 1 | Shutdown | 100 |
| SW-SMART, SW-GAME | `Fa0/2-9` | 1 | Shutdown | 100 |
| SW-DC (Servers) | `Fa0/2-5` | 1 | Shutdown | 99 |
| SW-154-MECH | `Fa0/2-4` | 1 | Shutdown | 154 |

---

## 🔄 Routing & NAT

### OSPF Configuration (Single Area 0)

All routers run OSPF Process 1 in Area 0. `EDGE-99` serves as the DR/BDR, aggregating routes from all connected campuses.

| Router | Advertised Networks |
| :--- | :--- |
| **EDGE-99** | `23.12.145.0/24`, `23.12.151.0/24`, `192.168.x.x`, `11.11.11.0/30` |
| **R-100** | `23.12.145.108/30`, `23.12.151.0/24`, `192.168.1.0/24`, `192.168.2.0/24` |
| **R-154** | `23.12.145.112/30`, `23.12.145.128/28`, `23.12.145.64/27` |
| **R-153** | `23.12.145.116/30`, `192.168.3.0/24` |
| **R-79** | `23.12.145.120/30`, `192.168.4.0/24` |
| **R-MEDIA** | `23.12.145.124/30`, `192.168.5.0/24` |

### NAT / PAT (Internet Access)

- **Type:** PAT (Port Address Translation / Overload)
- **Public IP:** `11.11.11.1` (EDGE-99 Se0/1/0)
- **Default Route:** `0.0.0.0/0` via `11.11.11.2` (ISP)
- **Inside Networks:** All private campus IPs (ACL 1 permit any)

---

## 🧪 Testing & Validation

| Test | Result |
| :--- | :---: |
| Same-VLAN Ping (PC to PC within lab) | ✅ Pass |
| Inter-VLAN Ping (PC to server in another VLAN) | ✅ Pass |
| Cross-Campus Ping (Campus 100 to Campus 79) | ✅ Pass |
| ISP Reachability (Ping `11.11.11.2`) | ✅ Pass |
| Internet Connectivity (Ping `8.8.8.8` via NAT) | ✅ Pass |

---

## ⚙️ Implemented Concepts

- **VLAN + 802.1Q Trunking:** Department-level isolation across 6 campuses.
- **Router-on-a-Stick:** Sub-interfaces on each router for inter-VLAN routing.
- **DHCP:** Per-VLAN dynamic IP pools on each campus router.
- **Static IPs:** Fixed addresses for all servers, printers, and core switches.
- **VLSM:** Subnets sized per department to minimize IP waste.
- **OSPF Area 0:** Dynamic routing between all campus routers.
- **NAT/PAT:** Single public IP for full campus internet access.
- **ACLs:** Restrict printer and server access by source network.
- **Port Security:** MAC-based port lockdown on lab and server switches.
- **Telnet:** Remote management configured on all routers and core switches.

---

## 📁 Project File

| File | Description |
| :--- | :--- |
| `CNDC_PROJECT_FINAL_ALL_CAMPUSES.pkt` | Complete Cisco Packet Tracer simulation with all 6 campuses configured |

> **⚠️ Note:** Requires **Cisco Packet Tracer 8.x** or later to open and run the simulation.

---

<div align="center">
  <sub>Built with Cisco Packet Tracer | Enterprise Network Design Project</sub>
</div>
```
