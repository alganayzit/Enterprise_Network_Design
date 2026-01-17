# Enterprise Network Design with Redundancy & Security

This project demonstrates a scalable and resilient enterprise network architecture designed using **Cisco Packet Tracer**. It features a multi-site topology (HQ, Branch, and Guest) with advanced routing, switching, and security protocols.

## 🚀 Key Technologies & Protocols
* **Routing:** OSPF (Multi-area simulation), Inter-VLAN Routing (Router-on-a-Stick).
* **High Availability:** HSRP (Gateway Redundancy) and LACP EtherChannel (Link Aggregation).
* **Security:** Extended ACLs for Guest isolation, SSH for secure management, and Port Security.
* **Edge Services:** NAT/PAT (Network Address Translation) and Default Route propagation.
* **Connectivity:** Wireless LAN (WPA2-PSK) and DHCP for automated addressing.

## 🏗️ Topology Overview
* **HQ (Headquarters):** Managed by R1 (Active) and R1-Backup (Standby) via HSRP.
* **Branch Office:** Connected via OSPF to the HQ core.
* **Guest Segment:** Isolated wireless network with restricted access to internal VLANs.
* **ISP Simulation:** Edge routers performing NAT to reach a simulated 8.8.8.8 internet endpoint.
   
## 🧪 **Verification Tests**
* **Redundancy Test:** Shutdown R1 and verify that R1-Backup takes over the gateway (HSRP).
* **Security Test:** Verify Guest PC cannot ping the Accounting VLAN (ACL 101).
* **Connectivity Test:** Ping 8.8.8.8 from any internal PC to verify NAT and Routing.
* ![Network Topology](./topology.screenshot.png)
