

# CCNA Lab 01 - Basic Connectivity Test

## Objective

Learn how to configure basic IPv4 addressing on end devices and verify connectivity using the `ping` command.

---

## Topology

PC0 -------- Switch0 -------- Laptop0

Devices Used:

- 1x PC
    
- 1x Laptop
    
- 1x Switch (2960)
    

---

## IP Addressing

### PC0

- IP Address: 192.168.1.10
    
- Subnet Mask: 255.255.255.0
    
- Default Gateway: 192.168.1.1
    

### Laptop0

- IP Address: 192.168.1.20
    
- Subnet Mask: 255.255.255.0
    
- Default Gateway: 192.168.1.1
    

Network:

- 192.168.1.0/24
    

---

## Configuration Steps

### PC0

Desktop → IP Configuration

Configure:

- IP Address: 192.168.1.10
    
- Subnet Mask: 255.255.255.0
    
- Default Gateway: 192.168.1.1
    

### Laptop0

Desktop → IP Configuration

Configure:

- IP Address: 192.168.1.20
    
- Subnet Mask: 255.255.255.0
    
- Default Gateway: 192.168.1.1
    

---

## Verification

### Check PC0 Configuration

```cmd
ipconfig
```

Expected Result:

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
```

### Check Laptop0 Configuration

```cmd
ipconfig
```

Expected Result:

```text
IP Address: 192.168.1.20
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
```

### Connectivity Test

From PC0:

```cmd
ping 192.168.1.20
```

Result:

```text
Reply from 192.168.1.20
Packets: Sent = 4, Received = 4, Lost = 0
```

From Laptop0:

```cmd
ping 192.168.1.10
```

Result:

```text
Reply from 192.168.1.10
Packets: Sent = 4, Received = 4, Lost = 0
```

---

## Concepts Learned

- What an IPv4 address is
    
- What a subnet mask does
    
- Purpose of a default gateway
    
- How devices communicate within the same network
    
- How to use `ipconfig`
    
- How to use `ping`
    
- Basic Packet Tracer navigation
    

---

## Notes

Both devices successfully communicated through the switch.

Since both hosts are in the same subnet (192.168.1.0/24), communication occurs directly through Layer 2 switching and does not require a router.

This was my first Packet Tracer lab while beginning CCNA studies with Jeremy's IT Lab.

File:  
01-basic-ping.pkt
![[images/Screenshot 2026-06-23 081058.png]]![[images/Screenshot 2026-06-23 081043.png]] ![[images/Screenshot 2026-06-23 081024.png]] 