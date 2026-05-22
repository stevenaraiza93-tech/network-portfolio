Lab 2 – OSPF Multi-Router Routing

Project Name: Multi-Site OSPF Routing Lab

Objective: Build a dynamic routing environment across three routers

What I Configured: OSPF, interface addressing, route advertisement

Validation: Verified OSPF neighbors and cross-site connectivity

Challenge: One network statement was missing, preventing route learning

Fix: Added the missing OSPF network

Outcome: Demonstrated dynamic route exchange and failover awareness

Issue I encountered:
Issue: OSPF neighbors were not forming between R1 and R2.
Cause: Subnet mask mismatch on the R1–R2 point-to-point link. R1 used /30 while R2 used /24sho 

Troubleshooting: Verified interface status with show ip interface brief, then compared interface configuration using show running-config.
Resolution: Corrected R2 G0/0 to 255.255.255.252 and restarted the OSPF process

