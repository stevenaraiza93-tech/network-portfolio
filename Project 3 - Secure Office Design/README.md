# Project 3: Secure Office Network Segmentation Lab

## Overview

This project demonstrates a secure office network design that includes VLAN segmentation, inter-VLAN routing, ACLs, DHCP, DNS, HTTP, FTP, printers, and a management VLAN. The goal of this lab is to simulate a business network where different departments and resources require controlled access.

This project focuses on both network functionality and security. Users need access to required services, but traffic between sensitive departments must be restricted.

## Scenario

A business office needs a secure internal network that separates departments, supports shared services, allows printer access, and provides IT with administrative control. Guest users must be isolated, and sensitive departments must be protected from unauthorized access.

## Objectives

- Design a segmented office network
- Configure VLANs for departments, servers, printers, guest access, and management
- Configure inter-VLAN routing
- Configure DHCP services for user networks
- Configure DNS, HTTP, and FTP services
- Apply ACLs to restrict unauthorized traffic
- Preserve IT administrative access
- Verify service access and security controls

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS CLI
- VLANs
- Trunking
- Inter-VLAN routing
- ACLs
- DHCP
- DNS
- HTTP
- FTP
- Printer and server network design
- Management VLAN

## Skills Demonstrated

- Office network design
- VLAN segmentation
- ACL-based access control
- DHCP scope configuration
- DNS record configuration
- Server and printer integration
- Guest network isolation
- Management VLAN planning
- Troubleshooting and validation

## Validation and Testing

I verified the design by confirming:

- Department VLANs were properly segmented
- DHCP assigned addresses correctly
- DNS resolved configured records
- HTTP and FTP services were reachable where allowed
- Guest traffic was isolated from internal resources
- HR-to-Finance traffic was blocked
- IT retained administrative access
- ACLs were applied in the correct direction and location

Useful verification commands included:

```bash
show vlan brief
show interfaces trunk
show ip interface brief
show access-lists
show running-config
ping
```

## Troubleshooting Example

I used `show access-lists` and interface verification commands to confirm ACL placement and packet filtering behavior. This helped verify that denied traffic was blocked while approved traffic continued to work.

## Real-World Use Case

This type of design is commonly used in schools, offices, and small businesses where users, servers, printers, guests, and IT administrators need different levels of access. Network segmentation helps reduce risk and makes the network easier to manage.

## Files Included

- Packet Tracer lab file
- Topology screenshot
- VLAN and trunk screenshot
- Interface and ACL configuration screenshot
- Configuration files

## What I Learned

This lab helped me connect multiple networking concepts into one realistic design. It reinforced the importance of planning VLANs, IP addressing, service access, and ACL rules before implementation.
