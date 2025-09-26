# Exploring Ubuntu Home Lab 



## 1. Identify Network Interfaces and IP Addresses
**Tool**: `ip` / `ifconfig`  
**What it does**: Displays all network interfaces and IP addresses.  
**Command**:
```bash
ip a
# or
ifconfig
```
**Why it matters**: Lets me see which interfaces are active and what subnet I’m on.  
**Screenshot**: ![ip a](../screenshots/01-ip-a.png)

---

## 2. Check Open Ports
**Tool**: `ss` / `netstat`  
**What it does**: Shows ports that are listening for connections.  
**Command**:
```bash
sudo ss -tuln
# or
sudo netstat -tuln
```
**Why it matters**: Identifies exposed services and possible entry points.  
**Screenshot**: ![ss -tuln](../screenshots/02-ss-tuln.png)

---

## 3. Analyze Network Connections
**Tool**: `lsof`  
**What it does**: Maps network connections to the exact process.  
**Command**:
```bash
sudo lsof -i -P -n
```
**Why it matters**: Confirms which program owns each port or connection.  
**Screenshot**: ![lsof](../screenshots/03-lsof.png)

---

## 4. Perform Network Scan
**Tool**: `nmap`  
**What it does**: Scans open ports, services, and guesses the OS.  
**Command**:
```bash
sudo nmap -sS -O localhost
```
**Why it matters**: Verifies externally visible services and fingerprints the system.  
**Screenshot**: ![nmap -sS -O](../screenshots/04-nmap.png)

---

## 5. Discover Live Hosts on the Network
**Tool**: `nmap -sn`  
**What it does**: Pings the subnet to see what devices are up.  
**Command**:
```bash
sudo nmap -sn 192.168.1.0/24
```
**Why it matters**: Builds an inventory of connected devices, highlights unknown hosts.  
**Screenshot**: ![nmap -sn](../screenshots/05-nmap-sn.png)

---

## 6. Detect Services and Versions
**Tool**: `nmap -sV`  
**What it does**: Identifies services and versions on open ports.  
**Command**:
```bash
sudo nmap -sV localhost
```
**Why it matters**: Helps detect outdated or vulnerable services.  
**Screenshot**: ![nmap -sV](../screenshots/06-nmap-sV.png)

---

## 7. Check for Vulnerabilities
**Tool**: `nmap --script vuln`  
**What it does**: Runs vulnerability scripts on discovered services.  
**Command**:
```bash
sudo nmap --script vuln localhost
```
**Why it matters**: Surfaces potential known vulnerabilities.  
**Screenshot**: ![nmap --script vuln](../screenshots/07-nmap-vuln.png)

---

## 8. Inspect Network Traffic
**Tool**: `tcpdump`  
**What it does**: Captures packets on the specified interface.  
**Command**:
```bash
sudo tcpdump -i eth0
```
**Why it matters**: Shows real-time traffic and anomalies.  
**Screenshot**: ![tcpdump](../screenshots/08-tcpdump.png)

---

## 9. Monitor Network in Real Time
**Tool**: `watch` + `netstat`  
**What it does**: Continuously updates the view of open connections.  
**Command**:
```bash
sudo watch -n 1 netstat -tulnp
```
**Why it matters**: Reveals new services or short-lived connections.  
**Screenshot**: ![watch netstat](../screenshots/09-watch.png)

---

## 10. Check Firewall Status
**Tool**: `ufw`  
**What it does**: Manages firewall rules in Ubuntu.  
**Command**:
```bash
sudo ufw status verbose
```
**Why it matters**: Ensures only required ports are allowed.  
**Screenshot**: ![ufw status](../screenshots/10-ufw.png)