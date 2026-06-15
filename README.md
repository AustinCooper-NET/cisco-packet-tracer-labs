# Enterprise Hybrid LAN with Routed Default Gateway

## Objective
To implement an enterprise-grade Layer 3 boundary device (Router) into a hybrid local infrastructure, defining a default gateway matrix to facilitate data routing outside the local collision domain.

## Network Topology
![Network Topology](topology.png)

## 1. Complete Infrastructure Inventory
* **1 x Cisco ISR 4331 Router (ISR-Router0):** Acts as the network's Default Gateway, establishing a Layer 3 boundary for external data routing.
* **1 x Cisco Catalyst 2960 Switch (Switch0):** Central Layer 2 core managing hardware MAC addresses and local data frame distribution.
* **1 x Linksys WRT300N Wireless Access Point (Wireless Router0):** Segregates mobile nodes and handles automated internal DHCP address leasing.
* **1 x HQ Intranet Server (COMPANY-SERVER):** Hosting localized corporate HTTP/HTTPS web platform operations.
* **4 x Diversified Workstations:** Comprising two static wired endpoints (HR and IT departments) and two mobile wireless clients (smartphone and modified interface laptop).

## 2. Definitive Network Addressing Matrix
The introduction of the Layer 3 boundary establishes a default exit route (`192.168.1.1`) required for all host configuration profiles across the primary subnet.

| Device Name | Connection Type | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **ISR-Router0** | Gateway Port (Gi0/0/0) | `192.168.1.1` | `255.255.255.0` | *Self* |
| **COMPANY-SERVER** | Wired (Fa0/3) | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` |
| **HR-DESKTOP** | Wired (Fa0/1) | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` |
| **IT-LAPTOP** | Wired (Fa0/2) | `192.168.1.12` | `255.255.255.0` | `192.168.1.1` |
| **Wireless Router0**| Wired (Fa0/4) | DHCP Assigned | `255.255.255.0` | Dynamic |
| **Smartphone0** | Wireless | DHCP Assigned | `255.255.255.0` | `192.168.0.1` |
| **Wireless-Laptop1**| Wireless | DHCP Assigned | `255.255.255.0` | `192.168.0.1` |

## 3. Layer 3 Boundary Verification
* **Gateway Connectivity:** ICMP echoes (pings) executed from local segments (`192.168.1.12`) to the default gateway address (`192.168.1.1`) returned a 100% success rate with 0% packet loss, validating optimal Layer 2 to Layer 3 configuration.
* **Core Services Persistence:** Intranet HTTP functionality and wireless DHCP sub-pools remain fully operational and unified under the new gateway coordinator.
