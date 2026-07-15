# 🌐 Routing Fundamentals

## 🎯 Objectives

- Understand what routing is.
- Learn the difference between static and dynamic routing.
- Understand how routers use the routing table.
- Learn Connected and Local routes.
- Understand route matching.
- Learn the Longest Prefix Match rule.
- Become familiar with the `show ip route` command.

---

# 📖 Main Topic

## 🔹 What is Routing?

**Routing** is the process routers use to determine the best path for an IP packet to reach its destination network.

Instead of guessing where packets should go (humans try that with life every day), routers consult a **routing table**.

Whenever a router receives a packet, it:

1. Reads the destination IP address.
2. Searches its routing table.
3. Finds the best matching route.
4. Forwards the packet to the correct interface or next-hop router.

---

## 🔹 Routing Table

A **routing table** is a database stored in every router.

It contains routes to known networks and instructions on how to reach them.

Think of it like Google Maps for routers.

Instead of:

> "Drive north."

It says:

> "To reach network X, send the packet out interface G0/0 or to next-hop Y."

View it using:

```bash
show ip route
```

---

## 🔹 Next-Hop

A **next-hop** is simply:

> The next router along the path toward the destination.

Example:

```
PC ---- R1 ---- R2 ---- R3 ---- Server
```

If R1 wants to reach the server, its next-hop is **R2**, not the server itself.

Routers usually don't know the complete path.

They only know:

> "Give the packet to this neighbor."

The next router repeats the same process.

---

## 🔹 Static vs Dynamic Routing

There are two primary ways routers learn routes.

### Static Routing

Routes are manually configured by a network administrator.

Example:

```
ip route 192.168.4.0 255.255.255.0 192.168.13.3
```

Advantages

- Simple
- Predictable
- Secure
- Low CPU usage

Disadvantages

- Doesn't scale well
- Manual updates required

---

### Dynamic Routing

Routers automatically exchange routing information using routing protocols.

Examples

- OSPF
- EIGRP
- RIP
- IS-IS
- BGP

Advantages

- Automatic
- Scalable
- Adapts to failures

Disadvantages

- More CPU and memory usage
- More complex

> **CCNA Note:** You'll study static routing first, then dynamic routing protocols like OSPF later.

---

# 🔹 Routing Table Codes

When running:

```bash
show ip route
```

You'll see route codes.

Some important ones:

| Code | Meaning |
|------|---------|
| L | Local |
| C | Connected |
| S | Static |
| O | OSPF |
| D | EIGRP |
| R | RIP |
| B | BGP |

For now, focus on:

- **C**
- **L**

---

# 🔹 Connected Routes

When you configure an interface with an IP address and enable it (`no shutdown`), Cisco automatically creates a **Connected route**.

Example

```
Interface:

192.168.1.1/24
```

Automatically creates

```
C 192.168.1.0/24
```

Meaning:

> "The entire 192.168.1.0 network is directly attached to this interface."

---

### What does it match?

```
192.168.1.0/24
```

Matches every address in:

```
192.168.1.0

through

192.168.1.255
```

Examples

✅ Match

```
192.168.1.2
192.168.1.35
192.168.1.100
192.168.1.250
```

❌ Doesn't match

```
192.168.2.1
192.168.5.20
10.0.0.1
```

---

# 🔹 Local Routes

Cisco IOS also creates a **Local route** automatically.

Example

```
Interface

192.168.1.1/24
```

Creates

```
L 192.168.1.1/32
```

This route represents:

> The router's own interface IP address.

Meaning

> "Packets destined for this exact IP are for me."

The router receives them instead of forwarding them.

---

## Why /32?

```
255.255.255.255
```

means

Every single bit is fixed.

Only ONE address exists.

```
192.168.1.1/32
```

matches

```
192.168.1.1
```

only.

Nothing else.

---

# 🔹 Connected vs Local Routes

| Connected Route | Local Route |
|----------------|-------------|
| Network | Interface IP |
| Example: 192.168.1.0/24 | Example: 192.168.1.1/32 |
| Used for forwarding | Used for receiving |
| Matches many hosts | Matches one host |

---

# 🔹 Route Matching

A route matches if:

> The packet's destination belongs to the network specified by the route.

Example

Route:

```
192.168.1.0/24
```

Destination

```
192.168.1.55
```

Result

✅ Match

Destination

```
192.168.2.5
```

Result

❌ No Match

---

# 🔹 Longest Prefix Match

Sometimes multiple routes match the same destination.

Example

```
192.168.1.0/24

192.168.1.1/32
```

Packet destination

```
192.168.1.1
```

Both routes match.

Which one wins?

The router always chooses the:

> **Most Specific Match**

Also called:

> **Longest Prefix Match**

---

### Why?

```
192.168.1.0/24

covers

256 addresses
```

while

```
192.168.1.1/32

covers

1 address
```

The /32 route is more specific.

Therefore it wins.

---

# 🔹 Route Selection Process

Whenever a router receives a packet:

```
Receive Packet
      │
      ▼
Read Destination IP
      │
      ▼
Search Routing Table
      │
      ▼
Matching Route?
      │
 ┌────┴────┐
 │         │
Yes        No
 │         │
 ▼         ▼
Choose     Drop Packet
Longest
Prefix
 │
 ▼
Forward Packet
```

---

# 🔹 What Happens if No Route Exists?

If the router cannot find any matching route:

```
Packet

↓

Dropped
```

Unlike switches:

- Switches flood unknown frames.
- Routers **do not flood packets**.

No matching route = Drop.

---

# 🔹 Cisco IOS Example

```
show ip route
```

Output

```
C 192.168.1.0/24 is directly connected, GigabitEthernet0/2

L 192.168.1.1/32 is directly connected, GigabitEthernet0/2
```

Interpretation

Connected route

```
Send packets destined for
192.168.1.0/24

out G0/2
```

Local route

```
Packets destined for
192.168.1.1

belong to me.
```

---

# 📝 Exam Tips

- Routing determines the best path to a destination.
- Routers use the **routing table** to forward packets.
- Use `show ip route` to view the routing table.
- Connected routes are automatically created when an interface is configured and enabled.
- Local routes are automatically created for the interface's own IP address.
- Connected routes represent **networks**.
- Local routes represent **a single IP address**.
- `/24` matches 256 addresses.
- `/32` matches exactly one address.
- Routers choose the **Longest Prefix Match**.
- If no matching route exists, the router drops the packet.
- **Next-hop** means the next router toward the destination, not the final destination itself.

---

# 📝 Summary

- Routing is the process of forwarding packets toward their destination.
- Routers consult a routing table to determine the best path.
- Static routes are manually configured, while dynamic routes are learned automatically through routing protocols.
- Configuring and enabling an interface automatically creates two routes:
  - A **Connected (C)** route for the directly attached network.
  - A **Local (L)** route for the router's own interface IP address.
- A route matches a packet when the destination IP belongs to that network.
- When multiple routes match, the router always selects the **Longest Prefix Match (most specific route)**.
- If no route matches the destination, the router drops the packet instead of forwarding or flooding it.

---
