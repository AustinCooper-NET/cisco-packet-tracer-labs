# Cisco Packet Tracer Networking Labs

A collection of progressively advanced networking labs built in Cisco Packet Tracer while studying Computer Networking.

## Lab Progression

| Lab Project | Concepts Covered | Topology |
| :--- | :--- | :--- |
| **Basic LAN** | Static IP, Layer 2 Switching | [View](images/basic-lan-topology.png) |
| **Secure SOHO** | Wireless, DHCP | [View](images/secure-soho-topology.png) |
| **Enterprise Gateway** | Default Gateways, L3 Routing | [View](images/enterprise-gateway-topology.png) |
| **Enterprise LAN/WAN** | ISP Connectivity, Public Routing | [View](images/enterprise-lan-wan-topology.png) |

---

## Lab Spotlight: Enterprise LAN/WAN

### Overview
This project expanded the local corporate network into a routed WAN environment.

### The Troubleshooting Log (Learning from Mistakes)
* **Issue:** Pinging the ISP/Public server resulted in `Request timed out`.
* **Root Cause:** Asymmetric routing. My `EDGE-ROUTER` could reach the destination, but the `ISP-ROUTER` did not have a return path to the private `192.168.1.0/24` network.
* **Resolution:** Configured a static route (`ip route 192.168.1.0 255.255.255.0 10.0.0.2`) on the ISP router to direct traffic back to the office gateway.

### Verification
* `show ip route`: Confirmed the existence of the Gateway of Last Resort.
* `ping 8.8.8.8`: Verified end-to-end connectivity across the WAN boundary.

### Lessons Learned
- Routing is a two-way street; routers must know how to reach the source *and* the destination.
- ARP resolution causes the first packet of a ping to drop on new routes.

---

## Skills Demonstrated
- IPv4 Subnetting & Addressing
- Static Routing & Default Gateways
- ISP WAN Transit Configuration
- Network Documentation & Troubleshooting

## Planned Labs
- [ ] VLAN Segmentation
- [ ] Inter-VLAN Routing
- [ ] ACL Configuration
