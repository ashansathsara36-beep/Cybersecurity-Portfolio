# Network Analysis: Detecting a Port Scan with Wireshark

## 📖 Scenario
I am a junior network security analyst. The IDS (Intrusion Detection System) flagged a spike in inbound traffic to our web server. Using packet analysis (Wireshark/TCPdump), I need to determine if this is a legitimate Denial of Service (DoS) attack or a reconnaissance port scan.

## 🎯 Objective
To capture and analyze live network packets to identify the source IP, destination ports, and attack patterns, then create a firewall rule to block the threat.

## 🛠️ Tools Used
- Wireshark (Packet Sniffer)
- TCPdump (Command-line capture)
- TCP/IP networking fundamentals

---

## 🔍 Step 1: Capture Suspicious Traffic
I ran a capture filter to isolate traffic specifically hitting our web server on Port 80 (HTTP) and Port 443 (HTTPS).

### Command Entered (TCPdump):
```bash
sudo tcpdump -i eth0 host 192.168.1.10 and (port 80 or 443)
```

### Wireshark Filter Applied:
```
ip.addr == 192.168.1.10 && (tcp.port == 80 || tcp.port == 443)
```

---

## 📊 Step 2: Analyzing the Packets (Screenshot Simulation)

**Observation 1: SYN Flood Pattern**
I noticed hundreds of `SYN` packets originating from a single IP (`203.0.113.45`) with a destination port 80, but **none** of them completed the 3-way handshake (No `SYN-ACK` or `ACK` responses).

> **Analysis:** This is a classic **SYN Flood** attack. The attacker is sending connection requests but never finalizing them, exhausting the server's connection queue.

**Observation 2: Unusual Port Sequence**
The same IP was sequentially scanning ports from 1 to 1024 in a single second.

| Source IP | Destination Port | Protocol | Flag |
| :--- | :--- | :--- | :--- |
| 203.0.113.45 | 21 (FTP) | TCP | SYN |
| 203.0.113.45 | 22 (SSH) | TCP | SYN |
| 203.0.113.45 | 23 (Telnet) | TCP | SYN |
| 203.0.113.45 | 80 (HTTP) | TCP | SYN |

> **Analysis:** This rapid-fire sequence across different ports indicates **Port Scanning**—the attacker is looking for open services to exploit.

---

## 🚧 Step 3: Mitigation (Firewall Rule)
Based on the analysis, I created a firewall rule to block the malicious IP entirely to stop both the SYN Flood and the Port Scan.

### Firewall Command (Linux iptables):
```bash
sudo iptables -A INPUT -s 203.0.113.45 -j DROP
```

---

## 📚 Summary of Indicators of Compromise (IoCs)
| IoC | Value |
| :--- | :--- |
| **Malicious IP** | 203.0.113.45 |
| **Attack Type** | SYN Flood + Port Scan |
| **Targeted Ports** | 21, 22, 23, 80, 443 |
| **Network Protocol** | TCP |

## 🏁 Outcome
The firewall rule was successfully deployed. Network traffic returned to baseline levels within 5 minutes. The attack was neutralized without affecting legitimate users.
