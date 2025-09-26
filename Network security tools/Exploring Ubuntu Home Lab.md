# Exploring Ubuntu Home Lab — Chapter 01

Objective: baseline visibility. Enumerate interfaces, ports, services, connections, and firewall posture. Capture screenshots and add one-paragraph takeaways per tool.

> Pro tip: install packages first
```bash
sudo apt update
sudo apt install -y net-tools nmap tcpdump lsof
```

---

## 1) Identify Network Interfaces and IPs
**Command**
```bash
ip a         # preferred
ifconfig     # legacy; requires net-tools
```
**Why**
Inventory network adapters and addresses to anchor every other finding.

**What to capture**
- Active interfaces and assigned IPv4/IPv6
- Loopback presence and MTU
- Any unexpected virtual adapters

**Screenshot**: `01-ip-a.png`

**Notes**
- Insert your observations here.

---

## 2) Check Open Ports
**Command**
```bash
sudo ss -tuln          # modern and fast
# or
sudo netstat -tuln
```
**Why**
Surface listening TCP/UDP sockets. Flag anything that should not be exposed.

**What to capture**
- Port, proto, and local address
- Match each port to an owning service in step 3

**Screenshot**: `02-ss-tuln.png`

**Notes**
- Insert your observations here.

---

## 3) Analyze Network Connections
**Command**
```bash
sudo lsof -i -P -n
```
**Why**
Map sockets to PIDs and binaries to validate intent and scope.

**What to capture**
- Process name ↔ port mapping
- Any external connections you did not initiate

**Screenshot**: `03-lsof.png`

**Notes**
- Insert your observations here.

---

## 4) Localhost scan (stealth SYN + OS detect)
**Command**
```bash
sudo nmap -sS -O localhost
```
**Why**
Corroborate listening services and fingerprint the OS stack.

**What to capture**
- Open ports and states
- OS guess and confidence

**Screenshot**: `04-nmap-sS-O.png`

**Notes**
- Insert your observations here.

---

## 5) Live hosts on your LAN
**Command**
```bash
# Replace the subnet with your LAN, e.g., 192.168.1.0/24 or 10.0.0.0/24
sudo nmap -sn 192.168.1.0/24
# (-sn is the modern replacement for -sP)
```
**Why**
Inventory devices on the broadcast domain. Spot shadow IT.

**What to capture**
- Count of live hosts
- Any unidentified MAC OUIs

**Screenshot**: `05-nmap-sn.png`

**Notes**
- Insert your observations here.

---

## 6) Service and version detection
**Command**
```bash
sudo nmap -sV localhost
```
**Why**
Identify service daemons and versions to drive patching and risk triage.

**What to capture**
- Port ↔ service name ↔ version
- Version strings that are EOL or outdated

**Screenshot**: `06-nmap-sV.png`

**Notes**
- Insert your observations here.

---

## 7) Quick vuln sweep
**Command**
```bash
sudo nmap --script vuln localhost
```
**Why**
Run NSE vulnerability checks for known issues. Treat results as leads, not truth.

**What to capture**
- Any findings and their CVE IDs if shown
- False positives you can explain

**Screenshot**: `07-nmap-vuln.png`

**Notes**
- Insert your observations here.

---

## 8) Inspect live traffic
**Command**
```bash
# update interface name if not eth0; use `ip a` to confirm (e.g., ens33, enp0s3)
sudo tcpdump -i eth0
# Stop with Ctrl+C
```
**Why**
Observe real traffic patterns. Validate DNS, ARP, DHCP noise or anomalies.

**What to capture**
- Protocol mix
- Suspicious repeated traffic

**Screenshot**: `08-tcpdump.png`

**Notes**
- Insert your observations here.

---

## 9) Real-time socket monitor
**Command**
```bash
sudo watch -n 1 ss -tulnp
# or: sudo watch -n 1 netstat -tulnp
```
**Why**
Detect ephemeral listeners or transient activity while you run tests.

**What to capture**
- New listeners appearing or closing
- Services that unexpectedly restart

**Screenshot**: `09-watch-ss.png`

**Notes**
- Insert your observations here.

---

## 10) Firewall posture
**Command**
```bash
sudo ufw status verbose
```
**Why**
Baseline ingress policy. Expect “inactive” on fresh VMs. We harden next module.

**What to capture**
- Status and any existing rules
- Default policies

**Screenshot**: `10-ufw-status.png`

**Notes**
- Insert your observations here.
