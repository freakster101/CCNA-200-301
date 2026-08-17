# 🌐 Day 15 - VLSM (Lab Notes)

> **Lab Source:** Jeremy's IT Lab - CCNA 200-301 Day 15 (VLSM)  
> These notes summarize the hands-on Packet Tracer lab and focus on subnet allocation, interface addressing, static routing, and connectivity verification.

---

## 🎯 Objectives

- Subnet the `192.168.5.0/24` network using VLSM.
- Allocate subnets according to different host requirements.
- Assign the first usable address to each PC.
- Assign the last usable address to each router LAN interface.
- Use a `/30` subnet for the point-to-point router connection.
- Configure static routes so all LANs can communicate.
- Verify connectivity between the LANs.

---

# 📖 Lab Topology

The topology contains four LANs connected through two routers.

| Segment | Host Requirement |
|---------|------------------|
| LAN 1 | 45 hosts |
| LAN 2 | 64 hosts |
| LAN 3 | 14 hosts |
| LAN 4 | 9 hosts |
| R1 ↔ R2 | Point-to-point link |

The parent network used for the entire lab was:

```text
192.168.5.0/24
```

---

# 📖 VLSM Addressing Plan

Subnets were allocated from largest to smallest host requirement.

| Segment | Network | Prefix | Subnet Mask | Usable Range | Broadcast |
|---------|---------|--------|-------------|--------------|-----------|
| LAN 2 | 192.168.5.0 | /25 | 255.255.255.128 | 192.168.5.1 - 192.168.5.126 | 192.168.5.127 |
| LAN 1 | 192.168.5.128 | /26 | 255.255.255.192 | 192.168.5.129 - 192.168.5.190 | 192.168.5.191 |
| LAN 3 | 192.168.5.192 | /28 | 255.255.255.240 | 192.168.5.193 - 192.168.5.206 | 192.168.5.207 |
| LAN 4 | 192.168.5.208 | /28 | 255.255.255.240 | 192.168.5.209 - 192.168.5.222 | 192.168.5.223 |
| R1 ↔ R2 | 192.168.5.224 | /30 | 255.255.255.252 | 192.168.5.225 - 192.168.5.226 | 192.168.5.227 |

> **Observation:** VLSM allowed each network segment to receive only the address space it required instead of giving every LAN the same subnet size.

---

# 📖 LAN 2 Address Configuration

LAN 2 required **64 hosts**, so the largest available subnet was assigned first.

- Network: `192.168.5.0/25`
- PC2: `192.168.5.1/25`
- R1 LAN interface: `192.168.5.126/25`
- Default gateway for PC2: `192.168.5.126`

### 📷 LAN 2 Configuration

![LAN 2 IP Configuration](assets/day15/day15-vlsm-01.png)

---

# 📖 LAN 1 Address Configuration

LAN 1 required **45 hosts**.

- Network: `192.168.5.128/26`
- PC1: `192.168.5.129/26`
- R1 LAN interface: `192.168.5.190/26`
- Default gateway for PC1: `192.168.5.190`

### 📷 LAN 1 Configuration

![LAN 1 IP Configuration](assets/day15/day15-vlsm-02.png)

---

# 📖 LAN 3 Address Configuration

LAN 3 required **14 hosts**.

- Network: `192.168.5.192/28`
- PC3: `192.168.5.193/28`
- R2 LAN interface: `192.168.5.206/28`
- Default gateway for PC3: `192.168.5.206`

### 📷 LAN 3 Configuration

![LAN 3 IP Configuration](assets/day15/day15-vlsm-03.png)

---

# 📖 LAN 4 Address Configuration

LAN 4 required **9 hosts**.

- Network: `192.168.5.208/28`
- PC4: `192.168.5.209/28`
- R2 LAN interface: `192.168.5.222/28`
- Default gateway for PC4: `192.168.5.222`

### 📷 LAN 4 Configuration

![LAN 4 IP Configuration](assets/day15/day15-vlsm-04.png)

---

# 📖 Point-to-Point Router Link

The R1-to-R2 connection required only two usable IPv4 addresses, so a `/30` subnet was used.

- Network: `192.168.5.224/30`
- R1: `192.168.5.225/30`
- R2: `192.168.5.226/30`

```bash
R1(config)# interface g0/0/0
R1(config-if)# ip address 192.168.5.225 255.255.255.252
R1(config-if)# no shutdown
```

```bash
R2(config)# interface g0/0/0
R2(config-if)# ip address 192.168.5.226 255.255.255.252
R2(config-if)# no shutdown
```

### 📷 Point-to-Point Configuration

![R1 to R2 Point-to-Point Link](assets/day15/day15-vlsm-05.png)

> **Observation:** A `/30` provides exactly two usable host addresses, making it suitable for this router-to-router link.

---

# 📖 Static Route Configuration

Each router already knew its directly connected LANs. Static routes were required only for the remote LANs.

### R1

```bash
R1(config)# ip route 192.168.5.192 255.255.255.240 192.168.5.226
R1(config)# ip route 192.168.5.208 255.255.255.240 192.168.5.226
```

### R2

```bash
R2(config)# ip route 192.168.5.0 255.255.255.128 192.168.5.225
R2(config)# ip route 192.168.5.128 255.255.255.192 192.168.5.225
```

Verification:

```bash
show ip route
```

The configured static routes appeared with the `S` route code.

---

# ✅ Connectivity Verification

After configuring VLSM addressing and static routes, connectivity was tested between hosts on different LANs.

### 📷 Inter-LAN Connectivity Test

![VLSM Connectivity Verification](assets/day15/day15-vlsm-06.png)

Successful replies confirmed that:

- PC addressing was correct.
- Default gateways were correct.
- Router interfaces were correctly subnetted.
- The point-to-point link was operational.
- Static routes correctly reached the remote LANs.

Some first ping attempts timed out while ARP resolution completed, after which communication succeeded.

---

# 🔍 Lab Observations

- VLSM subnets were assigned from the largest host requirement to the smallest.
- The first usable IPv4 address of each LAN was assigned to the PC.
- The last usable IPv4 address was assigned to the router interface.
- LAN 2 required `/25` because 64 hosts cannot fit inside a `/26`, which provides only 62 usable addresses.
- LAN 3 and LAN 4 both required `/28` subnets.
- A `/30` subnet efficiently provided two usable addresses for the R1-to-R2 link.
- Static routes were required only for networks not directly connected to each router.
- Final inter-LAN ping tests confirmed successful end-to-end communication.

---

# ⚠️ Lab-Specific Notes

### Allocate the Largest LAN First

LAN 2 had the largest requirement at 64 hosts, so it received the first and largest subnet:

```text
192.168.5.0/25
```

Allocating the largest networks first prevents the remaining address space from becoming fragmented.

### Do Not Count Network and Broadcast Addresses as Hosts

A `/26` contains 64 total addresses but only 62 usable addresses, so it cannot satisfy a requirement of 64 hosts.

### Next-Hop Routes Follow the Router Link

The static routes used the neighboring router's `/30` address as the next hop:

```text
R1 → 192.168.5.226
R2 → 192.168.5.225
```

---

# 📝 Summary

- Subnetted `192.168.5.0/24` using VLSM.
- Created `/25`, `/26`, `/28`, `/28`, and `/30` subnets based on host requirements.
- Assigned first usable addresses to PCs and last usable addresses to router LAN interfaces.
- Configured the R1-R2 point-to-point link using `192.168.5.224/30`.
- Configured static routes to reach all remote LANs.
- Verified routing and tested communication between the LANs.
- Confirmed that VLSM conserves IPv4 address space while supporting networks of different sizes.

---

## 📚 Credits

This lab is based on the **CCNA 200-301** course by **Jeremy's IT Lab**.

These notes were created as a personal study reference while completing the Packet Tracer VLSM lab.
