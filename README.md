# Enterprise Network Design with Redundancy & Security

This project demonstrates a scalable and resilient enterprise network architecture designed using **Cisco Packet Tracer**. It features a multi-site topology (HQ, Branch, and Guest) with advanced routing, switching, and security protocols.

## 🚀 Key Technologies & Protocols
* **Routing:** OSPF (Multi-area simulation), Inter-VLAN Routing (Router-on-a-Stick).
* **High Availability:** HSRP (Gateway Redundancy) and LACP EtherChannel (Link Aggregation).
* **Security:** Extended ACLs for Guest isolation, SSH for secure management, and Port Security.
* **Edge Services:** NAT/PAT (Network Address Translation) and Default Route propagation.
* **Connectivity:** Wireless LAN (WPA2-PSK) and DHCP for automated addressing.

## 🏗️ Topology Overview
- **HQ (Headquarters):** Managed by R1 (Active) and R1-Backup (Standby) via HSRP.
- **Branch Office:** Connected via OSPF to the HQ core.
- **Guest Segment:** Isolated wireless network with restricted access to internal VLANs.
- **ISP Simulation:** Edge routers performing NAT to reach a simulated 8.8.8.8 internet endpoint.

## 🛠️ Configuration Highlights

### HSRP (Hot Standby Router Protocol)
To ensure 99.9% uptime, R1 and R1-Backup share a Virtual IP:
```bash
# On R1 (Primary)
interface port-channel 1.10
 standby 1 ip 192.168.10.1
 standby 1 priority 110
 standby 1 preempt
