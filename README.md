<div align="center">

# 🌐 Multi-Campus Enterprise Network
### Computer Networks & Data Communications — SZABIST Karachi

![Cisco](https://img.shields.io/badge/Cisco%20Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Campuses](https://img.shields.io/badge/Campuses-6-orange?style=for-the-badge)
![VLANs](https://img.shields.io/badge/VLANs-30%2B-brightgreen?style=for-the-badge)
![OSPF](https://img.shields.io/badge/Routing-OSPF%20Area%200-9b59b6?style=for-the-badge)
![NAT](https://img.shields.io/badge/NAT-PAT%20Overload-red?style=for-the-badge)

*Full-scale enterprise network simulation — VLAN segmentation, inter-VLAN routing, OSPF, DHCP, ACLs, NAT, and ISP WAN connectivity across 6 campuses.*

</div>

---

## 📌 About This Project

A complete design and simulation of a **multi-campus enterprise network** for SZABIST built in Cisco Packet Tracer. The network connects 6 campuses through a centralized hub-and-spoke topology using OSPF dynamic routing, VLAN segmentation with Router-on-a-Stick, DHCP, static IPs, NAT/PAT for internet access, ACL-based security, and port security on switches.

---

## 🗺️ Network Topology

```
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

**Topology:** Hub-and-Spoke | **Routing Protocol:** OSPF Area 0 | **Internet:** NAT/PAT via EDGE-99

---

## 🏫 Campus Breakdown

| Campus | Router | VLANs | Key Departments | Link |
|--------|--------|-------|-----------------|------|
| **Campus 99** — Main | EDGE-99 | 7 | Classrooms, Faculty, IT, Exam, Admin, Data Center | Hub |
| **Campus 100** — Labs | R-100 | 13 | CS Lab, AI Lab, Lab3–6, Smart Lab, Gaming Lab, Faculty, Admin, IT | Gigabit Ethernet |
| **Campus 154** | R-154 | 5 | Classrooms, Faculty, Academic, Admin, Mechatronics | Gigabit Ethernet |
| **Campus 153** | R-153 | 3 | Classrooms, Admissions, Academic | Serial |
| **Campus 79** — Admin | R-79 | 6 | HR, Finance, Procurement, Admin, Library, EDC | Serial |
| **Media Villa** | R-MEDIA | 3 | Classrooms, Faculty, Academic | Serial |

---

## 🔗 WAN Links — Router Interconnects (/30 Subnets)

| Connection | Subnet | EDGE-99 IP | Remote Router IP | Medium |
|------------|--------|------------|-----------------|--------|
| EDGE-99 ↔ ISP | `11.11.11.0/30` | `11.11.11.1` (Se0/1/0) | `11.11.11.2` | Serial DCE |
| EDGE-99 ↔ R-100 | `23.12.145.108/30` | `23.12.145.109` (Gi0/1) | `23.12.145.110` (Gi0/0) | Ethernet |
| EDGE-99 ↔ R-154 | `23.12.145.112/30` | `23.12.145.113` (Gi0/2) | `23.12.145.114` (Gi0/0) | Ethernet |
| EDGE-99 ↔ R-153 | `23.12.145.116/30` | `23.12.145.117` (Se0/0/0) | `23.12.145.118` (Se0/0/0) | Serial DCE |
| EDGE-99 ↔ R-79 | `23.12.145.120/30` | `23.12.145.121` (Se0/0/1) | `23.12.145.122` (Se0/0/0) | Serial DCE |
| EDGE-99 ↔ R-MEDIA | `23.12.145.124/30` | `23.12.145.125` (Se0/1/1) | `23.12.145.126` (Se0/1/0) | Serial DCE |

---

## 🗄️ IP Address Plan

| Block | Assigned To | Available IPs |
|-------|------------|---------------|
| `23.12.145.0/24` | Campus 99 VLANs + all WAN links | 254 |
| `23.12.151.0/24` | Campus 100 — Labs 1–4 (CS, AI, Lab3, Lab4) | 254 |
| `192.168.1.0/24` | Campus 100 — Labs 5–7 (Lab5, Lab6, Smart Lab) | 254 |
| `192.168.2.0/24` | Campus 100 — Remaining departments | 254 |
| `192.168.3.0/24` | Campus 153 | 254 |
| `192.168.4.0/24` | Campus 79 | 254 |
| `192.168.5.0/24` | Media Villa | 254 |
| `11.11.11.0/30` | ISP WAN Link (Public IP) | 2 |

---

## 📋 VLAN & DHCP Configuration

<details>
<summary><b>Campus 99 — 7 VLANs</b></summary>

| VLAN | Name | Network | Gateway | DHCP Range |
|------|------|---------|---------|------------|
| 140 | CLASSROOMS-99 | `23.12.145.0/29` | `23.12.145.1` | `.2 – .6` |
| 150 | FACULTY-99 | `23.12.145.48/28` | `23.12.145.49` | `.50 – .62` |
| 160 | ACADEMIC-99 | `23.12.145.16/30` | `23.12.145.17` | `.18` |
| 170 | IT-99 | `23.12.145.20/30` | `23.12.145.21` | `.22` |
| 180 | EXAMINATION | `23.12.145.24/29` | `23.12.145.25` | `.26 – .30` |
| 190 | ADMIN-99 | `23.12.145.32/29` | `23.12.145.33` | `.34 – .38` |
| 200 | DATACENTER | `23.12.145.40/29` | `23.12.145.41` | Static only |

**Static Devices:**
| Device | IP | VLAN |
|--------|----|------|
| Web-Server | `23.12.145.42` | 200 |
| ZABDESK-Server | `23.12.145.43` | 200 |
| Email-Server | `23.12.145.44` | 200 |
| CMS-Server | `23.12.145.45` | 200 |
| Printer-Exam | `23.12.145.27` | 180 |
| Printer-Faculty | `23.12.145.50` | 150 |
| SW-99-CORE Mgmt | `23.12.145.34` | 190 |

</details>

<details>
<summary><b>Campus 100 — 13 VLANs</b></summary>

| VLAN | Name | Network | Gateway | DHCP Range |
|------|------|---------|---------|------------|
| 10 | CS-LAB | `23.12.151.0/26` | `23.12.151.1` | `.2 – .60` |
| 20 | AI-LAB | `23.12.151.64/26` | `23.12.151.65` | `.66 – .125` |
| 30 | LAB3 | `23.12.151.128/26` | `23.12.151.129` | `.130 – .188` |
| 40 | LAB4 | `23.12.151.192/26` | `23.12.151.193` | `.194 – .252` |
| 50 | LAB5 | `192.168.1.0/26` | `192.168.1.1` | `.2 – .60` |
| 60 | LAB6 | `192.168.1.64/26` | `192.168.1.65` | `.66 – .125` |
| 70 | SMART-LAB | `192.168.1.192/26` | `192.168.1.193` | `.194 – .253` |
| 80 | GAMING-LAB | `192.168.2.64/28` | `192.168.2.65` | `.66 – .77` |
| 90 | CLASSROOMS-100 | `192.168.2.128/28` | `192.168.2.129` | `.130 – .142` |
| 100 | FACULTY-100 | `192.168.2.96/27` | `192.168.2.97` | `.98 – .126` |
| 110 | ACADEMIC-100 | `192.168.2.144/28` | `192.168.2.145` | `.146 – .158` |
| 120 | ADMIN-100 | `192.168.2.160/29` | `192.168.2.161` | `.162 – .166` |
| 130 | IT-DEPT | `192.168.2.184/29` | `192.168.2.185` | `.186 – .190` |

</details>

<details>
<summary><b>Campus 154 — 5 VLANs</b></summary>

| VLAN | Name | Network | Gateway | DHCP Range |
|------|------|---------|---------|------------|
| 210 | CLASSROOMS-154 | `23.12.145.128/28` | `23.12.145.129` | `.130 – .142` |
| 220 | FACULTY-154 | `23.12.145.64/27` | `23.12.145.65` | `.66 – .94` |
| 230 | ACADEMIC-154 | `23.12.145.144/29` | `23.12.145.145` | `.146 – .150` |
| 240 | ADMIN-154 | `23.12.145.152/29` | `23.12.145.153` | `.154 – .158` |
| 250 | MECHATRONICS | `23.12.145.160/27` | `23.12.145.161` | `.162 – .190` |

</details>

<details>
<summary><b>Campus 153 — 3 VLANs</b></summary>

| VLAN | Name | Network | Gateway | DHCP Range |
|------|------|---------|---------|------------|
| 260 | CLASSROOMS-153 | `192.168.3.16/28` | `192.168.3.17` | `.18 – .30` |
| 270 | ADMISSIONS | `192.168.3.0/28` | `192.168.3.1` | `.2 – .14` |
| 280 | ACADEMIC-153 | `192.168.3.32/29` | `192.168.3.33` | `.34 – .38` |

</details>

<details>
<summary><b>Campus 79 — 6 VLANs</b></summary>

| VLAN | Name | Network | Gateway | DHCP Range |
|------|------|---------|---------|------------|
| 310 | LIBRARY-79 | `192.168.4.0/28` | `192.168.4.1` | `.2 – .14` |
| 320 | HR-79 | `192.168.4.16/28` | `192.168.4.17` | `.18 – .30` |
| 330 | PROCUREMENT-79 | `192.168.4.32/28` | `192.168.4.33` | `.34 – .46` |
| 340 | ADMIN-79 | `192.168.4.48/28` | `192.168.4.49` | `.50 – .62` |
| 350 | FINANCE-79 | `192.168.4.64/28` | `192.168.4.65` | `.66 – .78` |
| 360 | EDC-79 | `192.168.4.80/28` | `192.168.4.81` | `.82 – .94` |

</details>

<details>
<summary><b>Media Villa — 3 VLANs</b></summary>

| VLAN | Name | Network | Gateway | DHCP Range |
|------|------|---------|---------|------------|
| 380 | CLASSROOMS-MEDIA | `192.168.5.0/29` | `192.168.5.1` | `.2 – .6` |
| 390 | FACULTY-MEDIA | `192.168.5.16/28` | `192.168.5.17` | `.18 – .26` |
| 400 | ACADEMIC-MEDIA | `192.168.5.32/29` | `192.168.5.33` | `.34 – .38` |

</details>

---

## 🔒 Security Configuration

### ACL Rules (Applied on EDGE-99 — outbound)
Access control list restricts who can access Faculty printers and the ZABDESK server:

- ✅ **Faculty VLANs only** can access Faculty printers across all campuses
- ✅ **All Computer Labs** can access the ZABDESK server
- ❌ All other sources are denied access to printers and ZABDESK

### Port Security
All lab switches (Campus 100) and server switches (Campus 99) are configured with:
- **Max MACs:** 1 per port
- **Violation Action:** Shutdown
- **Applied on:** CS Lab, AI Lab, Lab3–6, Smart Lab, Gaming Lab, Data Center switches

---

## 🔄 Routing & NAT

### OSPF — Single Area 0
All 6 routers run OSPF Process 1 in Area 0. EDGE-99 acts as DR/BDR, with all campus routers advertising their connected networks.

### NAT/PAT (Internet Access)
- **Type:** PAT (Port Address Translation / Overload)
- **Public IP:** `11.11.11.1` (EDGE-99 Se0/1/0)
- **Default Route:** `0.0.0.0/0` via `11.11.11.2` (ISP)
- All private campus IPs are translated through this single public IP for internet access.

---

## 🧪 Testing Results

| Test | Result |
|------|--------|
| Same-VLAN ping | ✅ Pass |
| Inter-VLAN ping | ✅ Pass |
| Cross-campus ping | ✅ Pass |
| ISP reachability | ✅ Pass |
| Internet connectivity | ✅ Pass |

---

## ⚙️ Concepts Implemented

| Concept | Description |
|---------|-------------|
| **VLAN + 802.1Q Trunking** | Department-level isolation across all campuses |
| **Router-on-a-Stick** | Sub-interfaces on each router for inter-VLAN routing |
| **DHCP** | Per-VLAN dynamic IP pools on each campus router |
| **Static IP** | Fixed addresses for all servers, printers, and core switches |
| **VLSM** | Subnets sized per department to minimize IP waste |
| **OSPF Area 0** | Dynamic routing between all campus routers |
| **NAT/PAT** | Single public IP for full campus internet access |
| **ACLs** | Restrict printer and server access by source network |
| **Port Security** | MAC-based port lockdown on lab and server switches |
| **Telnet** | Remote management configured on all routers and core switches |

---

## 📁 Project File

| File | Description |
|------|-------------|
| `CNDC_PROJECT_FINAL_ALL_CAMPUSES.pkt` | Complete Cisco Packet Tracer simulation — all 6 campuses |

> ⚠️ Requires **Cisco Packet Tracer 8.x** or later to open.

---

<div align="center">

![Packet Tracer](https://img.shields.io/badge/Cisco%20Packet%20Tracer-1BA0D7?style=flat-square&logo=cisco&logoColor=white)
![OSPF](https://img.shields.io/badge/OSPF-Area%200-9b59b6?style=flat-square)
![VLAN](https://img.shields.io/badge/VLAN%20%26%20802.1Q-blue?style=flat-square)
![NAT](https://img.shields.io/badge/NAT%2FPAT-red?style=flat-square)
![ACL](https://img.shields.io/badge/ACL-Security-orange?style=flat-square)
![DHCP](https://img.shields.io/badge/DHCP-green?style=flat-square)
![VLSM](https://img.shields.io/badge/VLSM-grey?style=flat-square)

</div>
