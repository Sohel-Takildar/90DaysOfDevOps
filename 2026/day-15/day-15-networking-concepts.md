# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## Task 1: DNS – How Names Become IPs

### 1. What happens when you type google.com in a browser?

When I type `google.com` in a browser, my computer first checks if the IP address is already cached. If not, it sends a DNS query to a DNS server. The DNS server resolves the domain name into an IP address. The browser then connects to that IP address and loads the website.

### 2. DNS Record Types

| Record Type | Description                                           |
| ----------- | ----------------------------------------------------- |
| A           | Maps a domain name to an IPv4 address                 |
| AAAA        | Maps a domain name to an IPv6 address                 |
| CNAME       | Creates an alias pointing one domain to another       |
| MX          | Specifies mail servers responsible for email delivery |
| NS          | Identifies authoritative name servers for a domain    |

### 3. dig google.com Output

Command:

```bash
dig google.com
```

Example Output:

```bash
;; ANSWER SECTION:
google.com.     300     IN      A       142.250.183.14
```

**A Record:** `142.250.183.14`

**TTL:** `300`

---

# Task 2: IP Addressing

## 1. What is an IPv4 address?

An IPv4 address is a 32-bit numerical identifier assigned to devices on a network. It consists of four octets separated by dots, such as `192.168.1.10`. Each octet ranges from 0 to 255.

## 2. Public vs Private IP

| Type       | Description                  | Example      |
| ---------- | ---------------------------- | ------------ |
| Public IP  | Accessible over the internet | 8.8.8.8      |
| Private IP | Used inside local networks   | 192.168.1.10 |

## 3. Private IP Ranges

```text
10.0.0.0 - 10.255.255.255
172.16.0.0 - 172.31.255.255
192.168.0.0 - 192.168.255.255
```

## 4. ip addr show

Command:

```bash
ip addr show
```

Example:

```bash
inet 192.168.1.100/24 brd 192.168.1.255 scope global
```

Private IP identified:

```text
192.168.1.100
```

---

# Task 3: CIDR & Subnetting

## 1. What does /24 mean?

The `/24` indicates that the first 24 bits are used for the network portion of the address, leaving 8 bits for host addresses.

## 2. Usable Hosts

| CIDR | Usable Hosts |
| ---- | ------------ |
| /24  | 254          |
| /16  | 65,534       |
| /28  | 14           |

## 3. Why do we subnet?

Subnetting divides a large network into smaller networks. It improves network organization, reduces broadcast traffic, enhances security, and allows more efficient IP address management.

## 4. CIDR Table

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

---

# Task 4: Ports – The Doors to Services

## 1. What is a port?

A port is a logical communication endpoint used by applications and services. Ports allow multiple services to run on the same IP address while keeping network traffic organized.

## 2. Common Ports

| Port  | Service |
| ----- | ------- |
| 22    | SSH     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 53    | DNS     |
| 3306  | MySQL   |
| 6379  | Redis   |
| 27017 | MongoDB |

## 3. ss -tulpn Output

Command:

```bash
ss -tulpn
```

Example:

```bash
tcp LISTEN 0 128 0.0.0.0:22
tcp LISTEN 0 511 0.0.0.0:80
```

Matching Services:

| Port | Service    |
| ---- | ---------- |
| 22   | SSH        |
| 80   | Nginx/HTTP |

---

# Task 5: Putting It Together

## 1. curl http://myapp.com:8080

Several networking concepts are involved. DNS resolves `myapp.com` into an IP address. The client connects to that IP using TCP on port `8080`. Routing and IP networking deliver the packets between the client and server.

## 2. App can't reach database at 10.0.1.50:3306

First, I would verify network connectivity using `ping` or `telnet/nc`. Then I would check if MySQL is running and listening on port `3306`. Finally, I would verify firewall rules, security groups, routing, and database configuration.

---

# What I Learned

1. DNS translates human-readable domain names into IP addresses that computers use for communication.
2. CIDR notation helps define network size and determine available host addresses.
3. Ports allow multiple services such as SSH, HTTP, MySQL, and Redis to operate on the same server simultaneously.

---

# Commands Used

```bash
dig google.com

ip addr show

ss -tulpn

curl http://myapp.com:8080
```
