# Day 1 — Networking Fundamentals

**Date:** September 2026

## Topics Learned

- Computer networks
- LAN vs WAN
- IP address
- MAC address
- Switch
- Router
- Default Gateway
- DHCP
- DNS
- Basic network troubleshooting

## Key Concepts

### IP Address
An IP address is a logical address used to identify and communicate with a device on a network.

Example:

`192.168.1.10`

### MAC Address
A MAC address is associated with a network interface and is used for communication on the local network.

### Switch
A switch connects multiple devices within a local network and forwards traffic to the appropriate device.

### Router
A router connects different networks and forwards traffic between them.

### Default Gateway
The default gateway is the device a computer sends traffic to when the destination is outside its local network.

### DHCP
DHCP automatically provides network configuration such as:

- IP address
- Subnet mask
- Default gateway
- DNS server

### DNS
DNS helps resolve domain names to IP addresses.

Example:

`google.com → IP address`

## Practical Commands

```text
ipconfig
ipconfig /all
ping 8.8.8.8
ping google.com
nslookup google.com
