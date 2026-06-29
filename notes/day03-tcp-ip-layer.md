# 🌐 TCP/IP Model & Network Communication

## 🎯 Objectives

After completing this topic, you should be able to:

- Explain what protocols and standards are.
- Describe how TCP/IP became the Internet standard.
- Identify the organizations responsible for networking standards.
- Understand the TCP/IP and OSI models.
- Explain the purpose of each TCP/IP layer.
- Describe encapsulation and decapsulation.
- Identify Protocol Data Units (PDUs).
- Understand how layers interact during communication.

---

# 📖 Protocols and Standards

## 📜 Protocol

A **protocol** is a set of rules that devices follow to communicate across a network.

Without protocols, computers would not understand each other's messages.

### Example

- HTTP for web browsing
- TCP for reliable communication
- IP for addressing

---

## 📏 Standard

A **standard** is an agreed specification describing how technologies should work.

Standards allow devices made by different manufacturers to communicate.

### Example

A Windows PC can communicate with a Linux server because both follow the same networking standards.

---

# 📖 History of TCP/IP

Networking research began during the 1960s with **ARPANET**, funded by the U.S. Department of Defense.

Originally ARPANET used **NCP**, but in 1974 **Vint Cerf** and **Bob Kahn** developed TCP.

Later TCP was divided into:

- TCP
- IP

On **January 1, 1983**, ARPANET officially switched to TCP/IP, which eventually became the foundation of today's Internet.

---

# 📖 Networking Standards Organizations

## ⚡ IEEE

Responsible for technologies used mainly on Local Area Networks (LANs).

Examples:

- Ethernet (802.3)
- Wi-Fi (802.11)

---

## 🌍 IETF

Develops Internet protocols.

Examples:

- TCP
- UDP
- IP
- HTTP
- DNS

The IETF publishes standards as **RFCs (Request for Comments).**

---

# 📖 Why Use Layered Models?

Sending data across a network involves many independent tasks.

Instead of one huge complicated process, networking divides responsibilities into **layers**.

Benefits:

- Easier troubleshooting
- Modular design
- Easier upgrades
- Standardization

Each layer provides services to the layer above while using services from the layer below.

---

# 📖 TCP/IP Five-Layer Model

## 🟨 Layer 5 — Application

Provides network services directly to applications.

Common protocols:

- HTTP
- HTTPS
- FTP
- SMTP
- DNS

### Example

Opening a webpage in Chrome uses HTTP/HTTPS.

---

## 🟪 Layer 4 — Transport

Provides end-to-end communication between applications.

Uses:

- TCP
- UDP

Responsible for:

- Port numbers
- Reliability
- Flow control

### Example

A web browser sends data to **Port 80** (HTTP) or **Port 443** (HTTPS).

---

## 🟩 Layer 3 — Internet

Responsible for communication between different networks.

Uses:

- IPv4
- IPv6
- ICMP

Routers operate mainly at this layer.

### Example

The packet is addressed to **10.1.1.1**.

---

## 🟥 Layer 2 — Local Network

Responsible for communication inside the local network.

Uses:

- MAC addresses
- Ethernet
- Wi-Fi

Switches mainly operate here.

### Example

The switch forwards frames using the destination MAC address.

---

## ⬜ Layer 1 — Physical

Responsible for transmitting bits through the physical medium.

Examples:

- Copper cables
- Fiber optic cables
- Radio waves
- Network Interface Cards (NICs)

### Example

A binary 1 or 0 becomes an electrical or optical signal.

---

# 📖 Encapsulation

When data is sent, each layer adds its own information.

The process is called **encapsulation**.

Order:

```

Application Data
↓
Transport Header
↓
Internet Header
↓
Local Network Header + Trailer
↓
Bits

```

Each layer wraps the previous layer.

---

# 📖 Decapsulation

The receiving device removes headers one by one.

The process is called **decapsulation**.

Order:

```

Bits
↑
Frame
↑
Packet
↑
Segment
↑
Application Data

```

Eventually the application receives the original data.

---

# 📖 Protocol Data Units (PDUs)

Each layer gives the data a different name.

| Layer | PDU |
|--------|-----|
| Application | Data |
| Transport | Segment (TCP) / Datagram (UDP) |
| Internet | Packet |
| Local Network | Frame |
| Physical | Bits |

---

# 📖 Layer Interaction

## Adjacent-Layer Interaction

Each layer only communicates with the layer directly above and below it.

Example:

Transport uses Internet services.

Internet uses Local Network services.

---

## Same-Layer Interaction

Each layer appears to communicate with its corresponding layer on another device.

Example:

HTTP communicates with HTTP.

TCP communicates with TCP.

IP communicates with IP.

Ethernet communicates with Ethernet.

---

# 📖 Separation of Layers

Each layer performs a specific task.

Changing one layer usually does **not** require changing the others.

Example:

Replacing Ethernet with Wi-Fi only affects the Local Network and Physical layers.

Applications continue working normally.

---

# 📖 OSI Model

The OSI Model is a **7-layer reference model** created by ISO.

Although TCP/IP became the real-world standard, the OSI model is widely used for learning and troubleshooting.

| TCP/IP | OSI |
|---------|-----|
| Application | Application |
| | Presentation |
| | Session |
| Transport | Transport |
| Internet | Network |
| Local Network | Data Link |
| Physical | Physical |

---

# 📝 Summary

- A protocol defines communication rules.
- Standards allow different vendors' devices to communicate.
- TCP/IP became the Internet standard in 1983.
- IEEE develops LAN technologies like Ethernet and Wi-Fi.
- IETF develops Internet protocols and RFCs.
- The TCP/IP model has five layers.
- Data is encapsulated before transmission and decapsulated upon reception.
- PDUs change names as data moves through the stack.
- Each layer has a dedicated responsibility.
- The OSI model is mainly used as a learning and reference model.