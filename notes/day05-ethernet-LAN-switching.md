# 🌐 Day 05 - Ethernet LAN Switching (Part 1)

## 🎯 Objectives

After completing this topic, you should be able to:

- Review the roles of the Physical and Data Link layers.
- Explain what a Local Area Network (LAN) is.
- Describe Ethernet as the dominant LAN technology.
- Explain Ethernet frames and their purpose.
- Identify the fields of an Ethernet frame.
- Understand the function of the Preamble and Start Frame Delimiter (SFD).
- Explain Source and Destination MAC addresses.
- Describe the Type/Length field.
- Explain the purpose of the Frame Check Sequence (FCS).

---

# 📖 Physical & Data Link Layer Review

## 🔹 Physical Layer (Layer 1)

The Physical Layer is responsible for transmitting bits across the physical medium. It defines the electrical, optical, and mechanical characteristics of network communication.

Examples include copper cables, fiber-optic cables, connectors, voltage levels, and wireless radio signals.

### Example

An Ethernet cable carries binary bits as electrical signals between two devices.

---

## 🔹 Data Link Layer (Layer 2)

The Data Link Layer provides **node-to-node communication** within a Local Area Network (LAN). It formats data into frames and uses MAC addresses to identify devices.

It also detects transmission errors using the Frame Check Sequence (FCS).

### Example

A switch forwards Ethernet frames using destination MAC addresses.

---

# 📖 Local Area Network (LAN)

## 🔹 LAN

A **Local Area Network (LAN)** is a network that covers a relatively small geographic area, such as a home, office, or campus building.

Devices within the same LAN communicate directly using Layer 2 technologies like Ethernet.

### Key Points

- Switches extend a LAN.
- Routers separate LANs.
- Devices connected to different router interfaces belong to different LANs.

### Example

Several PCs connected to the same switch belong to one LAN.

---

# 📖 Ethernet Overview

## 🔹 Ethernet

Ethernet is the most widely used Layer 2 technology for wired Local Area Networks.

It defines how devices format, transmit, and receive frames over the physical medium.

### Example

When a PC sends data to another PC on the same LAN, the data is encapsulated into an Ethernet frame.

---

# 📖 Protocol Data Unit (PDU) Review

## 🔹 Ethernet Frame

At Layer 2, the Protocol Data Unit (PDU) is called a **Frame**.

A frame consists of:

- Ethernet Header
- Encapsulated Packet
- Ethernet Trailer

The frame is transmitted as bits by the Physical Layer.

### Example

```
Frame
├── Ethernet Header
├── Packet
└── Ethernet Trailer
```

---

# 📖 Ethernet Frame Structure

## 🔹 Ethernet Header

The Ethernet header contains information required for Layer 2 forwarding.

Main fields include:

- Preamble
- Start Frame Delimiter (SFD)
- Destination MAC Address
- Source MAC Address
- Type/Length

---

## 🔹 Ethernet Trailer

The Ethernet trailer contains a single field:

- Frame Check Sequence (FCS)

It is used to detect transmission errors.

---

# 📖 Preamble & Start Frame Delimiter (SFD)

## 🔹 Preamble

The **Preamble** is a 7-byte field consisting of alternating 1s and 0s.

Its purpose is to synchronize the sender's and receiver's clocks before frame transmission begins.

### Example

```
10101010
10101010
...
(7 bytes total)
```

---

## 🔹 Start Frame Delimiter (SFD)

The **Start Frame Delimiter (SFD)** is a 1-byte field immediately following the preamble.

It marks the end of the preamble and the beginning of the actual Ethernet frame.

### Example

```
10101011
```

---

# 📖 Destination & Source MAC Address

## 🔹 Destination MAC Address

The Destination MAC Address identifies the device that should receive the frame.

Length:

- 6 bytes (48 bits)

### Example

A frame sent from PC1 to PC2 contains PC2's MAC address as the destination.

---

## 🔹 Source MAC Address

The Source MAC Address identifies the device that transmitted the frame.

Length:

- 6 bytes (48 bits)

Switches use this address to build their MAC Address Tables.

### Example

When PC1 sends a frame, its MAC address becomes the Source MAC Address.

---

# 📖 Type / Length Field

## 🔹 Type / Length

The Type/Length field is 2 bytes long.

Its purpose depends on its value.

### Length

If the value is **1500 or less**, it represents the length of the encapsulated packet.

### Type

If the value is **1536 or greater**, it identifies the Layer 3 protocol.

Common values:

| Type | Protocol |
|------|----------|
| 0x0800 | IPv4 |
| 0x86DD | IPv6 |

### Example

A Type value of **0x0800** indicates that the frame contains an IPv4 packet.

---

# 📖 Frame Check Sequence (FCS)

## 🔹 FCS

The **Frame Check Sequence (FCS)** is a 4-byte field located in the Ethernet trailer.

It uses a **Cyclic Redundancy Check (CRC)** algorithm to detect transmission errors.

If the calculated CRC does not match the received FCS, the frame is discarded.

### Example

A corrupted Ethernet frame fails the CRC check and is dropped by the receiving device.

---

# 📖 Ethernet Frame Summary

| Field | Size |
|---------|------|
| Preamble | 7 Bytes |
| SFD | 1 Byte |
| Destination MAC | 6 Bytes |
| Source MAC | 6 Bytes |
| Type / Length | 2 Bytes |
| FCS | 4 Bytes |

**Total Header + Trailer:** **26 Bytes**

---

# 🔗 Connections to Previous Lessons

- Ethernet operates primarily at the **Data Link Layer (Layer 2)**.
- The Layer 2 PDU is a **Frame**.
- Frames encapsulate Layer 3 Packets.
- Frames are transmitted as Bits by the Physical Layer.
- Switches use Ethernet frames to communicate within a LAN.

---

# 📝 Summary

- The Physical Layer transmits bits across the physical medium.
- The Data Link Layer provides node-to-node communication using frames.
- Ethernet is the dominant Layer 2 LAN technology.
- An Ethernet frame consists of a header, packet, and trailer.
- The Preamble synchronizes devices before transmission.
- The SFD marks the beginning of the frame.
- Source and Destination MAC addresses identify communicating devices.
- The Type/Length field identifies the encapsulated protocol or packet length.
- The FCS detects transmission errors using CRC.