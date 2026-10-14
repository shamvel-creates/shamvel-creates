# Day 07 – Network Troubleshooting & Practical Review

## 🎯 Objective

Practise Windows networking commands, test connectivity, investigate DNS resolution, trace network routes, and apply basic troubleshooting techniques.

---

## 1. Practical Network Configuration

During this lab, I connected my Windows laptop to a mobile hotspot and inspected the assigned network configuration.

### Network Configuration

| Setting | Value |
|---|---|
| IPv4 Address | 10.104.249.76 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 10.104.249.208 |

### Key Learning

When I connected to a different network, my laptop received a different IP configuration through DHCP.

My earlier network used a `192.168.29.x` address range, while the mobile hotspot assigned an address in the `10.104.249.x` range.

This demonstrated that the same computer can receive different IP addresses when connecting to different networks.

---

## 2. Testing the Local TCP/IP Stack

### Command

```cmd
ping 127.0.0.1
```

### Purpose

The loopback address `127.0.0.1` tests local TCP/IP communication on the computer.

### Observation

The ping test succeeded.

### Learning

The local TCP/IP stack responded to the loopback test. This does not independently verify Wi-Fi or internet connectivity.

---

## 3. Testing the Default Gateway

### Command

```cmd
ping 10.104.249.208
```

### Purpose

Tests ICMP connectivity to the current default gateway.

### Observation

The gateway responded successfully.

### Learning

The computer could communicate with its mobile hotspot gateway during the test.

---

## 4. Testing Public IP Connectivity

### Command

```cmd
ping 8.8.8.8
```

### Purpose

Tests ICMP connectivity to Google's public DNS IP address.

### Observation

The test succeeded.

### Learning

The computer could reach the public IP address and receive ICMP replies at that time.

A successful ping does not prove that every internet service is working.

---

## 5. Testing DNS Resolution

### Command

```cmd
nslookup google.com
```

### Purpose

Queries a DNS server to resolve a domain name.

### Observation

The lookup succeeded and returned DNS information for `google.com`.

### Learning

DNS resolution was working for this query.

---

## 6. Investigating the Network Route

### Command

```cmd
tracert google.com
```

### Purpose

Traces the network path towards the destination by sending probes with increasing TTL values.

### Initial Observation

Some traceroute probes timed out, which initially appeared to indicate a failure.

### Further Investigation

The route trace eventually completed and reached the destination in 10 hops.

The output showed an IPv6 destination:

```text
2404:6800:4007:838::200e
```

Some intermediate hops did not respond to the probes, but later hops responded and the destination was reached.

### Learning

A traceroute timeout does not automatically mean that a router or network connection is broken. Some devices filter or deprioritize traceroute responses.

The final output included:

```text
Trace complete.
```

This confirmed that the trace reached its destination.

---

## 7. IPv4 and IPv6 Traceroute

Windows can use IPv4 or IPv6 depending on name resolution and network configuration.

### Force IPv4

```cmd
tracert -4 -d google.com
```

### Force IPv6

```cmd
tracert -6 -d google.com
```

These commands allow the routes to be investigated separately.

The two routes may differ because IPv4 and IPv6 can use different network paths.

---

## 8. Commands Practised

```cmd
ipconfig /all
ping 127.0.0.1
ping 10.104.249.208
ping 8.8.8.8
nslookup google.com
tracert google.com
tracert -4 -d google.com
tracert -6 -d google.com
```

---

## 9. Basic Troubleshooting Workflow

```text
Check IP configuration
          |
          v
Test local TCP/IP stack
          |
          v
Test default gateway
          |
          v
Test public IP connectivity
          |
          v
Test DNS resolution
          |
          v
Investigate the route using tracert
          |
          v
Analyse results before making changes
```

### Important troubleshooting principles

- Check the current IP configuration before testing a gateway.
- Use the current default gateway, not an address from an old network.
- Use ping to test ICMP connectivity, not to prove every service is working.
- Use nslookup to investigate DNS resolution.
- Use tracert to investigate the route towards a destination.
- Investigate timeouts instead of assuming that every timeout indicates a fault.
- Avoid changing network settings before identifying evidence of a problem.

---

## 10. Key Learnings

- IP addresses can change when a device connects to a different network.
- DHCP commonly assigns IP addresses and other network settings automatically.
- The default gateway is used to reach destinations outside the local subnet.
- The loopback address `127.0.0.1` tests local TCP/IP communication.
- Ping tests ICMP connectivity.
- Nslookup helps investigate DNS resolution.
- Tracert investigates the network path towards a destination.
- IPv4 and IPv6 can follow different routes.
- Some routers do not respond to traceroute probes even when they forward traffic.
- Troubleshooting should follow evidence and a logical sequence.

---

## 📌 Day 07 Status

**Completed:** Practical network troubleshooting and revision of networking fundamentals.

**Next topic:** Day 08 – Linux Fundamentals and Essential Terminal Commands.
