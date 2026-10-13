# Day 05 – DNS (Domain Name System)

## 🎯 Objective

Understand how DNS resolves domain names into IP addresses, learn common DNS record types, practise Windows DNS commands, and troubleshoot basic DNS issues.

---

## 1. What is DNS?

**DNS stands for Domain Name System.**

DNS helps translate human-readable domain names into IP addresses that computers use to communicate over a network.

### Example

When a user enters:

```text
google.com
```

DNS helps find the IP address associated with that domain name.

```text
Domain Name
google.com
     |
     v
 DNS Lookup
     |
     v
IP Address
     |
     v
Browser connects to the server
```

### Why do we need DNS?

- Domain names are easier for humans to remember than IP addresses.
- DNS helps applications locate network services.
- DNS supports website access and email delivery.
- DNS records provide information about domain names and services.

**Important:** DNS resolution is only one part of accessing a website. Network connectivity, server availability, and other factors also matter.

---

## 2. How DNS Works

When a user enters a domain name in a browser, the general process is:

1. The browser or operating system checks available cached information.
2. If the answer is not available, the device queries a DNS resolver.
3. The resolver finds the answer, potentially contacting other DNS servers.
4. The resolver returns the DNS response.
5. The browser uses the resulting IP address to connect to the destination server.

### DNS Resolution Flow

```text
User enters google.com
          |
          v
Browser / OS cache check
          |
          v
DNS Resolver
          |
          v
DNS lookup if required
          |
          v
IP address returned
          |
          v
Browser connects to server
```

A recursive DNS resolver may contact root DNS servers, Top-Level Domain (TLD) servers, and authoritative DNS servers when necessary.

---

## 3. Common DNS Record Types

| Record | Purpose |
|---|---|
| A | Maps a domain name to an IPv4 address |
| AAAA | Maps a domain name to an IPv6 address |
| CNAME | Creates an alias pointing to another domain name |
| MX | Identifies mail servers for a domain |
| TXT | Stores text information used for verification and other purposes |
| NS | Identifies authoritative name servers for a domain |

### Examples

**A record:** Returns an IPv4 address.

**AAAA record:** Returns an IPv6 address.

**CNAME record:** Points an alias to another domain name.

**MX record:** Helps other mail systems identify where to deliver email.

**TXT record:** Can contain domain verification information and email security policies.

---

## 4. DNS Cache

A DNS cache temporarily stores DNS answers so that repeated lookups may be completed faster.

Caching can occur in different places, including:

- Web browsers
- Operating systems
- DNS resolvers

### Windows commands

Display the Windows DNS resolver cache:

```cmd
ipconfig /displaydns
```

Clear the Windows DNS resolver cache:

```cmd
ipconfig /flushdns
```

Flushing the local cache does not change the configured DNS server or clear every DNS cache on the network.

---

## 5. Practical Windows DNS Commands

### Command 1: Inspect network configuration

```cmd
ipconfig /all
```

Check:

- IPv4 address
- Subnet mask
- Default gateway
- DHCP server
- DNS servers

### Command 2: Look up a domain name

```cmd
nslookup google.com
```

This queries a DNS server and displays information about the response.

Look for:

- DNS server used for the query
- Server address
- Returned domain information and IP addresses

The returned IP addresses can vary depending on location, DNS configuration, and the service's infrastructure.

### Command 3: Test IP connectivity

```cmd
ping 8.8.8.8
```

This tests ICMP connectivity to Google's public DNS IP address, if the destination and network permit ICMP replies.

A failed ping does not necessarily mean DNS is broken.

### Command 4: Test domain connectivity

```cmd
ping google.com
```

This attempts to resolve the domain and send ICMP requests to a returned address.

Ping replies may be blocked even when a website is accessible.

### Command 5: Clear the DNS cache

```cmd
ipconfig /flushdns
```

Use this when investigating a possible stale local DNS cache.

---

## 6. DNS Troubleshooting

### Scenario

A user reports:

"My internet is connected, but websites are not opening."

### Troubleshooting workflow

```text
Check Wi-Fi / Ethernet connection
              |
              v
Run ipconfig /all
              |
              v
Check IP, gateway and DNS settings
              |
              v
Test gateway connectivity
              |
              v
Test IP connectivity
              |
              v
Run nslookup google.com
              |
              v
Analyse the results
```

### Example: Possible DNS issue

Suppose:

- The default gateway is reachable.
- `ping 8.8.8.8` succeeds.
- `nslookup google.com` fails.

This suggests a possible DNS-resolution problem.

Investigate:

- Whether the configured DNS server is reachable.
- Whether the DNS server is responding.
- Whether network policies or firewall rules affect DNS.
- Whether the DNS configuration is correct.

Do not immediately change DNS settings without investigating the evidence.

### Important limitation

A successful ping to an IP address does not prove that all internet services are working. Likewise, a failed ping does not always indicate a network failure.

---

## 7. DNS and Other Networking Concepts

| Component | Main purpose |
|---|---|
| DHCP | Automatically provides network configuration |
| DNS | Resolves domain names into IP addresses |
| ARP | Resolves a known local IPv4 address to a MAC address |
| Switch | Forwards Ethernet frames within a local network |
| Router | Forwards traffic between IP networks |
| Default gateway | The next-hop router used for destinations outside the local subnet |

### How they work together

```text
Device connects to network
          |
          v
DHCP provides IP configuration
          |
          v
User enters a domain name
          |
          v
DNS resolves the domain
          |
          v
Device determines the destination network
          |
          v
Traffic is sent locally or through the gateway
```

---

## 8. Key Learnings

- DNS stands for Domain Name System.
- DNS helps resolve domain names into IP addresses.
- DNS resolution and network connectivity are separate concepts.
- A records map names to IPv4 addresses.
- AAAA records map names to IPv6 addresses.
- CNAME records provide aliases.
- MX records identify mail servers.
- TXT records store domain-related text information.
- `nslookup` helps investigate DNS resolution.
- `ipconfig /displaydns` displays the Windows DNS resolver cache.
- `ipconfig /flushdns` clears the local Windows DNS resolver cache.
- `ping` can help test connectivity but cannot independently confirm that DNS or a website is functioning correctly.

---

## 9. Commands Practised

```cmd
ipconfig /all
nslookup google.com
ping 8.8.8.8
ping google.com
ipconfig /displaydns
ipconfig /flushdns
```

---

## 10. Practical Learning Notes

Use this section to record your own observations after running the commands.

- DNS server shown by `ipconfig /all`:
- DNS server shown by `nslookup`:
- Domain lookup result:
- IP connectivity test result:
- One troubleshooting observation:

Avoid publishing public IP addresses or sensitive organizational network details.

---

## 📌 Day 05 Status

**Topics covered:** DNS fundamentals, resolution process, DNS records, caching, Windows commands, and basic troubleshooting.

**Next topic:** Day 06 – TCP vs UDP and networking ports.
