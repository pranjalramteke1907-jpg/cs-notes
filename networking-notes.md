# Networking Notes

Notes from TryHackMe rooms and cybersecurity study.

---

## What is a Network?

A network is two or more computers connected together to share data and resources.

- **LAN (Local Area Network)** — devices connected in a small area like a home or office
- **WAN (Wide Area Network)** — connects multiple LANs across large distances (the internet is a WAN)
- **MAN (Metropolitan Area Network)** — covers a city or campus
- **WLAN** — wireless LAN (Wi-Fi)

---

## IP Addresses

Every device on a network has an IP address — like a home address for computers.

### IPv4
- Format: 4 numbers separated by dots — `192.168.1.1`
- Range: 0.0.0.0 to 255.255.255.255
- Total addresses: about 4.3 billion

### IPv6
- Format: 8 groups of hexadecimal — `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Created because IPv4 addresses ran out
- Much larger address space

### Private vs Public IPs

| Type | Range | Used for |
|------|-------|----------|
| Private | 192.168.0.0 – 192.168.255.255 | Home and office networks |
| Private | 10.0.0.0 – 10.255.255.255 | Large internal networks |
| Private | 172.16.0.0 – 172.31.255.255 | Medium networks |
| Loopback | 127.0.0.1 | Your own machine (localhost) |
| Public | Everything else | Internet-facing addresses |

---

## MAC Address

- Stands for **Media Access Control**
- A unique physical address burned into every network card
- Format: 6 pairs of hexadecimal — `00:1A:2B:3C:4D:5E`
- First 3 pairs = manufacturer ID
- Last 3 pairs = unique device ID
- Used at Layer 2 (Data Link) of the OSI model
- Unlike IP addresses, MAC addresses do not change

---

## OSI Model — 7 Layers

The OSI model describes how data travels from one computer to another across a network.

**Memory trick: "Please Do Not Throw Sausage Pizza Away"** (layers 1 to 7)

| Layer | Number | Name | What it does | Examples |
|-------|--------|------|-------------|---------|
| 7 | Application | Application | What the user sees and interacts with | HTTP, HTTPS, FTP, DNS, SMTP |
| 6 | Presentation | Presentation | Formats and encrypts data | SSL/TLS, JPEG, ASCII |
| 5 | Session | Session | Opens and closes communication sessions | NetBIOS, RPC |
| 4 | Transport | Transport | Breaks data into segments, ensures delivery | TCP, UDP |
| 3 | Network | Network | Finds the best path across networks | IP, ICMP, routers |
| 2 | Data Link | Data Link | Transfers data between devices on same network | Ethernet, MAC, switches |
| 1 | Physical | Physical | The actual cables and hardware | Cables, Wi-Fi, hubs |

### Key things to remember about each layer

**Layer 7 — Application**
- Where applications like browsers and email clients live
- Data here is human-readable
- HTTP uses port 80, HTTPS uses port 443

**Layer 4 — Transport**
- Splits data into segments
- Adds port numbers
- TCP = reliable, connection-based
- UDP = fast, no guarantee of delivery

**Layer 3 — Network**
- Uses IP addresses to route data between networks
- Routers operate at this layer

**Layer 2 — Data Link**
- Uses MAC addresses to send data between devices on the same network
- Switches operate at this layer

**Layer 1 — Physical**
- The actual physical medium: ethernet cables, Wi-Fi signals, fibre optic

---

## TCP vs UDP

| Feature | TCP | UDP |
|---------|-----|-----|
| Full name | Transmission Control Protocol | User Datagram Protocol |
| Connection | Yes — establishes connection first | No — just sends data |
| Reliable? | Yes — guarantees all data arrives | No — data can be lost |
| Speed | Slower | Much faster |
| Order | Data arrives in order | Data can arrive out of order |
| Error checking | Yes | Minimal |
| Use cases | Web browsing, email, file transfer | Video calls, gaming, DNS, live streaming |

### TCP 3-Way Handshake

How TCP establishes a connection before sending data:

```
Client                    Server
  |                          |
  |-------- SYN ----------->|   "I want to connect"
  |                          |
  |<------ SYN-ACK ---------|   "OK, I'm ready"
  |                          |
  |-------- ACK ----------->|   "Great, let's go"
  |                          |
  |===== Data Transfer ======|
```

- **SYN** = Synchronise — client says hello
- **SYN-ACK** = Server acknowledges and says hello back
- **ACK** = Client confirms — connection established

---

## Key Protocols and Port Numbers

Port numbers identify which service data is meant for on a device.

| Protocol | Port | Description |
|----------|------|-------------|
| HTTP | 80 | Web traffic — unencrypted |
| HTTPS | 443 | Secure web traffic — encrypted |
| FTP | 21 | File Transfer Protocol |
| SSH | 22 | Secure remote login — encrypted |
| Telnet | 23 | Remote login — unencrypted (insecure) |
| SMTP | 25 | Sending emails |
| DNS | 53 | Domain name to IP address lookup |
| DHCP | 67/68 | Automatically assigns IP addresses |
| HTTP Alt | 8080 | Alternative HTTP port |
| RDP | 3389 | Remote Desktop Protocol (Windows) |

**Security tip:** Ports below 1024 are well-known ports. Attackers often scan these first with Nmap.

---

## DNS — Domain Name System

DNS converts human-readable domain names into IP addresses.

### How DNS works step by step

```
You type: google.com in your browser

Step 1 — Check local cache
Your computer checks if it already knows the IP for google.com.
If yes — skip to Step 5.

Step 2 — Ask Recursive Resolver
Your computer asks your ISP's DNS server.

Step 3 — Ask Root Server
The resolver asks a root server which knows where .com domains are managed.

Step 4 — Ask Authoritative Server
The resolver asks Google's nameserver for the exact IP of google.com.

Step 5 — Get the IP
DNS returns: 142.250.190.78

Step 6 — Connect
Your browser connects to 142.250.190.78 and loads the website.
```

### DNS Record Types

| Record | What it does |
|--------|-------------|
| A | Maps domain to IPv4 address |
| AAAA | Maps domain to IPv6 address |
| CNAME | Maps domain to another domain (alias) |
| MX | Points to mail servers |
| TXT | Stores text info — used for verification |
| NS | Lists the nameservers for a domain |

---

## DHCP — Dynamic Host Configuration Protocol

DHCP automatically assigns IP addresses to devices when they join a network.

**Without DHCP:** You would have to manually type an IP address, subnet mask, gateway, and DNS server on every device.

**With DHCP:** Your router automatically gives your phone/laptop an IP when it connects to Wi-Fi.

### DHCP process (DORA)
1. **Discover** — device broadcasts "I need an IP address"
2. **Offer** — DHCP server offers an available IP
3. **Request** — device says "I'll take that IP"
4. **Acknowledge** — server confirms the IP is assigned

---

## CIA Triad — Core Security Concept

Everything in cybersecurity maps back to these three principles.

| Letter | Principle | Meaning | Example |
|--------|-----------|---------|---------|
| C | Confidentiality | Only authorised people can access data | Encryption, passwords, access controls |
| I | Integrity | Data has not been tampered with | Hashing, digital signatures, checksums |
| A | Availability | Systems are accessible when needed | Backups, redundancy, DDoS protection |

### Real-world examples

**Confidentiality attack:** A hacker intercepts your login credentials — confidentiality is broken.

**Integrity attack:** A hacker modifies a file during transfer without you knowing — integrity is broken.

**Availability attack:** A DDoS attack takes down a website — availability is broken.

---

## Common Network Attacks (intro level)

| Attack | What happens |
|--------|-------------|
| DDoS | Floods a server with traffic until it crashes |
| Man-in-the-Middle | Attacker sits between two parties and intercepts communication |
| Phishing | Fake emails or websites trick users into giving credentials |
| Port Scanning | Attacker scans a system to find open ports and services |
| Packet Sniffing | Attacker captures network traffic to read unencrypted data |
| ARP Spoofing | Attacker links their MAC address to a legitimate IP on the network |

---

## Useful Network Commands (recap)

| Command | What it does |
|---------|-------------|
| `ping google.com` | Tests if a host is reachable |
| `traceroute google.com` | Shows every hop between you and a destination |
| `ifconfig` | Shows your network interfaces and IPs |
| `ip a` | Same as ifconfig on newer Linux systems |
| `netstat -an` | Shows all active connections and listening ports |
| `nmap 192.168.1.1` | Scans a host for open ports |
| `dig google.com` | DNS lookup — shows what IP a domain resolves to |
| `whois google.com` | Shows registration info for a domain |

---

## Notes

- HTTP is unencrypted — anyone sniffing the network can read the data
- Always prefer HTTPS — data is encrypted with TLS
- Port 22 (SSH) being open on a server is a common finding in penetration tests
- The OSI model is theoretical — TCP/IP model is what is actually used in practice, but OSI is used to explain concepts
