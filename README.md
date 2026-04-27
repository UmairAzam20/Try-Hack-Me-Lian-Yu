# Try-Hack-Me-Lian-Yu
This flag confirms that initial access was successfully achieved. It is usually located in the home directory of the compromised user and demonstrates:  Successful credential discovery Valid system access via SSH

## Overview
Platform: TryHackMe

Room: Lian Yu

Difficulty: Easy–Medium

Objective: Gain user and root access


### Methodology
1. Reconnaissance (Nmap)
 
2. Enumeration (Web + Files)
   
3. Initial Access
  
4. Privilege Escalation


 ## 1. Reconnaissance
Nmap Scan

nmap -sC -sV -oN scan.txt <TARGET_IP>

## 2. Web Enumeration
Access Website
Open browser → http://<TARGET_IP>
Found a basic webpage (island theme / Arrow reference)

# Directory Brute Force
gobuster dir -u http://<TARGET_IP> -w /usr/share/wordlists/dirb/common.txt
Discovered:
/island
/island/2100
Hidden directories with encoded hints
