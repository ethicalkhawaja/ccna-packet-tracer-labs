# Enterprise Network Lab | VLANs, DHCP, SSH, Inter-VLAN Routing & PAT

## Overview

This project simulates a small enterprise network built in Cisco Packet Tracer. The network is segmented using VLANs, supports dynamic IP allocation through DHCP, secure remote management via SSH, inter-VLAN communication through Router-on-a-Stick, and internet access using PAT (NAT Overload).

## Technologies

- Cisco IOS
- Cisco Packet Tracer
- VLAN Segmentation
- Router-on-a-Stick
- DHCP
- SSH
- PAT (NAT Overload)
- Static Routing
- Enterprise Network Design

---

## Network Topology

![Topology](images/topology.png)


## Network Design

### VLANs

| VLAN | Purpose | Network |
|--------|----------|------------|
| 10 | SALES| 192.168.10.0/24 |
| 20 | IT | 192.168.20.0/24 |
| 199 | Management | 192.168.199.0/24 |


## IP Addressing

### Router Interfaces

| Interface | Address |
|------------|------------|
| G0/1.1 | 192.168.10.254 |
| G0/1.2 | 192.168.20.254 |
| G0/1.199 | 192.168.199.254 |
| S0/0/0 | 203.0.113.1 |

### WAN Link

| Device | Address |
|---------|----------|
| ENT-R | 203.0.113.1 |
| ISP-R | 203.0.113.2 |

### Switch Management

| Device | Address |
|----------|----------|
| SW1 Management SVI | 192.168.199.2 |
| Default Gateway | 192.168.199.254 |


## Features Implemented

### VLAN Segmentation

Network traffic is separated into three VLANs to improve security, scalability, and management.

### Inter-VLAN Routing

Router-on-a-Stick was implemented using 802.1Q subinterfaces to allow communication between VLANs.

### DHCP Services

The enterprise router functions as the DHCP server.

Reserved infrastructure addresses:

| VLAN | Excluded Range |
|--------|----------------|
| VLAN 10 | 192.168.10.1 - 192.168.10.10 |
| VLAN 20 | 192.168.20.1 - 192.168.20.10 |
| VLAN 199 | 192.168.199.1 - 192.168.199.10 |

Dynamic addresses are automatically assigned to clients.

### SSH Management

SSH Version 2 was configured for secure remote administration of the switch through the management VLAN.

### PAT (NAT Overload)

PAT enables all internal VLANs to share the public WAN interface address.

access-list 1 permit 192.168.10.0 0.0.0.255
access-list 1 permit 192.168.20.0 0.0.0.255
access-list 1 permit 192.168.199.0 0.0.0.255

ip nat inside source list 1 interface Serial0/0/0 overload
```

### Routing

Default route:

ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

## Verification

### DHCP


show ip dhcp binding
```

### Inter-VLAN Routing

show ip interface brief
```

### PAT

show ip nat translations
show ip nat statistics
```
### SSH Management

SSH Version 2 was configured on the switch to provide secure remote administration through the Management VLAN (VLAN 199).

Management IP:

| Device | IP Address |
|----------|------------|
| SW1 | 192.168.199.2 |

Configuration:

hostname SW1

ip domain-name admin

username admin secret ccna123

crypto key generate rsa

ip ssh version 2

line vty 0 5
 exec-timeout 5
 login local
 transport input ssh
```

Verification:

show ip ssh
show users
```

Example:
ssh -l admin 192.168.199.
```

## Troubleshooting & Lessons Learned

While implementing PAT, translations were not being created even though:

- DHCP was working
- Inter-VLAN routing was operational
- Routing table was correct
- PAT configuration was correct

PAT statistics showed:

Hits: 0
Translations: 0
```

Root Cause:

`ip nat inside` was initially configured on the physical parent interface (G0/1).

Because Router-on-a-Stick uses subinterfaces for Layer 3 forwarding, NAT never processed the traffic.

Incorrect:

interface GigabitEthernet0/1
 ip nat inside
```

Correct

interface GigabitEthernet0/1.1
 ip nat inside

interface GigabitEthernet0/1.2
 ip nat inside

interface GigabitEthernet0/1.199
 ip nat inside
```

After moving NAT to the subinterfaces, PAT translations were successfully generated.

This troubleshooting process reinforced the importance of understanding packet flow and NAT processing in Router-on-a-Stick environments.


## Skills Demonstrated

- VLAN Configuration
- Router-on-a-Stick
- Inter-VLAN Routing
- DHCP Configuration
- DHCP Address Exclusions
- SSH Remote Management
- PAT (NAT Overload)
- Static Routing
- Cisco IOS Troubleshooting
- Enterprise Network Design




## Author

** ethicalkhawaja **
