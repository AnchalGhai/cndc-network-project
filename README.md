🌐 Multi-Campus Enterprise Network — CNDC Project
Computer Networks & Data Communications | SZABIST Karachi
Designed and simulated a full-scale multi-campus enterprise network for SZABIST, connecting 6 campuses with 30+ VLANs using Cisco Packet Tracer.

📌 Project Overview
This project involves designing and simulating a multi-campus enterprise network that connects 6 SZABIST campuses through a centralized hub-and-spoke topology. The network implements real-world concepts including VLAN segmentation, inter-VLAN routing via Router-on-a-Stick, DHCP, static IP allocation, and WAN connectivity through an ISP.

🗺️ Network Topology
                        ISP
                         |
                    [ EDGE-99 ]
                  (Campus 99 — Main Hub)
                /    |    |     \     \
           R-100  R-154  R-153  R-79  R-MEDIA
         (C100) (C154) (C153) (C79) (Media Villa)
Topology Type: Hub-and-Spoke
Central Router: EDGE-99 — handles all inter-campus routing + ISP internet access

🏫 Campus Details
Campus 99 — Main Campus (EDGE-99)

VLANs: 7 (Classrooms, Faculty, Academic, IT, Examination, Admin, Data Center)
Special: Hosts central Data Center with Web, Email, CMS, and ZABDESK servers
ISP Link: Serial — 11.11.11.0/30

Campus 100 — Computer Labs

VLANs: 13 (CS Lab, AI Lab, Gaming Lab, Smart Lab + admin departments)
Link to EDGE-99: Gigabit Ethernet
Special: Largest campus with FTP servers in multiple labs

Campus 154

VLANs: 5 (Classrooms, Faculty, Academic, Admin, Mechatronics)
Link to EDGE-99: Gigabit Ethernet

Campus 153

VLANs: 3 (Classrooms, Admission, Academic)
Link to EDGE-99: Serial

Campus 79 — Administrative Campus

VLANs: 6 (HR, Finance, Procurement, Admin, Library, EDC)
Link to EDGE-99: Serial

Media Villa

VLANs: 3 (Classrooms, Faculty, Academic)
Link to EDGE-99: Serial


🔗 Inter-Campus WAN Links
LinkNetworkMediumEDGE-99 ↔ ISP11.11.11.0/30SerialEDGE-99 ↔ R-10023.12.145.108/30EthernetEDGE-99 ↔ R-15423.12.145.112/30EthernetEDGE-99 ↔ R-15323.12.145.116/30SerialEDGE-99 ↔ R-7923.12.145.120/30SerialEDGE-99 ↔ R-MEDIA23.12.145.124/30Serial

🗄️ IP Address Plan
BlockUsed For23.12.145.0/24Campus 99 VLANs + all WAN links23.12.151.0/24Campus 100 — Labs 1–4192.168.1.0/24Campus 100 — Labs 5–7192.168.2.0/24Campus 100 — Remaining VLANs192.168.3.0/24Campus 153192.168.4.0/24Campus 79192.168.5.0/24Media Villa11.11.11.0/30ISP WAN Link

⚙️ Key Concepts Implemented

VLAN Segmentation — Each department isolated in its own VLAN for security and broadcast control
Router-on-a-Stick — Sub-interfaces on each campus router for inter-VLAN routing
DHCP — Dynamic IP assignment for all end-user PCs, one pool per VLAN
Static IP — All servers, printers, and core switches have fixed IPs
VLSM — Variable Length Subnet Masking to minimize IP address waste
Hub-and-Spoke WAN — EDGE-99 as central hub for all inter-campus and internet traffic


🧪 Testing
Each campus was tested for:

✅ Same-VLAN connectivity (ping within same department)
✅ Inter-VLAN connectivity (ping across departments on same campus)
✅ Cross-campus connectivity (ping from one campus to another)
✅ ISP reachability
✅ Internet connectivity


📁 Project File
FileDescriptionCNDC_PROJECT_FINAL_ALL_CAMPUSES.pktFull Cisco Packet Tracer simulation — open to view all 6 campuses

Note: Open the .pkt file in Cisco Packet Tracer 8.x or later.


🛠️ Tools Used

Cisco Packet Tracer 8.x
VLAN & 802.1Q Trunking
DHCP Server Configuration
Static Routing / Default Routes
VLSM for IP Planning

