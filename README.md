# Small Office Local Area Network (LAN) Simulation

## Objective
To design, physically cable, and logically configure a functional peer-to-peer business network to verify end-to-end communication using standard industry protocols.

## Network Topology
![Network Topology](topology.png)

## 1. Hardware Inventory
* **1 x Cisco Catalyst 2960 Switch:** Acts as the central core of the network, forwarding data packets based on physical MAC addresses.
* **1 x End-Device Laptop (IT Department):** Workstation used to initiate network requests.
* **1 x End-Device PC (HR Department):** Workstation used to verify network connectivity across different switch ports.
* **1 x End-Device Server (Data Storage):** Central repository configured to receive and respond to incoming network traffic.
* **3 x Copper Straight-Through Cables:** Used to connect the Network Interface Cards (NICs) of the computers directly to the switch ports.

## 2. Logical Addressing Schema (IP Map)
Every device was configured with a static IPv4 address inside the standard private Class C network range (`192.168.1.0/24`).

| Device Name | Switch Port Connection | IP Address | Subnet Mask |
| :--- | :--- | :--- | :--- |
| **Company-Server** | FastEthernet 0/3 | `192.168.1.10` | `255.255.255.0` |
| **HR-Desktop** | FastEthernet 0/1 | `192.168.1.11` | `255.255.255.0` |
| **IT-Laptop** | FastEthernet 0/2 | `192.168.1.12` | `255.255.255.0` |

## 3. Verification & Testing Procedure
To test the network, an ICMP (Internet Control Message Protocol) packet—commonly known as a **Ping**—was initiated from the IT-Laptop command prompt to the Company-Server.

* **The Command Used:** `ping 192.168.1.10`
* **The Packet Pathway:** 1. The IT-Laptop generated an ICMP request echo packet.
  2. The packet traveled through the copper cable into Switch Port `Fa0/2`.
  3. The Cisco Switch read the destination IP, mapped it to Switch Port `Fa0/3`, and forwarded the packet.
  4. The Company-Server received the request, processed it, and sent an ICMP reply packet back through the switch to the Laptop.
* **The Success Criteria:** The command line displayed a 100% success rate with 4 packets sent, 4 packets received, and 0% packet loss.
