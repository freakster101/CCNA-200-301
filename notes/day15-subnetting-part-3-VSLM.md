# 🌐 Subnetting Fundamentals (Part 3)

## 🎯 Objectives

- Practice subnetting Class A networks.
- Learn **VLSM (Variable-Length Subnet Masks)**.
- Understand how to allocate subnets efficiently.
- Identify network, broadcast, and usable host addresses.

---

# 📖 Subnetting Fundamentals (Part 3)

## 🔹 Class A Subnetting

The subnetting process is exactly the same as for Class B and Class C networks.

The only difference is that Class A networks have **24 host bits**, allowing many more possible subnets and hosts.

### Example

```text
Network: 10.0.0.0/8

Requirement:
2000 subnets
```

```
2¹¹ = 2048 subnets
```

Borrow **11 bits**

New Prefix:

```text
/19
```

Remaining Host Bits:

```
13
```

Usable Hosts:

```text
2¹³ − 2 = 8190
```

---

## 🔹 Finding Network Information

To identify a subnet:

### Network Address

Set all **host bits to 0**.

### Broadcast Address

Set all **host bits to 1**.

### First Host

```text
Network Address + 1
```

### Last Host

```text
Broadcast Address − 1
```

---

## 🔹 VLSM (Variable-Length Subnet Masks)

Unlike **FLSM (Fixed-Length Subnet Masks)**, VLSM allows different subnet sizes within the same network.

This improves IP address utilization and minimizes wasted addresses.

---

## 🔹 VLSM Steps

1. List all required subnets.
2. Sort them from **largest to smallest**.
3. Assign the largest subnet first.
4. Assign the next subnet immediately after the previous one.
5. Continue until all required subnets are allocated.

---

## 🔹 Example

Given:

```text
192.168.1.0/24
```

| Network | Hosts | Prefix |
|---------|------:|--------|
| Tokyo LAN A | 110 | /25 |
| Toronto LAN B | 45 | /26 |
| Toronto LAN A | 29 | /27 |
| Tokyo LAN B | 8 | /28 |
| Point-to-Point | 2 | /30 |

Assign subnets in this order:

```text
Largest → Smallest
```

This ensures efficient use of the available address space.

---

## 🔹 FLSM vs VLSM

| FLSM | VLSM |
|------|------|
| Same subnet size everywhere | Different subnet sizes |
| Easier to calculate | More efficient |
| Wastes more addresses | Conserves IPv4 addresses |

---

## 🔹 Important Tips

- Always assign the **largest subnet first**.
- Use the **smallest prefix** that satisfies the host requirement.
- Network Address → Host bits **0**
- Broadcast Address → Host bits **1**
- First Host = Network + 1
- Last Host = Broadcast − 1

---

# 📝 Summary

- Class A subnetting uses the same process as Class B and Class C subnetting.
- VLSM allows different subnet sizes within the same network.
- Allocate subnets from **largest to smallest**.
- VLSM improves IPv4 address efficiency by reducing wasted addresses.
- Determine:
  - Network Address
  - Broadcast Address
  - First Host
  - Last Host
  - Number of Usable Hosts
  for every subnet.