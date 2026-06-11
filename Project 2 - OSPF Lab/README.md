# Project 2: Multi-Site OSPF Routing Lab

## Overview

This project demonstrates a multi-router network using OSPF for dynamic routing. The lab includes three routers connected across different networks, with OSPF used to advertise routes and allow communication between sites.

The purpose of this project is to show how dynamic routing protocols reduce the need for manual static routes and allow routers to automatically learn network paths.

## Scenario

A company has multiple locations connected through routers. Each site has its own local network, and the routers must exchange routes dynamically so users at each site can communicate with resources at other locations.

## Objectives

- Configure IP addressing on router interfaces
- Enable OSPF on all routers
- Advertise connected networks into OSPF
- Verify OSPF neighbor relationships
- Confirm route learning across the topology
- Troubleshoot OSPF adjacency and routing issues

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS CLI
- OSPF
- IPv4 addressing
- Point-to-point router links
- Dynamic routing verification

## Skills Demonstrated

- OSPF configuration
- Network statement configuration
- Router interface addressing
- OSPF neighbor verification
- Routing table analysis
- Cross-site connectivity testing
- Troubleshooting subnet and routing issues

## Validation and Testing

I verified OSPF operation by checking:

- Router interface status
- OSPF neighbor relationships
- Learned routes in the routing table
- End-to-end connectivity between networks

Useful verification commands included:

```bash
show ip interface brief
show ip ospf neighbor
show ip route
show running-config
ping
```

## Troubleshooting Example

One issue encountered during the lab was that OSPF neighbors were not forming between two routers. After checking interface status and reviewing the running configuration, I found a subnet mask mismatch on the point-to-point link.

The issue was corrected by updating the interface subnet mask so both routers were in the same network. After the correction, the OSPF neighbor relationship formed successfully and routes were exchanged.

## Real-World Use Case

OSPF is commonly used in enterprise networks where multiple routers need to dynamically share route information. This lab demonstrates the foundation of how branch offices, departments, or network segments can communicate without relying only on static routes.

## Files Included

- Packet Tracer lab file
- Network topology screenshot
- Router interface screenshots
- OSPF neighbor verification screenshots

## What I Learned

This lab improved my understanding of OSPF neighbor formation, network advertisements, routing table verification, and how small configuration errors such as subnet mismatches can prevent routing protocols from working correctly.
