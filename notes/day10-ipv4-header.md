# 🌐 Day10 - IPv4 Header

## 🎯 Objectives

- Understand the structure of an IPv4 packet.
- Learn the purpose of each IPv4 header field.
- Understand IPv4 fragmentation and reassembly.
- Learn how TTL prevents routing loops.
- Identify important protocol numbers.
- Understand how IPv4 detects errors.
- Interpret IPv4 packets in Wireshark.

---

# 📖 Main Topic

## 🔹 IPv4 Packet Structure

An IPv4 packet is created when the Layer 3 (IP) header is added to a Layer 4 segment (TCP/UDP).

| OSI Layer | PDU | Encapsulation |
|-----------|-----|---------------|
| Layer 4 | Segment | L4 Header + Data |
| Layer 3 | Packet | IPv4 Header + Segment |
| Layer 2 | Frame | L2 Header + Packet + Trailer |

The IPv4 header contains the information routers use to forward packets across different networks.

---

## 🔹 IPv4 Header Overview

| Field | Size | Purpose |
|--------|------|---------|
| Version | 4 bits | IP version |
| IHL | 4 bits | Header length |
| DSCP | 6 bits | Quality of Service (QoS) |
| ECN | 2 bits | Congestion notification |
| Total Length | 16 bits | Entire packet length |
| Identification | 16 bits | Fragment identification |
| Flags | 3 bits | Fragmentation control |
| Fragment Offset | 13 bits | Fragment position |
| TTL | 8 bits | Prevent routing loops |
| Protocol | 8 bits | Encapsulated Layer 4 protocol |
| Header Checksum | 16 bits | Header error detection |
| Source IP Address | 32 bits | Sender IP |
| Destination IP Address | 32 bits | Receiver IP |
| Options | 0–320 bits | Optional features (rarely used) |

---

## 🔹 Version Field

**Length:** 4 bits

Identifies the IP version carried in the packet.

| Version | Binary |
|----------|--------|
| IPv4 | 0100 |
| IPv6 | 0110 |

### Important CCNA Facts

- IPv4 packets always contain **4**.
- IPv6 packets always contain **6**.

---

## 🔹 Internet Header Length (IHL)

**Length:** 4 bits

Specifies the size of the IPv4 header in **4-byte increments**.

| IHL Value | Header Size |
|-----------|-------------|
| 5 | 20 Bytes (Minimum) |
| 15 | 60 Bytes (Maximum) |

### Important CCNA Facts

- Minimum IPv4 header = **20 bytes**
- Maximum IPv4 header = **60 bytes**
- Extra size comes from the **Options** field.

---

## 🔹 DSCP (Differentiated Services Code Point)

**Length:** 6 bits

Used for **Quality of Service (QoS)**.

Allows important traffic such as:

- Voice
- Video
- Real-time applications

to receive higher priority than normal traffic.

---

## 🔹 ECN (Explicit Congestion Notification)

**Length:** 2 bits

Provides end-to-end notification of network congestion **without dropping packets**.

### Important CCNA Facts

- Optional feature
- Requires support from both endpoints and the network

---

## 🔹 Total Length

**Length:** 16 bits

Specifies the total size of the IPv4 packet.

Includes:

- IPv4 Header
- Layer 4 Header
- Encapsulated Data

Measured in **bytes**, not 4-byte increments.

| Value | Meaning |
|--------|---------|
| Minimum | 20 Bytes |
| Maximum | 65,535 Bytes |

---

## 🔹 Identification Field

**Length:** 16 bits

Used during packet fragmentation.

Every fragment created from the same packet shares the **same Identification value**, allowing the destination host to reassemble the original packet.

### Important CCNA Facts

- Fragmentation occurs when packet size exceeds the **MTU**.
- Typical Ethernet MTU = **1500 bytes**.
- Fragments are reassembled **only by the destination host**.

---

## 🔹 Flags Field

**Length:** 3 bits

Controls fragmentation.

| Bit | Name | Purpose |
|-----|------|---------|
| 0 | Reserved | Always 0 |
| 1 | DF (Don't Fragment) | Prevents fragmentation |
| 2 | MF (More Fragments) | Indicates more fragments follow |

### Important CCNA Facts

- **DF = 1** → Packet cannot be fragmented.
- **MF = 1** → More fragments follow.
- **MF = 0** → Last fragment or unfragmented packet.

---

## 🔹 Fragment Offset

**Length:** 13 bits

Specifies the fragment's position within the original packet.

This allows fragments to be correctly reassembled even if they arrive out of order.

---

## 🔹 Time To Live (TTL)

**Length:** 8 bits

Prevents packets from looping forever.

Every router that forwards a packet:

- Decreases TTL by **1**
- Drops the packet when TTL reaches **0**

### Example

```
PC → R1 → R2 → R3 → Server

TTL = 64

After R1 → 63

After R2 → 62

After R3 → 61
```

### Important CCNA Facts

- Prevents routing loops.
- Recommended default TTL = **64**.

---

## 🔹 Protocol Field

**Length:** 8 bits

Identifies the encapsulated Layer 4 (or other Layer 3) protocol.

| Value | Protocol |
|--------|----------|
| 1 | ICMP |
| 6 | TCP |
| 17 | UDP |
| 89 | OSPF |

### CCNA Memorization

| Protocol | Number |
|-----------|--------|
| ICMP | 1 |
| TCP | 6 |
| UDP | 17 |
| OSPF | 89 |

---

## 🔹 Header Checksum

**Length:** 16 bits

Detects errors **only in the IPv4 header**.

When a router receives a packet:

1. Calculates the checksum.
2. Compares it with the received checksum.
3. Drops the packet if they differ.

### Important CCNA Facts

- Does **not** check payload errors.
- TCP and UDP provide their own checksums for encapsulated data.

---

## 🔹 Source and Destination IP Address

**Length:** 32 bits each

| Field | Purpose |
|--------|---------|
| Source Address | Sender's IPv4 address |
| Destination Address | Receiver's IPv4 address |

Routers use the **destination IP address** to determine where to forward the packet.

---

## 🔹 Options Field

**Length:** 0–320 bits (0–40 bytes)

Rarely used optional field that extends the IPv4 header.

### Important CCNA Facts

- Present only when **IHL > 5**.
- Variable-length field.
- Maximum size = **40 bytes**.

---

## 🔹 IPv4 Fragmentation

Fragmentation occurs when a packet exceeds the outgoing interface's **MTU**.

Each fragment contains:

- Its own IPv4 header
- Same Identification value
- Different Fragment Offset
- Appropriate MF flag

### Example

Original Packet = 4000 Bytes

MTU = 1500 Bytes

Result:

| Fragment | MF | Offset |
|----------|----|--------|
| 1 | 1 | 0 |
| 2 | 1 | Next Offset |
| 3 | 0 | Final Offset |

---

## 🔹 DF and MF Bits

### Don't Fragment (DF)

```
DF = 1
```

Packet **must not** be fragmented.

If packet exceeds MTU:

- Router drops packet.
- ICMP "Fragmentation Needed" message is typically generated.

---

### More Fragments (MF)

```
MF = 1
```

Indicates additional fragments follow.

```
MF = 0
```

Indicates the last fragment (or packet was never fragmented).

---

## 🔹 Wireshark Analysis

Wireshark displays every IPv4 header field, making it an excellent troubleshooting tool.

Useful fields to inspect:

- Version
- IHL
- DSCP
- ECN
- Total Length
- Identification
- DF/MF flags
- Fragment Offset
- TTL
- Protocol
- Header Checksum
- Source IP
- Destination IP

### Practical Troubleshooting

Use Wireshark to:

- Detect fragmentation.
- Verify TTL values.
- Confirm protocol numbers.
- Identify checksum errors.
- Analyze packet forwarding.

---

## 📝 Exam Tips

- IPv4 Version field = **4 (0100)**.
- Minimum IPv4 header = **20 bytes**.
- Maximum IPv4 header = **60 bytes**.
- IHL is measured in **4-byte increments**.
- Total Length is measured in **bytes**.
- Ethernet MTU is usually **1500 bytes**.
- Fragments share the same **Identification** value.
- **DF** prevents fragmentation.
- **MF** is set on all fragments except the last.
- Routers decrement **TTL** by 1.
- Packet is discarded when **TTL = 0**.
- Header Checksum protects **only the IPv4 header**.
- TCP and UDP protect the payload with their own checksums.
- Memorize protocol numbers:
  - ICMP = **1**
  - TCP = **6**
  - UDP = **17**
  - OSPF = **89**
- Options is the **only variable-length field** in the IPv4 header.

---

# 📚 Summary

- IPv4 uses a structured Layer 3 header to route packets across networks.
- The Version and IHL fields identify the protocol version and header size.
- DSCP and ECN support QoS and congestion management.
- Total Length specifies the complete packet size.
- Identification, Flags, and Fragment Offset enable packet fragmentation and reassembly.
- TTL prevents infinite routing loops by decrementing at each router.
- The Protocol field identifies the encapsulated protocol, such as TCP, UDP, ICMP, or OSPF.
- Header Checksum verifies only the integrity of the IPv4 header.
- Source and Destination IP fields identify the communicating devices.
- The Options field is optional and rarely used.
- Wireshark is an essential tool for viewing IPv4 header fields and troubleshooting packet behavior.

---
