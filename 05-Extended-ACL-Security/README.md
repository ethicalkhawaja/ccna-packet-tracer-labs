# Extended ACL Security Lab

## Project Overview

This project demonstrates the implementation of Cisco Extended Access Control Lists (ACLs) to secure access to critical network resources within a segmented enterprise environment.

The network consists of multiple VLANs representing different departments. Access to the corporate server is restricted through Extended ACL policies configured on Router R1.

The lab showcases how network administrators can enforce least-privilege access by allowing only specific hosts and subnets to communicate with sensitive resources.

---

## Network Topology

### VLAN Structure

| VLAN | Department | Network |
|--------|------------|------------|
| VLAN 10 | HR | 192.168.1.0/24 |
| VLAN 20 | Sales | 192.168.2.0/24 |
| VLAN 30 | Home | 192.168.3.0/24 |
| Server Network | Corporate Services | 192.168.100.0/24 |

---

## IP Addressing Scheme

| Device | IP Address |
|----------|------------|
| HR-PC | 192.168.1.1 |
| SalesPC1 | 192.168.2.1 |
| SalesPC2 | 192.168.2.2 |
| Home-PC1 | 192.168.3.1 |
| Home-PC2 | 192.168.3.2 |
| Server | 192.168.100.10 |

---

## Router Interfaces

| Interface | Address |
|------------|-----------|
| G0/0 | 192.168.100.254 |
| G0/1.1 | 192.168.1.254 |
| G0/1.3 | 192.168.3.254 |
| G0/2.1 | 192.168.2.254 |

---

## Security Objective

Protect the corporate server by permitting access only from authorized hosts and departments.

### Authorized Access

| Source | Destination |
|----------|-------------|
| HR VLAN (192.168.1.0/24) | Server |
| SalesPC2 (192.168.2.2) | Server |
| Home-PC1 (192.168.3.1) | Server |

### Restricted Access

- SalesPC1 is denied access to the server.
- Home-PC2 is denied access to the server.
- Any device not explicitly permitted is denied by the implicit ACL deny rule.

---

## Extended ACL Configuration

```cisco
ip access-list extended OFFICE

20 permit ip host 192.168.2.2 host 192.168.100.10

30 permit ip 192.168.1.0 0.0.0.255 host 192.168.100.10

40 permit ip host 192.168.3.1 host 192.168.100.10
```

---

## Verification Commands

### View ACL

show access-lists
```

### Verify Interfaces

show ip interface brief
```

### Test Connectivity

ping 192.168.100.10
```

Expected Results:

| Device |   Result |
|----------|---------|
| HR-PC |   Success |
| SalesPC2 | Success |
| Home-PC1 | Success |
| SalesPC1 | Blocked |
| Home-PC2 | Blocked |

---

## Technologies Used

- Cisco IOS
- VLAN Segmentation
- Extended ACLs
- Inter-VLAN Routing
- IPv4 Networking
- Network Security

---

## Skills Demonstrated

- Network Access Control
- Extended ACL Design
- Cisco Router Configuration
- Traffic Filtering
- Enterprise Security Policy Enforcement
- Network Segmentation

---

## Learning Outcomes

This lab demonstrates how Extended ACLs can be used to implement granular security policies by filtering traffic based on:

- Source IP Address
- Destination IP Address
- Specific Hosts
- Entire Subnets

The implementation follows the principle of least privilege, allowing only approved devices to access sensitive corporate resources.

---

## Author

** ethicalkhawaja **