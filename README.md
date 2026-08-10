# Enterprise Network Security Infrastructure

> Multi-site enterprise network built with FortiGate, Cisco networking, and PNETLab.

## Overview

This project is a complete enterprise network security lab designed to simulate a real-world multi-site organization with a centralized Headquarters and multiple branches.

The architecture combines network infrastructure, segmentation, routing, firewall security, High Availability, and site-to-site VPN connectivity in a single PNETLab environment.

### Core Objectives

- Design a scalable enterprise network architecture
- Segment internal traffic using VLANs
- Implement Inter-VLAN routing
- Configure static routing across multiple sites
- Build FortiGate High Availability at HQ
- Establish secure site-to-site IPsec connectivity
- Implement centralized firewall security controls
- Validate connectivity and security through practical testing

---

## Architecture

The environment consists of three major sites:

```text
                         Internet / WAN
                              |
                +-------------+-------------+
                |                           |
             HQ Edge                     Branch WAN
                |                     /             \
          +-----+-----+             BR1             BR2
          |           |
   HQ-FW-Primary   HQ-FW-Secondary
       ACTIVE          PASSIVE
          |
       HA Cluster
          |
      HQ Core Switch
       /    |     \
      /     |      \
 Users   Servers   Management
 VLAN 10  VLAN 20   VLAN 30
Headquarters
ISP / WAN connectivity
Edge Router
FortiGate Active-Passive HA Cluster
Core Switch
Access Switches
Users Network
Servers Network
Management Network
Branch 1
ISP / WAN connectivity
Edge Router
FortiGate Firewall
Users Network
Servers Network
Branch 2
ISP / WAN connectivity
Edge Router
FortiGate Firewall
Users Network
Servers Network
Topology

The complete PNETLab topology is available in the .unl file.

Network Segmentation

The HQ network uses VLAN-based segmentation to separate different security zones.

VLAN	Purpose	Network	Gateway
VLAN 10	Users	192.168.10.0/24	192.168.10.1
VLAN 20	Servers	192.168.20.0/24	192.168.20.1
VLAN 30	Management	192.168.30.0/24	192.168.30.1

Segmentation provides logical separation between users, servers, and management traffic and allows security policies to be applied between network zones.

IP Addressing

The network uses private RFC1918 addressing with a structured addressing plan.

HQ
Network	Purpose
192.168.10.0/24	HQ Users
192.168.20.0/24	HQ Servers
192.168.30.0/24	HQ Management
Branch 1
Network	Purpose
192.168.110.0/24	Branch 1 Users
192.168.120.0/24	Branch 1 Servers
WAN

Point-to-point WAN links use /30 networks.

The addressing strategy provides:

Non-overlapping site networks
Predictable routing
Clear network boundaries
Easier troubleshooting
Future expansion capability
Routing Architecture

Static routing is used across the current topology.

The routing design provides connectivity between:

HQ internal networks
Branch networks
WAN transit networks
Internet-facing networks
VPN-connected networks

Static routing was selected because the current topology is relatively small and the traffic paths are predictable.

High Availability

HQ uses two FortiGate firewalls configured in an Active-Passive HA cluster.

                    HQ Network
                        |
             +----------+----------+
             |                     |
       HQ-FW-Primary        HQ-FW-Secondary
           ACTIVE                PASSIVE
             |
          HA Sync
HA Design Goals
Firewall redundancy
Configuration synchronization
Failover capability
Improved availability
Reduced single point of failure

The HA cluster was validated with both members synchronized and operating in Active-Passive mode.

Site-to-Site IPsec VPN

Secure site-to-site communication is implemented using IPsec VPN.

HQ ↔ Branch 1
HQ Networks
192.168.10.0/24
192.168.20.0/24
       |
     IPsec
       |
Branch 1 Networks
192.168.110.0/24
192.168.120.0/24

The VPN design provides secure connectivity between corresponding network segments.

Configured VPN technology includes:

IKEv2
IPsec
Pre-shared key authentication
DH Group 14
Phase 1 / Phase 2 negotiation
Security Architecture

FortiGate acts as the primary security enforcement point for the enterprise environment.

Security Controls
Control	Purpose
Firewall Policies	Traffic filtering and access control
NAT	Internet address translation
VIP	Published services
IPS	Intrusion prevention
Antivirus	Malware inspection
Web Filtering	Web access control
Application Control	Application-level filtering
IPsec VPN	Secure site-to-site connectivity
VLAN Segmentation	Network isolation

The security architecture is based on controlled communication between defined network zones.

Technologies
Network Infrastructure
Cisco Networking Devices
VLAN
802.1Q Trunking
Inter-VLAN Routing
Static Routing
DHCP
WAN Connectivity
Security
FortiGate-VM64-KVM
FortiGate HA
Firewall Policies
NAT
VIP
IPS
Antivirus
Web Filtering
Application Control
IPsec VPN
Lab Environment
PNETLab
FortiGate-VM64-KVM
Virtualized Network Devices
Verification & Testing

The implementation was validated through practical network and security testing.

Testing areas include:

Interface connectivity
VLAN communication
Inter-VLAN routing
Static routing
HQ-to-Branch connectivity
IPsec tunnel status
FortiGate HA status
Firewall policy behavior
Security inspection
Network reachability

Detailed testing evidence and CLI outputs are available in the project documentation.

Repository Structure
HQ-Enterprise-Security/
│
├── README.md
│
├── HQ_Enterprise_1786111675435_1786121515211.unl
│
├── Enterprise-Network-Security-Report.docx
│
└── screenshots/
    └── topology.png
Running the Lab
Requirements
PNETLab
Required FortiGate images
Required Cisco/network images
The provided .unl topology
Deployment
Import the .unl file into PNETLab.
Verify that all required network images are installed.
Start the complete topology.
Verify device interfaces.
Verify VLAN configuration.
Verify routing tables.
Verify FortiGate HA status.
Verify IPsec VPN status.
Perform the connectivity tests documented in the report.
Documentation

The complete technical documentation is available in:

Enterprise-Network-Security-Report.docx

The report contains the detailed:

Network architecture
IP addressing
VLAN design
Routing configuration
Firewall configuration
VPN configuration
HA configuration
Security controls
Testing results
Implementation evidence
Project Team
Enterprise Infrastructure Engineer

Responsible for:

HQ infrastructure
Core switching
Access switching
VLAN design
DHCP
Inter-VLAN routing
HQ static routing
HA interface preparation
WAN & Connectivity Engineer

Responsible for:

Branch 1
Branch 2
WAN connectivity
IPsec VPN
Remote VPN
Routing
HA configuration
Security Engineer

Responsible for:

Firewall policies
NAT
VIP
IPS
Antivirus
Web Filtering
Application Control
Security testing
Documentation
Project Status

The repository currently includes:

PNETLab topology
Technical project documentation
Network topology visualization
Network architecture
IP addressing information
Security architecture
Deployment instructions

The technical report should be referenced for detailed configuration and testing evidence.

Disclaimer

This project was developed in a controlled lab environment for educational and practical network engineering and cybersecurity purposes.