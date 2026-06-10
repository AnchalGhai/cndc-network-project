<div align="center">
🌐 Multi-Campus Enterprise Network
Computer Networks & Data Communications — SZABIST Karachi
Show Image
Show Image
Show Image
Show Image
Show Image
Full-scale enterprise network simulation — VLAN segmentation, inter-VLAN routing, OSPF, DHCP, ACLs, NAT, and ISP WAN connectivity across 6 campuses.
</div>

📌 About This Project
A complete design and simulation of a multi-campus enterprise network for SZABIST built in Cisco Packet Tracer. The network connects 6 campuses through a centralized hub-and-spoke topology using OSPF dynamic routing, VLAN segmentation with Router-on-a-Stick, DHCP, static IPs, NAT/PAT for internet access, ACL-based security, and port security on switches.

🗺️ Network Topology
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
Topology: Hub-and-Spoke | Routing Protocol: OSPF Area 0 | Internet: NAT/PAT via EDGE-99

🏫 Campus Breakdown
CampusRouterVLANsKey DepartmentsLinkCampus 99 — MainEDGE-997Classrooms, Faculty, IT, Exam, Admin, Data CenterHubCampus 100 — LabsR-10013CS Lab, AI Lab, Lab3–6, Smart Lab, Gaming Lab, Faculty, Admin, ITGigabit EthernetCampus 154R-1545Classrooms, Faculty, Academic, Admin, MechatronicsGigabit EthernetCampus 153R-1533Classrooms, Admissions, AcademicSerialCampus 79 — AdminR-796HR, Finance, Procurement, Admin, Library, EDCSerialMedia VillaR-MEDIA3Classrooms, Faculty, AcademicSerial

🔗 WAN Links — Router Interconnects (/30 Subnets)
ConnectionSubnetEDGE-99 IPRemote Router IPMediumEDGE-99 ↔ ISP11.11.11.0/3011.11.11.1 (Se0/1/0)11.11.11.2Serial DCEEDGE-99 ↔ R-10023.12.145.108/3023.12.145.109 (Gi0/1)23.12.145.110 (Gi0/0)EthernetEDGE-99 ↔ R-15423.12.145.112/3023.12.145.113 (Gi0/2)23.12.145.114 (Gi0/0)EthernetEDGE-99 ↔ R-15323.12.145.116/3023.12.145.117 (Se0/0/0)23.12.145.118 (Se0/0/0)Serial DCEEDGE-99 ↔ R-7923.12.145.120/3023.12.145.121 (Se0/0/1)23.12.145.122 (Se0/0/0)Serial DCEEDGE-99 ↔ R-MEDIA23.12.145.124/3023.12.145.125 (Se0/1/1)23.12.145.126 (Se0/1/0)Serial DCE

🗄️ IP Address Plan
BlockAssigned ToAvailable IPs23.12.145.0/24Campus 99 VLANs + all WAN links25423.12.151.0/24Campus 100 — Labs 1–4 (CS, AI, Lab3, Lab4)254192.168.1.0/24Campus 100 — Labs 5–7 (Lab5, Lab6, Smart Lab)254192.168.2.0/24Campus 100 — Remaining departments254192.168.3.0/24Campus 153254192.168.4.0/24Campus 79254192.168.5.0/24Media Villa25411.11.11.0/30ISP WAN Link (Public IP)2

📋 VLAN & DHCP Configuration
<details>
<summary><b>Campus 99 — 7 VLANs</b></summary>
VLANNameNetworkGatewayDHCP Range140CLASSROOMS-9923.12.145.0/2923.12.145.1.2 – .6150FACULTY-9923.12.145.48/2823.12.145.49.50 – .62160ACADEMIC-9923.12.145.16/3023.12.145.17.18170IT-9923.12.145.20/3023.12.145.21.22180EXAMINATION23.12.145.24/2923.12.145.25.26 – .30190ADMIN-9923.12.145.32/2923.12.145.33.34 – .38200DATACENTER23.12.145.40/2923.12.145.41Static only
Static Devices:
DeviceIPVLANWeb-Server23.12.145.42200ZABDESK-Server23.12.145.43200Email-Server23.12.145.44200CMS-Server23.12.145.45200Printer-Exam23.12.145.27180Printer-Faculty23.12.145.50150SW-99-CORE Mgmt23.12.145.34190
</details>
<details>
<summary><b>Campus 100 — 13 VLANs</b></summary>
VLANNameNetworkGatewayDHCP Range10CS-LAB23.12.151.0/2623.12.151.1.2 – .6020AI-LAB23.12.151.64/2623.12.151.65.66 – .12530LAB323.12.151.128/2623.12.151.129.130 – .18840LAB423.12.151.192/2623.12.151.193.194 – .25250LAB5192.168.1.0/26192.168.1.1.2 – .6060LAB6192.168.1.64/26192.168.1.65.66 – .12570SMART-LAB192.168.1.192/26192.168.1.193.194 – .25380GAMING-LAB192.168.2.64/28192.168.2.65.66 – .7790CLASSROOMS-100192.168.2.128/28192.168.2.129.130 – .142100FACULTY-100192.168.2.96/27192.168.2.97.98 – .126110ACADEMIC-100192.168.2.144/28192.168.2.145.146 – .158120ADMIN-100192.168.2.160/29192.168.2.161.162 – .166130IT-DEPT192.168.2.184/29192.168.2.185.186 – .190
</details>
<details>
<summary><b>Campus 154 — 5 VLANs</b></summary>
VLANNameNetworkGatewayDHCP Range210CLASSROOMS-15423.12.145.128/2823.12.145.129.130 – .142220FACULTY-15423.12.145.64/2723.12.145.65.66 – .94230ACADEMIC-15423.12.145.144/2923.12.145.145.146 – .150240ADMIN-15423.12.145.152/2923.12.145.153.154 – .158250MECHATRONICS23.12.145.160/2723.12.145.161.162 – .190
</details>
<details>
<summary><b>Campus 153 — 3 VLANs</b></summary>
VLANNameNetworkGatewayDHCP Range260CLASSROOMS-153192.168.3.16/28192.168.3.17.18 – .30270ADMISSIONS192.168.3.0/28192.168.3.1.2 – .14280ACADEMIC-153192.168.3.32/29192.168.3.33.34 – .38
</details>
<details>
<summary><b>Campus 79 — 6 VLANs</b></summary>
VLANNameNetworkGatewayDHCP Range310LIBRARY-79192.168.4.0/28192.168.4.1.2 – .14320HR-79192.168.4.16/28192.168.4.17.18 – .30330PROCUREMENT-79192.168.4.32/28192.168.4.33.34 – .46340ADMIN-79192.168.4.48/28192.168.4.49.50 – .62350FINANCE-79192.168.4.64/28192.168.4.65.66 – .78360EDC-79192.168.4.80/28192.168.4.81.82 – .94
</details>
<details>
<summary><b>Media Villa — 3 VLANs</b></summary>
VLANNameNetworkGatewayDHCP Range380CLASSROOMS-MEDIA192.168.5.0/29192.168.5.1.2 – .6390FACULTY-MEDIA192.168.5.16/28192.168.5.17.18 – .26400ACADEMIC-MEDIA192.168.5.32/29192.168.5.33.34 – .38
</details>

🔒 Security Configuration
ACL Rules (Applied on EDGE-99 — outbound)
Access control list restricts who can access Faculty printers and the ZABDESK server:

✅ Faculty VLANs only can access Faculty printers across all campuses
✅ All Computer Labs can access the ZABDESK server
❌ All other sources are denied access to printers and ZABDESK

Port Security
All lab switches (Campus 100) and server switches (Campus 99) are configured with:

Max MACs: 1 per port
Violation Action: Shutdown
Applied on: CS Lab, AI Lab, Lab3–6, Smart Lab, Gaming Lab, Data Center switches


🔄 Routing & NAT
OSPF — Single Area 0
All 6 routers run OSPF Process 1 in Area 0. EDGE-99 acts as DR/BDR, with all campus routers advertising their connected networks.
NAT/PAT (Internet Access)

Type: PAT (Port Address Translation / Overload)
Public IP: 11.11.11.1 (EDGE-99 Se0/1/0)
Default Route: 0.0.0.0/0 via 11.11.11.2 (ISP)
All private campus IPs are translated through this single public IP for internet access.


🧪 Testing Results
TestResultSame-VLAN ping✅ PassInter-VLAN ping✅ PassCross-campus ping✅ PassISP reachability✅ PassInternet connectivity✅ Pass

⚙️ Concepts Implemented
ConceptDescriptionVLAN + 802.1Q TrunkingDepartment-level isolation across all campusesRouter-on-a-StickSub-interfaces on each router for inter-VLAN routingDHCPPer-VLAN dynamic IP pools on each campus routerStatic IPFixed addresses for all servers, printers, and core switchesVLSMSubnets sized per department to minimize IP wasteOSPF Area 0Dynamic routing between all campus routersNAT/PATSingle public IP for full campus internet accessACLsRestrict printer and server access by source networkPort SecurityMAC-based port lockdown on lab and server switchesTelnetRemote management configured on all routers and core switches

📁 Project File
FileDescriptionCNDC_PROJECT_FINAL_ALL_CAMPUSES.pktComplete Cisco Packet Tracer simulation — all 6 campuses

⚠️ Requires Cisco Packet Tracer 8.x or later to open.


<div align="center">
Show Image
Show Image
Show Image
Show Image
Show Image
Show Image
Show Image
</div>
