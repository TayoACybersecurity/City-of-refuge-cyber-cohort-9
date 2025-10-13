title: Week 7 Lab – IP Addressing & Subnetting
author: Tayo A.
date: 2025-10-10
course: CompTIA Network+
---

## Objective
To apply IP addressing and subnetting concepts by configuring a small local network, testing connectivity, and troubleshooting common issues.

## Steps
1. Created a simulated network with three PCs and one router using Cisco Packet Tracer.  
2. Assigned static IPs and subnet masks to each device.  
3. Verified connectivity using ping and tracert commands.  
4. Introduced an intentional subnet error to test troubleshooting methods.  
5. Adjusted configurations and restored full network communication.

## Lab 1: Understanding My Home Network
Mapped all connected devices from router (192.168.1.1)
Found IoT devices: Ring doorbell, Smart TV, Alexa
Learned DHCP gives each device its own IP
Realized all devices share one network = security risk

INTERNET            
                 [ROUTER/MODEM]
                  192.168.1.1
                  (DHCP Server) 
    [Laptop] [Phone] [Smart] [Ring]  [Alexa]
   .1.45    .1.32    TV     Doorbell  .1.28
                    .1.50   .1.48
                    
    Regular Devices  |  IoT Devices (Security Risk!)

<img width="919" height="299" alt="Screenshot 2025-10-13 083955" src="https://github.com/user-attachments/assets/7d8aa664-03ab-4900-b8e7-36fdabb758c5" />  

Key Findings:

All devices on 192.168.1.0/24 subnet
IoT devices share network with personal laptop
No network segmentation = security risk
Next step: Create guest network for IoT devices

## Lab 2: Ping & Traceroute
ping 192.168.1.1 (router) ... 1ms
ping 8.8.8.8 (Google) ... 15ms  
tracert google.com ... 12 hops  
Now I know how to test network issues before calling the ISP.

C:\> ping 192.168.1.1

Pinging 192.168.1.1 with 32 bytes of data:
Reply from 192.168.1.1: bytes=32 time=1ms TTL=64
Reply from 192.168.1.1: bytes=32 time=1ms TTL=64
Reply from 192.168.1.1: bytes=32 time=2ms TTL=64
Reply from 192.168.1.1: bytes=32 time=1ms TTL=64

 Result: Excellent - Local network working perfectly

#### Internet Connection (Google DNS)

C:\> ping 8.8.8.8

Pinging 8.8.8.8 with 32 bytes of data:
Reply from 8.8.8.8: bytes=32 time=15ms TTL=117
Reply from 8.8.8.8: bytes=32 time=18ms TTL=117
Reply from 8.8.8.8: bytes=32 time=16ms TTL=117
Reply from 8.8.8.8: bytes=32 time=17ms TTL=117

Result: Good - Internet connectivity confirmed

### Traceroute Visualization

C:\> tracert google.com

Tracing route to google.com [172.217.164.110] over 12 hops:

 1    1 ms    <1 ms    1 ms   192.168.1.1         [My Router]
 2    8 ms     9 ms    8 ms   10.x.x.x            [ISP Gateway]
 3   12 ms    11 ms   12 ms   172.x.x.x           [ISP Regional]
 4   15 ms    14 ms   15 ms   x.x.x.x             [Backbone Router]
 5   16 ms    16 ms   15 ms   x.x.x.x             [Backbone Router]
 ...
12   18 ms    17 ms   18 ms   172.217.164.110     [Google Server]

Visual Path:
[My Laptop] → [Router] → [ISP] → [Regional Hub] → [Backbone] → [Google]
   (1ms)        (8ms)     (12ms)      (15ms)         (18ms)

   What I Learned:

Latency under 20ms = Great for gaming/video calls
12 hops = Typical for cross-country connection
Some routers don't respond (*** timeout) = Normal security practice


## Lab 3: ChatGPT Troubleshooting Simulation
Used AI to simulate broken network scenarios  
Diagnosed DHCP and DNS issues using the OSI model  
Practiced identifying which layer the problem sits on 

## ChatGPT Troubleshooting Simulation

### Scenario 1: No Internet Access

#### Troubleshooting Using OS
  OSI Layer        Test Performed              Result        

  Layer 7          Can browse websites?         No         
  (Application)                                               

  Layer 4          Ports open?                  Yes        
  (Transport)                                                 

  Layer 3          Valid IP address?           No 169.254.x  
  (Network)        Can ping gateway?            No         
                   ← PROBLEM FOUND HERE                       

  Layer 2          Network adapter enabled?     Yes        
  (Data Link)                                                 

  Layer 1          Cable plugged in?            Yes        
  (Physical)       Link light on?               Yes        


DIAGNOSIS: APIPA address (169.254.x.x) = DHCP failure
SOLUTION: Restart router or manually configure static IP

### Scenario 2: Can't Access Specific Website
Test 1: ping 8.8.8.8
Result:  Success (Internet works)

Test 2: ping google.com  
Result:  Failed ("could not find host")

     [My PC] can ping - [8.8.8.8] 
        can't resolve - [google.com] 
        
DIAGNOSIS: DNS resolution failure
SOLUTION: Change DNS to 8.8.8.8 (Google Public DNS)

## AI Prompts I Used:

"Act as a network troubleshooting simulator with OSI model steps"
"Give me 5 scenarios where Layer 3 is the problem"
"Create a troubleshooting flowchart for common home network issues"

## Lab 4: AI-Powered Study Partner
Used ChatGPT to simplify subnetting and network diagrams  
Example prompt: “Explain switches like I’m 12”  
Helps me learn faster and document cleaner

Subnetting Calculations (AI-Assisted)

### The Subnetting Cheat Sheet


  CIDR    Subnet Mask        Total IPs    Usable IPs    Networks  

  /24     255.255.255.0      256          254            1         
  /25     255.255.255.128    128          126            2         
  /26     255.255.255.192     64           62            4         
  /27     255.255.255.224     32           30            8         
  /28     255.255.255.240     16           14           16         
  /29     255.255.255.248      8            6           32         
  /30     255.255.255.252      4            2           64         

Formula: Usable IPs = (2^host bits) - 2
         (Subtract network address + broadcast address)

         Given: 192.168.1.0/24
Task: Create 4 equal subnets

Solution:
- Need 4 subnets → Borrow 2 bits (2² = 4)
- New subnet: /26 (24 + 2)
- Each subnet: 64 IPs (62 usable)

### Practice Problem (AI-Generated)
┌─────────────────────────────────────────────────────────────┐
 Subnet 1: 192.168.1.0/26                                    
  Network:    192.168.1.0                                   
   First Host: 192.168.1.1                                   
  Last Host:  192.168.1.62                                  
   Broadcast:  192.168.1.63                                  
├─────────────────────────────────────────────────────────────┤
 Subnet 2: 192.168.1.64/26                                   
   Network:    192.168.1.64                                  
   First Host: 192.168.1.65                                  
   Last Host:  192.168.1.126                                 
   Broadcast:  192.168.1.127                                 
├─────────────────────────────────────────────────────────────┤
 Subnet 3: 192.168.1.128/26                                  
   Network:    192.168.1.128                                 
   First Host: 192.168.1.129                                 
   Last Host:  192.168.1.190                                 
   Broadcast:  192.168.1.191                                 
├─────────────────────────────────────────────────────────────┤
 Subnet 4: 192.168.1.192/26                                  
   Network:    192.168.1.192                                 
   First Host: 192.168.1.193                                 
   Last Host:  192.168.1.254                                 
   Broadcast:  192.168.1.255                                 
└─────────────────────────────────────────────────────────────┘
## How AI Helped:

Generated 20 practice problems with solutions
Checked my calculations instantly
Explained my mistakes in simple terms

## Lab 5: IoT Home Lab Project
Noticed IoT devices share my main WiFi  
Plan to create a guest network or VLAN for them  
Goal: Understand IoT security and how AI fits into home automation

INTERNET
                  
                   [ROUTER]
                  192.168.1.1
        ┌───────────────┼───────────────┐
                                      
    [Laptop]      [Smart TV]      [Ring Doorbell]
   (Personal)      (IoT)           (IoT - Cloud)
        |               │               |
        └───── Same Network = Risk ─────┘
                        
 PROBLEM: If IoT device gets hacked, attacker is 
            on same network as my personal laptop

## Results
After resolving the subnet mismatch, all devices communicated successfully. Learned to identify IP conflicts, verify gateway settings, and confirm routes using CLI tools.

## Key Takeaway
Subnetting isn’t just math .... it’s structure. It keeps network traffic organized, efficient, and predictable.  
When it fails, everything downstream feels it.  
Lesson locked: precision in setup saves hours in troubleshooting.

**Time Spent:**
Class: 6 hrs  
Labs: 5 hrs  
Self-study: 8 hrs  
Networking: 5 hrs  
Total = 25 hrs
