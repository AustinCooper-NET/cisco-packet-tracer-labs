# Cisco Packet Tracer Networking Labs

## 📡 Network Simulation Portfolio

A structured collection of Cisco Packet Tracer labs simulating real-world enterprise network environments.

These labs demonstrate progressive skill development across:
- LAN design and switching
- VLAN segmentation and inter-VLAN routing
- Network security (ACLs)
- WAN connectivity and routing behavior
- IPv4 addressing, subnetting, and NAT/PAT

---

## Skills Demonstrated

- VLAN design and segmentation (802.1Q trunking)
- Inter-VLAN routing (Router-on-a-Stick)
- IPv4 subnetting and network planning
- Static routing and default gateway configuration
- ACL-based traffic filtering and security policies
- NAT/PAT (Port Address Translation) implementation
- Cisco IOS CLI configuration and troubleshooting
- Network verification using ping, ARP, and routing tables

---

## Lab Progression

| Lab Project | Concepts Covered | Date Completed | Topology |
| :--- | :--- | :--- | :--- |
| **Basic LAN** | Static IP, Layer 2 Switching | June 2026 | [View](images/basic-lan-topology.png) |
| **Secure SOHO** | Wireless, DHCP | June 2026 | [View](images/secure-soho-topology.png) |
| **Enterprise Gateway** | Default Gateway, L3 Routing | June 2026 | [View](images/enterprise-gateway-topology.png) |
| **Enterprise LAN/WAN** | ISP Connectivity, Static Routing | June 2026 | [View](images/enterprise-lan-wan-topology.png) |
| **VLAN & Inter-VLAN Routing** | 802.1Q, Sub-interfaces, ROAS | June 2026 | [View](images/roas-topology.png) |
| **Access Control Lists (ACLs)** | Traffic Filtering, Security Policies | June 2026 | [View](images/acl-topology.png) |
| **Dynamic NAT / PAT** | NAT Overload, Public/Private Translation | June 2026 | [View](images/nat-topology.png) |

---

## Featured Lab: Enterprise LAN/WAN

### Overview
Connects a local office network to an ISP router using static routing and a default gateway configuration to enable external connectivity.

### Key Technologies
- Layer 2 Switching + Layer 3 Routing
- WAN transit subnet design
- DHCP services
- IPv4 subnetting and ICMP troubleshooting

### Troubleshooting Summary
- **Issue:** Internal devices could not reach external ISP server  
- **Cause:** ISP router missing return route for internal subnet  
- **Fix:** Added static route pointing to edge gateway interface  

---

## Featured Lab: VLAN Segmentation (ROAS)

### Overview
Implements VLAN separation for HR, IT, and Server networks, enabling controlled inter-VLAN communication through a Router-on-a-Stick architecture.

### Key Technologies
- 802.1Q trunking
- VLAN isolation
- Inter-VLAN routing via sub-interfaces

### Troubleshooting Summary
- Fixed router interface shutdown preventing trunk formation
- Resolved incorrect sub-interface naming due to hardware slot format mismatch

---

## Featured Lab: Access Control Lists (ACLs)

### Overview
Implements Layer 3 security policies to restrict traffic between VLANs while preserving access to shared services.

### Policy Example
- Block HR → IT traffic
- Allow HR/IT → Server network

### Key Fix
- Corrected wildcard mask usage (0.0.0.255 vs subnet mask)

---

## Featured Lab: Dynamic NAT / PAT

### Overview
Implements NAT overload to allow multiple internal networks to share a single public IP address.

### Key Technologies
- NAT inside/outside interfaces
- ACL-based traffic matching
- Port translation tracking

---

## 📌 Planned Labs
- [x] Basic LAN
- [x] Secure SOHO
- [x] Enterprise Gateway
- [x] Enterprise LAN/WAN
- [x] VLAN Routing (ROAS)
- [x] ACL Security
- [x] NAT/PAT
- [ ] OSPF Routing
- [ ] Port Security
