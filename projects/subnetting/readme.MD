# Subnetting

---

# Objective

The objective of this activity is to design and configure a network in Cisco Packet Tracer.  
Multiple devices will be configured with IP addresses, subnet masks, and default gateways.

Additionally, the main network will be divided into multiple subnets using **VLSM (Variable Length Subnet Masking)**.

---

# Main Network

The company network is identified as:

192.168.16.0/21


### Network Information

| Concept | Value |
|----------|--------|
| Subnet Mask | 255.255.248.0 |
| Network Address | 192.168.16.0 |
| First Usable IP | 192.168.16.1 |
| Last Usable IP | 192.168.23.254 |
| Broadcast Address | 192.168.23.255 |
| Total IP Addresses | 2048 |
| Usable IP Addresses | 2046 |

---

# Subnetting (VLSM)

To improve network management, the network is divided into four subnets:

- Finance Department  
- IT Department  
- Administration Department  
- Router-to-Router connection  

Subnets are assigned consecutively, starting from the lowest available network addresses.

---

## Finance Subnet

| Concept | Value |
|----------|--------|
| Devices | 218 |
| Subnet Mask | 255.255.255.0 |
| Network Address | 192.168.16.0 |
| First Usable IP | 192.168.16.1 |
| Last Usable IP | 192.168.16.254 |
| Broadcast Address | 192.168.16.255 |
| Total IPs | 256 |
| Usable IPs | 254 |

---

## IT Subnet

| Concept | Value |
|----------|--------|
| Devices | 118 |
| Subnet Mask | 255.255.255.128 |
| Network Address | 192.168.17.0 |
| First Usable IP | 192.168.17.1 |
| Last Usable IP | 192.168.17.126 |
| Broadcast Address | 192.168.17.127 |
| Total IPs | 128 |
| Usable IPs | 126 |

---

## Administration Subnet

| Concept | Value |
|----------|--------|
| Devices | 18 |
| Subnet Mask | 255.255.255.224 |
| Network Address | 192.168.17.128 |
| First Usable IP | 192.168.17.129 |
| Last Usable IP | 192.168.17.158 |
| Broadcast Address | 192.168.17.159 |
| Total IPs | 32 |
| Usable IPs | 30 |

---

## Router Subnet

| Concept | Value |
|----------|--------|
| Devices | 2 |
| Subnet Mask | 255.255.255.252 |
| Network Address | 192.168.17.160 |
| First Usable IP | 192.168.17.161 |
| Last Usable IP | 192.168.17.162 |
| Broadcast Address | 192.168.17.163 |
| Total IPs | 4 |
| Usable IPs | 2 |

---

# Network Topology (Cisco Packet Tracer)

## Devices Used

- 1 Router 2911 (Router0)
- 3 Switch 2960 (Switch0, Switch1, Switch2)
- 4 PCs (PC0, PC1, PC2, PC3)

Each department is connected to its own switch, and each switch connects to the router.

---

# Router Configuration

Each GigabitEthernet interface was configured with:

- The **first usable IP address** of its corresponding subnet
- The correct subnet mask
- Interface enabled (Port Status: ON)

---

# PC Configuration

Each PC was configured with:

- A static IP address within its subnet range  
- The correct subnet mask  
- Default gateway set to the router interface IP (except PC1)

---

# Connectivity Test

Ping tests were performed between all PCs.

| Source \ Destination | PC0 | PC1 | PC2 | PC3 |
|----------------------|------|------|------|------|
| **PC0** | - | YES | YES | YES |
| **PC1** | YES | - | NO | NO |
| **PC2** | YES | NO | - | YES |
| **PC3** | YES | NO | YES | - |

---

# Explanation

Not all PCs can communicate with each other.

Only devices with a configured **default gateway** can communicate with other subnets.

- PC0 can ping all devices because it has a gateway configured.
- PC1 cannot reach other subnets because it does not have a gateway configured.
- Devices without a gateway can only communicate within their own subnet.

For full inter-subnet communication, every device must have its default gateway properly configured.
