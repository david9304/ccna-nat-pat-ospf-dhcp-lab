# ccna-nat-pat-ospf-lab
Multi-router Cisco Packet Tracer lab implementing OSPF, static routing, and NAT/PAT with end-to-end connectivity testing.
🌐 NAT + OSPF Multi-Router Lab (Packet Tracer)
📌 Overview

This project demonstrates a multi-router enterprise-style network using:

DHCP for R1 and R2 LAN
OSPF dynamic routing between internal routers
Static routing toward an ISP router
NAT Overload (PAT) configuration on the edge router
Multiple LAN segments with interconnectivity testing

The lab was built and tested in Cisco Packet Tracer.

🧱 Network Topology
Devices:
PC0 (Client)
PC1 (Client)
PC2 (Client)
PC3 (Client)
PC4 (Client)
PC5 (Client)
PC6 (Client)
Switch
Switch
Switch
R1 (Internal router)
R2 (Edge router - NAT gateway)
R3 (ISP router)
Networks:
Device	Network
R1 LAN	192.168.10.0/24, 192.168.30.0/24
R2 LAN	172.16.30.0/24
R3 LAN	10.0.1.0/24
NAT Outside	10.0.0.0/30 (example)
🔀 Routing
OSPF is configured between R1 and R2
Static routing is used between R2 and R3 (ISP side)
Full end-to-end connectivity is achieved via route redistribution logic
🔥 NAT Configuration

R2 acts as the edge NAT router.

NAT type: PAT (NAT Overload)
Inside networks: internal LANs (R1 + R2 LANs)
Outside interface: ISP-facing interface (R3 side)

Example config:

ip nat pool POOL1 10.0.0.0 10.0.0.6 netmask 255.255.255.0
ip nat inside source list 1 pool POOL1 overload

📊 Verification
NAT Table Example

Router#show ip nat translations 
Pro  Inside global     Inside local       Outside local      Outside global
icmp 10.0.0.1:16       192.168.10.3:16    10.0.1.2:16        10.0.1.2:16
icmp 10.0.0.1:21       172.16.30.3:21     10.0.1.2:21        10.0.1.2:21
icmp 10.0.0.1:4        192.168.30.2:4     10.0.1.2:4         10.0.1.2:4

Demonstrates:

PAT behavior using ICMP identifiers
Multiple internal hosts sharing one public IP
OSPF Neighbors

R2:
Neighbor ID     Pri   State           Dead Time   Address         Interface
1.1.1.1           0   FULL/  -        00:00:36    172.16.31.2     GigabitEthernet0/0/1

R1:
Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           0   FULL/  -        00:00:39    172.16.31.1     GigabitEthernet0/0/1


Connectivity Tests
Ping from R1 LAN → R3 LAN
Ping from R2 LAN → ISP network
Cross-subnet verification
🎯 Key Learnings
Difference between NAT and PAT
How OSPF interacts with static routing
Role of inside/outside NAT interfaces
Troubleshooting NAT ACL and interface misconfigurations
🧩 Tools Used
Cisco Packet Tracer
Cisco IOS CLI

<img width="959" height="539" alt="ccna-nat-pat-ospf-lab" src="https://github.com/user-attachments/assets/c2f42bfd-55fb-470f-bac2-866e3302ae2d" />
