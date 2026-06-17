# Cisco Packet Tracer Networking Labs

A collection of progressively advanced networking labs built in Cisco Packet Tracer while studying Computer Networking.

## Lab Progression

| Lab Project | Concepts Covered | Date Completed | Topology |
| :--- | :--- | :--- | :--- |
| **Basic LAN** | Static IP, Layer 2 Switching | June 2026 | [View](images/basic-lan-topology.png) |
| **Secure SOHO** | Wireless, DHCP | June 2026 | [View](images/secure-soho-topology.png) |
| **Enterprise Gateway** | Default Gateways, L3 Routing | June 2026 | [View](images/enterprise-gateway-topology.png) |
| **Enterprise LAN/WAN** | ISP Connectivity, Public Routing | June 2026 | [View](images/enterprise-lan-wan-topology.png) |
| **VLAN & Inter-VLAN Routing** | 802.1Q Trunking, Sub-interfaces, ROAS | June 2026 | [View](images/roas-topology.png) |

---

## Lab Spotlight: Enterprise LAN/WAN

### Overview
This lab connects a local office network to an ISP router, using a default route to give internal devices access to the public internet.

### Technologies Used
- **Network Architecture:** Layer 2 Switching, Layer 3 Architecture, WAN Transit Subnets
- **Routing & Services:** Static Routing (Gateway of Last Resort), DHCP Services
- **Protocols & Analysis:** IPv4 Subnetting, ICMP Troubleshooting
- **Environment:** Cisco Packet Tracer, Cisco IOS CLI

### Troubleshooting Log
* **Issue:** Devices inside the local network could not ping the ISP public server.
* **Root Cause:** Asymmetric routing. The ISP router received the packets but did not have a return route in its routing table for the local `192.168.1.0/24` subnet.
* **Resolution:** Added a static route (`ip route 192.168.1.0 255.255.255.0 10.0.0.2`) on the ISP router pointing back to the edge gateway to handle return traffic.

### Verification

#### EDGE-ROUTER
* **Interface Status:** ![Interface Brief](images/edge-router-brief.png)
  *Verified that all local LAN and WAN interfaces are up and assigned the correct IPs.*
* **Routing Table:** ![Routing Table](images/edge-router-route.png)
  *Verified the default route (`S*`) is active and pointing traffic out to the ISP.*

#### ISP-ROUTER
* **Interface Status:** ![Interface Brief](images/isp-router-brief.png)
  *Verified the public-facing and transit interfaces are operational.*
* **Routing Table:** ![Routing Table](images/isp-router-route.png)
  *Verified the static return route to the internal network is active, ensuring two-way communication.*

---

## Lab Spotlight: VLAN Segmentation & Inter-VLAN Routing (ROAS)

### Overview
This lab isolates HR, IT, and Server devices into distinct logical subnets (VLANs 10, 20, and 30) on a single switch to limit broadcast domains. It then utilizes a single physical trunk link to an upstream router (Router-on-a-Stick) to enable controlled, routable communication between those subnets.

### Technologies Used
- **Network Architecture:** Layer 2 Switching, Broadcast Domain Isolation, 802.1Q Virtual Local Area Networks (VLANs)
- **Routing & Services:** Router-on-a-Stick (Sub-interfaces), Inter-VLAN Routing
- **Protocols & Analysis:** IPv4 Subnetting, ARP Resolution, ICMP Verification
- **Environment:** Cisco Packet Tracer, Cisco IOS CLI

### Troubleshooting Log
* **Issue 1:** The `show interface trunk` command on the switch returned a completely blank output, and the link light between the switch and router remained red.
  * **Root Cause:** Cisco router ports are turned off (`shutdown`) by default from the factory. Because the upstream interface was inactive, the switch port entered a disabled/non-connecting state and refused to initialize trunking negotiated behavior.
  * **Resolution:** Entered the router CLI and issued a `no shutdown` command on the physical interface to activate the link.
* **Issue 2:** The router CLI rejected sub-interface setup commands with an `%Invalid interface type and number` error.
  * **Root Cause:** Attempted to configure `interface gig0/0.10`, assuming standard 2911 interface naming. The specific ISR router module installed uses a three-slot hardware mapping scheme (`slot/subslot/port`).
  * **Resolution:** Executed `show ip interface brief` to reveal the exact hardware name format (`GigabitEthernet0/0/0`). Adjusted configuration inputs to reference `gig0/0/0.10` successfully.

### Verification

#### CORE-SWITCH
* **Port Trunking Status:**
  *Verified that `Gig0/1` is successfully acting as an active 802.1Q trunk, allowing tagged frames from VLANs 10, 20, and 30 to pass up to the routing engine.*

#### EDGE-ROUTER
* **Active Routing Table:**
  *Confirmed that virtual sub-interfaces `Gig0/0/0.10`, `Gig0/0/0.20`, and `Gig0/0/0.30` are recognized by the IOS kernel as directly connected (`C`) and serving as the valid gateway endpoints for their respective subnets.*

### Testing Results (Cross-VLAN Verification)
* **Successful Inter-VLAN Routing:** ![Ping Test](images/ping-test.png)
  *Executed cross-subnet diagnostic pings from HR-DESKTOP (`192.168.10.2`) to IT-LAPTOP (`192.168.20.2`) and COMPANY-SERVER (`192.168.30.10`). Initial packet drops occurred normally due to standard ARP resolution, followed by 100% continuous ICMP success responses routed via the sub-interfaces.*

---

## Planned Labs
- [x] Basic LAN
- [x] Secure SOHO
- [x] Enterprise Gateway
- [x] Enterprise LAN/WAN
- [x] VLAN Segmentation & Router-on-a-Stick
- [ ] Access Control Lists (ACLs)
- [ ] NAT/PAT
- [ ] OSPF Routing
- [ ] Port Security
