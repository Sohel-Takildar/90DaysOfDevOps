# Day 14 – Networking Fundamentals & Hands-on Checks

## Objective

Learn core networking concepts and practice essential troubleshooting commands used by DevOps engineers.

---

# Quick Concepts

## OSI Model vs TCP/IP Model

### OSI Layers (L1–L7)

* Layer 1 – Physical: Cables, switches, signals
* Layer 2 – Data Link: MAC addresses, Ethernet
* Layer 3 – Network: IP addressing and routing
* Layer 4 – Transport: TCP and UDP communication
* Layer 5 – Session: Session management
* Layer 6 – Presentation: Encryption and formatting
* Layer 7 – Application: HTTP, DNS, SSH, FTP

### TCP/IP Stack

* Link Layer → Physical + Data Link
* Internet Layer → IP routing
* Transport Layer → TCP/UDP
* Application Layer → HTTP, HTTPS, DNS, SSH

### Protocol Locations

| Protocol | Layer              |
| -------- | ------------------ |
| IP       | Network / Internet |
| TCP      | Transport          |
| UDP      | Transport          |
| DNS      | Application        |
| HTTP     | Application        |
| HTTPS    | Application        |

### Real Example

```text
curl https://example.com
```

Flow:

```text
Application (HTTPS)
        ↓
Transport (TCP)
        ↓
Internet (IP)
        ↓
Link Layer (Ethernet/Wi-Fi)
```

---

# Hands-on Checklist

Target Host: google.com

## 1. Identity Check

### Command

```bash
hostname -I
```

### Output

```text
192.168.1.100
```

### Observation

* System IP address identified successfully.
* Host is connected to the local network.

---

## 2. Reachability Check

### Command

```bash
ping -c 4 google.com
```

### Output

```text
4 packets transmitted, 4 received, 0% packet loss
avg latency = 18 ms
```

### Observation

* No packet loss detected.
* Network connectivity is healthy.

---

## 3. Path Check

### Command

```bash
traceroute google.com
```

### Observation

* Traffic passed through ISP gateway and several upstream routers.
* A few hops showed higher latency but destination remained reachable.

---

## 4. Listening Ports

### Command

```bash
ss -tulpn
```

### Sample Output

```text
LISTEN 0 128 *:22 *:* users:(("sshd",pid=701))
```

### Observation

* SSH service is listening on port 22.
* Remote administration is enabled.

---

## 5. DNS Resolution

### Command

```bash
dig google.com +short
```

### Output

```text
142.250.183.14
```

### Observation

* DNS successfully resolved the domain name to an IP address.

---

## 6. HTTP Check

### Command

```bash
curl -I https://google.com
```

### Output

```text
HTTP/2 301
```

### Observation

* Website is reachable.
* Server responded with a redirect status.

---

## 7. Connections Snapshot

### Command

```bash
netstat -an | head
```

### Observation

* LISTEN sockets observed for SSH and system services.
* ESTABLISHED connections indicate active communication.

---

# Mini Task: Port Probe & Interpret

## Identify Listening Port

```bash
ss -tulpn | grep :22
```

SSH found on port 22.

### Test Connectivity

```bash
nc -zv localhost 22
```

### Output

```text
Connection to localhost 22 port [tcp/ssh] succeeded!
```

### Interpretation

* Port 22 is reachable locally.
* SSH service is operational.

### If Not Reachable

Next checks:

```bash
systemctl status ssh
sudo ufw status
sudo journalctl -u ssh
```

---

# Reflection

## Which command gives the fastest signal when something is broken?

`ping` provides the quickest indication of network connectivity problems.

## What layer would you inspect if DNS fails?

* Application Layer (DNS service)
* Network Layer (IP connectivity)

## What layer would you inspect if HTTP 500 appears?

* Application Layer
* Web server logs
* Backend application logs

## Two Follow-Up Checks During a Real Incident

1. Verify service status:

```bash
systemctl status <service>
```

2. Review logs:

```bash
journalctl -xe
```

or

```bash
tail -f /var/log/nginx/error.log
```

---

# Key Learnings

* Learned how networking protocols map to the OSI and TCP/IP models.
* Practiced troubleshooting using ping, traceroute, ss, dig, netstat, and curl.
* Verified DNS resolution, HTTP responses, and local port availability.
* Built a repeatable workflow for basic network diagnostics.

---
