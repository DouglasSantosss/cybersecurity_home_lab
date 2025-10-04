# Network Security with UFW  

In this lab I learned how to configure the Uncomplicated Firewall (UFW) on Ubuntu, check ports and services, and enable logging.   

---

## Part I Enable UFW  

### 1. Check UFW status  
**Command**:  
```bash
sudo ufw status
```  
Checks if UFW is installed and running. By default it’s often inactive.   
![ufw status](image.png)
---

### 2. Allow SSH before enabling  
**Command**:  
```bash
sudo ufw allow 22/tcp
```  
This opens port 22 for SSH. If you enable the firewall without this, you could lock yourself out of the VM.  
**Answer**: It’s important because if you are connected remotely, blocking port 22 would cut off your SSH session.  
![ufw 22](image-1.png)
---

### 3. Check open ports  
**Command**:  
```bash
sudo ss -tuln
```  
Lists TCP/UDP sockets that are open and listening. Shows addresses and ports.  
If unsure about a port:  
```bash
sudo lsof -i :PORT
```  
This tells which service is using that port.   
![ss tuln](image-2.png)
---

### 4. Enable UFW  
**Command**:  
```bash
sudo ufw enable
```  
Activates the firewall.   
![ufw enable](image-3.png)
---

### 5. Check UFW status again  
**Command**:  
```bash
sudo ufw status
```  
Confirms the firewall is running and which rules are active.   
![status](image-4.png)
---

### 6. Web server ports  
For a web server, ports **80 (HTTP)** and **443 (HTTPS)** should be allowed.  
**Commands**:  
```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```   
![ufw allow web](image-5.png)
---

### 7. Verbose status  
**Command**:  
```bash
sudo ufw status verbose
```  
Shows rules plus default policies (incoming = deny, outgoing = allow). Useful to confirm defaults.    
![verbose](image-6.png)
---

### 8. Block an IP address  
**Command**:  
```bash
sudo ufw deny from 10.0.0.0
```  
Blocks traffic from this IP (example: a disgruntled ex-employee).  
![block ip](image-7.png)
---

### 9. Allow host access to port 587  
**Command**:  
```bash
sudo ufw allow from 192.168.1.50 to any port 587
```  
Port 587 is typically used for sending email (SMTP submission).   
t![allow 587](image-8.png)
---

### 10. Confirm rules  
**Command**:  
```bash
sudo ufw status numbered
```  
Shows rules with numbers so they can be managed or deleted.   
![rules](image-9.png)
---

## Part II UFW Logging  

### 1. Enable logging  
**Command**:  
```bash
sudo ufw logging on
```  
Turns on firewall logging.   
![logging](image-10.png)
---

### 2. Set logging level to high  
**Command**:  
```bash
sudo ufw logging high
```  
Logs all blocked packets with connection details.   
![log high](image-11.png)
---

### 3. Example log entry breakdown  
A blocked packet log shows MAC, source IP, destination IP, source port, destination port, and protocol.  
**Why useful?** It helps identify where unwanted traffic is coming from and what it was targeting.  

---

### 4. View logs live  
**Command**:  
```bash
sudo tail -f /var/log/ufw.log
```  
Shows UFW logs in real time. The `-f` keeps it updating.   
![tail](image-12.png)
---

### 5. Filter DENY and ALLOW  
**Commands**:  
```bash
sudo grep 'DENY' /var/log/ufw.log
sudo grep 'ALLOW' /var/log/ufw.log
```  
Lets me see just blocked or allowed traffic.  
**Answer**: If DENY shows no output, it means no traffic has been blocked yet.  
![grep](image-13.png)