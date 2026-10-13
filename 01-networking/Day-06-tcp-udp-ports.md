# Day 06 – TCP, UDP & Networking Ports

## 🎯 Objective

Understand TCP and UDP, learn the purpose of port numbers, identify common networking ports, and practise inspecting network connections using Windows Command Prompt.

---

## 1. What Are TCP and UDP?

TCP stands for **Transmission Control Protocol**.

UDP stands for **User Datagram Protocol**.

They are transport-layer protocols used to carry data between applications over IP networks.

### TCP – Transmission Control Protocol

TCP provides reliable, ordered delivery of a byte stream.

Important features:
- Connection-oriented communication.
- Acknowledgements and retransmissions help deliver data reliably.
- Data is delivered to the receiving application in order.
- Commonly used for HTTPS, SSH, and many file transfers.

### UDP – User Datagram Protocol

UDP sends independent datagrams without built-in delivery or ordering guarantees.

Important features:
- Connectionless communication.
- Lower protocol overhead than TCP.
- Does not automatically retransmit lost datagrams.
- Commonly used for DNS queries, online gaming, and real-time voice/video applications.

### TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Communication | Connection-oriented | Connectionless |
| Delivery guarantee | Reliable delivery mechanisms | No built-in guarantee |
| Ordering | Preserves byte-stream order | No built-in ordering |
| Overhead | Generally higher | Generally lower |
| Common uses | HTTPS, SSH, file transfers | DNS, gaming, real-time media |

**Important:** UDP is not always faster in every situation. The appropriate protocol depends on the application's requirements.

---

## 2. What Is a Port Number?

A port number identifies an application or service endpoint on a device.

An IP address helps identify the network destination, while the transport protocol and port help deliver traffic to the appropriate application.

### Example

```text
192.168.1.10:443
```

- `192.168.1.10` – IP address.
- `443` – port number.
- TCP or UDP – transport protocol used by the connection.

Port numbers range from **0 to 65535**.

### Simple analogy

Imagine an apartment building:

- IP address = building address.
- Port number = apartment number.
- Application or service = the intended recipient.

This analogy helps explain why one computer can run several network services at the same time.

---

## 3. Important Networking Ports

| Port | Protocol | Service | Purpose |
|---:|---|---|---|
| 20/21 | TCP | FTP | Traditional file transfer |
| 22 | TCP | SSH | Secure remote terminal access |
| 25 | TCP | SMTP | Email transfer between servers |
| 53 | UDP/TCP | DNS | Domain name resolution |
| 67/68 | UDP | DHCPv4 | Automatic IPv4 configuration |
| 80 | TCP | HTTP | Traditional unencrypted web traffic |
| 443 | TCP | HTTPS | Encrypted web traffic; HTTP/3 uses QUIC over UDP |
| 3389 | TCP/UDP | RDP | Windows Remote Desktop |

### Ports to Memorize First

- **22** – SSH
- **53** – DNS
- **67/68** – DHCPv4
- **80** – HTTP
- **443** – HTTPS
- **3389** – RDP

These are useful for IT Support, NOC, and system administration interviews.

---

## 4. How TCP Establishes a Connection

TCP commonly establishes a connection using a three-way handshake.

The steps are:

1. SYN – The client requests a connection.
2. SYN-ACK – The server acknowledges the request.
3. ACK – The client acknowledges the server's response.

### TCP Three-Way Handshake

```text
Client                         Server
  |                               |
  | -------- SYN ---------------> |
  | <------ SYN-ACK ------------- |
  | -------- ACK ---------------> |
  |                               |
  |     Connection established    |
```

After the connection is established, the applications can exchange data.

---

## 5. Practical Windows Commands

### Command 1: Display network connections

```cmd
netstat -ano
```

This displays network connections and listening endpoints, along with their process IDs.

Common columns include:

- Proto – TCP or UDP.
- Local Address – Local IP address and port.
- Foreign Address – Remote IP address and port.
- State – Connection state, where applicable.
- PID – Process ID.

### Command 2: Display numerical addresses and ports

```cmd
netstat -an
```

This displays addresses and port numbers numerically.

### Command 3: Filter entries containing port 443

```cmd
netstat -ano | findstr :443
```

This filters the output for text containing `:443`.

The command may return no results if no matching endpoint exists at that moment.

### Command 4: List running processes

```cmd
tasklist
```

This lists running Windows processes.

Use the PID from `netstat -ano` to help identify the associated process.

Example:

```cmd
tasklist /FI "PID eq 1234"
```

Replace `1234` with the actual PID you want to investigate.

**Note:** A listening port does not automatically mean that the service is reachable from other computers. Firewalls, routing, and service configuration also affect accessibility.

---

## 6. TCP, UDP, and DNS

DNS commonly uses UDP port 53 for standard queries, while TCP port 53 is also used in situations such as responses requiring TCP and zone transfers.

HTTPS commonly uses TCP port 443. HTTP/3 uses QUIC over UDP, normally on port 443.

This shows why a port number should be understood together with its transport protocol.

---

## 7. Basic Network Troubleshooting

Suppose a user says:

"I cannot connect to a remote application."

A basic troubleshooting workflow is:

```text
Check local network configuration
             |
             v
Check IP and gateway
             |
             v
Test connectivity to destination
             |
             v
Check DNS resolution if using a domain
             |
             v
Investigate required service port
             |
             v
Check firewall and service status
```

Useful commands:

```cmd
ipconfig /all
ping <destination-IP>
nslookup <domain-name>
netstat -ano
```

A failed ping does not necessarily mean the application is unavailable because ICMP traffic may be blocked.

Similarly, a successful ping does not prove that a particular TCP or UDP service is working.

---

## 8. Key Learnings

- TCP provides reliable, ordered byte-stream delivery.
- UDP sends datagrams without built-in delivery or ordering guarantees.
- IP addresses identify network destinations.
- Port numbers identify application or service endpoints.
- Port numbers range from 0 to 65535.
- TCP commonly uses a three-way handshake.
- DNS uses both UDP and TCP port 53.
- HTTP commonly uses TCP port 80.
- HTTPS commonly uses TCP port 443; HTTP/3 uses QUIC over UDP.
- SSH commonly uses TCP port 22.
- DHCPv4 uses UDP ports 67 and 68.
- `netstat -ano` displays connections and process IDs.
- `tasklist` helps identify running processes.

---

## 9. Commands Practised

```cmd
netstat -ano
netstat -an
netstat -ano | findstr :443
tasklist
ipconfig /all
nslookup google.com
```

---

## 10. Practical Learning Notes

Record your own observations after practising:

- Number of network entries observed:
- A TCP entry you identified:
- A listening port you observed:
- What you learned from the PID:
- One troubleshooting observation:

Do not publish sensitive network details, public IP addresses, confidential organizational information, or credentials.

---

## 📌 Day 06 Status

**Topics covered:** TCP, UDP, port numbers, common services, TCP handshake, Windows network inspection, and basic troubleshooting.

**Next topic:** Day 07 – Ping, Tracert, Path Troubleshooting & Networking Review.
