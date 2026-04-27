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

Directory Brute Force

gobuster dir -u http://<TARGET_IP> -w /usr/share/wordlists/dirb/common.txt
Discovered:
/island
/island/2100
Hidden directories with encoded hints

Clue Analysis

Found Base64 encoded strings
Decoded using:
echo "encoded_string" | base64 -d

Username
Possible password hints

## 3. Initial Access
Login / SSH
ssh <username>@<TARGET_IP>
Used decoded credentials
Successfully gained user access

 ## 4. User Flag
cat user.txt

✅ User flag obtained

##  5. Privilege Escalation
Check Sudo Permissions
sudo -l

Found binary allowed to run as root

Exploit SUID / Binary

Example:

find / -perm -u=s -type f 2>/dev/null
Identified exploitable binary
Used GTFOBins technique

Example:

sudo <binary> -option

➡️ Spawned root shell

## 6. Root Access
whoami

Output:

root
Get Root Flag
cat root.txt

✅ Root flag obtained

## Key Takeaways
Always enumerate hidden directories
Encoding (Base64) is commonly used in CTF hints
SUID binaries are critical for privilege escalation
GTFOBins is extremely useful

## Tools Used
Nmap
Gobuster
Base64
SSH
GTFOBins
