# 🌐 Day 07 - IPv4 Addresses

## 🎯 Objectives

- Understand the purpose of the Network Layer.
- Learn how IPv4 addresses are structured.
- Understand binary, decimal, and hexadecimal basics.
- Identify network and host portions of an IPv4 address.
- Learn IPv4 address classes and prefix lengths.
- Understand network and broadcast addresses.

---

# 📖 OSI Model - Network Layer

## 🔹 Network Layer (Layer 3)

The Network Layer provides communication between devices on different networks. It uses logical addressing (IP addresses), selects the best path between source and destination, and routers operate at this layer.

### Example

A router forwards traffic from **192.168.1.0/24** to **192.168.2.0/24**.

---

# 📖 IPv4 Header

## 🔹 Source & Destination IP Address

The IPv4 header contains the Source IP Address and Destination IP Address fields. Each address is **32 bits (4 bytes)** long and identifies where packets come from and where they should be delivered.

### Example

Source: **192.168.1.10**  
Destination: **192.168.2.20**

---

# 📖 IPv4 Addresses

## 🔹 IPv4 Address Format

An IPv4 address consists of **32 bits**, divided into **4 octets** of **8 bits** each. It is written in **dotted decimal notation** to make it easier for humans to read.

### Example

```
192.168.1.254
```

```
11000000.10101000.00000001.11111110
```

---

# 📖 Decimal, Hexadecimal & Binary

## 🔹 Number Systems

Computers use **binary (base 2)**, while humans commonly use **decimal (base 10)**. **Hexadecimal (base 16)** provides a shorter way to represent binary values.

### Example

Decimal:

```
3294
```

Hexadecimal:

```
CDE
```

---

# 📖 Network & Host Portion

## 🔹 Prefix Length

The prefix length determines which bits belong to the network and which belong to the host. In **/24**, the first **24 bits** represent the network, while the remaining **8 bits** represent the host.

### Example

```
192.168.1.254/24
```

Network Portion:

```
192.168.1
```

Host Portion:

```
254
```

---

# 📖 Routing

## 🔹 Routing Between Networks

Routers connect different networks and forward packets based on the destination IP address. Devices on different networks require a router to communicate.

### Example

```
192.168.1.0/24
        │
     Router
        │
192.168.2.0/24
```

---

# 📖 IPv4 Address Classes

## 🔹 IPv4 Classes

IPv4 addresses are divided into Classes A, B, C, D, and E based on the first octet. For CCNA, the focus is mainly on Classes A, B, and C.

| Class | First Octet |
|--------|-------------|
| A | 0–127* |
| B | 128–191 |
| C | 192–223 |
| D | 224–239 |
| E | 240–255 |

> **Note:** 127.x.x.x is reserved for loopback addresses.

---

# 📖 Loopback Addresses

## 🔹 Loopback Address

The **127.0.0.0/8** range is reserved for loopback testing. Traffic sent to these addresses never leaves the device and is used to verify the local TCP/IP stack.

### Example

```bash
ping 127.0.0.1
```

---

# 📖 Network Address

## 🔹 Network Address

A network address has all **host bits set to 0** and identifies the network itself. It cannot be assigned to a host.

### Example

```
192.168.1.0/24
```

---

# 📖 Broadcast Address

## 🔹 Broadcast Address

A broadcast address has all **host bits set to 1** and is used to send traffic to every device on the local network. It cannot be assigned to a host.

### Example

```
192.168.1.255/24
```

---

# 📝 Summary

- Layer 3 uses IP addresses for communication between networks.
- IPv4 addresses are 32 bits long and written in dotted decimal format.
- Each IPv4 address consists of network and host portions.
- Prefix lengths (/8, /16, /24) define the network portion.
- IPv4 addresses are grouped into Classes A, B, C, D, and E.
- Loopback addresses use the 127.0.0.0/8 range.
- Network addresses have all host bits set to **0**.
- Broadcast addresses have all host bits set to **1**.