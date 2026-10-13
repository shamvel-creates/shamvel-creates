# Day 04 – DHCP (Dynamic Host Configuration Protocol)

## 🎯 Objective

Understand how devices automatically obtain IP addresses and network configuration using DHCP, how the DORA process works, and how to troubleshoot basic DHCP problems in Windows.

---

## 1. What is DHCP?

**DHCP stands for Dynamic Host Configuration Protocol.**

DHCP automatically provides network configuration to devices when they connect to a network.

These settings can include:

- IPv4 address
- Subnet mask
- Default gateway
- DNS server
- IP address lease duration

### Example

When a laptop connects to Wi-Fi, it may automatically receive:

| Network Setting | Example |
|---|---|
| IPv4 Address | 192.168.1.100 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.1.1 |
| DNS Server | Provided by the network |

A DHCP server manages and assigns IP addresses from an available address pool.

In a home network, the router often acts as the DHCP server. In an organization, a dedicated DHCP server may be used.

---

## 2. Why Do We Need DHCP?

Without DHCP, an administrator might need to configure network settings manually on every device.

DHCP helps to:

- Reduce manual configuration.
- Prevent many common IP configuration mistakes.
- Manage IP address allocation.
- Reuse addresses when leases expire and addresses become available.
- Provide gateway and DNS settings automatically.

---

## 3. DORA Process

DORA represents the four main steps in the initial DHCP IPv4 address assignment process.

### D – Discover

The client searches for an available DHCP server.

### O – Offer

The DHCP server offers an IP address and other configuration details.

### R – Request

The client requests the offered IP address.

### A – Acknowledge

The DHCP server confirms the assignment.

### DORA Flow

```text
Client connects to network
          |
          v
      DISCOVER
          |
          v
        OFFER
          |
          v
       REQUEST
          |
          v
     ACKNOWLEDGE
          |
          v
Client receives network configuration
```

**Remember: DORA = Discover → Offer → Request → Acknowledge.**

The initial discovery commonly uses a broadcast because the client may not yet have an IPv4 address or know the DHCP server's address.

---

## 4. DHCP Lease

A DHCP lease is a time-limited assignment of an IP address to a client.

For example, a laptop may receive an IP address for a specified lease period.

Before the lease expires, the client can attempt to renew it.

### Why is a lease useful?

- Addresses can be reused when they are no longer needed.
- Administrators can manage address pools efficiently.
- Temporary devices can obtain network access without permanent manual configuration.

### DHCP Reservation vs Static IP

**DHCP reservation:** The DHCP server is configured to assign a particular address to a specific device, commonly identified by its MAC address.

**Static IP:** The address is manually configured on the device or interface.

These are different methods of managing IP addresses.

---

## 5. Practical Windows Commands

### Command 1: View complete network configuration

```cmd
ipconfig /all
```

This displays detailed information about network adapters, including:

- IPv4 address
- Subnet mask
- Default gateway
- DHCP Enabled
- DHCP Server
- DNS servers
- Lease Obtained
- Lease Expires

### Command 2: Release the current DHCP IPv4 configuration

```cmd
ipconfig /release
```

This releases the current DHCP-assigned IPv4 configuration for the selected adapter. Connectivity may be interrupted.

### Command 3: Request or renew the DHCP configuration

```cmd
ipconfig /renew
```

This asks DHCP to obtain or renew the IPv4 configuration.

### Command 4: Verify the result

```cmd
ipconfig
```

Check whether the adapter has an IPv4 address, subnet mask, and default gateway.

**Safety note:** Do not release your IP address if you depend on that network for a remote session or cannot easily reconnect. Your IP may remain the same or change after renewal.

---

## 6. DHCP Troubleshooting

### What is an APIPA address?

On Windows, an IPv4 address beginning with `169.254.x.x` commonly indicates that the computer has not obtained a normal DHCP IPv4 configuration.

APIPA stands for **Automatic Private IP Addressing**.

### Possible causes

- DHCP server is unavailable.
- Wi-Fi or Ethernet connectivity is interrupted.
- The DHCP address pool has no available addresses.
- A DHCP relay or network configuration problem exists.

### Basic troubleshooting workflow

```text
Check Wi-Fi or Ethernet
          |
          v
Run ipconfig /all
          |
          v
Check DHCP Enabled and IPv4 address
          |
          v
Check DHCP server details
          |
          v
Try ipconfig /renew
          |
          v
Verify IP, gateway and DNS settings
```

An APIPA address does not automatically mean the router is faulty. The underlying issue needs investigation.

---

## 7. DHCP and Other Networking Concepts

DHCP works alongside other networking protocols and settings.

| Component | Purpose |
|---|---|
| DHCP | Automatically provides network configuration |
| IP address | Identifies a device logically on an IP network |
| Subnet mask | Identifies the network and host portions of an IPv4 address |
| Default gateway | Forwards traffic to destinations outside the local network |
| DNS | Resolves domain names to IP addresses |
| ARP | Resolves a known local IPv4 address to a MAC address |

### Example flow

```text
Laptop connects to Wi-Fi
          |
          v
DHCP provides IP configuration
          |
          v
Laptop identifies local network
          |
          v
Uses gateway for external destinations
          |
          v
Uses DNS to resolve domain names
```

---

## 8. Key Learnings

- DHCP stands for Dynamic Host Configuration Protocol.
- DHCP automatically provides IP configuration to clients.
- DORA means Discover, Offer, Request, Acknowledge.
- A DHCP lease is time-limited.
- DHCP reservations and static IPs are different.
- `ipconfig /all` displays detailed adapter configuration.
- `ipconfig /release` releases the current DHCP IPv4 configuration.
- `ipconfig /renew` requests or renews DHCP configuration.
- An IPv4 address beginning with `169.254` may indicate DHCP configuration failure.
- DHCP, DNS, ARP, IP addressing, and routing work together in computer networks.

---

## 9. Commands Practiced

```cmd
ipconfig
ipconfig /all
ipconfig /release
ipconfig /renew
```

---

## 📌 Day 04 Status

**Topics studied:** DHCP fundamentals, DORA, leases, reservations, Windows commands, and basic DHCP troubleshooting.

**Next topic:** Day 05 – DNS (Domain Name System).
