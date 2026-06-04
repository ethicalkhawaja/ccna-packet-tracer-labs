Static Routing Lab

"Topology" (topology.png)

Project Overview

This project demonstrates Static Routing between three routers connecting three separate LANs. The objective is to provide end-to-end connectivity between all networks using manually configured static routes.

Network Topology

LAN Networks

LAN| Network| Default Gateway
LAN 1| 192.168.1.0/24| 192.168.1.254
LAN 2| 192.168.2.0/24| 192.168.2.254
LAN 3| 192.168.3.0/24| 192.168.3.254

WAN Links

Connection| Network
R1 ↔ R2| 10.0.12.0/30
R2 ↔ R3| 10.0.23.0/30

Devices Used

- 3 Cisco Routers
- 3 Cisco Switches
- 6 PCs
- Cisco Packet Tracer

Skills Demonstrated

- Static Routing
- IP Addressing
- Subnetting
- Router Configuration
- Network Troubleshooting
- End-to-End Connectivity Testing

Verification Commands

show ip route
show ip interface brief
ping <destination-ip>

Results

All LANs can successfully communicate with each other through manually configured static routes.

Author

ethicalkhawaja