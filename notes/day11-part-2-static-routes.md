# 🌐 Static Routing

## 🎯 Objectives

- Review Connected and Local routes.
- Understand why Static Routes are needed.
- Learn how routers forward packets to remote networks.
- Understand the concept of a Default Gateway.
- Configure Static Routes on Cisco routers.
- Learn the three methods of configuring Static Routes.
- Understand Default Routes and the Gateway of Last Resort.

---

# 📖 Main Topic

## 🔹 Why Connected and Local Routes Are Not Enough

Previously we learned that configuring an interface automatically creates:

- **Connected (C)** routes
- **Local (L)** routes

These routes only allow a router to reach:

- Its own interface IP addresses (Local routes)
- Directly connected networks (Connected routes)

Example

```
R1

Connected:
192.168.1.0/24
192.168.12.0/24
192.168.13.0/24

Local:
192.168.1.1/32
192.168.12.1/32
192.168.13.1/32
```

Can R1 reach

```
192.168.4.0/24 ?
```

❌ No.

That network is **remote**, meaning it is not directly connected.

Without another route, R1 drops the packet.

---

# 🔹 What is a Static Route?

A **Static Route** is a route manually configured by a network administrator.

Instead of discovering routes automatically, you explicitly tell the router:

> "To reach network X, send packets to router Y."

Think of it like leaving written directions instead of relying on GPS. Less flexible, but also less likely to suddenly decide that the fastest route is through a lake.

---

# 🔹 Remote Networks

A **remote network** is any network that is **not directly connected** to the router.

Example

```
PC1
 |
R1 ---- R3 ---- R4 ---- PC4
```

For R1

```
Connected

192.168.1.0/24
192.168.12.0/24
192.168.13.0/24
```

Remote

```
192.168.4.0/24
192.168.34.0/24
192.168.24.0/24
```

Connected routes cannot reach these networks.

Static routes solve this problem.

---

# 🔹 Default Gateway (Hosts)

Every end device (PC, Laptop, Server) has a **Default Gateway**.

It is:

> The router the host sends packets to whenever the destination is outside the local network.

Example

```
PC1

IP
192.168.1.10

Gateway
192.168.1.1
```

If PC1 wants to reach

```
192.168.4.10
```

it sends the frame to

```
192.168.1.1
```

which is R1.

The host doesn't know the entire Internet.

It only knows:

> "Ask the router."

---

# 🔹 Host Default Route

A host's default gateway is actually a route:

```
0.0.0.0/0
```

This means

```
Match everything.
```

It is the **least specific route** possible.

If no better route exists,

send the packet here.

---

# 🔹 Packet Journey

Suppose

```
PC1

↓

PC4
```

The packet travels

```
PC1

↓

R1

↓

R3

↓

R4

↓

PC4
```

Notice something important.

The

**IP addresses**

never change.

```
Src IP

192.168.1.10

Dst IP

192.168.4.10
```

stay exactly the same from start to finish.

However,

the

**MAC addresses**

change at every hop.

Each router removes the Ethernet frame and builds a new one for the next hop.

| Layer | Changes? |
|--------|----------|
| IP Address | ❌ No |
| MAC Address | ✅ Yes |

A favorite CCNA trick. Cisco enjoys asking it because apparently one layer changing while another doesn't is irresistible exam material.

---

# 🔹 Why Static Routes Are Needed

Suppose R1 receives

```
Destination

192.168.4.10
```

R1 checks

```
show ip route
```

Without a route,

```
No Match

↓

Drop Packet
```

So we configure

```
To reach

192.168.4.0/24

↓

Send to

192.168.13.3
```

Now R1 knows what to do.

---

# 🔹 Planning Static Routes

For communication to work,

every router along the path needs routes.

Example path

```
PC1

↓

R1

↓

R3

↓

R4

↓

PC4
```

Routes required

### R1

Already knows

```
192.168.1.0/24
```

Needs

```
192.168.4.0/24

via

192.168.13.3
```

---

### R3

Needs

```
192.168.1.0/24

via

192.168.13.1
```

and

```
192.168.4.0/24

via

192.168.34.4
```

---

### R4

Already knows

```
192.168.4.0/24
```

Needs

```
192.168.1.0/24

via

192.168.34.3
```

---

# 🔹 Static Route Syntax

General format

```bash
ip route network mask next-hop
```

Example

```bash
ip route 192.168.4.0 255.255.255.0 192.168.13.3
```

Meaning

> To reach **192.168.4.0/24**, send packets to **192.168.13.3**.

---

# 🔹 Example Configurations

### R1

```bash
ip route 192.168.4.0 255.255.255.0 192.168.13.3
```

---

### R3

```bash
ip route 192.168.1.0 255.255.255.0 192.168.13.1

ip route 192.168.4.0 255.255.255.0 192.168.34.4
```

---

### R4

```bash
ip route 192.168.1.0 255.255.255.0 192.168.34.3
```

---

# 🔹 Route Code

After configuration

```
show ip route
```

You'll see

```
S
```

which means

```
Static Route
```

Example

```
S 192.168.4.0/24

via 192.168.13.3
```

---

# 🔹 Administrative Distance and Metric

Example

```
S 192.168.4.0/24

[1/0]
```

These numbers represent

```
[Administrative Distance / Metric]
```

For now, simply remember:

```
Static Route

AD = 1
```

We'll study Administrative Distance and Metrics later in CCNA.

---

# 🔹 Three Ways to Configure Static Routes

## Method 1

Specify **Next-Hop**

```bash
ip route network mask next-hop
```

Example

```bash
ip route 192.168.4.0 255.255.255.0 192.168.13.3
```

Recommended for most CCNA labs.

---

## Method 2

Specify **Exit Interface**

```bash
ip route network mask g0/0
```

Example

```bash
ip route 192.168.1.0 255.255.255.0 g0/0
```

---

## Method 3

Specify **Both**

```bash
ip route network mask exit-interface next-hop
```

Example

```bash
ip route 192.168.4.0 255.255.255.0 g0/1 192.168.24.4
```

This is perfectly valid.

---

# 🔹 Default Route (Router)

A router's default route is

```
0.0.0.0/0
```

It means

> "If you don't know where to send the packet, send it here."

It is often used to reach

- Internet
- ISP
- Unknown external networks

---

# 🔹 Configuring Default Route

Syntax

```bash
ip route 0.0.0.0 0.0.0.0 next-hop
```

Example

```bash
ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

Now

all unknown destinations

go to

```
203.0.113.2
```

---

# 🔹 Gateway of Last Resort

Before configuring a default route

```
Gateway of last resort

is not set
```

After configuration

```
Gateway of last resort

is

203.0.113.2
```

This simply means

```
Default Route

Configured
```

Cisco calls it the **Gateway of Last Resort**, which sounds dramatically heroic for what is basically "send it to Bob if you have no better idea."

---

# 🔹 Candidate Default

You'll often see

```
S*
```

Example

```
S* 0.0.0.0/0
```

The asterisk means

```
Candidate Default
```

This route is being used as the router's default route.

---

# 🔹 Static Route vs Default Route

| Static Route | Default Route |
|--------------|---------------|
| Specific network | All unknown networks |
| Example: 192.168.4.0/24 | Example: 0.0.0.0/0 |
| More specific | Least specific |
| Used for known destinations | Used as a fallback |

---

# 🔹 Packet Flow Example

```
PC1

↓

R1

↓

Static Route

↓

R3

↓

Static Route

↓

R4

↓

Connected Route

↓

PC4
```

Notice

Each router only needs to know

the **next hop**, not the complete journey.

---

# 📝 Exam Tips

- Static routes are **manually configured**.
- Connected and Local routes are **automatically created** when an interface is configured and enabled.
- Use the command:

```bash
show ip route
```

to verify routes.
- Static routes appear with code **S**.
- The general syntax is:

```bash
ip route network mask next-hop
```

- A router forwards packets to the **next hop**, not directly to the final destination unless it is on a connected network.
- End hosts use a **default gateway** to reach remote networks.
- The **IP header stays the same** throughout the journey, but the **Ethernet (MAC) header changes at every hop**.
- A default route is:

```text
0.0.0.0/0
```

- The **Gateway of Last Resort** is the router's selected default route.
- `S*` in the routing table indicates the **candidate default route**.
- A route using a **longer prefix** is preferred over the default route because of the **Longest Prefix Match** rule.

---

# 📝 Summary

- Connected and Local routes allow routers to reach only directly connected networks and their own interface IP addresses.
- Static routes are manually configured to reach remote networks.
- End devices rely on a **default gateway** to send traffic outside their local subnet.
- Routers forward packets hop by hop using **next-hop IP addresses**.
- Static routes can be configured using a next-hop IP, an exit interface, or both.
- The packet's **IP addresses remain unchanged**, while the **MAC addresses are rewritten at every hop**.
- A **default route (0.0.0.0/0)** acts as a fallback when no more specific route exists.
- The **Gateway of Last Resort** is the active default route used by the router.

---
