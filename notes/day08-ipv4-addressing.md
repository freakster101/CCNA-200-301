# 🌐 Day 08 - IPv4 Addressing (Part 2)

## 🎯 Objectives

- Review IPv4 address classes.
- Calculate the maximum number of hosts in a network.
- Identify the network and broadcast addresses.
- Find the first and last usable IP addresses.
- Configure IPv4 addresses on Cisco routers.
- Learn common interface verification commands.

---

# 📖 IPv4 Address Classes (Review)

## 🔹 IPv4 Classes

IPv4 addresses are divided into different classes based on the first octet. Although modern networking uses CIDR instead of classes, CCNA still expects you to understand Class A, B, and C.

| Class | First Octet | Default Prefix | Default Subnet Mask |
|--------|-------------|----------------|---------------------|
| A | 1–126* | /8 | 255.0.0.0 |
| B | 128–191 | /16 | 255.255.0.0 |
| C | 192–223 | /24 | 255.255.255.0 |

> **Note**
>
> - **0.x.x.x** is reserved.
> - **127.x.x.x** is reserved for loopback.

### Example

```
10.0.0.1      → Class A
172.16.5.10   → Class B
192.168.1.20  → Class C
```

---

# 📖 Maximum Hosts Per Network

## 🔹 Formula

Every network reserves two addresses:

- Network Address
- Broadcast Address

Therefore,

```
Maximum Hosts = 2ᴴ − 2
```

Where **H = number of host bits**

### Examples

| Prefix | Host Bits | Formula | Usable Hosts |
|---------|-----------|----------|--------------|
| /8 | 24 | 2²⁴ − 2 | 16,777,214 |
| /16 | 16 | 2¹⁶ − 2 | 65,534 |
| /24 | 8 | 2⁸ − 2 | 254 |

---

# 📖 Network Address

## 🔹 Network Address

The network address identifies the network itself.

- Host bits are **all 0**
- Cannot be assigned to a host

### Example

```
Network:
192.168.1.0/24
```

---

# 📖 Broadcast Address

## 🔹 Broadcast Address

The broadcast address sends traffic to every device within the local network.

- Host bits are **all 1**
- Cannot be assigned to a host

### Example

```
Broadcast:
192.168.1.255/24
```

---

# 📖 First & Last Usable Address

## 🔹 First Usable Address

The first usable address is:

```
Network Address + 1
```

### Example

```
Network:
192.168.1.0

First Host:
192.168.1.1
```

---

## 🔹 Last Usable Address

The last usable address is:

```
Broadcast Address − 1
```

### Example

```
Broadcast:
192.168.1.255

Last Host:
192.168.1.254
```

---

# 📖 Configuring IPv4 Addresses on Cisco Routers

## 🔹 Basic Interface Configuration

To assign an IPv4 address:

```bash
R1(config)# interface g0/0
R1(config-if)# ip address 10.255.255.254 255.0.0.0
R1(config-if)# no shutdown
```

### Explanation

- **interface g0/0** → Enter interface configuration mode.
- **ip address** → Assign an IPv4 address and subnet mask.
- **no shutdown** → Enable the interface.

---

# 📖 Interface Status

## 🔹 Status vs Protocol

The `show ip interface brief` command displays two important status fields.

| Column | OSI Layer | Meaning |
|----------|-----------|---------|
| Status | Layer 1 | Physical connection |
| Protocol | Layer 2 | Data Link status |

Possible outputs:

| Status | Protocol | Meaning |
|----------|----------|---------|
| up | up | Interface is working normally |
| administratively down | down | Disabled using `shutdown` |
| down | down | Cable disconnected or physical issue |

---

# 📖 show ip interface brief

## 🔹 Purpose

Displays a quick summary of all interfaces.

Shows:

- Interface name
- IP Address
- Assignment method
- Layer 1 status
- Layer 2 status

### Example

```bash
show ip interface brief
```

Output

```
Gig0/0 10.255.255.254 up up
Gig0/1 172.16.255.254 up up
Gig0/2 192.168.0.254 up up
```

---

# 📖 show interfaces

## 🔹 Purpose

Displays detailed Layer 1 and Layer 2 information for an interface.

Information includes:

- Interface status
- MAC address
- IP address
- MTU
- Speed
- Duplex
- Error counters
- Traffic statistics

### Example

```bash
show interfaces g0/0
```

---

# 📖 Interface Descriptions

## 🔹 Description Command

Descriptions help identify what an interface connects to.

### Configuration

```bash
R1(config)# interface g0/0
R1(config-if)# description ## To SW1 ##
```

---

# 📖 show interfaces description

## 🔹 Purpose

Displays interface descriptions together with interface status.

### Example

```bash
show interfaces description
```

Example Output

```
Gi0/0   up   up   ## To SW1 ##
Gi0/1   up   up   ## To SW2 ##
Gi0/2   up   up   ## To SW3 ##
```

---

# 📖 Useful CLI Shortcuts

## 🔹 Common Shortcuts

| Full Command | Shortcut |
|--------------|----------|
| configure terminal | conf t |
| interface | int |
| ip address | ip add |
| no shutdown | no shut |
| show ip interface brief | sh ip int br |
| show interfaces description | sh int desc |

These shortcuts save time but perform the same function as the full commands.

---

# 📝 Summary

- IPv4 Classes A, B, and C use default prefixes of **/8**, **/16**, and **/24**.
- Maximum usable hosts are calculated using **2ᴴ − 2**.
- The network address has all host bits set to **0**.
- The broadcast address has all host bits set to **1**.
- The first usable address is **Network + 1**.
- The last usable address is **Broadcast − 1**.
- Configure interfaces using **ip address** and **no shutdown**.
- Use **show ip interface brief** to quickly verify interfaces.
- Use **show interfaces** for detailed interface information.
- Interface descriptions make troubleshooting much easier.