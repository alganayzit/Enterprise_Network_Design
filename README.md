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
## 🛠️ Troubleshooting & Engineering Insights

A key part of this project was identifying and resolving real-world networking conflicts. Below are the technical challenges encountered during the implementation and the systematic approach used to solve them.

### 1. HSRP "Split-Brain" & Packet Loss
* **The Problem:** Ping tests to the gateway showed intermittent connectivity (approx. 50% packet loss).
* **Diagnosis:** Running `show standby brief` on both HQ routers revealed that both were in the **Active** state. This meant they weren't "hearing" each other's Hello packets, causing IP address conflicts.
* **The Fix:** * Verified the **Trunk** configuration on the interconnecting switch ports.
    * Adjusted **HSRP Priorities** (Primary: 110, Backup: 90).
    * Result: Stable failover with R1-Backup correctly transitioning to **Standby**.



### 2. OSPF Route Propagation Issues
* **The Problem:** The Branch Office router (R2) could not reach HQ VLANs, returning `Destination Host Unreachable`.
* **Diagnosis:** `show ip ospf neighbor` on R1-Backup was empty. The backup router was not advertising internal routes to the OSPF backbone.
* **The Fix:** * Corrected the `network` statements under the OSPF process to include the transit link between the router and the core switch.
    * Implemented `default-information originate` to ensure the internet path was known by all OSPF neighbors.



### 3. Port Density & Interface Failures
* **The Problem:** Physical interface limitations on the routers prevented redundant cabling.
* **Diagnosis:** Standard Router-on-a-Stick (sub-interfaces) on a single port created a "Single Point of Failure."
* **The Fix:** Implemented **LACP EtherChannel** between the access and distribution switches. This provided 2Gbps of aggregated bandwidth and ensured that if one physical cable failed, the VLAN trunks remained operational.
