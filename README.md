# RIP Simulation Using Cisco Packet Tracer

### Vasanth M
### 212223060295
### Department of ECE

# Introduction

Routing Information Protocol (RIP) is a dynamic routing protocol used in computer networks to exchange routing information between routers automatically. RIP helps routers determine the best path for forwarding packets using hop count as the routing metric.

RIP is one of the simplest routing protocols and is widely used for educational purposes and small networks.

---

# Objective

- To understand the working of RIP
- To configure dynamic routing between routers
- To establish communication between different networks
- To simulate routing using Cisco Packet Tracer
- To observe routing updates and packet flow

---

# Software Requirements

- Cisco Packet Tracer

---

# Devices Used

| Device | Quantity |
|---|---|
| PC | 2 |
| Switch | 2 |
| Router | 2 |
| Copper Straight Through Cable | Multiple |
| Serial DCE Cable | 1 |

---

# Network Topology


<img width="1774" height="887" alt="image" src="https://github.com/user-attachments/assets/0c65f943-6287-4bba-a928-43cc5ed802f0" />

# IP Address Configuration

| Device | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| PC0 | FastEthernet0 | 192.168.1.2 | 255.255.255.0 |
| Router0 | FastEthernet0/0 | 192.168.1.1 | 255.255.255.0 |
| Router0 | Serial0/0/0 | 10.0.0.1 | 255.255.255.252 |
| Router1 | Serial0/0/0 | 10.0.0.2 | 255.255.255.252 |
| Router1 | FastEthernet0/0 | 192.168.2.1 | 255.255.255.0 |
| PC1 | FastEthernet0 | 192.168.2.2 | 255.255.255.0 |


# Theory of RIP

Routing Information Protocol (RIP) is a distance-vector routing protocol that uses hop count to find the best path between networks.
<img width="937" height="364" alt="image" src="https://github.com/user-attachments/assets/d4e5f365-1fbc-472b-acce-67151dc5c379" />


## Features of RIP

- Distance-vector routing protocol
- Uses hop count as metric
- Maximum hop count is 15
- Routing updates every 30 seconds
- Uses UDP port 520
- Easy to configure

---

# Working Principle of RIP

1. Routers are configured with RIP.
2. Each router discovers directly connected networks.
3. Routers exchange routing tables periodically.
4. Routers update routing tables using received information.
5. Best path is selected using minimum hop count.
6. Data packets are forwarded through the selected path.
<img width="944" height="265" alt="image" src="https://github.com/user-attachments/assets/218ce497-c0f8-4bb1-922f-817685e8ae13" />

---

# RIP Routing Process

## Step 1 — Router Initialization

Each router creates its routing table using directly connected networks.
<img width="1920" height="1080" alt="Screenshot 2026-06-02 111939" src="https://github.com/user-attachments/assets/a3ef1000-89fb-4ed2-a2ee-3bf30630820b" />


---

## Step 2 — Discover Connected Networks

Router0 discovers:
- 192.168.1.0/24
- 10.0.0.0/30

Router1 discovers:
- 192.168.2.0/24
- 10.0.0.0/30

---

## Step 3 — Exchange Routing Information

Routers exchange routing tables every 30 seconds using UDP port 520.

---

## Step 4 — Routing Table Update

Routers update routing tables with received network information.

---

## Step 5 — Best Path Selection

The shortest path is selected using minimum hop count.

---

## Step 6 — Packet Transmission

Data packets are forwarded between networks successfully.

---

# Procedure

## Step 1 — Open Cisco Packet Tracer

Launch Cisco Packet Tracer software.

---

## Step 2 — Add Devices

Add:
- 2 PCs
- 2 Switches
- 2 Routers

---

## Step 3 — Connect Devices

### Connections

```text
PC0 → Switch0
Switch0 → Router0
Router0 → Router1
Router1 → Switch1
Switch1 → PC1
```

Use:
- Copper Straight Through Cable
- Serial DCE Cable

---

# PC Configuration

## PC0

```text
IP Address : 192.168.1.2
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
```
<img width="992" height="560" alt="image" src="https://github.com/user-attachments/assets/768e7969-1f29-4d24-be3e-e738424db31b" />

---

## PC1

```text
IP Address : 192.168.2.2
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.2.1
```
<img width="992" height="561" alt="image" src="https://github.com/user-attachments/assets/64705dc3-0b53-426f-beac-f978e8741690" />

---

# Router Configuration

## Router0 Configuration

```bash
enable
configure terminal

interface fastethernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

interface serial0/0/0
ip address 10.0.0.1 255.255.255.252
clock rate 64000
no shutdown

router rip
version 2
network 192.168.1.0
network 10.0.0.0
no auto-summary
```

---

## Router1 Configuration

```bash
enable
configure terminal

interface fastethernet0/0
ip address 192.168.2.1 255.255.255.0
no shutdown

interface serial0/0/0
ip address 10.0.0.2 255.255.255.252
no shutdown

router rip
version 2
network 192.168.2.0
network 10.0.0.0
no auto-summary
```

---

# Packet Flow

## ICMP Echo Request Flow

```text
PC0 → Switch0 → Router0 → Router1 → Switch1 → PC1
```

---

## ICMP Echo Reply Flow

```text
PC1 → Switch1 → Router1 → Router0 → Switch0 → PC0
```

---

# Testing Connectivity

From PC0 Command Prompt:

```bash
ping 192.168.2.2
```

---

# Expected Output

```bash
Reply from 192.168.2.2: bytes=32 time<1ms TTL=126
```

Ping Statistics:

```text
Packets: Sent = 4
Packets: Received = 4
Packets: Lost = 0
```

---

# Advantages of RIP

1. Easy to configure
2. Automatic route updates
3. Suitable for small networks
4. Simple routing mechanism
5. Low configuration complexity

---

# Disadvantages of RIP

1. Slow convergence
2. Maximum hop count is 15
3. Not suitable for large networks
4. Generates periodic traffic
5. Less efficient than modern protocols

---

# Applications of RIP

1. Small office networks
2. Educational simulations
3. Basic routing implementation
4. LAN routing
5. Academic networking experiments

---

# Real-Time Scenario of RIP

Consider two branch offices connected using routers.

- Office A network: 192.168.1.0/24
- Office B network: 192.168.2.0/24

RIP automatically exchanges routing information between routers and allows communication between devices in both offices.

---

# Conclusion

Thus, the RIP simulation was successfully implemented using Cisco Packet Tracer. Dynamic routing was established between two different networks using RIP. Routers exchanged routing information automatically and successfully forwarded packets between networks.

---

# Viva Questions and Answers

## 1. What is RIP?

RIP stands for Routing Information Protocol.

---

## 2. Which metric is used by RIP?

Hop count.

---

## 3. What is the maximum hop count in RIP?

15 hops.

---

## 4. Which port does RIP use?

UDP port 520.

---

## 5. Which type of routing protocol is RIP?

Distance-vector routing protocol.

---

## 6. Why is RIP called dynamic routing?

Because routers exchange routing information automatically.

---

## 7. Which software is used for this simulation?

Cisco Packet Tracer.

---

## 8. What is the purpose of RIP?

To determine the best path between networks automatically.

---

## 9. What happens when hop count exceeds 15?

Destination becomes unreachable.

---

## 10. Which command enables RIP?

```bash
router rip
```

---

# References

1. Cisco Networking Academy

2. Cisco Packet Tracer Documentation

3. Data Communications and Networking — Behrouz A. Forouzan

4. Computer Networks — Andrew S. Tanenbaum

5. Routing and Switching Essentials — Cisco
