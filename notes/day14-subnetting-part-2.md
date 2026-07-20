# 🌐 Subnetting Fundamentals (Part 2)

## 🎯 Objectives

- Divide networks into equal-sized subnets.
- Calculate the required prefix length.
- Identify network and broadcast addresses.
- Determine which subnet a host belongs to.
- Apply subnetting to both Class C and Class B networks.

---

# 📖 Subnetting Fundamentals (Part 2)

## 🔹 Subnetting Process

1. Determine the required number of **hosts** or **subnets**.
2. Borrow enough host bits to satisfy the requirement.
3. Calculate the new prefix length.
4. Determine each subnet's network and broadcast addresses.

---

## 🔹 Finding Subnets Quickly

The **increment (block size)** is the value of the **last network bit**.

### Example

```text
192.168.1.0/26
```

Last network bit = **64**

Subnets:

```text
192.168.1.0
192.168.1.64
192.168.1.128
192.168.1.192
```

Simply keep adding **64**.

---

## 🔹 Number of Subnets

```text
Number of Subnets = 2^(Borrowed Bits)
```

Example:

| Borrowed Bits | Subnets |
|--------------:|--------:|
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 4 | 16 |

---

## 🔹 Finding a Network Address

To identify the subnet a host belongs to:

1. Locate the network bits.
2. Set all **host bits to 0**.
3. Convert back to decimal.

### Example

```text
Host:
192.168.5.57/27

Network:
192.168.5.32/27
```

---

## 🔹 Finding the Broadcast Address

To find the broadcast address:

1. Keep the network bits unchanged.
2. Set all **host bits to 1**.

Example:

```text
Network:
192.168.1.64/26

Broadcast:
192.168.1.127
```

---

## 🔹 Class C Subnetting

The subnetting process is the same regardless of address class.

Example:

```text
192.168.255.0/24
```

Need **5 subnets**

```text
2³ = 8 Subnets
```

Borrow **3 bits**

New Prefix:

```text
/27
```

---

## 🔹 Class B Subnetting

Example:

```text
172.16.0.0/16
```

Need **80 subnets**

```text
2⁷ = 128
```

Borrow **7 bits**

New Prefix:

```text
/23
```

The subnetting process is identical to Class C; only the number of available host bits changes.

---

## 🔹 Important Formulas

### Number of Hosts

```text
Usable Hosts = 2^(Host Bits) − 2
```

### Number of Subnets

```text
Subnets = 2^(Borrowed Bits)
```

---

## 🔹 Quick Tips

- **Host bits → determine hosts**
- **Borrowed bits → determine subnets**
- Network Address → all host bits **0**
- Broadcast Address → all host bits **1**
- Block Size (Increment) = value of the **last network bit**

---

# 📝 Summary

- Borrow host bits to create additional subnets.
- Use **2^(Borrowed Bits)** to calculate the number of subnets.
- Use **2^(Host Bits) − 2** to calculate usable hosts.
- Network address = host bits set to **0**.
- Broadcast address = host bits set to **1**.
- The subnetting process is the same for Class A, B, and C networks; only the default prefix length changes.