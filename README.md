# Network-Based Intrusion Detection System
Network-based intrusion detection system using snort. A project for CodeAlpha internship.

## 🛠 Requirements
- Virtual box
- Kali linux OS
- Ubuntu server(latest version)
- Active internet
- Snort installation
- Nmap for scanning IP
---
## 📥 Initial Installations
**1️⃣ First Install Virtualbox**

**2️⃣ Import Kali Linux**

**3️⃣ Download Ubuntu server .iso file from its main website:**
- https://ubuntu.com/download/server

**4️⃣ Import the iso file to virtualbox and run the new instance**

Quick remainder: Change the network setting to bridged adapter and set promiscuous mode to 'Allow All', before running the server(also do it for kali linux).

---
## Snort Installation
**1️⃣ Identify your IP address:**
```bash
ifconfig
```
Get the interface info i.e, wlan0 or enp0s3

*screenshot:

**2️⃣ In Ubuntu instance update system packages:**
```bash
sudo apt update && sudo apt upgrade -y
```

**3️⃣ Install Snort:**
```bash
sudo apt install snort
```
During mid installation an option to enter the local network range is shown. Type your machine's network ip range, for example 192.168.xx.0/32

**4️⃣ Verify Snort installation:**
```bash
snort -V
```
*screenshot:

---
## ⚙️ Configuration

**1️⃣ You can add/change rules for detection by(This step is not mandatory as snort comes with many set of rules):**
```bash
sudo nano /etc/snort/rules/local.rules
```
We only need to add new rules for additional security and protective measures as there are plenty of built-in rules for snort. 
*screenshot:

**2️⃣ Ensure the configuration file is present:**
```bash
sudo nano /etc/snort/snort.conf
```
*screenshot:

---
## 🏃‍♂️‍➡️ Running Snort IDS 

**1️⃣ First check if snort.conf file is successfully running:**
```bash
sudo snort -T -c /etc/snort/snort.conf -i enp0s3
```
*screenshot:

**2️⃣ Next the snort IDS in alert mode:**
```bash
sudo snort -A console -c /etc/snort/snort.conf -I enp0s3
```
*screenshot:

**3️⃣ Back in Kali OS open terminal and scan the server using the above IP address**
```bash
nmap -Pn 192.168.x.x
```
**4️⃣ Next give a ping request**
```bash
ping 192.168.x.x
```
In the Ubuntu server instance you will be able to see the alerts popping up for the snort scan.

---
## 📝 Logging Alerts
**1️⃣ Run Snort with logging enabled:**
```bash
sudo snort -A console -c /etc/snort/snort.conf -I enp0s3 -l /var/log/snort
```
**2️⃣ View alerts:**
```bash
sudo cat /var/log/snort/snort.alert.fast
```
*screenshot: 

## 📊 Example Alerts
- Scan UPnP service discover attempt
- ICMP Ping Detected
- Suspicious TCP connection attempts

  *screenshot:
