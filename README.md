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

```bash
nmap -sV -sC -Pn -vv 10.48.158.92
```

Find Open Port Available:

Which is:
1. Port 21 ftp
2. Port 22 ssh
3. Port 80 http
4. Port 111 rcpbind
   
![Nmap Scan Results](screenshot/nmap2.png)
![Nmap Scan Results](screenshot/nmap3.png)

## 2. Web Enumeration
Access Website
Open browser → http://10.48.158.92
![Nmap Scan Results](screenshot/websitepage.png)

Found a basic webpage (island theme / Arrow reference)

Directory Brute Force
```bash
gobuster dir -u http://10.48.158.92 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```
Discovered:
/island

![Nmap Scan Results](screenshot/island.png)

And then open the browser  → http://10.48.158.92/island

![Nmap Scan Results](screenshot/islandboy.png)

I Forgot to ScreenShot it, Actually if you view the page source you will get the code which is 'vigilante' 

/island/2100

```bash
gobuster dir -u http://10.48.158.92/island -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt 
```
![Nmap Scan Results](screenshot/2100.png)

And then open the browser  → http://10.48.158.92/island/2100

![Nmap Scan Results](screenshot/2100web.png)

View the page source we found a clue: 

![Nmap Scan Results](screenshot/2100clue.png)

.ticket
Using -x (Extension for the .ticket)

```bash
gobuster dir -u http://10.48.158.92/island/2100 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x .ticket
```
![Nmap Scan Results](screenshot/.ticket-clue.png)

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
