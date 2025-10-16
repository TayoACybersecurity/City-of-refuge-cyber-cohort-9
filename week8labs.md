# Week 8 Lab – Network Devices, VLANs & Real-World Asset Management  
**Author:** Tayo A.  
**Date:** 2025-10-14  
**Course:** CompTIA Network+  


## Objective  
To understand how switches, VLANs, and network segmentation improve performance and security ... and apply asset management concepts through real-world volunteer work at Inspiredu.


## Steps  

### Lab 1: Managed vs Unmanaged Switch  
1. Compared managed and unmanaged switches in Packet Tracer.  
2. Learned how managed switches support VLANs, PoE, and SNMP monitoring.  
3. Configured VLANs to separate IoT and user devices.  
4. Verified segmentation with ping tests across VLANs.  

**Key Takeaway:**  
Unmanaged switches = plug and play.  
Managed switches = visibility, control, and security.  


### Lab 2: VLAN Configuration  
Created two VLANs:  
 **VLAN 10 – Admin Devices**  
 **VLAN 20 – IoT Devices**  

Assigned ports and tested communication:  
 Devices on VLAN 10 could ping each other.  
 VLAN 10 ↔ VLAN 20 blocked by design (security success).  
 Used router-on-a-stick setup to allow controlled inter-VLAN routing.  

**Lesson Learned:**  
> Network segmentation = digital neighborhoods. Keeps noise and threats contained.  


### Lab 3: Network+ Meets Real Life (Inspiredu Volunteer Event)  
Volunteered with **City of Refuge Cyber Cohort 9** at **Inspiredu**, helping reimage and organize donated computers for underserved families.  

Tasks completed:  
 Logged devices into **asset inventory sheets** (tracking serials, conditions, and OS).  
 Assisted in **reimaging** systems and confirming software readiness.  
 Ensured **data wipe verification** before redeployment.  
 Practiced GRC basics — **asset control, documentation, and risk mitigation** through clean recordkeeping.  

> Felt like small-scale enterprise asset management — only this time, every machine restored meant a child or adult gaining digital access.  


### Lab 4: Command Line Drills  
Ran and documented key commands:  

ipconfig /all
ping 192.168.10.1
tracert 8.8.8.8
netstat -an

Learned how to identify open ports, IP conflicts, and gateway routes.  
**Noted:** Physical layer errors often hide as “network” problems — always check cables first.  


### Lab 5: PoE & Network Devices in Action  
Explored how Power over Ethernet works.  
Simulated powering IP cameras and access points using a PoE-enabled switch.  

**Advantages:**  
 One cable for data + power (less clutter).  
 Easier deployment for cameras and APs.  
 Centralized power management.  

**Drawbacks:**  
 Higher switch cost.  
 Power limits per port.  


## Results  
 VLANs improved logical isolation and simplified troubleshooting.  
 Asset tracking and documentation skills from Inspiredu directly connect to **GRC frameworks** like NIST CSF and ITIL asset lifecycle.  
 Developed stronger understanding of how technical + administrative controls work together.  

## Key Takeaway  
Networking isn’t just cables and IPs — it’s structure, accountability, and people.  
This week bridged **technical practice (VLANs, PoE)** with **governance in action (asset management)**.  

> Whether in a lab or a community center, organization is the backbone of security.  

**Time Spent:**  
 Class: 5 hrs  
 Labs: 6 hrs  
 Volunteer (Inspiredu): 4 hrs  
 Self-Study: 7 hrs  
 Networking: 3 hrs  
**Total = 25 hrs**
