# 🌐 Day 03 - TCP/IP Model & Network Communication

## 🎯 Objectives

After completing this topic, you should be able to:

* Explain what protocols and standards are.
* Describe how TCP/IP became the Internet standard.
* Identify the organizations responsible for networking standards.
* Understand the TCP/IP and OSI models.
* Explain the purpose of each TCP/IP layer.
* Describe encapsulation and decapsulation.
* Identify Protocol Data Units (PDUs).
* Explain payloads.
* Understand how layers interact during communication.

---

# 📖 Protocols and Standards

## 📜 Protocol

A **protocol** is a set of rules that devices follow to communicate across a network.

Without protocols, computers would not understand each other's messages.

### Example

* HTTP for web browsing
* TCP for reliable communication
* IP for addressing

---

## 📏 Standard

A **standard** is an agreed-upon specification describing how technologies and protocols should operate.

Standards allow devices made by different manufacturers to communicate with one another.

### Example

A Windows PC can communicate with a Linux server because both follow the same networking standards.

---

# 📖 History of TCP/IP

Networking research began during the 1960s with **ARPANET**, funded by the U.S. Department of Defense.

Originally, ARPANET used the **Network Control Program (NCP)**. In 1974, **Vint Cerf** and **Bob Kahn** developed TCP, which was later divided into:

* Transmission Control Protocol (TCP)
* Internet Protocol (IP)

On **January 1, 1983**, ARPANET officially switched to TCP/IP, which eventually became the foundation of today's Internet.

---

# 📖 Networking Standards Organizations

## ⚡ IEEE (Institute of Electrical and Electronics Engineers)

Develops standards primarily for Local Area Networks (LANs).

Examples:

* IEEE 802.3 → Ethernet
* IEEE 802.11 → Wi-Fi

---

## 🌍 IETF (Internet Engineering Task Force)

Develops Internet protocols and publishes standards as **RFCs (Requests for Comments).**

Examples:

* TCP
* UDP
* IP
* HTTP
* DNS

---

# 📖 Why Use Layered Models?

Sending data across a network involves many independent tasks.

Instead of one large, complex process, networking divides responsibilities into layers.

### Benefits

* Easier troubleshooting
* Modular design
* Easier upgrades
* Standardization
* Independent layer operation

Each layer provides services to the layer above while using the services of the layer below.

---

# 📖 TCP/IP Five-Layer Model

## 🟨 Layer 5 — Application

Provides network services directly to applications and defines how application data is formatted, transmitted, and interpreted.

Common protocols:

* HTTP
* HTTPS
* FTP
* SMTP
* DNS

### Example

Opening a webpage in Chrome uses HTTP or HTTPS.

---

## 🟪 Layer 4 — Transport

Provides **process-to-process (end-to-end)** communication between applications.

Responsible for:

* Port numbers
* Reliability (TCP)
* Flow control (TCP)
* Multiplexing application traffic

Common protocols:

* TCP
* UDP

### Example

A web browser sends data to **Port 80 (HTTP)** or **Port 443 (HTTPS).**

---

## 🟩 Layer 3 — Internet

Provides **end-to-end communication between hosts** across multiple networks using IP addresses.

Responsible for:

* Logical addressing
* Routing
* Packet forwarding

Common protocols:

* IPv4
* IPv6
* ICMP

Routers primarily operate at this layer.

### Example

A router forwards a packet toward the destination IP address **10.1.1.1**.

---

## 🟥 Layer 2 — Local Network

Provides **hop-to-hop communication** within a local network using MAC addresses.

Responsible for:

* MAC addressing
* Frame forwarding
* Error detection

Common protocols:

* Ethernet
* Wi-Fi

Switches primarily operate at this layer.

### Example

A switch forwards a frame using the destination MAC address.

---

## ⬜ Layer 1 — Physical

Responsible for transmitting bits across the physical medium as electrical, optical, or radio signals.

Examples:

* Copper UTP cables
* Fiber-optic cables
* Radio waves
* Network Interface Cards (NICs)

### Example

A binary 1 or 0 is transmitted as an electrical or optical signal.

---

# 📖 Encapsulation

As data moves down the TCP/IP stack, each layer adds information needed for communication.

* Layer 4 adds a header.
* Layer 3 adds a header.
* Layer 2 adds both a header and a trailer.

Each layer creates a new Protocol Data Unit (PDU) for transmission.

```text
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

---

# 📖 Decapsulation

The receiving device removes headers (and the Layer 2 trailer) one layer at a time until the original application data reaches the destination application.

```text
Bits
 ↑
Frame
 ↑
Packet
 ↑
Segment / Datagram
 ↑
Application Data
```

---

# 📖 Protocol Data Units (PDUs)

Each layer refers to the transmitted data by a different name.

| Layer         | PDU                            |
| ------------- | ------------------------------ |
| Application   | Data                           |
| Transport     | Segment (TCP) / Datagram (UDP) |
| Internet      | Packet                         |
| Local Network | Frame                          |
| Physical      | Bits                           |

---

# 📖 Payload

A **payload** is the data carried inside a Protocol Data Unit (PDU), excluding that layer's own header (and trailer, if applicable).

As data moves through the stack, each layer treats the entire PDU from the layer above as its payload.

### Example

* A Layer 3 packet contains a Layer 4 segment as its payload.
* A Layer 2 frame contains the entire Layer 3 packet as its payload.

---

# 📖 Layer Interaction

## Adjacent-Layer Interaction

Each layer communicates directly with the layer immediately above and below it.

Examples:

* Transport uses Internet layer services.
* Internet uses Local Network layer services.
* Local Network uses Physical layer services.

---

## Same-Layer Interaction

Each layer logically communicates with the corresponding layer on another device.

Examples:

* HTTP ↔ HTTP
* TCP ↔ TCP
* IP ↔ IP
* Ethernet ↔ Ethernet

---

# 📖 Separation of Layers

Each layer performs a specific responsibility while remaining largely independent from the others.

Changing one layer usually does **not** require changes to the remaining layers.

### Example

Replacing Ethernet with Wi-Fi only affects the Local Network and Physical layers. Applications such as HTTP continue working without modification.

---

# 📖 OSI Model

The **OSI (Open Systems Interconnection)** model is a seven-layer reference model developed by ISO.

Although TCP/IP became the networking standard used in real-world networks, the OSI model remains widely used for learning, troubleshooting, and discussing network communication.

| TCP/IP        | OSI          |
| ------------- | ------------ |
| Application   | Application  |
|               | Presentation |
|               | Session      |
| Transport     | Transport    |
| Internet      | Network      |
| Local Network | Data Link    |
| Physical      | Physical     |

---

# 📖 TCP/IP vs OSI

| TCP/IP                   | OSI                                |
| ------------------------ | ---------------------------------- |
| 5 layers                 | 7 layers                           |
| Used in modern networks  | Reference model                    |
| Practical implementation | Conceptual model                   |
| Protocol suite           | Teaching and troubleshooting model |

---

# 📝 Summary

* A protocol defines the rules for network communication.
* Standards allow devices from different vendors to communicate.
* TCP/IP became the Internet standard in **1983**.
* IEEE develops LAN technologies such as Ethernet and Wi-Fi.
* IETF develops Internet protocols and publishes RFCs.
* The TCP/IP model divides communication into five layers.
* Layer 2 provides hop-to-hop communication using MAC addresses.
* Layer 3 provides end-to-end communication using IP addresses.
* Layer 4 provides process-to-process communication using port numbers.
* Data is encapsulated before transmission and decapsulated upon reception.
* PDUs change names as data moves through the network stack.
* Payload is the data carried inside a PDU after excluding that layer's own header.
* The OSI model is mainly used for learning and troubleshooting.
* Each layer has a dedicated responsibility, making networks modular and easier to maintain.
