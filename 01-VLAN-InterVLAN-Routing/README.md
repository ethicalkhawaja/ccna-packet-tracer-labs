# CCNA Packet Tracer Lab 1: VLAN + Inter-VLAN Routing

## 📌 Overview
This lab demonstrates VLAN creation and Inter-VLAN routing using Cisco Packet Tracer. It simulates a small enterprise network using router-on-a-stick configuration.

---

## 🧠 Objectives
- Create and configure VLANs on a switch
- Assign switch ports to VLANs
- Configure trunk link between switch and router
- Enable Inter-VLAN routing using router subinterfaces
- Test connectivity between VLANs using ping

---

## 🏗️ Topology
- 1 Router (R1)
- 1 Switch (SW1)
- 3 VLANs (10, 20, 30)
- Multiple PCs connected to different
- ![Topology][topology.png]


---

## 🧾 VLAN Details

### VLAN 10 - Guest
- Network: 192.168.10.0/24
- Gateway: 192.168.10.254

### VLAN 20 - Sales
- Network: 192.168.20.0/24
- Gateway: 192.168.20.254

### VLAN 30 - IT
- Network: 192.168.30.0/24
- Gateway: 192.168.30.254

---

## ⚙️ Technologies Used
- Cisco Packet Tracer
- VLANs (802.1Q)
- Router-on-a-Stick
- Inter-VLAN Routing

---

## 📸 Screenshots
- Topology Diagram
- VLAN Configuration
- Router Configuration
- Trunkport Status
- Ping Test (Connectivity Verification)

---

## ✅ Verification
- PCs in same VLAN can communicate
- PCs in different VLANs communicate via router
- All VLANs are properly segmented

---

## 🎯 Purpose
To build practical networking skills for CCNA-level understanding and real-world IT/networking roles.

---

## 👨‍💻 Author
ethicalkhawaja (CCNA Student - Networking Practice Labs)
