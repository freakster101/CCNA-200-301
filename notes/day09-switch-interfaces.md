# 🌐 Day 09 - Switch Interfaces: Speed, Duplex, Interface Status & Errors

## 🎯 Objectives

- Understand switch interface states.
- Configure interface speed, duplex, and descriptions.
- Configure multiple interfaces using `interface range`.
- Understand full-duplex vs half-duplex communication.
- Learn Ethernet autonegotiation.
- Recognize duplex mismatches and collisions.
- Interpret interface status and interface error counters.
- Use Cisco IOS commands to troubleshoot switch interfaces.

---

# 📖 Main Topic

## 🔹 Switch Interface Status

Unlike router interfaces, **switch interfaces are enabled by default**.

- Connected switch ports become **up/up** automatically.
- Unused ports remain **down/down**.
- Router interfaces start in **administratively down/down** because the `shutdown` command is enabled by default.

| Device | Default State |
|---------|---------------|
| Router Interface | Administratively Down/Down |
| Switch Interface (Connected) | Up/Up |
| Switch Interface (Disconnected) | Down/Down |

> **CCNA Tip:**  
> `down/down` means **no physical connection**, while `administratively down/down` means the interface has been manually disabled using `shutdown`.

---

## 🔹 Viewing Interface Status

### `show ip interface brief`

Displays Layer 1 and Layer 2 status.

```bash
SW1# show ip interface brief
```

Important columns:

| Column | Meaning |
|---------|----------|
| Interface | Port name |
| IP Address | Assigned IP (Layer 3 interfaces only) |
| Status | Physical Layer (Layer 1) |
| Protocol | Data Link Layer (Layer 2) |

Common states:

| Status | Meaning |
|---------|----------|
| up/up | Working correctly |
| down/down | Cable disconnected |
| administratively down/down | Disabled using `shutdown` |

---

### `show interfaces status`

Useful command for switch ports.

```bash
SW1# show interfaces status
```

Shows:

| Field | Description |
|--------|-------------|
| Port | Interface |
| Name | Interface description |
| Status | Connected / Notconnect / Disabled |
| VLAN | Assigned VLAN |
| Duplex | Auto or configured duplex |
| Speed | Auto or configured speed |
| Type | Physical media type |

Common Status values:

| Status | Meaning |
|---------|----------|
| connected | Device connected |
| notconnect | No cable connected |
| disabled | Interface shut down |

---

## 🔹 Configuring Speed and Duplex

Most Cisco switch interfaces default to:

- `speed auto`
- `duplex auto`

Manual configuration is rarely required but is useful for troubleshooting.

### Cisco Configuration

```bash
SW1(config)# interface f0/1
SW1(config-if)# speed 100
SW1(config-if)# duplex full
SW1(config-if)# description ## To R1 ##
```

Verify:

```bash
SW1# show interfaces status
```

When manually configured:

| Before | After |
|---------|--------|
| a-full | full |
| a-100 | 100 |

> `a-` means **autonegotiated**.

---

## 🔹 Configuring Multiple Interfaces

Cisco allows configuring multiple interfaces simultaneously.

### Consecutive Interfaces

```bash
SW1(config)# interface range f0/5 - 12
SW1(config-if-range)# description ## Not in use ##
SW1(config-if-range)# shutdown
```

### Non-Consecutive Interfaces

```bash
SW1(config)# interface range f0/5 - 6 , f0/9 - 12
SW1(config-if-range)# no shutdown
```

### Why Disable Unused Ports?

Unused switch ports should be disabled because they:

- Improve network security.
- Prevent unauthorized device connections.
- Reduce attack surface.

---

## 🔹 Full Duplex vs Half Duplex

### Half Duplex

A device **cannot send and receive simultaneously**.

It must finish receiving before transmitting.

Used with:

- Ethernet hubs

### Full Duplex

A device **can send and receive simultaneously**.

Used with:

- Ethernet switches
- Modern Ethernet networks

| Half Duplex | Full Duplex |
|--------------|-------------|
| One direction at a time | Send and receive simultaneously |
| Collisions occur | No normal collisions |
| Used by hubs | Used by switches |

### Example

Imagine a walkie-talkie.

Only one person talks at a time.

That is **half duplex**.

A telephone call allows both people to talk simultaneously.

That is **full duplex**.

---

## 🔹 Ethernet Hubs vs Switches

| Hub | Switch |
|------|---------|
| Layer 1 | Layer 2 |
| Repeats every frame | Uses MAC addresses |
| One collision domain | One collision domain per port |
| Half duplex | Full duplex |

Because switches isolate collision domains, collisions are practically eliminated in modern Ethernet networks.

---

## 🔹 CSMA/CD

**Carrier Sense Multiple Access with Collision Detection**

Used only in **half-duplex Ethernet**.

Process:

1. Listen before transmitting.
2. If medium is free, send frame.
3. Detect collision.
4. Send jamming signal.
5. Wait random time.
6. Retransmit.

> **CCNA Exam Tip:**  
> CSMA/CD applies to **half-duplex Ethernet only**. Modern switched Ethernet running full duplex does **not** use CSMA/CD.

---

## 🔹 Speed & Duplex Autonegotiation

Interfaces capable of multiple speeds use:

- `speed auto`
- `duplex auto`

Devices advertise supported capabilities and negotiate:

- Highest common speed
- Best duplex setting (normally Full)

### Example

| Device | Negotiated Speed | Duplex |
|---------|------------------|---------|
| Ethernet (10 Mbps) | 10 Mbps | Full |
| FastEthernet | 100 Mbps | Full |
| GigabitEthernet | 1000 Mbps | Full |

---

## 🔹 Autonegotiation Failure

If one device has autonegotiation disabled:

### Speed

The switch attempts to detect speed.

If detection fails:

- Uses the **lowest supported speed**

Example:

- 10 Mbps on a 10/100/1000 interface

### Duplex

| Detected Speed | Duplex Selected |
|----------------|-----------------|
| 10 Mbps | Half |
| 100 Mbps | Half |
| 1000 Mbps or higher | Full |

---

## 🔹 Duplex Mismatch

Occurs when one device uses:

- Full Duplex

while the other uses:

- Half Duplex

Results:

- Collisions
- Frame loss
- Slow network performance
- Retransmissions

> **Best Practice:** Leave autonegotiation enabled on both ends unless a specific requirement exists.

---

## 🔹 Interface Errors

View detailed statistics:

```bash
SW1# show interfaces f0/2
```

Useful counters:

| Counter | Meaning |
|----------|---------|
| Packets Input | Total received packets |
| Bytes | Total received bytes |
| Runts | Frames smaller than 64 bytes |
| Giants | Frames larger than 1518 bytes |
| CRC | Failed Frame Check Sequence (FCS) |
| Frame | Invalid Ethernet frame format |
| Input Errors | Total receive errors |
| Output Errors | Failed transmitted frames |

### Common Errors

| Error | Description |
|--------|-------------|
| Runts | Frame < 64 bytes |
| Giants | Frame > 1518 bytes |
| CRC | Corrupted frame detected |
| Frame | Incorrect frame format |
| Input Errors | Sum of receive-related errors |
| Output Errors | Failed transmission attempts |

### Troubleshooting Tips

- Rising **CRC errors** often indicate bad cables, interference, or duplex mismatches.
- **Runts** commonly occur because of collisions in half-duplex environments.
- **Giants** may indicate malformed frames or MTU-related issues.
- Frequent **output errors** can point to interface hardware problems or congestion.

---

## 📝 Exam Tips

- Switch interfaces are **enabled by default**.
- Router interfaces are **disabled by default**.
- `show ip interface brief` displays Layer 1 and Layer 2 status.
- `show interfaces status` provides a quick summary of switch ports.
- `interface range` saves time when configuring multiple ports.
- Modern Ethernet networks use **full duplex**.
- Ethernet hubs require **half duplex**.
- **CSMA/CD** is only relevant to half-duplex Ethernet.
- Autonegotiation should generally remain enabled.
- A **duplex mismatch** is a classic CCNA troubleshooting scenario.
- Know the definitions of **Runts, Giants, CRC, Frame, Input Errors, and Output Errors**.

---

# 📚 Summary

- Switch ports are enabled by default, unlike router interfaces.
- Use `show ip interface brief` and `show interfaces status` to verify interface states.
- Configure speed, duplex, and descriptions from interface configuration mode.
- Use `interface range` to configure multiple ports efficiently.
- Full duplex allows simultaneous transmission and reception; half duplex does not.
- Hubs operate in half duplex and rely on CSMA/CD, while switches support full duplex.
- Autonegotiation selects the best common speed and duplex automatically.
- Duplex mismatches cause collisions and degraded performance.
- `show interfaces` is essential for diagnosing interface statistics and physical-layer errors.

---

