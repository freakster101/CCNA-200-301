# 🌐 Life of a Packet

## 🎯 Objectives

- Understand how a packet travels to a remote network.
- Review ARP, routing, encapsulation, and de-encapsulation.
- Understand which addresses change at each hop.

---

# 📖 Life of a Packet

When a host sends data to a device in another network, it sends the frame to its **default gateway**.

The destination IP remains the final destination's IP address, while the destination MAC address is the MAC address of the next-hop device.

### Example Path

```text
PC1 → R1 → R2 → R4 → PC4
```

## 🔹 ARP and the Default Gateway

Before PC1 can send the frame to R1, it must learn R1's MAC address.

It sends an ARP request using:

```text
Destination MAC: FFFF.FFFF.FFFF
```

The ARP reply is sent as a unicast frame.

PC1 then stores the mapping in its ARP table and sends the packet to R1.

## 🔹 Router Processing

At each router, the same process occurs:

1. The router removes the incoming Ethernet header and trailer.
2. It checks the destination IP address.
3. It searches the routing table for the longest prefix match.
4. It uses ARP if the next-hop MAC address is unknown.
5. It creates a new Ethernet frame and forwards the packet.

## 🔹 What Changes at Each Hop?

| Field | Changes? |
|---|---|
| Source IP | No |
| Destination IP | No |
| Source MAC | Yes |
| Destination MAC | Yes |
| Ethernet frame | Rebuilt by each router |

The IP packet stays mostly unchanged from source to destination.

The Ethernet header changes at every routed hop because each link has a different source and destination MAC address.

## 🔹 Role of Switches

Switches forward frames using their MAC address tables.

They learn source MAC addresses but do not remove and rebuild the Ethernet frame like routers do.

## 🔹 Return Traffic

When PC4 replies to PC1, the same forwarding process happens in reverse.

If ARP entries already exist, the devices can send the frames without repeating the ARP request and reply process.

## 📝 Summary

- Remote traffic is first sent to the default gateway.
- ARP resolves the MAC address of the next-hop device.
- Routers de-encapsulate, route, and re-encapsulate packets at every hop.
- Source and destination IP addresses remain the same.
- Source and destination MAC addresses change at every routed hop.
- Switches forward frames but do not rebuild them.