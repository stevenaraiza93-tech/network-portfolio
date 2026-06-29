# Spanning Tree Protocol (STP) Fundamentals

## Overview

Spanning Tree Protocol (STP) prevents Layer 2 switching loops while still allowing network redundancy. Redundant switch links are useful for backup paths, but without STP, they can create broadcast storms that can slow down or crash an entire network.

## Why STP Is Needed

Adding multiple links between switches creates redundancy, but it also creates a loop. When a broadcast frame, such as a DHCP request, enters a looped switch network, switches continue forwarding it endlessly.

This can cause a **broadcast storm**, where frames multiply across the network until devices become unreachable.

## Layer 2 vs Layer 3 Loop Prevention

Routers use **TTL (Time to Live)** to prevent packets from looping forever at Layer 3. Each router hop lowers the TTL value until the packet is dropped.

Switches operate at **Layer 2** and forward frames based on MAC addresses. Layer 2 frames do not use TTL, so a switching loop can continue until the loop is physically broken or STP blocks it.

## What STP Does

STP analyzes the switch topology and blocks redundant links that could create loops.

The blocked links are not removed. They remain available as backup paths. If an active link fails, STP can unblock a backup path to restore connectivity.

## Key STP Terms

### Root Bridge

The **root bridge** is the central switch in the STP topology. All switches calculate their best path toward the root bridge.

The switch with the lowest **Bridge ID** becomes the root bridge.

### Bridge ID

The Bridge ID is made of:

- Bridge priority
- Switch MAC address

By default, Cisco switches use a priority of **32768**. If priorities tie, the switch with the lowest MAC address wins.

### BPDU

**BPDU** stands for Bridge Protocol Data Unit. Switches use BPDUs to exchange STP information, elect the root bridge, detect topology changes, and prevent loops.

## STP Port Roles

### Root Port

The best port on a non-root switch used to reach the root bridge.

Each non-root switch has one root port.

### Designated Port

A forwarding port on a network segment. The root bridge has all designated ports.

### Blocked Port

A port that does not forward user traffic because it would create a loop. It still listens for BPDUs.

## How STP Chooses Ports

STP uses these rules in order:

1. Lowest path cost to the root bridge
2. Lowest bridge ID
3. Lowest port number

Lower cost paths are preferred. Faster links have lower costs.

Common STP costs:

- 100 Mbps = 19
- 1 Gbps = 4

## STP Port States

Classic STP ports move through several states before forwarding traffic:

### Blocking

The port does not forward traffic. It only listens for BPDUs.

### Listening

The switch listens for BPDUs and determines the STP topology.

### Learning

The switch builds its MAC address table but still does not forward user traffic.

### Forwarding

The port forwards traffic normally.

Classic STP can take around **30 to 50 seconds** to recover from changes, which is slow for modern networks.

## PVST

Cisco switches commonly use **PVST**, or Per-VLAN Spanning Tree.

PVST runs a separate STP instance for each VLAN. This allows different VLANs to use different root bridges and can help with load balancing.

Example:

```bash
show spanning-tree
```

## Configuring the Root Bridge

It is best practice to manually control which switch becomes the root bridge.

Set the priority manually:

```bash
spanning-tree vlan 1 priority 4096
```

Or use Cisco shortcut commands:

```bash
spanning-tree vlan 1 root primary
spanning-tree vlan 1 root secondary
```

For multiple VLANs:

```bash
spanning-tree vlan 1,10,20 root primary
```

## Rapid Spanning Tree Protocol

**Rapid Spanning Tree Protocol (RSTP)** is a faster version of STP.

RSTP uses the same basic logic as STP, but it converges much faster. Instead of waiting up to 50 seconds, RSTP can recover in a few seconds or less.

On Cisco switches, enable Rapid PVST+ with:

```bash
spanning-tree mode rapid-pvst
```

## Multiple Spanning Tree

**MST**, or Multiple Spanning Tree, is used in larger networks with many VLANs.

Instead of running one STP instance per VLAN, MST allows multiple VLANs to share the same spanning tree instance. This reduces switch CPU usage and scales better in enterprise environments.

## PortFast

**PortFast** allows access ports connected to end devices to skip STP listening and learning states and move directly to forwarding.

Use PortFast on ports connected to:

- Computers
- Printers
- IP phones
- Access points
- Other end devices

Enable PortFast on an interface:

```bash
spanning tree portfast
```

Enable PortFast globally on access ports:

```bash
spanning tree portfast default
```

## BPDU Guard

**BPDU Guard** protects access ports from accidental switch connections.

If a PortFast-enabled port receives a BPDU, BPDU Guard places the port into an error-disabled state. This helps prevent loops caused by unmanaged switches or incorrect cabling.

Enable BPDU Guard globally on PortFast ports:

```bash
spanning tree portfast bpduguard default
```

Recover an error-disabled port:

```bash
interface fa0/1
shutdown
no shutdown
```

## Real-World Best Practices

- Always manually set the root bridge and backup root bridge
- Use Rapid PVST+ instead of classic STP when possible
- Enable PortFast on end-device access ports
- Enable BPDU Guard on PortFast ports
- Never connect unmanaged switches without approval
- Verify STP before adding redundant links
- Use `show spanning-tree` to confirm STP behavior

## Useful Commands

```bash
show spanning-tree
show spanning-tree vlan 1
show interfaces status
show interfaces trunk
show running-config
show interfaces
```

## Key Takeaways

- Redundant switch links can create Layer 2 loops
- Layer 2 loops can cause broadcast storms
- STP prevents loops by blocking redundant paths
- The root bridge controls the STP topology
- STP chooses paths using cost, bridge ID, and port number
- Rapid PVST+ is faster than classic STP
- PortFast speeds up end-device ports
- BPDU Guard protects the network from accidental loops
