# 🌐 Subnetting Fundamentals (Part 1)

## 🎯 Objectives

- Understand why subnetting is needed.
- Learn what **CIDR (Classless Inter-Domain Routing)** is.
- Calculate the number of usable hosts using different prefix lengths.
- Understand how subnetting reduces wasted IPv4 addresses.

---

# 📖 Subnetting Fundamentals

## 🔹 Why Subnetting?

Subnetting is the process of dividing a larger network into **smaller subnetworks (subnets)**.

### Benefits

- Better IP address utilization
- Reduced wasted addresses
- Easier network management
- Improved scalability

---

## 🔹 Classful Addressing (Review)

| Class | First Octet | Default Prefix |
|--------|-------------|----------------|
| A | 0 – 127 | /8 |
| B | 128 – 191 | /16 |
| C | 192 – 223 | /24 |

In the classful addressing scheme:

- Class A → `/8`
- Class B → `/16`
- Class C → `/24`

This often resulted in a large number of unused IPv4 addresses.

---

## 🔹 CIDR (Classless Inter-Domain Routing)

CIDR removes the fixed Class A, B, and C boundaries and allows **any prefix length**.

### Examples

```text
192.168.1.0/24
192.168.1.0/26
192.168.1.0/30
203.0.113.0/31
```

CIDR makes subnetting flexible and helps conserve IPv4 address space.

---

## 🔹 Host Calculation Formula

```text
Usable Hosts = 2^(Host Bits) − 2
```

Where:

- **Host Bits = 32 − Prefix Length**
- Subtract **2** for:
  - Network Address
  - Broadcast Address

---

## 🔹 Common Prefix Lengths

| Prefix | Subnet Mask | Usable Hosts |
|---------|-------------|-------------:|
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /29 | 255.255.255.248 | 6 |
| /30 | 255.255.255.252 | 2 |
| /31 | 255.255.255.254 | Point-to-Point |
| /32 | 255.255.255.255 | Single Host |

---

## 🔹 /30 vs /31

| /30 | /31 |
|------|------|
| 4 total addresses | 2 total addresses |
| 2 usable hosts | Both addresses are usable |
| Common for point-to-point links | More efficient for point-to-point links |

---

## 🔹 /32

A **/32** prefix identifies **one specific host**.

### Common Uses

- Host routes
- Loopback interfaces
- Static routes to a single device

---

## 🔹 Example

Instead of assigning:

```text
203.0.113.0/24
```

to a point-to-point link, use:

```text
203.0.113.0/30
```

or even:

```text
203.0.113.0/31
```

This conserves IPv4 addresses by allocating only the addresses that are actually required.

---

## 🔹 Choosing the Correct Subnet

**Requirement:** 45 hosts per subnet

| Prefix | Usable Hosts | Suitable? |
|---------|-------------:|-----------|
| /27 | 30 | ❌ No |
| /26 | 62 | ✅ Yes |

**Rule:** Choose the **smallest subnet** that provides enough usable host addresses.

---

# 📝 Summary

- Subnetting divides a network into smaller subnetworks.
- CIDR replaces the old Class A/B/C addressing restrictions.
- Calculate usable hosts using:

```text
Usable Hosts = 2^(Host Bits) − 2
```

- `/30` is commonly used for point-to-point links.
- `/31` is valid for point-to-point links and is more efficient.
- `/32` identifies a single host.
- Always select the smallest subnet that meets the required number of hosts.