# 🌐 Day 06 - Ethernet LAN Switching (Part 2)

## 🎯 Objectives

After completing this topic, you should be able to:

- Explain the minimum Ethernet frame size.
- Describe why Ethernet padding is required.
- Explain the purpose of Address Resolution Protocol (ARP).
- Differentiate between ARP Request and ARP Reply.
- Explain how devices build an ARP table.
- Describe how Ping uses ICMP.
- Explain how switches learn MAC addresses.
- View and manage the MAC Address Table.
- Explain the Ethernet Type field.

---

# 📖 Ethernet Frame Review

## 🔹 Ethernet Frame

An Ethernet frame is the Layer 2 Protocol Data Unit (PDU) used to carry Layer 3 packets across a Local Area Network (LAN).

It consists of:

- Ethernet Header
- Payload (Packet)
- Ethernet Trailer

### Example

```
Frame
├── Ethernet Header
├── Packet (Payload)
└── Ethernet Trailer
```

---

# 📖 Minimum Ethernet Frame Size

## 🔹 Ethernet Minimum Frame Size

An Ethernet frame must be at least **64 bytes** long.

The Ethernet Header and Trailer together occupy **18 bytes**, leaving a minimum payload size of **46 bytes**.

Calculation:

```
64 Bytes (Minimum Frame)

−18 Bytes (Header + Trailer)

=46 Bytes (Minimum Payload)
```

---

## 🔹 Ethernet Padding

If the payload is smaller than 46 bytes, extra bytes called **Padding** are added until the frame reaches the minimum size.

Padding contains no useful information and exists only to satisfy the Ethernet standard.

### Example

```
34-byte payload

+12-byte padding

=46-byte payload
```

---

# 📖 Address Resolution Protocol (ARP)

## 🔹 ARP

**Address Resolution Protocol (ARP)** is used to discover the **MAC Address** of a device when its **IP Address** is already known.

ARP translates:

```
IP Address

↓

MAC Address
```

Without ARP, devices on the same LAN cannot communicate using Ethernet.

### Example

PC1 wants to communicate with **192.168.1.3**, but only knows its IP address.

ARP discovers the corresponding MAC address before communication begins.

---

# 📖 ARP Messages

## 🔹 ARP Request

An **ARP Request** is sent as a **Broadcast**.

Every device on the LAN receives the request.

Destination MAC Address:

```
FFFF.FFFF.FFFF
```

### Example

```
Who has 192.168.1.3?

Tell 192.168.1.1
```

---

## 🔹 ARP Reply

The device owning the requested IP address responds with an **ARP Reply**.

Unlike the request, the reply is sent as a **Unicast** directly to the requesting device.

### Example

```
192.168.1.3 is at

0C2F.B06A.3900
```

---

# 📖 ARP Table

## 🔹 ARP Table

The ARP Table stores mappings between **IP Addresses** and **MAC Addresses**.

Once an ARP Reply is received, the mapping is stored so ARP does not need to be performed every time.

### Example

| IP Address | MAC Address |
|------------|-------------|
|192.168.1.3|0C2F.B06A.3900|

---

## 🔹 Viewing the ARP Table

Common commands:

Windows

```
arp -a
```

Cisco IOS

```
show arp
```

Dynamic entries are learned automatically through ARP.

Static entries are configured manually.

---

# 📖 Ping

## 🔹 Ping

**Ping** is a network utility used to test whether another device is reachable across the network.

It also measures the **Round-Trip Time (RTT)** between two devices.

Ping uses the **Internet Control Message Protocol (ICMP)**.

### ICMP Messages

- ICMP Echo Request
- ICMP Echo Reply

### Example

```
PC1

↓

ICMP Echo Request

↓

PC3

↓

ICMP Echo Reply

↓

PC1
```

---

## 🔹 Why the First Ping May Fail

When a device does not know the destination MAC address, it must first perform ARP.

Because ARP takes time, the first ICMP Echo Request may timeout.

After ARP completes, later Echo Requests usually succeed.

### Example

```
.!!!!
```

The first packet failed while ARP was being completed.

---

# 📖 MAC Address Table

## 🔹 MAC Address Table

A switch stores learned MAC addresses in a **MAC Address Table**.

Each entry contains:

- VLAN
- MAC Address
- Type
- Interface (Port)

The table allows switches to forward frames efficiently.

### Example

```
MAC Address          Interface

0C2F.B011.9D00       Gi0/0

0C2F.B06A.3900       Gi0/2
```

---

## 🔹 How MAC Addresses Are Learned

Switches learn MAC addresses by examining the **Source MAC Address** of every incoming Ethernet frame.

The switch records:

```
Source MAC

↓

Incoming Interface
```

This process happens automatically.

### Example

If PC1 sends a frame through GigabitEthernet0/0, the switch associates PC1's MAC address with that interface.

---

# 📖 Viewing the MAC Address Table

## 🔹 Show MAC Address Table

Cisco IOS command:

```
show mac address-table
```

The output displays all learned MAC addresses along with their VLANs and interfaces.

---

# 📖 Clearing the MAC Address Table

## 🔹 Clear Dynamic Entries

Cisco IOS provides several commands to remove dynamically learned MAC addresses.

Clear all dynamic entries:

```
clear mac address-table dynamic
```

Clear a specific MAC address:

```
clear mac address-table dynamic address <mac-address>
```

Clear entries learned on a specific interface:

```
clear mac address-table dynamic interface <interface>
```

Only **Dynamic** entries are removed.

Static entries remain until manually deleted.

---

# 📖 Ethernet Type Field Review

## 🔹 Ethernet Type

The Ethernet **Type** field identifies which Layer 3 protocol is encapsulated inside the frame.

Common values include:

| Type | Protocol |
|------|----------|
|0x0800|IPv4|
|0x0806|ARP|
|0x86DD|IPv6|

### Example

When the Type field contains **0x0806**, the payload contains an ARP message.

---

# 🔗 Connections to Previous Lessons

- Ethernet operates at the **Data Link Layer (Layer 2)**.
- Ethernet frames encapsulate Layer 3 packets.
- ARP translates IP addresses into MAC addresses.
- Switches forward frames using MAC addresses.
- Hosts maintain ARP Tables.
- Switches maintain MAC Address Tables.
- Ping uses ICMP after ARP has resolved the destination MAC address.

---

# 📝 Summary

- Ethernet frames have a minimum size of **64 bytes**.
- The minimum Ethernet payload is **46 bytes**.
- Padding is added if the payload is too small.
- ARP resolves IP addresses into MAC addresses.
- ARP Request is a Broadcast.
- ARP Reply is a Unicast.
- ARP mappings are stored in the ARP Table.
- Ping uses ICMP Echo Request and Echo Reply.
- The first ping may fail while ARP completes.
- Switches learn MAC addresses from the Source MAC Address.
- The MAC Address Table stores MAC-to-interface mappings.
- Dynamic MAC entries can be viewed and cleared using Cisco IOS commands.
- The Ethernet Type field identifies the encapsulated Layer 3 protocol.